<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="docs/img/banner-dark.svg">
    <img alt="Social Science Gauntlet. Your draft and a paper that already got into the journal both have their names stripped off, then two AI referees from two companies each pick one, and the single objection that would block yours goes back for another revision." src="docs/img/banner-light.svg" width="100%">
  </picture>
</p>

# Social Science Gauntlet

**Hear what your referees are going to say, before you submit.**

You send a paper to APSR. Four months later three reports come back, and two of them raise something you could have fixed in an afternoon if anyone had told you.

This is a way to hear those objections first. An AI reads your paper the way a referee would, over and over, and compares it against a paper that already got into the journal you are aiming at. Names stripped off both. It has to pick one. If it picks the published paper, it names the single biggest reason, your paper gets revised, and it goes again.

What you get back is a revised draft, a list of every change that touched a claim, and a list of the objections it could not answer. That last list is what your actual referees are going to say.

You decide how much of the revising it does. It can do all of it while you are asleep, it can hand you each objection and wait, or it can never touch your prose at all and just tell you what is wrong with it.

📄 **[The illustrated version, with diagrams →](https://matthewdigiuseppe.github.io/social-science-gauntlet-loop-/)**

---

## Is this cheating?

Everybody asks this first, so here is the straight answer.

**The loop cannot touch your results.** Before it starts, you write your headline specification into a file it is forbidden to edit: estimator, sample, dependent variable, treatment, fixed effects, clustering. That stays frozen for the whole run. The loop revises how the paper argues, explains and presents. It does not go looking for a better result.

It *can* run robustness checks, and that is where the real danger sits. If a referee says the effect is not robust, the easy way to make the complaint go away is to hunt for a specification where it holds. So every check gets written down before it runs, including what result would count as failing, and every check that gets written down appears in the paper whether it passed or not. Nothing is quietly dropped. A separate auditor reads that log and asks one question: does this look like someone trying to break their result, or someone shopping for one that survives?

My honest view is that this is more disciplined than how most of us work by hand. You run a check in Stata at eleven at night, it comes out badly, you try a different one, and nothing anywhere records that. Here it does.

And if what bothers you is having a model write your sentences rather than having it near your data, there is a setting where it never touches the manuscript. It referees, it objects, it audits the log, and every word of the revision is yours. Same bar, same panel, same rules.

You should still disclose it. Most journals now have a policy on AI assistance. Follow it, and say plainly that the analyses and the reported specification were fixed in advance and are unchanged.

## Why not just ask ChatGPT if it is any good

Because it will say yes.

Hand a good model your draft and ask whether it is ready for AJPS, and it will tell you the paper is strong, give you a page of feedback, and mean every word of it. Revise, ask again, and now the draft is stronger. The standard climbs with you. Nothing can ever fail, and a test nothing can fail teaches you nothing.

Put a published paper on the other side of the comparison and the standard stops moving.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/img/02-bar-vs-rubric-dark.svg">
  <img alt="Two line charts. On the left, asking a model if the draft is good: draft quality rises over rounds and the model's standard rises alongside it, staying just above, so the two lines never cross. On the right, racing a published paper: the bar is a flat horizontal line that does not move, and the rising draft line eventually crosses it." src="docs/img/02-bar-vs-rubric-light.svg">
</picture>

Ask a coach whether you are fast and you get an opinion. Race someone who made the Olympic team and you get a time.

## What actually happens

Your paper gets split seven ways, and each piece is worked on separately until it is finished.

The seven pieces are the objections that kill papers. I have written enough referee reports to know that nothing dies of a weak Section 3. Papers die because the identification strategy will not carry the causal claim, or because the referee already knew the finding from something you cite. So the split follows those lines instead of the section headings.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/img/01-the-loop-dark.svg">
  <img alt="Process diagram: five setup steps run once, beginning with deciding who does the revising, then the manuscript is split into seven objection tracks. Each track runs a cycle: you or the loop revises the piece, names are stripped from both it and the published comparison paper, two AI referees at two orderings pick one, and the objection goes back for another revision until the piece is finished." src="docs/img/01-the-loop-light.svg">
</picture>

Two AI referees see your piece and the published paper side by side with the names stripped off, and each has to pick one. Every comparison runs four times, both referees at both orderings, because whoever is shown first tends to win. All four, or it does not count. Whoever did the revising never gets to judge it.

**It knows the objections you would raise yourself.** The methodological referee works from a checklist of what actually gets said about observational IR and IPE papers at this tier: two-way fixed effects under staggered or time-varying treatment, exclusion restrictions asserted rather than argued, interactions estimated off a handful of observations at one end of the moderator (Hainmueller, Mummolo and Xu 2019), confounding on the moderator and not just on the treatment (Blackwell and Olson 2022), non-proportional hazards (Licht 2011), within-country variation too thin to carry country fixed effects, and what happens to power as each new moderator goes in.

## How the robustness checks stay honest

Every check is declared before it runs, with its failure line written in advance, and both outcomes lead to the same place.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/img/03-the-ledger-dark.svg">
  <img alt="The robustness log. A referee objection leads to an entry stating what the check is, which objection it answers, the exact specification, and what result would count as failing. That entry is committed before any code runs. Only then is the check run. Whether it passes or fails, both paths converge on the same outcome: reported in the paper. A dashed path from the failure back to trying another variant is crossed out. An auditor reads only the log, never the paper." src="docs/img/03-the-ledger-light.svg">
</picture>

**A robustness check is evidence only if it could have come out badly and you would have reported it anyway.** Writing the failure line in advance is what makes that true rather than merely claimed. Pass and fail land in the same box.

## Who does the work

One setting, chosen before the run starts. It moves who holds the pen and nothing else — the bar, the frozen specification, the log, the referees and the stopping rules are identical in all three, and none of them is the easy option.

| Setting | What it does | Who it suits |
|---|---|---|
| **Hands off** | It revises everything and never asks. You read the handoff brief at the end. | A deadline, and a paper whose prose you are not precious about. |
| **Split** | Every objection becomes a task with an owner. You decide which of the seven pieces are yours and which are its. Yours wait in a queue; it works the rest meanwhile. | Most people, most of the time. |
| **Referee only** | It never writes a word of your paper. It referees, names the objections, keeps the log honest, and hands you all of it. | Anyone who would rather not have a model in their prose, and has the evenings. |

In split you set it per piece, once, before the run. A starting point:

| Piece | Who | Why |
|---|---|---|
| Contribution | you | Nobody can write your contribution claim but you. It is the one thing in the paper you know and the model does not. |
| Theory, identification, measurement | ask me | Sometimes the objection is that a paragraph is unclear, and sometimes it is that your mechanism has no actors in it. They arrive looking the same, and only one of them is the machine's to fix. |
| Alternative explanations | it | It is good at generating these and you have stopped being able to see them, which is what four years on one paper does. |
| Inference and power | it | Under the log, which is what makes this safe to hand over. |
| Presentation | it | This is the one it is straightforwardly better at than you are at eleven at night. |

**Why per piece and not per task.** Because the forty-approvals problem applies to you too. Deciding once, while you are thinking about the paper rather than about a queue, is a better decision than the fortieth one you make at speed. Set two pieces to ask you, not seven.

**A piece waiting on you parks and the other six keep going.** That is what splitting the paper seven ways buys. When everything is either finished or waiting on you, it says so once and stops. It does not nag.

**Your own edits go in the log too**, classified exactly the way its are. Not bookkeeping for its own sake: the check on whether the paper still says what you meant is a diff against what you wrote down at the start, and it does not care who moved the claim. You will drift your own paper. That is most of what a fourth revision is.

**Where this one goes wrong** is routing five pieces to yourself on a Sunday. Come Monday you are revising the paper alone again, only now with a dashboard watching you not do it. Take what you will actually sit down and do this week.

## Either way, it keeps a record

A run that stops to ask permission every time it touches a sentence is a run nobody finishes. Ask an author forty times and you get forty approvals and no reading. So on hands off it never asks, and on split it asks only where you told it to. The rest of the time it keeps a record instead, and it follows three rules that make the decisions it takes on your behalf safe ones.

| Rule | What it means |
|---|---|
| It can weaken a claim, never strengthen one | Where a revision would change what the paper asserts, it takes the more cautious version. "Is consistent with" never becomes "shows". A failed robustness check narrows your claim to where it holds rather than disappearing. Walking a claim back needs no permission from you. Pushing one further would. The rule binds it, not you — strengthen your own claim if you think it is right, and the log will say it was your call. |
| Your sentences are never deleted silently | Anything of yours it cuts or rewrites is kept word for word in the log. You can put any of it back without hunting through version history. |
| New citations are flagged until you read them | Every reference it adds is marked `[UNVERIFIED]` in the draft and stays that way until you confirm you have read the work. You are accountable for every reference in your paper. This is the most likely way the whole approach embarrasses somebody. Approving the task does not clear the flag: saying yes to a citation is not the same act as reading one. |

Anywhere it changes what the paper claims, it leaves a flag at that spot in the document. **The paper is not submittable while any flag is still there.** Clearing them is the work you have to do, and it is proportional to how much actually changed. On hands off they pile up and you work through them at the end. On split they clear as you go, which is the real reason to use split: signing off on a choice you remember making is easier than reconstructing one you were not there for.

At the end you get a handoff brief. What the paper claims now, against what you wrote down at the start. Then the changes that moved it furthest, the open flags, every robustness check that failed and how it narrowed things, and whatever the referees were still objecting to when they ran dry.

That last list is the one to read twice.

## What you actually do

Six steps. Most of your time goes into step two, and it takes about twenty minutes.

1. **Get your files together.** The manuscript and the replication code in one folder. The code has to run from the raw data, because the loop checks that before it starts and traces every number in every table back to output.
2. **Write two short files.** Your headline specification, and what your paper claims, in your own words. The second matters more than it sounds. It is the reference that catches the draft drifting away from what you meant, so if the AI writes it for you it drifts along with the draft and catches nothing.
3. **Say who does the work.** Hands off, split, or referee only. In split, which of the seven pieces are yours.
4. **Pick the bar.** You get two or three suggested papers from your target journal. Pick the one you would least like to be compared against.
5. **Start it.** On hands off you can leave — it does not need you and it will not ask. On the other two, check the dashboard when you have an evening.
6. **Read the handoff brief.** Clear the flags, decide what to keep, decide what to revert.

## When it stops

Different pieces finish differently, and pretending otherwise would be a lie.

| Piece | How it finishes |
|---|---|
| Writing, tables, figures | When your version beats the published paper four times out of four. Genuinely winnable. You can out-present a paper that is already in print. |
| Contribution | It will never beat a published paper's contribution, which took somebody three years. Finishes when two rounds go by without a *new* objection. |
| Identification, measurement | Same rule, with a floor. An objection your design genuinely cannot answer belongs in your limitations section rather than in another round of revision. |
| All of them | Nothing finishes while your code fails to run, a table disagrees with the code, a declared robustness check is missing from the paper, or a task is still sitting in your queue. A piece waiting on you has not finished, and it will say so rather than round it up. |
| **And then you** | "Everything has finished" means the loop has nothing left to do. The loop reaches *done*. Only you reach *ready*. |

## Where I think this breaks

Two of these worry me. The third is a caution.

Published papers are in the training data. A model that recognises the APSR piece is remembering which one is famous rather than judging two manuscripts, and every win after that is noise. Use papers published recently enough that the models have not seen them, and ask each referee once per run whether it can name either paper.

Models from the same company share training data and taste, so two referees from one company agree with each other for reasons that have nothing to do with your paper. Use two companies.

And running out of objections is weaker evidence than winning. Two quiet rounds tell you the machine is out of ideas. Read the accumulated objections yourself before you decide anything.

It will not tell you whether you will get in, it does not replace a referee, and it cannot make a boring finding interesting. It also cannot fix a design problem. If your identification does not work, it will tell you so clearly, repeatedly and correctly, and there is nothing it can do about it from the draft.

## Getting it running

You need [Claude Code](https://claude.com/claude-code), and access to models from two different companies for the referee panel.

```bash
cp -r .claude/skills/social-science-gauntlet your-project/.claude/skills/
```

Then, in your manuscript's folder:

```
/social-science-gauntlet polish this manuscript for AJPS
```

It asks who does the work before anything else. If you already know, say so and skip the question:

```
/social-science-gauntlet polish this manuscript for AJPS, referee only
```

## What is in here

```
.claude/skills/social-science-gauntlet/
├── SKILL.md                      # the loop: setup, the seven pieces, exits, the prompt
└── references/
    ├── who-does-the-work.md      # the three settings, routing, the queue, what you disclose under each
    ├── referee-panel.md          # blinding, the two-company panel, order swaps, referee prompts, objection checklist
    ├── robustness-ledger.md      # the log, its rules, worked examples of a check that passes and one that fails
    ├── change-tracking.md        # what counts as consequential, the three rules, flags, the handoff brief
    └── progress-dashboard.md     # the live page: which panels, where each one's numbers come from
docs/                             # the illustrated version, served by GitHub Pages
```

A run creates five files in your folder. `FROZEN.md` holds the specification. `CLAIMS.md` holds what the paper says, in your words, written before anything starts. `ROUTING.md` holds who does what. Then the robustness log and the changelog. On split and referee only there is a sixth, `TASKS.md`, which is the queue.

## Scope

Built for polishing a draft that already exists and already has results. A project at the design stage needs the freeze to happen at pre-analysis time, which is a different workflow and should be a different skill.

## Credit

The gauntlet loop technique is **[Matt Shumer's](https://github.com/mshumer)**, from the [original prompt](https://github.com/mshumer/Claude-of-Duty/blob/main/prompt.md) he wrote for [Claude of Duty](https://github.com/mshumer/Claude-of-Duty). This adapts **[gauntlet-loop](https://github.com/robonuggets/gauntlet-loop)** by Jay E at [RoboNuggets](https://robonuggets.com), which packaged that technique as a reusable skill.

Modified for empirical social science: reviewer models moved from bar to critic, splitting by referee objection, the frozen specification and the robustness log, change tracking that interrupts only where you ask it to, a choice of who does the revising, and a blinding protocol for the training-data problem.

## License

CC BY 4.0, inherited from the original. Free to use with attribution.
