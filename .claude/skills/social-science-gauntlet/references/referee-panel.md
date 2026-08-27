# The referee panel

How to run the critic side of the loop so that a win means something.

## The blinding problem

This is the failure mode with no analogue in the coding version of the gauntlet loop, and it is the one most likely to make a run worthless.

The bar paper is published. It is therefore probably in the referee model's training data. A model that recognizes it is not comparing two manuscripts — it is retrieving a verdict. It may pick the bar because it knows the bar is the real APSR paper, or pick against it because it has learned that the thing being tested is usually the one it is supposed to praise. Both produce a number that looks like a comparison and is not.

Mitigations, in descending order of how much they buy you:

1. **Use a bar paper past the referee models' training cutoff.** Forthcoming, OnlineFirst, or an accepted manuscript posted in the last few months. This is worth more than every other mitigation combined.
2. **Strip the tells before the comparison.** Title page, author names, acknowledgments footnote, funding statement, DOI, journal formatting, running heads, "forthcoming at", self-citations in the first person, and the reference list's formatting conventions. Convert both manuscripts to plain markdown in the same citation style.
3. **Compare at section level, not whole manuscript.** A referee judging "the identification section of A vs the identification section of B" has less surface area to recognize than one reading two full papers. It also matches the objection-based decomposition, so do it anyway.
4. **Match length.** Trim or pad to comparable word counts before comparing. Judges prefer longer and more citation-dense text independent of quality, and a 12,000-word published paper against your 9,000-word section is a length test, not a quality test.
5. **Probe for recognition.** Once per run, ask each referee, in a separate fresh context, whether it recognizes either manuscript and what it thinks they are. If it names the bar paper, that referee's verdicts for this run are suspect. Log the answer.

If you cannot get a post-cutoff bar paper, the loop is still useful — the objections the panel raises are real feedback regardless. But treat the blind win as unearned and exit on dry-up instead.

## Composition

Two referees per comparison, from different model families. Cross-vendor is the design requirement, not a nicety: two referees from the same family share training data, refusal patterns, and taste, so their agreement carries far less information than it appears to.

If only one family is reachable in your setup, run two referees from that family with deliberately different prompts (one methodologist, one area specialist), note the limitation in the run log, and lean on dry-up rather than blind wins as the exit.

Each referee gets fresh context every round. It never sees prior rounds, prior verdicts, the ledger, or any indication of how much work has gone in. A referee that knows the builder is on round eleven starts being kind.

## Order and repetition

Position bias is large and consistent in LLM judges. Every comparison runs four times:

| Run | Referee | Order |
|---|---|---|
| 1 | Model A | ours first |
| 2 | Model A | bar first |
| 3 | Model B | ours first |
| 4 | Model B | bar first |

A win is four wins. Three out of four is not a win; it is a coin flip with one referee showing position bias. Log all four verdicts, not the tally.

Disagreement between the two models is itself the finding. When Model A picks ours and Model B picks the bar, the contested thing they name is almost always the paper's actual weak point. Route it straight to the builder.

## The referee prompt

Keep it binary. Scores out of ten drift upward every round because each round genuinely is a little better than the last, and the scale has nowhere to go but up.

```
You are refereeing for [JOURNAL]. Below are two manuscripts, A and B, at the
same stage and on comparable topics. Identifying information has been removed
from both.

Read the [OBJECTION CLASS] portion of each.

Answer three things, briefly:

1. Which one would you recommend for R&R at [JOURNAL] — A or B? Pick one. You
   may not say both, neither, or that it depends.
2. What is the single most damaging objection to the one you would not
   recommend? One objection, the one that would actually block publication,
   not a list.
3. Independent of the comparison, what is your verdict on A alone: desk
   reject, reject, R&R, or accept?

Be harsh. [JOURNAL] rejects roughly ninety percent of what it receives at
desk. Praise is not useful here. If you find yourself writing that both are
strong, you have not found the objection yet.
```

Swap A and B between runs. Item 3 uses whichever manuscript is ours in that run — track which is which outside the prompt, never inside it.

## Objection library

Give the methodologist referee this list as a checklist for the identification, inference, and measurement pieces. It is drawn from what actually gets raised against observational IR/IPE papers at this tier.

**Identification**
- Two-way fixed effects with staggered or time-varying treatment. TWFE is hard to justify for a causal target; the estimator needs to match the design.
- IV exclusion restrictions asserted rather than argued.
- Selection into treatment unaddressed, or addressed only with controls.
- Reverse causality where the theory itself implies feedback.
- Within-country variation too thin to carry country fixed effects.

**Inference and power**
- Interaction effects estimated off very few observations at one end of the moderator. Does support exist across the moderator's range?
- What happens to power as successive moderators enter.
- Confounding on the moderator, not just on the treatment (Blackwell and Olson 2022).
- Marginal effects presented as a single coefficient rather than over the observed range (Hainmueller, Mummolo and Xu 2019 / Interflex).
- Rare events, clustering, and multiple comparisons across a table of many specifications.
- Non-proportional hazards in survival models (Licht 2011).

**Theory**
- The theory addresses demand but not supply or opportunity.
- Scope conditions asserted rather than justified.
- The mechanism has no actors — nobody in the theory makes a decision.
- An alternative theoretical story generates the same empirical pattern and is not addressed.

**Contribution**
- The finding is a marginal empirical extension of a cited paper.
- The link between the specific outcome measured and the broad concept claimed is too weak to carry the framing.

## The specification-search auditor

A third referee, run once per round, that never sees the manuscript's prose. It sees `gauntlet/FROZEN.md` and the full `gauntlet/robustness-ledger.md`, including every entry that failed.

```
Below is a frozen headline specification and a complete, append-only log of
every robustness check run against it, including failures.

Answer:

1. Does the pattern of checks look like a good-faith attempt to break the
   result, or like a search for specifications that preserve it?
2. Is any check family represented by many variants where only some are
   reported in the paper?
3. Was any check declared after its result was already known? Look for
   declarations whose stated failure criterion could only have been written
   by someone who already knew the answer.
4. Given only this ledger, would you believe the headline result?
```

If the auditor flags a search pattern, that is a stop-the-loop event, not a builder task. Bring it to the author.
