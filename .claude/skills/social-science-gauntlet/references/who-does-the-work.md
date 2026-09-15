# Who does the work

The loop can revise your paper, or it can hand you the objection and wait while you revise it yourself. That is one setting, chosen at setup, and it moves who holds the pen and nothing else. The bar, the freeze, the ledger, the panel, the exit conditions and the hard gates are identical in all three settings. None of them is the gentle option.

## The three settings

**Hands off** (`mode: auto`). The loop does everything. It never asks, it logs instead, and the three standing rules in `change-tracking.md` stand in for your judgment while you are not watching. This is the original design.

**Split** (`mode: split`). Every objection the panel raises becomes a task with an owner. You set the routing per track once at setup — this track is mine, that one is the loop's, this third one asks me each time — and the loop works the tracks it owns while your tasks wait in a queue.

**Referee only** (`mode: referee`). The loop never writes a word of your manuscript. It runs the panel, names the objections, keeps the ledger, audits for specification search, and hands you all of it. Mechanically this is `split` with every track routed to you. It is worth a name of its own because it is the setting with the shortest disclosure statement.

| | Hands off | Split | Referee only |
|---|---|---|---|
| Who revises | the loop | both, by track | you |
| Interruptions | none | only where you asked for them | none, and nothing moves without you |
| Rounds per day | many | fewer, and it depends on you | as many as you have evenings |
| What markers are for | the decisions the loop made alone | the decisions it still made alone | nothing — there are none |
| Where the run can stall | nowhere | on you | on you |

## Routing

`gauntlet/ROUTING.md`, written at setup alongside `FROZEN.md`. The mode on the first line, then one row per track.

| Value | What happens when the panel raises an objection on this track |
|---|---|
| `loop` | It revises. You find out from the changelog and the dashboard. |
| `author` | The task goes in the queue with your name on it and the track parks. |
| `ask` | The track parks, the loop puts the objection to you, and it waits for one word. |

A starting point. Change it to suit the paper — these are defaults, not findings.

| Track | Suggested | Why |
|---|---|---|
| Contribution | `author` | Nobody can write your contribution claim but you. It is the one thing in the paper you know and the model does not. |
| Theory and mechanism | `ask` | Sometimes the objection is that a paragraph is unclear. Sometimes it is that your mechanism has no actors in it. Only one of those is the loop's to fix, and you cannot tell which you have until you read it. |
| Identification | `ask` | Same reason, higher stakes. |
| Measurement | `ask` | Same reason again. Whether an operationalization measures the concept is a question about your field, not about the text. |
| Alternative explanations | `loop` | It is good at generating these and you have stopped being able to see them, which is what four years on one paper does. |
| Inference and power | `loop` | Under the ledger, which is what makes this safe to delegate. |
| Presentation | `loop` | This is the one it is straightforwardly better at than you are at eleven at night. |

### Why the routing is per track and not per task

Because the skill's own argument applies to you. An author asked forty times approves forty times without reading, and a per-task prompt on all seven tracks is how you get there. Deciding once, before the run, while you are thinking about the paper rather than about the queue, is a better decision than the fortieth one you make at speed.

`ask` exists because there are tracks where the two kinds of objection are genuinely mixed and you cannot route them in advance. Use it on two tracks, not seven.

## The queue

`gauntlet/TASKS.md`, append-only like the other two logs. One entry per task, and entries are closed rather than deleted.

```markdown
### r7 · identification · task 12 · AUTHOR · open

**The objection.** Model B, both orderings: the staggered adoption of the
treatment means TWFE is estimating a weighted average that includes
already-treated comparisons, and the paper does not say why that weighting
is the estimand it wants.

**What answering it would take.** Either a Callaway–Sant'Anna or
Borusyak–Jaravel–Spiess estimate reported alongside the frozen one, or two
paragraphs in Section 4 defending TWFE as the target here. The first is a
ledger entry; the second is prose.

**Touches a claim.** No, unless the estimate moves.

**Raised.** r7. **Routed.** author, per ROUTING.md. **Closed.** —
```

States are `open`, `done`, `declined`, and `to limitations`. Declined means you looked at it and decided it does not need answering, which is a legitimate answer and gets a one-line reason. To limitations means the design cannot answer it and the paper will say so — the same exit the skill already gives identification and measurement.

## The offer

On an `ask` track the loop prints one screen and stops. Not a paragraph of context, not a recap of the round. One screen:

```
r7 · identification · task 12

The objection      Model B, both orderings: TWFE under staggered adoption is
                   estimating a weighted average including already-treated
                   comparisons, and the paper does not say why that is the
                   estimand it wants.

To answer it       An alternative estimator reported alongside the frozen one,
                   or two paragraphs defending TWFE as the target here.

Touches a claim    No, unless the estimate moves.

  author        I will do this. Park the track.
  loop          You do it.
  draft         You draft it, I edit before it goes to the panel.
  limitations   The design cannot answer this. Write it in and stop looping.
```

`draft` is the answer most people want most of the time and the one worth building the habit of. The loop writes, you edit, the panel sees your version. It is faster than writing from nothing and it leaves the paper in your voice, which matters more in the theory sections than anywhere else.

## Parking

A track waiting on you parks. The other six keep running — that is what the decomposition into seven independent tracks buys, and it is the reason split is not simply a slower version of hands off.

When every track is either exited or parked, the loop says so once, in one line, and waits. It does not remind you. The queue is on the dashboard and the dashboard is where you look.

## Handing work back

Tell the loop the task is done, or mark it done in `TASKS.md`. It then does four things, none of which is a compliment on your revision:

1. Reads what changed in the manuscript.
2. Sends it to the same classifier that triages its own work. **Your edits are classified exactly like the loop's**, at the same three levels, into the same changelog.
3. Re-derives the claim set and diffs it against `CLAIMS.md`.
4. Sends the revised piece to the panel, blind, in the usual four comparisons.

Step 2 is the one authors object to and the one worth keeping. The claims diff is the only mechanical check on whether the paper still says what you meant it to say, and it does not care who moved the claim. Authors drift their own papers. That is most of what a fourth revision is.

## What the standing rules do in each setting

| Rule | Hands off | Split | Referee only |
|---|---|---|---|
| Never strengthen a claim | Binds the loop absolutely | Binds the loop absolutely. Does not bind you — but when you take the stronger form, the changelog records it as your decision, in your words, so that the handoff brief distinguishes a claim you chose to make from one that appeared | Does not arise |
| Never delete authored text without preserving it | Verbatim in the changelog | Verbatim in the changelog, including text you delete yourself | Git is the record |
| Never add an unread citation | `[UNVERIFIED]` in the document | `[UNVERIFIED]` in the document | Does not arise |

**Rule 3 does not relax in split, and approving a task does not clear it.** Saying yes to "add a citation supporting the scope condition" is not the same act as having read the cited work, and the flag is keyed to the second one. This is the rule most likely to embarrass somebody and the one with the least reason to bend.

## Markers, and when you pay for them

In hands off the markers accumulate through the run and you clear them at the end, against a changelog of decisions you were not present for. In split they clear as you go, because a change you approved or made is a change you can sign off on the spot.

The total work is similar. What changes is whether it arrives in one block afterwards, about choices you are reconstructing, or in pieces during the run, about choices you remember making. The second is easier and produces better decisions. It is also slower, and you have to actually be there.

## What you disclose

Journal policies on AI assistance differ and are moving, so read the one you are submitting to. But the three settings produce three different true sentences, and it is worth knowing which one you are buying before the run rather than after.

- **Referee only.** No AI-generated text in the manuscript. Models were used to generate referee-style criticism; every word of the revision is the author's.
- **Split.** Specified sections were revised with AI assistance; the rest were revised by the author in response to AI-generated criticism. The changelog says which is which, line by line, if anyone asks.
- **Hands off.** The manuscript was revised throughout with AI assistance, under a specification frozen in advance, with a complete log of every consequential change.

One sentence is the same in all three and is the one that matters most: **the analysis and the reported specification were fixed before the run and are unchanged, and every robustness check that was run is reported.** That is what the freeze and the ledger are for, and no setting weakens it.

## How each setting fails

**Hands off fails by volume.** Forty rounds of accepted changes, a handoff brief you skim, and a paper you have to re-read from the top before you can defend it in a seminar. The brief is ordered by risk for exactly this reason. Read down it until it stops mattering, and if it never stops mattering, that is the finding.

**Split fails by stalling.** You route five tracks to yourself in an optimistic moment on a Sunday, the loop parks five tracks on Monday, and you are revising the paper alone again — only now with a queue and a dashboard reminding you. Route to yourself what you will sit down and do this week, and nothing else. An unopened queue is worse than hands off, because it looks like progress.

**Referee only fails by being ignored.** The objections arrive, you agree with all of them, and nothing happens. It has the least machinery and therefore the least that carries you forward. It is the right setting for an author with time and a strong view about their own prose, and the wrong one for an author with a deadline.

**And `ask` fails by frequency.** Two tracks, not seven.

## Changing your mind mid-run

Routing is a file, not a vow. Edit `ROUTING.md` between rounds and the loop picks it up on the next one. Moving a track from `author` to `loop` releases its parked tasks to the builder; moving one the other way lets the loop finish the task in flight and then parks.

Log the change in the changelog like any other consequential decision. A reader of the run later will want to know which parts of the paper were revised under which setting. So will you, in six months, when a referee asks how a paragraph got there.
