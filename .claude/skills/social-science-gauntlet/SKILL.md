---
name: social-science-gauntlet
description: Runs a gauntlet loop on a finished social science manuscript being polished for a top-5 journal. Sets a real published paper as the bar, decomposes the paper by referee objection rather than by section, freezes the headline result, and loops builder/referee pairs until a two-model blind panel picks the manuscript over the bar or stops finding new blocking objections. Lets the loop run robustness checks under an append-only ledger that makes specification search impossible to hide, and records every consequential change to the analysis or the prose. The author chooses who does the revising: the loop alone and never pausing, the work split task by task between author and loop, or the loop refereeing only and never touching the manuscript. Triggers on "/social-science-gauntlet", "gauntlet my paper", "gauntlet this manuscript", "referee loop", "polish this for APSR/AJPS/JOP/BJPS/IO/ISQ".
---

# Social Science Gauntlet

Adapted from the gauntlet loop (Matt Shumer's technique, packaged as a skill by Jay E at RoboNuggets). Same engine: a real bar, small judgeable pieces, a builder and a separate harsh critic on each, blind comparison, loop until it wins.

Four things change for empirical social science, and they are the whole skill:

1. **The reviewer model is the critic, never the bar.** "Fable 5 rates this highly" is a rubric wearing a referee's coat. The bar stays a specific published paper.
2. **The pieces are referee objections, not paper sections.** Papers do not die of a weak subheading. They die of a defensible alternative explanation.
3. **The core is frozen, the robustness work is logged, and every consequential change is recorded.** A loop pointed at "make the referee stop objecting" is a specification-search engine unless you take that move off the table — and a loop that runs unwatched for forty rounds will hand back a paper the author cannot defend unless it leaves a trace of what it did.
4. **Who does the revising is the author's call.** In a coding gauntlet nobody asks who wrote the function. Here the author signs the paper, answers for every reference in it, and discloses what the tool did. So the loop does all the revising, none of it, or the part of it the author routes to it — and that setting is the first line of their disclosure statement.

Use this on a draft that already exists and already has results. Do not use it on a project at the design stage — the freeze in step 3 below has to happen at pre-analysis time there, which is a different workflow.

## Setup

Run all of this before any looping. Write each artifact to `gauntlet/` in the manuscript's repo.

### 1. Choose who does the work

Ask this first, before the bar, and offer three answers. Full protocol in `references/who-does-the-work.md`.

- **Hands off** (`mode: auto`) — the loop revises everything and never asks.
- **Split** (`mode: split`) — every objection becomes a task, routed per track to the author, to the loop, or to a question asked at the moment it arises.
- **Referee only** (`mode: referee`) — the loop never touches the manuscript. It referees, objects, audits the ledger, and hands the author all of it.

Write the answer to `gauntlet/ROUTING.md`, with the per-track routing if it is split. Suggested defaults and the routing table are in the reference — offer them, do not impose them.

The setting moves who holds the pen and nothing else. The bar, the freeze, the ledger, the panel and the exit conditions are identical in all three, and none of them is the gentle option. If the author does not choose, take hands off and say so: it is the original design and the only setting that finishes without them.

### 2. Pick the bar

Offer **2 or 3 candidate bar papers**, one line each, then stop and wait. A bar paper qualifies only if it is:

- **Published in the target journal.** Not a comparable journal. The referee prompt keys off the journal's actual standard, and APSR is not JOP.
- **Same method family.** A CSTS observational paper is not judged against a survey experiment. Match the design, not just the topic.
- **Recent, and preferably past the referee models' training cutoff.** Forthcoming / OnlineFirst pieces are best. See the blinding problem in `references/referee-panel.md` — this is the single biggest threat to the comparison being real.
- **Comparable in length and structure.** Same rough word count, same number of empirical sections.

Prefer the hardest paper the panel can genuinely reach in full text. A bar that is too easy exits the loop on round one.

### 3. Freeze the core

Two files, written before round one. Both are the author's own words, and neither is the loop's to edit — in any setting, including the ones where the author does the revising themselves.

`gauntlet/FROZEN.md` freezes the **analysis**:

- The headline specification — estimator, DV, treatment, sample, fixed effects, clustering.
- The table or figure that *is* the paper's claim.
- The claim itself, in one sentence, with its sign and rough magnitude.

`gauntlet/CLAIMS.md` freezes the **meaning** — what the paper asserts, its causal register, the population, the scope conditions, the mechanism, the contribution, and the nearby claims it explicitly does *not* make. Template in `references/change-tracking.md`. Every round, a separate agent re-derives the claim set from the current draft and diffs it against this file; a difference is a consequential change by definition. This is the only mechanical check on whether the paper still says what the author meant, so it has to be in the author's voice — a claim set the loop wrote for itself cannot detect the loop's own drift.

The loop polishes how the paper argues, presents, and defends this result. It does not shop for a better one. If the loop's own work convinces you the frozen spec is wrong, that is a real finding and a reason to stop the loop and rethink the paper — not a reason to edit either file.

### 4. Open the logs

All append-only, all created before round one.

`gauntlet/robustness-ledger.md`, from the template in `references/robustness-ledger.md`. Every check run against the frozen spec is declared in it *before* it runs and reported afterward whether it passes or fails. Read that file before letting any builder touch the data — and before running a check yourself, if the checks are yours.

`gauntlet/CHANGELOG.md`, from `references/change-tracking.md`. Every consequential change to the analysis or the prose, by either party, with what changed, why, and what it was before.

`gauntlet/TASKS.md`, in split and referee-only, from `references/who-does-the-work.md`. One entry per objection, with its owner and its state.

### 5. Verify the replication package

Before round one, confirm the package runs end to end from raw data and that every number in every table traces to code output. If it does not, fix that first. A gauntlet on a paper whose tables do not reproduce is polishing a wrong answer.

## Decomposition: objection classes

Split the paper into these, not into intro/theory/data/results. Each gets its own reviser and its own referee panel, and each loops independently. Who the reviser is — the loop, the author, or both — is set per track in step 1 and does not change the decomposition.

| Piece | The objection it has to survive |
|---|---|
| **Contribution** | What does a referee at this journal learn that they did not already know from the papers you cite? |
| **Theory and mechanism** | Who are the actors, what is the causal story, does it address supply and opportunity or only demand, are the scope conditions justified rather than asserted? |
| **Identification** | Does the design support a causal claim, or is the paper making one the design cannot carry? TWFE under staggered or time-varying treatment, IV exclusion restrictions, selection into treatment, reverse causality. |
| **Measurement** | Does the operationalization measure the concept, and does the paper show that rather than assert it? |
| **Alternative explanations** | What else generates this exact pattern, and is it ruled out or merely unmentioned? |
| **Inference and power** | Interactions estimated off thin support, rare events, clustering, multiple comparisons, non-proportional hazards, what happens to power as moderators enter. |
| **Presentation** | Tables, figures, marginal-effects plots over the observed range of the moderator, and the prose. |

Contribution and identification are where top-5 papers actually get rejected. Weight the loop accordingly. Presentation is the cheapest to win and should not be mistaken for progress.

## The referee panel

Full protocol in `references/referee-panel.md`. The short version:

- **Two independent referees per comparison**, from different model families where you can reach them. Cross-vendor is the point — two referees from the same family agree with each other for reasons that have nothing to do with the manuscript. If only one family is reachable, say so in the run notes and treat a win as weaker evidence.
- **Fresh context every round.** The referee never learns how many rounds have run, how hard the reviser tried, or whether the reviser was the loop or the author. A referee told a human wrote this paragraph grades it differently, in both directions.
- **Binary job.** Blind, labels stripped: which of these two would you recommend for R&R at [JOURNAL]? Plus the single most damaging objection to the one it would reject. No scores — scores drift upward every round.
- **Order swapped, run twice.** Judges favor whichever manuscript comes first. A win requires both referees at both orderings. Four comparisons, four wins, or it is not a win.
- **A third referee auditing for specification search.** It reads the ledger, not the prose, and answers one question: was the headline result chosen because it is right, or because it survived?

## Keeping the author informed

On hands off the loop never pauses to ask. On split it pauses only where the routing tells it to. Neither setting asks forty times, because an author asked forty times approves forty times without reading — and that is true of the questions the author chose to be asked as much as of the ones the loop invented. What follows is how the loop pays for the questions it does not ask. Full protocol in `references/change-tracking.md`. The shape of it:

**A separate classifier triages every accepted change** into CLAIM (changes what the paper asserts), SUBSTANTIVE (hedges, new checks, reframing, deleted authored text), or ROUTINE. Not the builder — the builder has an interest in calling its own work minor, exactly as it has an interest in judging its own quality. Nor the author, who has the same interest in their own revisions and rather more practice at it. When unsure between two levels, the classifier takes the higher one.

**Three standing rules replace the gate.** Each turns a decision the author would have made into one the loop can make safely alone. They bind the loop, not the author — an author who takes the stronger claim on their own track is exercising judgment, and the changelog records it as theirs. Rule 3 is the exception and binds everybody.

1. *Never strengthen a claim.* Where a change would alter what the paper asserts, take the weaker, more hedged, more narrowly scoped form and flag it. This settles the failed-check case too: a check that fails bounds the claim to where it holds. Bounding down needs no permission; bounding up would.
2. *Never delete authored text without preserving it verbatim* in the changelog entry.
3. *Never add a citation without an inline `[UNVERIFIED]` marker* that stays until the author confirms they have read it. The author is accountable for every reference in the paper, and a log entry is not enough protection — the flag belongs in the document.

**Markers are the one genuinely blocking thing.** CLAIM-level changes and new citations leave a marker at the exact location in the manuscript, and the paper is not submittable while any marker remains. Clearing them is the author's obligatory work, and it is proportional to how much the loop actually changed. On hands off they accumulate and the author clears them at the end; on split a marker on a task they approved or performed clears then and there. `[UNVERIFIED]` clears one way only, in every setting: the author reads the work.

**None of this switches off in split.** An author present for some of the decisions does not make a record of the rest unnecessary, and their own edits go through the same classifier and the same changelog. The claims diff is a check on the paper, not on the loop, and authors drift their own papers.

**The run ends with a handoff brief, not a verdict.** `gauntlet/HANDOFF.md`: the claims diff first, then CLAIM-level changes ordered by how much they moved the paper, open markers, failed checks and how each bounded the paper, and the objections that were still live when each track dried up. Ordered by risk, not chronology.

## When the work is split

Full protocol in `references/who-does-the-work.md`. Four things about it are load-bearing.

**Routing is per track and set once**, in `gauntlet/ROUTING.md`, with `ask` available for the tracks where the two kinds of objection are genuinely mixed — a paragraph that reads badly and a mechanism with no actors in it arrive looking the same. Per-task prompting on all seven tracks is how you get to forty unread approvals. Two `ask` tracks, not seven.

**A parked track parks alone.** The other six keep running, which is what the decomposition buys and the reason split is not just a slower hands off. When every track is exited or parked, the loop says so once and waits. It does not remind — the queue is on the dashboard.

**Work the author does goes through the same machinery**: the classifier, the changelog, the claims diff, and then the panel, blind, in the usual four comparisons. Their edits are classified at the same three levels as the loop's.

**The queue is `gauntlet/TASKS.md`**, append-only, one entry per objection, closed rather than deleted. A task the author declines closes with a reason. One the design cannot answer closes to the limitations section, which is the exit identification and measurement already have.

## Letting the loop run robustness checks

This is the part that makes the adaptation dangerous and the part the ledger exists for. The rules are not optional.

1. **Declare before running.** Whoever runs the check writes it into the ledger first — what it is, which referee objection demands it, and what result would count as a failure. A check declared after seeing its result is not a robustness check.
2. **Report regardless of outcome.** Every declared check appears in the paper or its appendix with its actual result. Nothing is ever removed from the ledger.
3. **Never re-headline.** A check that overturns the frozen result gets reported and discussed. It does not become the new main specification.
4. **One preferred form per check family.** Declare which variant is the one you would defend, then run it. Running more variants of the same family is allowed only if every variant is in the ledger, with its result.
5. **A failed check is bounded, not buried.** The permitted responses are: report it and narrow the paper's claim, or diagnose why it fails and report the diagnosis. Not: keep going until something passes.

If the ledger and the appendix ever disagree, the ledger is right and the paper is wrong.

## The dashboard

The run publishes one page and keeps republishing it to the same URL. Full spec in `references/progress-dashboard.md`. Three things about it are not negotiable.

**Every panel is generated from a file on disk** (`CLAIMS.md`, the ledger, the changelog, the queue, track state), never from the loop's own account of how the run is going. A dashboard the loop writes about itself is a status report from the party with an interest in the answer.

**Running dry never renders as winning.** They are different exits and they mean different things, so they get different words and different colours, with the round count beside each. The panel that matters most is the claims diff, which goes first; the panel most easily scrolled past is the list of objections nobody could answer, which is what a real referee will raise, so it gets a heading that stops the author.

**Parked never renders as running.** A track waiting on the author is not a track in progress; nothing is happening on it and nothing will until they act. It carries their name and the date it parked, and on split the page republishes when a track parks rather than only when a round completes — it is where the author finds out there is something waiting.

No percentages anywhere. There is no denominator.

## Exit conditions

Different pieces exit differently, and pretending otherwise is how the loop lies to you.

- **Presentation, exposition, robustness completeness** — exit on winning the blind panel four-for-four. These are genuinely winnable against a published paper.
- **Contribution** — do not expect to win. That paper's contribution took someone three years. Exit instead on **dry-up**: two consecutive rounds in which neither referee names a *new* objection that would block an R&R. Repeated objections do not reset the counter; a new one does.
- **Identification and measurement** — dry-up as well, with a floor: any objection the panel raises that the design genuinely cannot answer gets written into the paper's limitations rather than looped on. Loop on what can be fixed. Disclose what cannot.

**A parked track has not exited.** Waiting on the author is a state, not a result, and it renders as its own thing on the dashboard for that reason. A track routed to the author and never worked is an unfinished track. Say so at the end rather than quietly counting it as dry.

**Hard gates, all pieces.** The loop cannot exit while any of these is false: the replication package runs clean from raw data, every reported number traces to code output, the ledger has zero declared-but-unreported entries, and every task in the queue is closed.

Never exit on a round count.

**And the loop's exit is not the paper's.** "Every track has hit its exit condition" means there is nothing left for the loop to do. It does not mean the paper is ready. Submission is an authorial act: the author clears the handoff brief and the open markers, and that gate belongs to them. The loop reaches done. Only the author reaches ready.

## The prompt

The skill's output is one paste-ready prompt, as in the original. Keep it short. The protocol lives in the repo files, so the prompt points at them rather than restating them.

```
Polish [MANUSCRIPT] for submission to [JOURNAL].

The bar is [BAR PAPER], published there. Get the full text and compare against the paper itself, not against a description of it.

Read gauntlet/FROZEN.md, gauntlet/CLAIMS.md, gauntlet/ROUTING.md, and the skill's references/ before you start. The headline result and the claim set are frozen. You may add robustness checks; declare each one in the ledger before you run it and report it whether it passes or fails.

[WHO DOES THE WORK]

Log every consequential change to gauntlet/CHANGELOG.md, whoever made it, take the weaker form of any claim rather than the stronger one, and leave a marker in the draft wherever you change what the paper asserts or add a citation. Finish with a handoff brief.

Break the paper into referee objections, not sections - contribution, theory, identification, measurement, alternative explanations, inference, presentation. For each, fan out a referee panel with fresh context, and a reviser wherever the routing gives you one. The panel reads ours and the bar blind with identifying material stripped, says which one it would recommend for R&R at [JOURNAL], and names the single most damaging remaining objection. Then the objection goes back for the next revision.

The referees should be harsh. Praise is not useful. Two models, both orderings, four wins or it is not a win.

/loop on each piece until it hits its exit condition in the skill. Do not stop before that.

Publish a live dashboard as an artifact and republish it to the same URL after every round, following references/progress-dashboard.md. Generate every panel from the files on disk rather than from your own summary of how the run is going.

Fan out subagents and ultracode.
```

Replace `[WHO DOES THE WORK]` with the one line that matches `gauntlet/ROUTING.md`.

**Hands off.**

```
Never stop to ask me anything. Do all the revising yourself.
```

**Split.**

```
Follow the routing in gauntlet/ROUTING.md. On my tracks, write the objection into
gauntlet/TASKS.md with what answering it would take, and park the track. On yours,
revise and log. On an ask track, put the objection to me in one screen and wait for
one word. Keep the other tracks running while one is parked, and when every track
is exited or parked, say so once and wait. Classify my edits the way you classify
your own.
```

**Referee only.**

```
Do not edit the manuscript. Run the panel, write every objection into
gauntlet/TASKS.md with what answering it would take, and park. I do the revising
and hand it back for the next comparison. Classify my edits the way you would
classify your own.
```

Fill the remaining brackets. Add a cost ceiling only if the user named one. Do not add file layout, decomposition detail, or a round count — those are in the skill or they are the agent's to decide.

## What breaks this loop

- **Using the reviewer model as the bar.** Then there is no bar, and the loop terminates whenever the model feels generous.
- **A bar paper the referees recognize.** They know which one is the published APSR paper and pick it, or pick against it out of contrarianism. Either way the comparison is noise. Post-cutoff bar papers and hard blinding, every round.
- **Editing FROZEN.md.** The moment the frozen spec becomes negotiable, the loop is a p-hacking engine with good manners.
- **Same-family referees.** Correlated referees are one referee with extra steps.
- **Treating dry-up as a win.** Two rounds without a new objection means the panel is out of ideas. It does not mean the paper is at APSR standard. Read the accumulated objections yourself before you submit.
- **Letting presentation wins stand in for substance.** The loop will win prose comparisons early and often. That is not the paper getting better.
- **A CLAIMS.md the loop wrote.** The claims diff only detects drift because the reference was written by the author before the run. Generated from the draft, it drifts along with it and detects nothing.
- **Routing everything to the author.** Five tracks parked on Monday and they are revising the paper alone again, now with a dashboard watching them not do it. An unopened queue is worse than hands off, because it looks like progress. Route what gets done this week.
- **Reading the setting as a quality dial.** Hands off is not the sloppy one and referee only is not the rigorous one. The bar, the freeze, the ledger, the panel and the exits do not move between them. What moves is who writes and what the author has to disclose.
- **Reading the handoff brief as a summary.** It is a list of decisions made on the author's behalf. Every CLAIM entry the loop made alone is a place where it chose and the author did not.
