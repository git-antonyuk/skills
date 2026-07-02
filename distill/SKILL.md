---
name: distill
description: >-
  Boil a wall of AI-generated text down to the smallest thing a human actually
  needs. Use when handed a long AI answer, spec, report, or doc and asked to
  "summarize", "tldr", "what's the gist", "boil this down", "just the key
  points", "it's too long", "cut the fluff", or "explain this". Answer only what
  was asked, lead with the core idea, then the key points step by step — with a
  concrete example, and an analogy when the idea is abstract.
metadata:
  category: writing
---

# Distill

**TL;DR:** Throw most of the text away. Lead with the one idea that matters, in
the first sentence. Three moves: **strip** the noise → **find the spine** →
**rebuild small**.

AI text says ten things at medium confidence and buries the one that matters.
Your job is to throw most of it away and hand back the core — small enough that
a tired person gets it on the first read.

## 1. Strip the noise

Delete everything that carries no information. In AI text that's usually most of
it:

- Restated question, preamble, "great question", the recap at the end.
- Hedging stacked on hedging ("may, in certain cases, sometimes, potentially").
- Repetition — the same point made three ways; intro, then body, then summary.
- Rule-of-three padding, filler words, headers and bullets on a short answer.
- Anything answering something the human didn't ask.

## 2. Find the spine

- **What was actually asked?** Answer only that. Ignore the other nine things
  the text volunteered.
- **What's the one idea everything hangs on?** Say it in a single sentence. If
  you can't, you haven't found it yet — reread until you can.
- **Is there an order?** If the points depend on each other, they're a sequence,
  not a bullet pile.

## 3. Rebuild small

- **Lead with the answer.** The first sentence carries it. Support comes after,
  and only if it changes what the reader does.
- **One idea per point, step by step** when order matters. No step that hides
  three.
- **Give one concrete example.** An example lands harder than any definition.
- **Name the pattern (the abstraction)** so it transfers: "this is just a
  cache", "this is retry-on-failure". One good name replaces a paragraph.
- **Reach for an analogy when the idea is abstract** — map it onto something the
  reader already lives with. Drop it once it has done its job.

Saying it in plain, human words is its own discipline — see [[write-for-human]].
Teaching the idea so it sticks (not just summarizing) is
[[learning-worked-example]].

## Before / after

> **Before (AI slop):** Great question! There are several important factors to
> consider regarding caching. Caching is a powerful and widely-used technique
> that can significantly improve performance. Essentially, at its core, a cache
> is a component that stores data so that future requests for that data can be
> served faster. It's worth noting that caches are used in many layers of modern
> systems... *(200 words)*

> **After:** A cache keeps a copy of slow-to-fetch data somewhere fast, so you
> don't fetch it twice. Like keeping snacks on your desk instead of walking to
> the kitchen each time. Use it when the same data gets read a lot and rarely
> changes.

Same fact. A tenth of the words. The idea, an analogy, and when to use it.

## Check before you hand it back

1. Did I answer only what was asked?
2. Is the main idea in the first sentence?
3. Can I cut another quarter and lose no meaning?
4. Would a tired human get this on one read?
