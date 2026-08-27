# Social Science Gauntlet

**A gauntlet loop for empirical social science papers, where the bar is a paper that actually got published in the journal you're aiming at.**

You have a finished manuscript and you want to know whether it clears the bar at a top-5 journal — before you send it, not four months later in a rejection letter.

> It races your draft against a paper that actually got into the journal you're targeting, blind, judged by AI referees from two different companies — and keeps revising until it wins, or until the referees stop finding new problems.

📄 **[Read the full illustrated explainer →](https://matthewdigiuseppe.github.io/social-science-gauntlet-loop-/)**

---

## The shape of the thing

Four setup steps that happen once, then a cycle that runs separately on each of seven tracks. The tracks are the objections that actually kill papers — not the sections a paper is organised into. Nobody rejects a manuscript for having a weak Section 3.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/img/01-the-loop-dark.svg">
  <img alt="Process diagram: four setup steps run once — pick the bar, freeze the analysis and the claims, open the ledger and the changelog, check the code runs. The manuscript is then split into seven objection tracks, and each track runs a cycle: a builder revises the track, labels are stripped from both it and the bar paper, a referee panel of two models at two orderings picks one, and the objection goes back to the builder until the track exits." src="docs/img/01-the-loop-light.svg">
</picture>

The builder never judges its own work. The panel is a separate set of models with no memory of previous rounds and no idea how hard the builder tried. A win means all four comparisons: two models, each shown the pair in both orders, because AI judges reliably favour whichever manuscript they see first. Three out of four is position bias, not a win.

## Why a published paper, and not a rubric

The obvious version of this is to hand your draft to a smart model and ask whether it's good enough for AJPS. That fails, and it's worth being precise about why: the model grades you against a standard it invented on the spot, and it wants to be helpful. Revise, ask again, and it says the draft is stronger now. The standard climbs with you.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/img/02-bar-vs-rubric-dark.svg">
  <img alt="Two line charts. On the left, asking a model if the draft is good: draft quality rises over rounds and the model's standard rises alongside it, staying just above, so the two lines never cross. On the right, racing a published paper: the bar is a flat horizontal line that does not move, and the rising draft line eventually crosses it, which is the exit." src="docs/img/02-bar-vs-rubric-light.svg">
</picture>

On the left there is no round at which the draft can fail, which means there is no round at which you learn anything. On the right the comparison is fixed before the first round and the draft either crosses it or doesn't. It's the difference between asking a coach whether you're fast and racing someone who made the Olympic team.

## The part that stops it cheating

If you tell an AI to keep working until the referee stops complaining, and the referee complains that your result isn't robust, the cheapest way to make that complaint disappear is to find a version of the analysis where the result holds. That is p-hacking, automated and tireless. So the loop is allowed to run robustness checks, but only through a gate.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/img/03-the-ledger-dark.svg">
  <img alt="The robustness ledger. A referee objection leads to a ledger entry stating what the check is, which objection it answers, the exact specification, and what result would count as failing. That entry is committed before any code runs, marked by a vertical commit line. Only then is the check run. Whether it passes or fails, both paths converge on the same outcome: reported in the paper. A dashed path from the failure back to trying another variant is crossed out, because it would have to cross the commit line backwards. A spec-search auditor reads only the ledger, never the paper." src="docs/img/03-the-ledger-light.svg">
</picture>

The idea underneath it: **a robustness check is only evidence if it could have come out badly and you'd have reported it anyway.** Writing the failure line in advance is what makes that true rather than merely claimed. Both branches end at the same box — pass and fail are reported identically — and a separate auditor reads only the log, including every entry that failed, and answers one question: does this look like someone honestly trying to break their result, or someone shopping for one that survives?

Worth saying out loud: this is arguably *more* honest than how most of us work by hand. Nobody keeps a record of the checks that never made it into the appendix.

## It never stops to ask you

A run that halts every time it touches a claim is a run nobody finishes, and an author asked forty times will approve forty times without reading. So the loop doesn't ask. It pays the cost three other ways.

A separate classifier triages every accepted change into one that alters what the paper **claims**, one that's **substantive** but doesn't, and one that's **routine** — not the builder, which has an interest in calling its own work minor. Then three standing rules make the loop's unsupervised choices safe by construction:

| Rule | Why |
|---|---|
| **Never strengthen a claim** | Where a change would alter what the paper asserts, it takes the weaker, more hedged, more narrowly scoped form. This settles failed robustness checks too: a check that fails narrows the claim to where it holds. Bounding down needs no permission — bounding up would. |
| **Never delete your words silently** | Any sentence you wrote that the loop cuts or rewrites is preserved verbatim in the changelog, in full. |
| **Never add a citation you haven't read** | Every reference the loop introduces carries an inline `[UNVERIFIED]` marker until you confirm you've read the work. You're accountable for every reference in the paper. |

Claim-level changes leave a marker at the exact spot in the manuscript, and **the paper isn't submittable while any marker remains**. The run finishes with a handoff brief — the claims diff first, then claim-level changes ordered by how far they moved the paper, open markers, failed checks, and the objections that were still live when each track ran dry.

## When it stops

Three different finish lines, because pretending there's one would be a lie.

| Track | How it ends |
|---|---|
| Writing, tables, figures | When your version beats the published paper, four out of four. Genuinely winnable — you can out-present a paper that's already in print. |
| Contribution | It will never beat a published paper's contribution; that took someone three years. Ends when two consecutive rounds pass without a *new* objection. |
| Identification, measurement | Same running-dry rule, with a floor: an objection your design genuinely cannot answer goes into the limitations section, not into another round. |
| Every track | Nothing ends while the replication code fails to run, a table number doesn't match the code, or a declared check is missing from the manuscript. |
| **And then you** | "Every track has hit its exit" means there's nothing left for the loop to do. It does not mean the paper is ready. The loop reaches *done*. Only you reach *ready*. |

## Say the limits out loud

- **The comparison paper may already be memorised.** If the AI recognises the published paper, it isn't comparing two manuscripts — it's remembering which one is famous. Use papers published after the models' training cutoff, and probe each referee once per run.
- **Two referees from one company are one referee.** Models from the same family share training data and taste. The panel is deliberately cross-vendor.
- **Running dry is not passing.** Two rounds without a new objection means the machine is out of ideas, not that you have a top-5 paper.

It doesn't predict whether you'll get in, it doesn't replace a human referee, and it can't make a boring finding interesting. What it does is burn through the obvious objections before a real referee reaches them, with machinery that makes it hard to fool yourself along the way.

## Install

```bash
cp -r .claude/skills/social-science-gauntlet your-project/.claude/skills/
```

Then:

```
/social-science-gauntlet polish this manuscript for AJPS
```

It offers you two or three candidate bar papers, you pick one, and it sets up the four files the run depends on before handing back a single prompt to paste into a fresh session.

## What's included

```
.claude/skills/social-science-gauntlet/
├── SKILL.md                      # the loop: setup, decomposition, exits, the prompt
└── references/
    ├── referee-panel.md          # blinding, cross-vendor panel, order swaps, referee prompts, objection library
    ├── robustness-ledger.md      # the append-only ledger, its rules, worked pass and fail examples
    └── change-tracking.md        # severity levels, the three standing rules, markers, CLAIMS.md, the handoff brief
docs/                             # the illustrated explainer, served by GitHub Pages
```

The run creates four files in the manuscript's repo: `FROZEN.md` (the analysis), `CLAIMS.md` (what the paper asserts — in your words, before round one), `robustness-ledger.md`, and `CHANGELOG.md`.

## Scope

Built for polishing a draft that already exists and already has results. Not for a project at the design stage — the freeze has to happen at pre-analysis time there, which is a different workflow and should be a different skill.

## Credit

The gauntlet loop technique is **[Matt Shumer's](https://github.com/mshumer)** — the harsh critic, the blind comparison, the refusal to stop until the work wins all come from the [original prompt](https://github.com/mshumer/Claude-of-Duty/blob/main/prompt.md) he wrote for [Claude of Duty](https://github.com/mshumer/Claude-of-Duty).

This repo adapts **[gauntlet-loop](https://github.com/robonuggets/gauntlet-loop)** by Jay E at [RoboNuggets](https://robonuggets.com), which packaged that technique as a reusable skill. Modified for empirical social science: reviewer models moved from bar to critic, decomposition by referee objection, the frozen core and the robustness ledger, non-blocking change tracking, split exit conditions, and a blinding protocol for training-data contamination.

## License

CC BY 4.0, inherited from the original. Free to use with attribution.
