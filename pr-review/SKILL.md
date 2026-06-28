---
name: pr-review
description: >-
  Review a pull request or diff slowly and adversarially to find real bugs —
  not to approve fast. Use when asked to review a PR, a diff, or a change before
  merging. Optimizes for catching correctness, security, and edge-case failures,
  is willing to recommend abandoning a flawed PR, and is designed to be run
  independently by several models and synthesized. Stack- and model-agnostic.
metadata:
  category: engineering
---

# PR Review

Review to **find bugs**, not to bless the change. The goal is not throughput —
it's confidence that the diff is correct, safe, and worth merging. Spend the time
the author saved writing it on understanding whether it actually works. A slow,
skeptical review that surfaces one real defect beats a fast LGTM every time.

Use models deliberately to raise quality: throw several of them at the same PR,
review in fresh passes, and ask how the code fails before deciding it's fine.

## Mindset

- **Adversarial, not agreeable.** Assume the diff is wrong until you've shown
  yourself it isn't. For each change ask: *how does this fail? what input breaks
  it? what did the author not think about?*
- **Approving is not the default.** A valid outcome is "this should not merge as-is"
  or even "abandon this PR — the approach is wrong." Say so plainly when it's true.
- **Understand before judging.** Restate what the change does and why before
  critiquing it. If you can't explain the mechanism, you can't review it — read
  more first.

## The multi-model workflow (the point of this skill)

This skill is meant to be run **independently by several models** — different
models, or separate fresh runs of the same one — and the findings synthesized:

1. **Run the same review prompt on multiple models** against the same diff, each
   with a clean context — no shared conversation, no peeking at each other's output.
2. **Pool the findings.** Cross-model agreement is signal: a bug that several
   models flag independently is almost certainly real.
3. **Treat single-model findings as suspects, not facts.** LLM reviews hallucinate
   and produce false positives. Before reporting any finding, re-read the actual
   code and confirm the bug exists — quote the lines that prove it. Drop anything
   you can't substantiate.
4. **Synthesize, deduplicate, rank by severity.** One merged report, not three.

When only one model is available, approximate this with **multiple passes,
clearing context between them** so each pass looks fresh and isn't anchored by the
last.

## What to scrutinize

Read the actual code, not just the diff hunks — a change is only correct in the
context it lands in.

- **Correctness & edge cases** — off-by-one, null/empty/zero, boundary values,
  unhandled branches, wrong operator, async/ordering races, error paths.
- **Security** — authz/row-level access gaps, injection, unvalidated input,
  secrets, unsafe defaults. Ask who else can reach this code path.
- **Error handling** — what happens when the call fails, the input is malformed,
  the resource is missing? Swallowed errors and bad fallbacks hide bugs.
- **Tests** — do they exercise the new behavior *and* its failure modes, or just
  the happy path? Missing tests for a risky change is itself a finding.
- **Side quests** — pre-existing bugs you stumble on while reviewing. Note them
  even though they're outside the diff; that's how the codebase gets healthier.

Defer pure style/taste unless it hides a bug or hurts readability materially —
those belong to [[code-kiss]] / [[code-dry]], not to a bug hunt.

## Output

For each finding:

- **Severity** — blocker / major / minor.
- **Location** — `file:line`.
- **The bug** — what's wrong and the lines that prove it (quote them).
- **How it fails** — the concrete input or scenario that triggers it.
- **Fix** — the minimal change, or the question to ask the author if unsure.

End with an explicit **verdict**: *merge*, *merge after fixes* (list the
blockers), or *do not merge / rethink the approach* (say why). Don't hedge — a
review with no verdict is not a review.

## Guard against your own failure modes

- Don't invent findings to look thorough. "No blocking issues found" is a
  legitimate result once you've genuinely looked.
- Verify every claim against the code before stating it. A confident false
  positive wastes more of the author's time than silence.
- Flag your own uncertainty: mark a finding *needs verification* rather than
  asserting it, when you couldn't fully confirm it.
