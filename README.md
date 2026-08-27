# Social Science Gauntlet

A gauntlet loop for empirical social science manuscripts being polished for a top-5 journal.

Same engine as the original: a real bar, small judgeable pieces, a builder and a separate harsh critic on each, blind comparison, loop until it wins. Three things change, and they are the whole adaptation.

## What changes

**The reviewer model is the critic, never the bar.** The obvious way to do this — "loop until Fable 5 and GPT-5.6 Sol say the paper is strong" — is the exact failure the original skill is built to avoid. It is a rubric wearing a referee's coat, and frontier models will find something admirable in almost any competent manuscript. So the bar stays a real artifact: a specific paper published in the journal you are actually targeting. The reviewer models become the referee panel, and their job stays binary — blind, labels stripped, which of these two would you recommend for R&R at *this* journal.

**The pieces are referee objections, not paper sections.** For a landing page the pieces are hero, motion, type, mobile. The obvious port is intro / theory / data / results, and it is wrong, because that is not how a paper dies. Papers die on objections. The loop splits into contribution, theory and mechanism, identification, measurement, alternative explanations, inference and power, and presentation — each with its own builder, its own referee profile, and its own exit.

**The empirical core is frozen and the robustness work is logged.** A loop pointed at "make the referee stop objecting" is a specification-search engine. If the referee says the effect is not robust, the cheapest path to a win is finding a spec where it is. So the headline result is frozen before round one, and every robustness check the loop runs is declared in an append-only ledger *before* it runs — with its failure criterion written in advance — and reported afterward whether it passes or fails. A third referee audits the ledger for search patterns and never sees the prose.

## Exit conditions

Presentation and exposition are genuinely winnable against a published paper, and exit on a four-for-four blind panel win. Contribution is not — that paper's contribution took someone three years — and exits on dry-up instead: two consecutive rounds where neither referee names a *new* blocking objection. Identification and measurement dry up too, with a floor: objections the design genuinely cannot answer go into the limitations section rather than into another round.

Nothing exits while the replication package fails to run, a reported number does not trace to code output, or the ledger has a declared check that appears nowhere in the manuscript.

## Install

```
cp -r .claude/skills/social-science-gauntlet your-project/.claude/skills/
```

Then:

```
/social-science-gauntlet polish this manuscript for AJPS
```

It offers you two or three candidate bar papers, you pick one, and it sets up `gauntlet/FROZEN.md` and `gauntlet/robustness-ledger.md` and hands back one prompt to paste into a fresh session.

## What's included

```
.claude/skills/social-science-gauntlet/
├── SKILL.md                        # the loop: setup, decomposition, exits, the prompt
└── references/
    ├── referee-panel.md            # blinding, cross-vendor panel, order swaps, referee prompts, objection library
    └── robustness-ledger.md        # the append-only ledger, its rules, worked pass and fail examples
README.md
LICENSE                             # CC BY 4.0
```

## Scope

Built for polishing a draft that already exists and already has results. Not for a project at the design stage — the freeze has to happen at pre-analysis time there, which is a different workflow and should be a different skill.

## What breaks it

- **Using the reviewer model as the bar.** Then there is no bar, and the loop ends whenever the model feels generous.
- **A bar paper the referees recognize.** The published paper is probably in their training data. A model that recognizes it retrieves a verdict instead of forming one. Post-cutoff bar papers, hard blinding, and a recognition probe every run.
- **Editing the frozen spec.** The moment it is negotiable, the loop is a p-hacking engine with good manners.
- **Same-family referees.** Correlated referees are one referee with extra steps.
- **Reading dry-up as a win.** Two rounds without a new objection means the panel is out of ideas, not that the paper clears the bar.

## Credit

The gauntlet loop technique is **[Matt Shumer's](https://github.com/mshumer)** — the harsh critic, the blind comparison, the refusal to stop until the work wins all come from the [original prompt](https://github.com/mshumer/Claude-of-Duty/blob/main/prompt.md) he wrote for [Claude of Duty](https://github.com/mshumer/Claude-of-Duty).

This repo is an adaptation of **[gauntlet-loop](https://github.com/robonuggets/gauntlet-loop)** by Jay E at [RoboNuggets](https://robonuggets.com), which packaged that technique as a reusable skill. Modified here for empirical social science: reviewer models moved from bar to critic, objection-based decomposition, the frozen core and the robustness ledger, split exit conditions, and the blinding protocol for training-data contamination.

## License

CC BY 4.0, inherited from the original. Free to use with attribution.
