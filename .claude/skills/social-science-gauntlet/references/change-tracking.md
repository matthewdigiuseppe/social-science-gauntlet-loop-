# Tracking consequential changes

The loop never stops to ask. That is a deliberate choice, and it has a cost: decisions that are properly the author's get made by the loop while the author is not watching. This file is how that cost is paid rather than ignored.

Three parts. A record of what changed and why. Three standing rules that make the loop's unsupervised choices safe by construction. And markers left in the manuscript itself for the things the author must personally sign off before submission.

## What counts as consequential

A separate classifier agent triages every accepted change. It is not the builder — the builder has an interest in calling its own work minor, exactly as it has an interest in judging its own quality. Fresh context, one job.

| Level | What it covers | Where it lands |
|---|---|---|
| **CLAIM** | Anything that changes what the paper asserts: sign, magnitude, the population it generalises to, the causal register ("causes" vs "is associated with"), scope conditions, the contribution statement, a hypothesis added or dropped, how the paper positions against a cited literature | Changelog entry **and** an in-document marker |
| **SUBSTANTIVE** | Hedge changes, a new robustness check, reframing of the mechanism, restructured tables or figures, any deletion of text the author wrote | Changelog entry |
| **ROUTINE** | Typos, formatting, reference style, table alignment | Git commit only |

When the classifier is unsure which of two levels applies, it takes the higher one. An over-flagged routine change costs the author ten seconds. An under-flagged claim change costs them a paper they cannot defend.

## The three standing rules

These replace the blocking gate. Each one turns a decision the author would have made into a decision the loop can make safely on its own.

**1. Never strengthen a claim.** When a change would alter what the paper asserts, the loop takes the weaker, more hedged, more narrowly scoped form and flags it. "Is consistent with" does not become "shows". A finding about middle-income democracies does not quietly become a finding about states. Weakening on its own is safe and reversible by the author in one edit; strengthening is neither.

This also settles the failed-check case cleanly. When a declared robustness check fails, the loop bounds the claim to the range where it holds and records the bound. It does not drop the check, and it does not leave the broad claim standing. Bounding down needs no permission; bounding up would.

**2. Never delete authored text without preserving it.** Any sentence the author wrote that the loop removes or rewrites goes into the changelog entry verbatim, in full. The author can restore any of it from the record without going back through git.

**3. Never add an unread citation.** Every reference the loop introduces is written into the manuscript with an inline `[UNVERIFIED]` marker directly after it, and stays that way until the author confirms they have read the cited work. The author is professionally accountable for every reference in the paper. A model adding plausible-sounding citations is the most likely way this whole approach embarrasses somebody, and a log entry is not enough protection — the flag has to be in the document where it cannot be skipped.

## In-document markers

CLAIM-level changes and new citations get a marker at the exact location, not just an entry in a file the author may never open:

```
[CLAIM-CHANGED: r14/identification — scope narrowed to post-1990. see changelog]
[UNVERIFIED: Blackwell and Olson 2022]
```

Markers are the one thing that is genuinely blocking, and they block only at the end: **the manuscript is not submittable while any marker remains.** The author clears each one by reading it and either accepting the change or reverting it. That is the whole of the author's obligatory work, and it is proportional to how much the loop actually changed.

## The changelog

`gauntlet/CHANGELOG.md`, append-only like the robustness ledger. One entry per consequential change, newest last.

```markdown
### r14 · identification · CLAIM

**What changed.** The scope of the main finding narrowed from "democracies"
to "democracies since 1990".

**Why.** Round 13 panel objection: the pre-1990 sample has too few treated
observations to support the interaction, and the panel picked the bar on
inference and power.

**Before.** "Across democracies, austerity announcements shift bond spreads
by roughly 18 basis points."

**After.** "Among democracies since 1990, austerity announcements shift bond
spreads by roughly 18 basis points."

**Rule applied.** Rule 1 — weaker form taken without asking.

**Marker.** Section 5.1, first paragraph.
```

For SUBSTANTIVE deletions, the **Before** field carries the removed text in full, however long.

## Git as the audit trail

One commit per accepted change. The message carries the provenance so that `git log --oneline` is a readable history of the run rather than a wall of "update draft":

```
r14 identification CLAIM: narrow main finding to post-1990
r14 identification SUBSTANTIVE: add Callaway-Sant'Anna to appendix
r15 presentation ROUTINE: fix Table 3 column alignment
```

A branch per objection track keeps the tracks separable, so the author can accept the presentation work and reject the theory work without untangling them. Skip this if the manuscript is not already versioned — the changelog stands on its own.

## The handoff brief

The loop's finish line is "nothing left to do", not "ready to submit". When every track has hit its exit condition, the loop writes `gauntlet/HANDOFF.md` and stops. It contains, in this order:

1. **The claims diff.** The claim set derived from the current draft, against `gauntlet/CLAIMS.md` as the author wrote it at setup. Every difference, with the changelog entry that produced it. This is the first thing the author reads and the most important.
2. **Every CLAIM-level entry**, ordered by how much it moved the paper, not by round.
3. **Open markers**, with their locations.
4. **Failed robustness checks** from the ledger, and how each one bounded the paper.
5. **What the panel never stopped objecting to** — the objections that were still live when the track dried up. These are what a real referee will raise, and the author should have an answer ready.
6. **A count of routine changes**, not a list.

Ordered by risk, not chronology. The author reads the top and stops when it stops mattering.

## CLAIMS.md

Written by the author at setup, before round one, alongside `FROZEN.md`. This is the reference the claims diff runs against every round, and it only works if it is in the author's own words — a claim set the loop wrote for itself cannot detect the loop's own drift.

```markdown
# What this paper claims

## The finding
One sentence. Sign, rough magnitude, and the estimator it comes from.

## Causal register
Exactly one of: this paper claims a causal effect / this paper claims an
association and says so. If causal, name the design feature that carries it.

## Population
Who the finding is about, and the period. Be narrower than you want to be.

## Scope conditions
The conditions under which the argument is expected to hold, and why each
one is there.

## Mechanism
The causal story in two or three sentences, naming the actors who make
decisions in it.

## Contribution
What a referee at this journal learns that they did not already know from
[the two or three papers closest to this one].

## What this paper does not claim
The nearby claims a reader might mistake for yours. This section is the one
that catches drift, because drift moves toward these.
```

A derived claim set that differs from this file is a CLAIM-level event, every time, no exceptions. It is the only fully mechanical check on whether the paper still says what the author meant it to say.
