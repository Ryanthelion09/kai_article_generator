---
name: threat-brief-article
description: Pull the daily threat intelligence brief from devsecopsdadattack.com and write a Galina-voice thought-leadership article based on it (by invoking the galina-article skill). Use when the user asks to "write an article from today's threat brief", "turn the threat intel brief into an article", "galina article from the daily brief", or similar. Accepts an optional date, brief URL, or focus topic; defaults to today's brief.
---

# Threat-Brief → Galina Article

Fetch the daily **Threat Intelligence Brief** from DevSecOpsDadAttack (devsecopsdadattack.com), distill it into an article-worthy subject + angle + evidence pack, then **invoke the `galina-article` skill** (via the Skill tool) to write the article. This skill does the sourcing and framing; `galina-article` owns the voice, verification, voice-editor check, and save flow — do not duplicate or override its process.

## Inputs (all optional)

- **Date or URL**: a specific brief to use (e.g. "June 10's brief" or a full URL). Default: today's brief.
- **Focus**: a specific item or theme from the brief to center the article on (e.g. "the water utility breach"). Default: you choose the strongest angle.
- **Pass-through options**: anything aimed at the article itself (`geo:on`, a desired format, a thesis, "don't save") — forward these verbatim to `galina-article`.

## Step 1 — Resolve the brief URL

Brief URLs follow this pattern (note: zero-padded date in the prefix, **non-padded day** in the suffix, all lowercase):

```
https://devsecopsdadattack.com/YYYY-MM-DD-threat-intelligence-brief-<dayname>-<monthname>-<D>-YYYY/
```

Example: `https://devsecopsdadattack.com/2026-06-09-threat-intelligence-brief-tuesday-june-9-2026/`

Build today's URL with one Bash call (works on macOS/BSD date):

```bash
date "+https://devsecopsdadattack.com/%Y-%m-%d-threat-intelligence-brief-%A-%B-%-d-%Y/" | tr '[:upper:]' '[:lower:]'
```

If the user gave a date, substitute it; if they gave a URL, use it as-is. **Fallback:** if the constructed URL 404s or fetches empty (e.g. weekend, brief not yet published), fetch `https://devsecopsdadattack.com/` and take the most recent post whose slug contains `threat-intelligence-brief` (the site also publishes `detection-engineering-brief` posts — skip those unless the user asks for one). Tell the user which brief you actually used if it differs from what they asked for.

## Step 2 — Extract the evidence pack

WebFetch the brief and pull out, preserving the brief's own confidence framing:

- The brief's date and title.
- Every item across its tiers — **Executive Signal**, **Immediate Action Required**, **High-Impact Developments**, **Monitor Only**, **Analyst Observation** (tier names may vary slightly day to day).
- For each item: what happened, named CVEs, threat actors/groups, affected products/sectors, any numbers, and the brief's confidence level (e.g. "medium confidence, actor-sourced claim").
- The **Source Links** section — capture every URL. These primary sources, not the brief itself, are what article statistics must ultimately cite.

If one WebFetch summary is too lossy for the chosen angle, fetch the brief again with a prompt targeted at the specific items you're using, and fetch the 1–3 source links behind those items so the facts come from primaries.

## Step 3 — Choose the subject and angle

A Galina article is a thesis, not a news roundup. Pick the strongest article-worthy theme from the brief (or the user's focus item) and frame it the way she would — the systemic problem behind the day's headlines, not the headlines themselves. Examples of the move: an AI-agent RCE chain plus an "agentjacking" technique becomes "AI agents are the new unmanaged asset class — you can't protect what you can't see"; a utility breach claim becomes the disappearing red line around critical infrastructure. Items from different tiers can serve one thesis as evidence. Prefer angles where the brief's items are *illustrations* of a structural argument Galina would make.

## Step 4 — Invoke `galina-article`

Call the **Skill tool** with `skill: galina-article` — it ships in this same plugin, so if the bare name isn't in the available-skills list, use the plugin-qualified form (e.g. `galina-article:galina-article`). Pass an `args` string containing:

1. **Subject** — the thesis-level topic you chose.
2. **Angle / takeaways** — your chosen argument and 3–5 candidate points.
3. **Evidence pack** — the relevant brief items with their facts, confidence levels, and the primary source URLs from Step 2, plus the brief's own URL for attribution.
4. **Pass-through options** — any user-supplied format/GEO/save preferences, verbatim.

Then let `galina-article` run its full process (drafting, stat verification, voice check, ask-before-save). Do not re-implement any of it here.

## Guardrails

- **Honor the brief's confidence levels.** An actor-claimed, unverified breach must be written as a claim ("Handala claims…"), never as established fact. Items the brief marks "monitor only" or medium-confidence cannot carry load-bearing assertions.
- **The brief is a tip sheet, not a citation.** Statistics in the article must satisfy `galina-article`'s verification rules — confirmed against primary/reputable sources with real links. The brief's URL may be cited for "today's threat brief flagged…" framing, but numbers need their underlying source.
- **Timeliness:** name the date of the brief or the events; a piece pegged to a daily brief should read as current commentary.
- Kai mentions, bio, voice, and save behavior are all governed by `galina-article` — add nothing about them here.
