---
name: code-dry
description: >-
  Don't Repeat Yourself (DRY) — give each piece of knowledge one authoritative
  source. Use when the same rule, constant, schema, or logic is duplicated and
  risks drifting out of sync, OR when deciding whether to extract a shared
  abstraction (and whether you should). Language- and stack-agnostic (frontend,
  backend, JS, TS, Go, Node).
metadata:
  category: engineering
---

# Don't Repeat Yourself (DRY)

Every piece of **knowledge** — a business rule, a constant, a schema, a
calculation, a config value — should have a single, authoritative
representation. When the same fact lives in two places, the two will eventually
disagree; that drift is the real bug DRY prevents.

DRY is about deduplicating *knowledge and intent*, not lines of text. Two
snippets that merely look alike but encode **different decisions** are not a
violation — coupling them is.

## Apply

- **Find the single source of truth.** Constants, validation rules, types/schemas,
  domain calculations, and config belong in exactly one place that everything
  else references. Fixing or changing a rule should mean editing one location.
- **Deduplicate intent, not coincidence.** Before extracting, ask: *do these
  call sites represent the same decision, such that they must always change
  together?* If yes, unify. If they're alike today but free to diverge, leave
  them apart.

## The counter-trap: don't over-DRY

Premature abstraction is worse than duplication. A wrong shared abstraction
couples things that should be independent, and every caller then warps it with
special cases until it's harder to understand than the copies were.

- **Rule of Three.** Tolerate duplication until the *third* occurrence — by then
  the real, stable shape of the abstraction is visible.
- **Duplication is cheaper than the wrong abstraction.** When unsure, prefer to
  repeat and wait. Inlining a bad abstraction later is costly.
- **An abstraction must make things simpler, not just shorter.** If the shared
  helper needs flags and branches to serve each caller, it's coupling unrelated
  code — that fails the simplicity test. See [[code-kiss]].

This is a quality concern, not a bug hunt — when reviewing a diff for
correctness, security, and edge-case failures instead, see [[pr-review]].
