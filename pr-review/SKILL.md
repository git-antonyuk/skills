---
name: pr-review
description: >-
  Review a pull request or diff slowly and adversarially to find real bugs —
  not to approve fast. Use when asked to review a PR, a diff, or a change before
  merging. Launches three independent reviewer subagents (Claude Opus, Composer
  Fast, GPT), synthesizes findings, and verifies each against the code. Stack-
  agnostic.
metadata:
  category: engineering
---

# PR Review

Review to **find bugs**, not to bless the change. The goal is not throughput —
it's confidence that the diff is correct, safe, and worth merging. Spend the time
the author saved writing it on understanding whether it actually works. A slow,
skeptical review that surfaces one real defect beats a fast LGTM every time.

## Mindset

- **Adversarial, not agreeable.** Assume the diff is wrong until you've shown
  yourself it isn't. For each change ask: *how does this fail? what input breaks
  it? what did the author not think about?*
- **Approving is not the default.** A valid outcome is "this should not merge as-is"
  or even "abandon this PR — the approach is wrong." Say so plainly when it's true.
- **Understand before judging.** Restate what the change does and why before
  critiquing it. If you can't explain the mechanism, you can't review it — read
  more first.

## Reviewer models (exactly three)

Launch **three** independent reviewers in **parallel** via the Task tool. Use
only these families — no extras, no substitutes:

| # | Family |
|---|---|
| 1 | **Claude Opus** — latest available |
| 2 | **Composer Fast** — latest available |
| 3 | **GPT** — latest available |

At run time, pick the **newest slug** from the agent's available model list that
matches each family (e.g. highest Opus, the fast Composer variant, highest GPT).
Do **not** hardcode version numbers here — they change often.

Each reviewer is a `generalPurpose` subagent with `readonly: true`. Give each a
clean context — same diff, same instructions, no peeking at other reviewers'
output.

## Orchestration workflow

1. **Gather the diff** — branch vs base, uncommitted changes, or a checked-out PR
   branch. Read surrounding code, not just hunks.
2. **Launch all three reviewers in one message** — three parallel Task calls, one
   per family above, each with the resolved latest slug.
3. **Pool findings** — cross-model agreement is strong signal; single-model hits are
   suspects until verified.
4. **Verify before reporting** — re-read the actual code for every finding. Quote
   the lines that prove it. Drop anything you can't substantiate.
5. **Synthesize** — one merged report: deduplicate, rank by severity, explicit verdict.

If a subagent fails, retry it once. If it still fails, note the gap and continue
with the reviewers that succeeded — do not add a fourth model.

### Subagent prompt

Use this shape for each reviewer (fill in repo path and diff):

```text
You are an adversarial PR reviewer. Find real bugs — not style nits.

Repository: <absolute path>
Diff scope: <branch changes | uncommitted changes | describe PR/branch>
Base branch: <only if branch changes against a non-default base>

<full diff or clear pointer to what changed>

For each finding report:
- Severity: blocker / major / minor
- Location: file:line
- The bug (quote proving lines)
- How it fails (concrete scenario)
- Fix (minimal change or question for author)

End with verdict: merge | merge after fixes | do not merge.
Do not invent findings. "No blocking issues" is valid if genuine.
```

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
- **Agreement** — which reviewers flagged it (e.g. 3/3, 2/3, 1/3).

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
