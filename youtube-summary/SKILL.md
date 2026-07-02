---
name: youtube-summary
description: >-
  Pull the main ideas out of a YouTube video — each idea plus the proof the
  video gives for it (its data, example, demo, or argument). Use when the user
  gives a YouTube link or a pasted transcript and asks to "summarize this video",
  "tldr", "what's the main idea", "key takeaways", "notes from this talk", or
  "should I watch this". Writes it for a human. Self-contained, engine-agnostic.
metadata:
  category: research
---

# YouTube Summary

Turn a video into its **main ideas**, each with the **proof** the video offers
for it — the evidence, example, demo, number, or argument. Not a table of
contents. A person should read it in a minute and know what the video claims and
whether those claims hold up.

## Input

You get one of two things:

- **A transcript** (pasted text) → summarize it directly.
- **A video URL** → read the video with whatever capability you have. If you
  can't access its content, don't guess from the title — say you need the
  transcript and ask for it.

Either way, work only from the actual content.

## Find the ideas, then their proof

Read for claims, not topics. For each main idea the video advances, note *how*
it's backed: a study, a number, a live demo, a worked example, a personal
result, or just an argument. An idea with no proof is still worth listing —
mark it as asserted, not shown.

## Output

Scale it to the video: a 3-min clip might have one idea; a 90-min talk, five to
eight. Write in the video's language unless asked otherwise.

```markdown
**<Video title>** — <channel>, <duration>

**In one line:** <the single thing the whole video is arguing.>

**Main ideas**

1. **<The idea, stated as a claim — "X beats Y", not "talks about X vs Y">**
   Proof: <what the video uses to back it — the study, number, demo, example, or
   line of argument. If it just asserts it with nothing behind it, say so.>

2. **<next idea>**
   Proof: <…>

<3–8 ideas, ordered by how central they are. Merge overlapping points; don't
split one idea into three to look thorough.>

**Weak spots** *(optional)*
- <a claim with thin or no evidence, a cherry-picked number, a caveat the video
  skips. Only if there's something real to flag.>

**Verdict:** <who should watch the whole thing, and who's done after this.>
```

## Write it like a human

The summary is for a person, not a scorecard. It has to read like a sharp friend
telling you what the video was actually about. These rules are the whole point,
not decoration:

- **Lead with the claim, then the proof.** Each idea's first line is the claim in
  plain words. The proof line supports it. Don't bury the idea inside setup.
- **Ideas are claims, not topics.** "Discusses caching" is useless. "Says
  write-through caching beats TTL-only, because TTL invalidation silently serves
  stale data" is an idea. If your bullet could be a chapter title, it's not done.
- **Proof means proof.** Name what actually backs the claim: "a 2019 RCT, n=300",
  "a live benchmark showing 4× throughput", "his own A/B test", "just his
  opinion, no data". Vague proof ("research shows") is not proof — say what the
  video actually showed.
- **Use the smallest exact word.** *use* not *utilize*, *about* not *regarding*,
  *is* not *serves as*. If the thing is a queue, say it's a queue.
- **Cut filler.** Delete words that carry no information: *basically, it's worth
  noting, in order to, at the end of the day, dive in.* If removing it loses
  nothing, it was filler.
- **One example beats a definition.** If the video makes an abstract point land
  with a concrete example, keep that example — it's often the best proof.
- **No padding, no flattery, no hype.** Skip "this is a game-changer", "marks a
  pivotal moment", rule-of-three fluff ("fast, clean, and reliable"), and empty
  sections. If the video has three ideas, hand back three.
- **Delete the AI tells on a final pass:** em-dashes stapling two clauses,
  "it's not just X, it's Y", *Moreover / Furthermore / Additionally*, *delve,
  leverage, landscape, robust, seamless, unlock, in conclusion*, and emoji or
  bold sprinkled for tone. Let the words carry it.
- **Read it back as the reader.** Would a real person say this out loud to a
  friend? Could a smart newcomer follow it without already knowing the answer?
  Cut or fix every line that fails.

## Rules that keep it honest

- **Content over vibes.** Every idea and every proof comes from the video, not
  from what a video with this title *probably* says.
- **Never fabricate proof.** If the video asserts something with no evidence, the
  Proof line says exactly that. Don't invent a study to make a claim look solid.
- **Flag low-signal input.** If the transcript is mostly music, cross-talk, or
  `[Music]`/`[Applause]`, say the summary is limited by poor captions instead of
  confabulating ideas.
- **Very long video** → if it fits, summarize in one pass. If it's huge, pull
  ideas section by section, then merge duplicates and order by importance before
  writing the one-liner.
