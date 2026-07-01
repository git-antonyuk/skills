# skills

A collection of skills built from research notes.

Each skill is grounded in a documented method or technique. The research and rationale
behind every skill lives in my Obsidian vault. This repo holds the
executable skills themselves.

## Structure

```
skills/
  <skill-name>/
    SKILL.md      # the skill definition (frontmatter + instructions)
```

## Skills

| Skill | Category | What it does |
|---|---|---|
| `learning-worked-example` | learning | Tutors a topic using the Worked Examples method — atomic, step-by-step breakdowns for better retention. |
| `diet-coach` | health/fitness | Evidence-based, dynamic diet & weight-loss coach — reads a personal profile + progress log each run and recomputes calories, protein, phase (grind/chill) and steps. Answers in the user's language. |
| `code-kiss` | engineering | Keep It Simple — biases code toward the simplest solution that solves the actual problem; flags over-engineering, premature flexibility, and needless cleverness. Stack-agnostic. |
| `code-dry` | engineering | Don't Repeat Yourself — gives each piece of knowledge one authoritative source, while guarding against premature/over-abstraction (Rule of Three). Stack-agnostic. |
| `pr-review` | engineering | Slow, adversarial PR/diff review that optimizes for finding real bugs (not approving fast) — built to be run independently by several models and synthesized. Stack- and model-agnostic. |
| `alex-reviewer` | engineering | Review frontend code (Vue 3 + TypeScript) the way Alex does — distilled from 1000+ real PR comments. Covers tests, typing, composables & DRY, Vue/i18n idioms, error handling, scope discipline, and review tone. |
| `write-for-human` | writing | Write and explain like a human, not an AI — short, answers only what was asked, no flattery, no em-dashes or AI tells, plus plain-words/examples/analogy explanation with a self-audit second pass. |
| `distill` | writing | Boil a wall of AI-generated text down to the core — strip the noise, find the one idea, rebuild small with an example and analogy. Answers only what was asked. Stack-agnostic. |

## Installing a skill

Every skill here is a self-contained `<skill-name>/SKILL.md` folder, and the
format is identical across Claude, Cursor, and Gemini — only the install
directory differs. Copy (or symlink) the skill folder into the agent's skills
directory and it's auto-discovered via its `name` + `description` frontmatter.

| Agent | Personal (all projects) | Project-scoped |
|---|---|---|
| Claude Code | `~/.claude/skills/` | `.claude/skills/` |
| Cursor | `~/.cursor/skills/` | `.cursor/skills/` |
| Gemini CLI | `~/.gemini/skills/` | `.gemini/skills/` |

`name` must be lowercase letters/numbers/hyphens and match the folder name;
`description` tells the agent what the skill does and when to use it.

### Quick install (one agent)

First clone the repo and `cd` into it — the commands below symlink/copy out of
the working tree, so they must run from inside it:

```sh
git clone <repo-url> skills
cd skills
```

Then symlink (stays in sync on `git pull`, but needs the clone to stay on disk)
or copy (independent snapshot, won't auto-update):

```sh
# Claude Code, personal — symlink
ln -s "$PWD/learning-worked-example" ~/.claude/skills/learning-worked-example

# …or copy
cp -r learning-worked-example ~/.claude/skills/
```

Then start a new session and ask for something the skill's `description` matches.

### Install once, share across all three agents

Cursor and Gemini both read the interoperable `~/.agents/skills/` path, and
Cursor also reads `~/.claude/skills/`. Put the skill in `~/.agents/skills/` once
and symlink it into Claude's directory:

```sh
mkdir -p ~/.agents/skills
ln -s "$PWD/learning-worked-example" ~/.agents/skills/learning-worked-example
ln -s ~/.agents/skills/learning-worked-example ~/.claude/skills/learning-worked-example
```

Now Cursor and Gemini pick it up from `~/.agents/skills/`, and Claude from the
symlink in `~/.claude/skills/`.

## Adding a skill

1. Write or pick a research note in the Obsidian `skills/` folder.
2. Create `<skill-name>/SKILL.md` here with `name` + `description` frontmatter.
3. Link the note and the skill in both READMEs.
