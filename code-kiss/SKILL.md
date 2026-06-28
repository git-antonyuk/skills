---
name: code-kiss
description: >-
  Keep It Simple (KISS) — bias code toward the simplest solution that solves the
  actual problem. Use when writing, reviewing, or refactoring code and something
  feels over-engineered, clever, or heavier than it needs to be — too many
  abstractions, layers, options, or "for later" flexibility. Language- and
  stack-agnostic (frontend, backend, JS, TS, Go, Node).
metadata:
  category: engineering
---

# Keep It Simple (KISS)

Prefer the simplest solution that fully solves the problem in front of you.
Simple means **easy to read, change, and delete** — not the fewest lines and not
the cleverest trick. Complexity must earn its place; the default is to leave it
out.

## Apply

- **Solve the real problem, not an imagined one.** Build for today's known
  requirements. Don't add config, flags, generics, or extension points for a
  future that may never arrive (YAGNI). Speculative flexibility is the most
  common source of complexity.
- **Minimize moving parts.** Fewer abstractions, layers, dependencies, and
  states. Every indirection a reader must follow is a cost — add one only when it
  removes more complexity than it introduces.
- **Be explicit, not clever.** Straightforward code a teammate understands in one
  pass beats a dense one-liner or a too-general mechanism. Optimize for the next
  reader.
- **Flatten.** Prefer early returns and guard clauses over deep nesting; prefer a
  plain function over a class/pattern when the pattern buys nothing here.
- **Optimize when you measure, not when you guess.** Reach for the clear
  implementation first; complicate it only against a real, demonstrated need.

## Smell check

Pause when you notice: an abstraction with a single caller; a parameter or option
nobody uses; "we might need this later"; a pattern added for its own sake; a
reader who'd need a diagram to follow the flow. Ask: *what's the simplest thing
that fully works, and can I remove anything and still solve the problem?*

Simplicity and de-duplication can pull against each other — an abstraction that
makes things shorter but harder to follow fails this test even if it's DRY. See
[[code-dry]].

This is a quality concern, not a bug hunt — when reviewing a diff for
correctness, security, and edge-case failures instead, see [[pr-review]].
