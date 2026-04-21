# CLAUDE.md — Superpowers for Knowledge Work

A deliberate fork of [Superpowers](https://github.com/obra/superpowers) by Jesse Vincent, adapted for creative, strategic, and business knowledge work. Originally forked by Rollo Bryant (v0.1.0), maintained and extended by Monty Bryant from v0.2.0 onwards.

## What This Plugin Is

Structured workflow discipline for non-code knowledge work — proposals, campaigns, research, strategy, creative briefs. Enforces brainstorm → plan → execute → review → verify gates that prevent ad-hoc execution and ensure evidence-based completion. Runs in Claude Code CLI, Cowork, and Cursor.

## Structure

```
.claude-plugin/
  plugin.json          — plugin metadata (name, version, author)
  marketplace.json     — self-hosted marketplace listing for Claude Code install
skills/
  <skill-name>/
    SKILL.md           — the skill document loaded by the Skill tool
UPSTREAM.md            — sync history and methodology mapping vs. upstream
ROADMAP.md             — future directions and improvement ideas
CHANGELOG.md           — narrative change history
DECISIONS.md           — architectural decision log
```

## Distribution

This plugin supports two installation paths:

- **Claude Code CLI:** `claude plugins install github.com/montymerlin/superpowers-MM-plugin` (uses `marketplace.json`)
- **Claude Cowork (desktop):** Package as `.plugin` zip and drag into Cowork chat, or install from the plugin marketplace

Both paths load the same skills from the same source. The plugin has no host-specific code — all skills are pure markdown workflow specifications.

**Auto-update:** Claude Code pins to a commit SHA at install time; users update manually or via marketplace sync. Cowork requires re-uploading the `.plugin` file or GitHub sync if configured at the organization level.

## Coexistence with Official Superpowers

This plugin can be installed **alongside** Jesse Vincent's [Superpowers](https://github.com/obra/superpowers) plugin. The two serve different domains:

- **Official Superpowers** → software development (TDD, debugging, code review, git workflows)
- **This plugin** → knowledge work (proposals, campaigns, research, strategy, creative briefs)

### Skill categories

**Shared methodology (adapted from upstream):** brainstorming, writing-plans, executing-plans, verification-before-completion, using-superpowers, writing-skills, parallel-work. These exist in both plugins but are domain-scoped — this plugin's versions use knowledge-work examples, deliverable types, and verification criteria rather than code-specific ones.

**Knowledge-work originals (no upstream equivalent):**

| Skill | Upstream counterpart | Why it's distinct |
|---|---|---|
| systematic-problem-solving | systematic-debugging | Applies root-cause analysis to business/operational problems, not code bugs |
| two-stage-review | (none — extracted from subagent-driven-development) | Standalone spec-compliance + quality review for any deliverable |
| feedback-reception | receiving-code-review | Evaluates client/stakeholder/collaborator feedback, not code review comments |

### When both plugins are installed

**Domain routing:** If the task is code (writing, debugging, testing, git operations), prefer the official Superpowers skill. If the task is knowledge work (writing, strategy, research, creative, business), prefer this plugin's skill. The `superpowers-mm:` namespace prefix makes disambiguation explicit.

**The 3 originals always add value:** systematic-problem-solving, two-stage-review, and feedback-reception have no upstream equivalent. They're useful regardless of whether the official plugin is installed.

**Standalone use:** If this is the only Superpowers-family plugin installed, it provides the complete methodology pipeline. No gaps — the 7 shared skills cover the same discipline patterns as upstream, just for a different domain.

## Key Conventions

- **Skills live in `skills/<name>/SKILL.md`** — each skill is a single markdown file. No subdirectories within skill folders unless adding `references/` for supporting material.
- **Plugin metadata is in `.claude-plugin/plugin.json`** — update `version` on every release.
- **Bump version on release** — follows semantic versioning. Patch for skill tweaks, minor for new skills, major for methodology overhauls.
- **UPSTREAM.md is the source of truth** for what we've adopted and why. Update the Sync Status table after every upstream review.

## Skill Authoring

When creating or editing a skill:

1. Follow the `writing-skills` skill methodology (hypothesis-driven, test before writing)
2. Every skill needs: frontmatter (`name`, `description`), an Iron Law, When to Use, When NOT to Use, and the process
3. Descriptions must trigger correctly — they're used by the harness to match skill invocations
4. After editing, re-package: run the `.plugin` build step and update the version

## Relationship to Upstream

This is a **deliberate fork**, not a mirror. Upstream targets software development; this plugin targets knowledge work. See UPSTREAM.md for the full skill mapping and review process.

**Review upstream** when a new Superpowers version is released — diff the shared skills, adopt methodology improvements, skip code-specific content.

## Claude Code Responsibilities

- Editing or reviewing skills → follow the `writing-skills` methodology
- Adding a new skill → check UPSTREAM.md first (does an upstream equivalent exist to adapt?)
- Releasing a version → bump `plugin.json`, update UPSTREAM.md Sync Status, add CHANGELOG entry, commit and push
- Upstream sync → follow the "How to Review" steps in UPSTREAM.md
