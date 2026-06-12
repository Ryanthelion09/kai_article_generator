# galina-article (Claude Code plugin)

Write thought-leadership articles in **Galina Antova's** voice, then automatically check the
draft against her voice before saving.

This plugin bundles everything the workflow needs:

- **`galina-article` skill** — generates a Galina-voice article (data-driven, first-person,
  prescriptive and/or argued), with an optional GEO (answer-engine optimization) mode.
- **`threat-brief-article` skill** — pulls the daily threat intelligence brief from
  devsecopsdadattack.com (today's by default, or a given date/URL), distills it into a thesis +
  evidence pack, and hands off to `galina-article` to write the article.
- **`galina-voice-editor` agent** — auto-invoked by the skill after drafting; analyzes the draft
  against Galina's voice and suggests/applies voice-fidelity edits before you're asked to save.
- **7 reference samples** of her published work (Forbes, *Fortune*, *Dark Reading*, kai.security)
  used to re-anchor the voice.
- **Seed voice profile** — the accumulated stylometric notes the agent uses on first run.

## Install

In Claude Code:

```
/plugin marketplace add https://github.com/Ryanthelion09/kai_article_generator
/plugin install galina-article@galina-tools
```

Once installed, run it with:

```
/galina-article <subject>            # e.g. recent breaches and how to prevent them
/galina-article <subject>  geo:on     # turn on generative-engine optimization

/threat-brief-article                       # article from today's threat intel brief
/threat-brief-article june 10               # ...or a specific day's brief
/threat-brief-article focus: <item>  geo:on  # center on one item; options pass through
```

## Recommended permissions

The skill verifies every statistic against a live source and saves HTML output, so each user will
be prompted to allow these the first time. None are granted by the plugin — they're approved on the
user's side:

- **WebSearch / WebFetch** — to verify statistics, capture real source URLs, and (for
  `threat-brief-article`) fetch the daily brief and its source links.
- **Write** — to save the generated article as HTML.
- **Read** — to read the bundled reference samples and seed files.
- **Bash (`date`)** — `threat-brief-article` runs one `date` command to build the brief's URL.

## Where output is saved

Generated articles are written to a `galina/generated galina articles/` folder **in your current
working directory** (created automatically). The blank `generated galina articles/` folder shipped
inside the plugin is only a structural template — the plugin's own install directory is managed by
Claude Code and is not written to.

## How the voice memory works

The `galina-voice-editor` agent uses **project-scoped memory** (`.claude/agent-memory/galina-voice-editor/`
in whatever project you run it from). On first run it's seeded from the bundled `seeds/` files, then
it grows its own memory per project. Each teammate accumulates their own notes — nobody writes back
to the shipped seeds, and edits never collide.

## Local development / testing

```
claude --plugin-dir ./galina-article-plugin
/galina-article:galina-article write about X  geo:on
```

## Layout

```
.claude-plugin/{plugin.json, marketplace.json}
skills/galina-article/
  SKILL.md
  galina/                      # 7 reference samples + blank output template
  seeds/                       # seeded voice profile, bio facts, known draft gaps
skills/threat-brief-article/
  SKILL.md                     # daily threat-intel brief -> galina-article handoff
agents/galina-voice-editor.md
```
