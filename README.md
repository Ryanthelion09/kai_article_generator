# galina-article (Claude Code plugin)

Write thought-leadership articles in **Galina Antova's** voice, then automatically check the
draft against her voice before saving.

This plugin bundles everything the workflow needs:

- **`galina-article` skill** — generates a Galina-voice article (data-driven, first-person,
  prescriptive and/or argued), with an optional GEO (answer-engine optimization) mode.
- **`galina-voice-editor` agent** — auto-invoked by the skill after drafting; analyzes the draft
  against Galina's voice and suggests/applies voice-fidelity edits before you're asked to save.
- **6 reference samples** of her published work (Forbes, *Fortune*, *Dark Reading*) used to
  re-anchor the voice.
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
```

## Recommended permissions

The skill verifies every statistic against a live source and saves HTML output, so each user will
be prompted to allow these the first time. None are granted by the plugin — they're approved on the
user's side:

- **WebSearch / WebFetch** — to verify statistics and capture real source URLs.
- **Write** — to save the generated article as HTML.
- **Read** — to read the bundled reference samples and seed files.

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
  galina/                      # 6 reference samples + blank output template
  seeds/                       # seeded voice profile, bio facts, known draft gaps
agents/galina-voice-editor.md
```
