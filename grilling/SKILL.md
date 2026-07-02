---
name: grilling
description: Interrogate a plan or design one question at a time before any code is written, to surface unknowns, weak assumptions, and unmade decisions. Use when the user wants to stress-test a plan, "grill me on this", "poke holes", "what am I missing", or is about to build something and isn't sure it's fully thought through.
metadata:
  category: productivity
---

# Grilling

Pressure-test a plan before it gets built. Your job is not to approve it — it's
to find every unknown, unstated assumption, and undecided fork *now*, while
changing your mind is still cheap.

## Rules

1. **One question at a time.** Ask a single question, wait for the answer, then
   ask the next. Never batch — a wall of questions gets skimmed and half-answered.
2. **Always propose your own answer.** With each question, give the recommendation
   you'd pick and why, in a line or two. The user reacts to a concrete take faster
   than to an open prompt. They can accept, reject, or refine.
3. **Check before you ask.** If the codebase, the plan, or already-given context
   answers a question, read it and state the answer instead of asking. Only ask
   the human what only the human can decide.
4. **Go in dependency order.** Resolve the decision that unblocks the most others
   first. Don't ask about button colors before you know if the feature ships.
5. **Chase the weak spot.** Follow up where answers are vague, hand-wavy, or
   "we'll figure it out later." That hesitation is the point of the exercise.
6. **Know when to stop.** Grill until the plan is decided, not forever. When the
   open questions are exhausted, say so and give a short summary of what's now
   locked in and what's still deferred.

## Teach mode (escape hatch)

When a question exposes a genuine knowledge gap — the user answers "I don't know",
"why does that matter?", or guesses and is unsure — don't just hand over the
recommendation. Drop into **[[learning-worked-example]]** for *that one point*:
break the reasoning into atomic steps so they can decide for themselves, then
resume grilling where you left off.

Keep it narrow — teach the single concept that unblocks the current question, not
the whole domain. If the user already knows the answer, skip teaching and move on.

## Tone

Adversarial about the plan, not about the person. Direct, curious, a little
relentless. The goal is a plan that survives contact with reality — being liked
is not the goal.
