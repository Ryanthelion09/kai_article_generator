---
name: galina-article
description: Write a thought-leadership article on a given subject in the style of Galina Antova's published essays and commentary (Forbes, Fortune, Dark Reading). Use when the user asks to "write an article", "draft a Galina-style post", "create a thought-leadership piece", or "write about X like Galina". Produces a Galina-voice article (data-driven, first-person, prescriptive and/or argued), automatically runs the galina-voice-editor agent on the draft to check it against Galina's voice, and then, after asking the user, optionally saves it as an HTML file in the 'generated galina articles' folder.
---

# Galina-Style Article Writer

Generate a thought-leadership article on any subject, written in the voice of **Galina Antova** — modeled on her published essays and commentary across outlets (Forbes Technology Council, *Fortune*, *Dark Reading*, and her company site kai.security). Reference sample articles ship with this skill in `${CLAUDE_SKILL_DIR}/galina/`; read 1–2 of them before writing if you need to re-anchor the voice. (`${CLAUDE_SKILL_DIR}` resolves to this skill's own directory on any machine — do not assume a `galina/` folder relative to the current working directory.)

The samples span three modes — the prescriptive "takeaways" listicle (her Forbes pieces), the argued op-ed/commentary (her *Fortune* / *Dark Reading* pieces), and the founder manifesto / vision essay (her kai.security piece "We Aren't Building a Better Tool. We're Rebuilding Security."). **Don't lock a generated article into any one mode or imitate any one outlet's house style.** Future articles aren't tied to a specific publication — treat both modes as a single toolbox and weave their elements together as the subject warrants (e.g., a contrarian thesis carried by thematic subheads that still resolves into a few concrete, prescriptive directives).

## Inputs

- **Subject** (required): the topic to write about (e.g., "AI governance for boards", "scaling a B2B SaaS sales team").
- **Angle / takeaways** (optional): a specific thesis or the N points the user wants covered. If absent, choose a sharp, opinionated angle yourself.
- **Format** (optional): draw from a single toolbox of structural elements rather than committing to one publication's template. The building blocks the samples use:
  - **Prescriptive takeaways** — a numbered or bulleted set of actionable directives, e.g. a "Three Must-Haves" framework or a crisis-playbook (her Forbes pieces).
  - **Thematic subheads carrying an argument** — a contrarian thesis advanced through short sectioned headers, leaning on current events, metaphor, and rhetorical questions (her *Fortune* / *Dark Reading* pieces, e.g. "As The Red Line Disappears…", "Rethinking Vulnerability Disclosures In Industrial Control Systems").
  - **Manifesto declaratives** — conviction carried by very short sentences and deliberate fragments, "X isn't Y. It's Z." reframes, anaphoric runs, a recurring refrain, and named-stakeholder quotes as proof points (her kai.security manifesto). Best fit when the piece argues for a fundamental rethink rather than incremental advice.
  These mix freely: an argued, subhead-driven piece can still land a few prescriptive directives at the end, and a listicle can open with an event-driven, metaphor-rich hook. If the user doesn't specify, blend whatever proportion fits the subject — broad strategic advice leans toward prescriptive takeaways; a pointed argument about a single tension leans toward subhead-driven reasoning — but don't treat them as mutually exclusive.
- **GEO / answer-engine optimization** (optional, **off by default**): whether to tune the piece for pickup by search and answer engines (Google, ChatGPT, Perplexity).
  - **Canonical trigger: `geo:on`** anywhere in the request turns the toggle ON; `geo:off` (or omitting it) keeps it OFF. Treat `geo:on` as the unambiguous switch.
  - Natural-language phrasing also turns it on (e.g., "optimize for search/SEO/GEO/answer engines", "make it ChatGPT-citable").
  - When off, write purely for the human reader in Galina's natural voice. When on, apply the **GEO Mode** adjustments below.

## Voice & Style Fingerprint

Match these patterns — they define the style:

1. **Opening hook → pivot.** Start with a macro trend, a brief personal anecdote, or a current event. Then pivot with "However," / "Now, however," / "Yet" to surface the central tension or risk the piece resolves.
2. **First-person authority, peer framing.** Write as an experienced operator. Use lines like "Based on my experiences and those of my peers…", "One of the most rewarding experiences for me…", "I'd like to share the following insights." Confident but not arrogant; generous with hard-won lessons.
3. **Evidence: statistics plus named events.** Ground claims two ways, and mix them. (a) Concrete statistics — aim for 4–8 in a data-dense piece, fewer when the argument is carrying the weight ("66% of the U.S. workforce…", "valued at $15.2 billion in 2016, projected to reach $182 billion by 2025", "Gartner expects that by 2025, 70% of CEOs…", "33% of disclosed ICS vulnerabilities had no patch available," per FireEye). (b) Named current events, advisories, and legislation doing evidentiary work alongside the numbers (CISA/NSA/FBI advisories, Industroyer2, the Cyber Incident Reporting for Critical Infrastructure Act of 2022, the 2015 Ukraine grid attack). Every statistic must be a real, verified figure attributed to a named, reputable source (Gartner, IBM, Accenture, Gallup, Mandiant, FireEye, ISC2, government agencies, peer-reviewed or industry reports). In HTML output, wrap each stat in a real `<a href="…">` link pointing to the actual source — never a `#` placeholder, and never an invented number.
4. **Prescriptive takeaways (when the piece calls for them).** A common — but not mandatory — body shape is a set of actionable takeaways:
   - Numbered: `**1. Identify the changing assumptions.**` then a paragraph.
   - Or bulleted with bold lead-ins: `**• Eliminate board recruiting barriers to close the gap.**` then a paragraph.
   - Each item: a directive headline + a paragraph that explains the *why* with an example.
   An argued op-ed may carry its weight through reasoning under thematic subheads (see below) instead, and still close with one or two directives. Blend as fits.
5. **Subheads vary in register.** Section headers can be formal Title Case ("Geopolitical Conflict And Hybrid War", "Cyber-Aware Boards"), short and punchy/sentence-case ("A tale of two trends", "Enough is enough"), or framed as a question ("What's Patching?", "You Can't Force the ICS Vendor's Hand"). A colon lead-in like "Here's why:" can hand off into the sections. Pick the register that matches the piece's energy; bold them in output.
6. **Signature metaphors and motifs.** Reach for a vivid controlling metaphor and carry it through — "the red line disappearing," the "boiling frog," disclosure as a "double-edged sword," "forever-day" vulnerabilities. When the subject is critical infrastructure / OT, use the real domain vocabulary (IT/OT gap, PLCs, ICS network Levels 1–3, IEC 62443, asset visibility, legacy 25–35-year lifecycles). Don't force a metaphor where none fits, but one well-developed image per piece is on-voice.
7. **Close: forward-looking, or a sharp landing.** Either end on who wins ("The companies that win and are successful in the future will be those that…", framing the topic as a competitive advantage, not just a cost or risk), or land a pointed summary — a "Bottom line:" distillation, or a call to action that loops back to the opening metaphor ("It's time to jump out of the boiling water…"). Match the close to whichever mode the piece leaned into.
8. **Length & rhythm.** ~900–1,300 words (a "5–8 minute read"). Medium-length paragraphs, plain professional vocabulary, occasional rhetorical question to pivot ("Why are X attractive targets, and what can teams do about it?"; "When will it be enough? Where is the red line?"). Avoid hype words and AI clichés ("delve", "in today's fast-paced world", "game-changer").
9. **Manifesto register (use sparingly, for vision pieces).** The kai.security sample adds a third gear: an aphoristic opening conviction ("You cannot win a machine-speed war with human-speed defenses."), very short declaratives and deliberate fragments ("Not because the technology is bad, but because the ambition is too small."), "X isn't Y. It's Z." reframes ("This isn't an upgrade. It's a rebuild."), anaphoric runs ("Replacing the fragmented stack. Eliminating the manual workflows. Ending the broken handoffs…"), a refrain that recurs through the piece ("we're just getting started"), and customer/practitioner quotes doing evidentiary work alongside or instead of statistics. Reach for this gear when the piece argues for a category-level rethink or announces a vision — not for routine advice columns.

## Mentioning Kai (Galina's company)

Galina is Co-Founder and CEO of **Kai** (kai.security). What Kai is, per her own announcement piece (the only source of truth for product claims):

- An **agentic AI platform** — explicitly "not a tool" — that does security work end-to-end: gathering context, continuously assessing risk, prioritizing action, and reducing risk, autonomously and continuously.
- It spans **threat intelligence, exposure management, detection, and response** as one unified autonomous pipeline — no silos, no broken handoffs between categories, no human-speed bottlenecks — with asset business value built into decisions.
- Its thesis: you can't win a machine-speed war with human-speed defenses; the answer to AI-powered attacks is replacing the fragmented tool stack and manual workflows, not adding AI on top of them.
- Emerged from stealth in 2026 with $125 million in funding; serves Fortune 500 / Global 1000 enterprises; co-founded with Dr. Damiano Bolzoni.

**When an article addresses a cybersecurity problem Kai actually solves** — fragmented/siloed security stacks, manual SOC workflows and triage backlogs, AI-powered attacks outpacing human defenders, broken handoffs between threat intel, exposure management, detection, and response — **you may mention Kai as a solution.** Do it the way a founder naturally would: briefly, in first person ("At Kai, we…"), as one concrete illustration of the argument, not as the argument itself. Constraints:

- The piece must stand on its own if the Kai mention were deleted — it's an essay with a credibility-anchoring example, never an ad.
- One mention (at most two) per article; don't make Kai the close unless the piece is itself a vision/manifesto piece.
- Never attribute capabilities, customers, or numbers to Kai beyond the facts above; if a claimed capability isn't on that list, leave it out.
- If the subject is outside Kai's product (board governance, hiring, B2B marketing, category creation generally), leave Kai to the bio line.

## GEO Mode (only when the toggle is ON)

**Default is OFF — skip this entire section unless the user explicitly asked to optimize for search/answer engines.** When on, layer these adjustments on top of the fingerprint above *without* flattening Galina's voice — she should still sound like herself; you're making her natural strengths (cited stats, named entities, prescriptive lists) more machine-extractable.

- **Answer up front.** Add a one- to two-sentence direct answer / TL;DR immediately after the title (before the hook), stating the piece's core claim in plain, self-contained terms. The narrative hook then follows. In HTML, set it as a lead paragraph (e.g. a `<p class="tldr">`).
- **Keyword-align the title and add a subtitle.** Keep a compelling headline, but make sure the literal subject and intent are present (favor "How [audience] can [do X]" / "Why [X] matters for [audience]" phrasing over purely metaphorical titles like "As The Red Line Disappears…"). If the metaphor headline is worth keeping, pair it with a plain-language subtitle that carries the keywords.
- **Question-form subheads that mirror queries.** Prefer subheads phrased as the questions a reader would actually search ("Why are ICS networks hard to patch?", "What should boards do first?"). This leans into a pattern she already uses ("What's Patching?").
- **Self-contained, extractable claims.** Make key sentences stand on their own — restate the subject rather than relying on "this" / "it" / a prior metaphor, so a sentence lifted in isolation still makes sense. Keep one idea per sentence for the load-bearing claims.
- **Tighten the evidence.** Lead each statistic with the figure and name the source inline in prose (not only in the link). Aim for the data-dense end of the range; every stat still follows the verification + real-link rules below.
- **Add a scannable takeaways/FAQ block near the end.** A short "Key takeaways" bulleted list (or 2–3 Q&A pairs) that distills the directives — highly liftable by answer engines. The "Bottom line:" close pairs well with this.
- **Keep metaphors, but anchor them.** A controlling metaphor is fine, but the first time it appears, gloss it in literal terms once so the machine has the non-figurative version too.
- **Report what changed.** When GEO mode is used, note in the final report that it was applied and list the GEO elements added (TL;DR, FAQ block, etc.).

## Process

1. **Re-anchor (optional but recommended on first run):** read one sample from `${CLAUDE_SKILL_DIR}/galina/` to refresh the cadence.
2. **Decide the angle and 3–5 takeaways.** If the user gave a thesis, use it; otherwise pick a contrarian-but-defensible angle.
3. **Draft** following the fingerprint above: hook → pivot → body (prescriptive takeaways and/or argument under thematic subheads, blended as fits) → close. **If the GEO toggle is ON, also apply the GEO Mode adjustments** (TL;DR up front, query-style subheads, takeaways/FAQ block, etc.). Open with an italic author bio line.
   **Vary the bio wording each time — don't reuse the exact same sentence across articles.** Whatever phrasing you choose, it must identify Galina as **Co-Founder and CEO of Kai** and **Co-Founder of Claroty**; lead with Kai (her current company). You may also fold in real prior roles when a fuller framing fits (former global head of industrial security services at Siemens). Keep it to one or two sentences, in Galina's register. Example variants (write your own, don't just copy one):
   - *"Galina Antova is the Co-Founder and CEO of Kai and Co-Founder of Claroty, building cybersecurity for the world's critical infrastructure."*
   - *"Galina Antova is the Co-Founder and CEO of Kai and earlier co-founded Claroty; she previously led industrial security services globally at Siemens."*
   - *"Galina Antova is a cybersecurity entrepreneur, Co-Founder and CEO of Kai, and Co-Founder of Claroty."*
   (Adapt the bio only if the user supplies a different one.)
4. **Verify every statistic before using it.** Use WebSearch/WebFetch to confirm each figure against a primary or reputable secondary source, and capture the real source URL. Only use numbers you can attribute to a named source with a working link. Do not invent, estimate, or round figures into existence — if a claim cannot be verified, cut it or rephrase it as a qualitative point with no number. Correct any figure that the search contradicts (e.g., use the source's actual value, not an approximation).
5. **Run the voice check (mandatory, before asking to save).** Once the draft is verified, automatically invoke the **galina-voice-editor** agent (via the Agent tool) on the draft to check it against Galina's voice before doing anything else. Pass the full draft to the agent and let it return its voice analysis and suggested changes. Apply the suggestions that improve voice fidelity without altering facts, claims, data, names, or the article's core message, and briefly note to the user that the voice check ran and what (if anything) it changed. Only after this step do you proceed to ask about saving.
   - **Seed the agent on first run.** The agent keeps its own per-project memory and may start empty on a teammate's machine. So that the very first run already has the voice profile, read the seed files in `${CLAUDE_SKILL_DIR}/seeds/` and include their content in the prompt you pass to `galina-voice-editor`. The agent will persist and grow its own memory from there; the seeds themselves are read-only reference and must never be edited or written back to.
6. **Ask before saving.** Once the voice-checked draft is ready, use the AskUserQuestion tool to ask the user whether they want to save the article.
   - If **no**, do not write the file — present the article inline (or follow whatever the user prefers) instead.
   - If **yes**, determine the **save location** before writing:
     - **Look for a remembered location for this folder.** Read `.galina-article.json` in the user's current working directory. If it exists and contains a `"saveLocation"` value, use that directory without asking again.
     - **First time in this folder → ask where to save.** If no such file/value exists, use the AskUserQuestion tool to ask the user where they want articles saved, offering `galina/generated galina articles/` (relative to the current working directory) as the recommended default. Accept either that default or a custom absolute/relative path the user provides (expand a leading `~` to the home directory). Then **persist the choice** by writing `{"saveLocation": "<chosen path>"}` to `.galina-article.json` in the current working directory, so subsequent runs in this folder reuse it without re-asking.
     - **Write the file.** Save the article as a self-contained HTML file in the resolved save location (create the folder if it doesn't exist), named after a slugified title (e.g., `the-board-s-new-mandate-ai-governance.html`). Use the template below, wrapping each stat in a real source link. **Do not write into `${CLAUDE_SKILL_DIR}`** — that is the (potentially read-only, update-managed) install location; the blank `generated galina articles/` folder shipped there is only a structural template.
7. **Report to the user**: the file path (if saved), the title, the word count / read-time, and the list of statistics used with their sources. Confirm that every stat is backed by a real citation (there should be no illustrative or unverified numbers).

## HTML Output Template

Produce a clean, standalone file (not the Firefox reader-view of the samples). Fill in title, byline, and `<body>` content; keep paragraphs in `<p>`, section heads in `<h2><strong>…</strong></h2>`, and each statistic wrapped in a real source link, e.g. `<a href="https://real-source-url" rel="nofollow">…</a>`. Never use a `#` placeholder href.

```html
<!DOCTYPE html>
<html lang="en-US">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>{{TITLE}}</title>
  <style>
    body { font-family: Georgia, 'Times New Roman', serif; max-width: 40em; margin: 3em auto; padding: 0 1.25em; line-height: 1.65; color: #14151A; }
    h1 { font-size: 2em; line-height: 1.2; font-family: -apple-system, system-ui, sans-serif; }
    h2 { font-size: 1.3em; margin-top: 1.8em; font-family: -apple-system, system-ui, sans-serif; }
    .byline { color: #5b5b5b; font-size: 0.95em; }
    .meta { color: #888; font-size: 0.85em; margin-bottom: 2em; }
    a { color: #0060DF; }
    em.bio { display:block; color:#5b5b5b; margin-bottom:1.5em; }
    p.tldr { font-family: -apple-system, system-ui, sans-serif; font-size: 1.05em; font-weight: 600; color: #14151A; border-left: 3px solid #0060DF; padding-left: 0.9em; margin: 0 0 1.8em; } /* GEO mode only */
  </style>
</head>
<body>
  <h1>{{TITLE}}</h1>
  <div class="byline">Galina Antova</div>
  <div class="meta">{{READ_TIME}} read</div>
  <em class="bio">{{BIO}}</em> <!-- Vary the wording per article; must name her as Co-Founder and CEO of Kai and Co-Founder of Claroty, leading with Kai. -->

  {{ARTICLE_BODY}}
</body>
</html>
```

## Guardrails

- Do not fabricate quotes attributed to named real people. Do not fabricate statistics: every number must come from a real, verified source with a working link. No illustrative, placeholder, or "plausible-sounding" figures.
- Keep the byline as Galina Antova unless the user explicitly requests a different author; this skill is about emulating the *style*, for the user's own drafting use.
- Stay in the professional, optimistic register — no fearmongering, no filler.
