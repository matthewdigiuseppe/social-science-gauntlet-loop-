# The live dashboard

The run publishes one page and keeps republishing it to the same URL as the work evolves. The author opens it whenever they want and closes it again.

This is not decoration and it is not a progress bar. It is the live view of the accountability record: what the paper claims now, what the referees keep saying, what the loop decided while nobody was watching, and what is still blocking submission. Everything on it comes from a file on disk, so nothing on the page is the loop's own summary of how it thinks the run is going.

## Two design rules that matter more than the layout

**Never show a percentage.** There is no denominator. A track can run for three rounds or thirty, and the loop has no idea which until it happens. A progress bar here would be an invented number, and an invented number on a dashboard is worse than no dashboard.

**Never let running dry look like winning.** The two exits mean completely different things (see the exit conditions in `SKILL.md`), and a green tick against both is a lie the author will act on. Won means the panel picked the manuscript over a published paper four times out of four. Dry means the referees stopped having ideas. Give them different words and different colours, and put the round count next to both.

## The panels, in the order they belong on the page

### 1. Masthead

Manuscript title, target journal, the bar paper cited properly, round count, when the run started, whether it is still going. One line, no ceremony.

### 2. What the paper claims now

The most important panel, so it goes first and it gets the most space. `gauntlet/CLAIMS.md` as the author wrote it before round one, against the claim set derived from the current draft. Differences marked, each one linked to the changelog entry that produced it.

When nothing has moved, say so in plain words rather than leaving the panel empty. "The paper still claims what you said it claims" is the single most useful sentence this page can show, and an empty panel does not say it.

### 3. The seven tracks

One row each: track name, state, rounds so far, the latest panel result as a fraction (`1 of 4`), and the objection currently in play, in one line.

States are `running`, `won`, `dry`, and `blocked`. Blocked is for a track waiting on something outside the loop, which in practice means the replication package. Do not invent a fifth.

### 4. The referee panel

For each track's most recent comparison, all four votes: two models, each at both orderings, and which manuscript each picked. Show all four rather than the tally, because the pattern is the information. A model that picks whichever it sees first is telling you its vote is worthless this round.

**Flag disagreement between the two models loudly.** When one picks ours and the other picks the bar, the thing they disagree about is almost always the paper's genuine weak point, and it is worth more than either verdict on its own.

### 5. The robustness ledger

Every check: what it was, the failure line written in advance, whether it ran, and its verdict against that line.

**Failures pin to the top of the panel, in the same visual weight as passes.** The ledger's whole rule is that a check which fails is reported exactly like one that passes, and a dashboard that greys out the failures quietly undoes that. Next to each failure, the bound it forced on the paper.

### 6. What is blocking submission

Open `[UNVERIFIED]` citations with their locations. Open claim markers with theirs. Whether the replication package currently runs clean. Whether any declared check is missing from the manuscript.

This panel is a checklist the author works through, so give it counts and locations rather than prose.

### 7. Objections still standing

What the panel raised that the loop could not answer, accumulated across the run and deduplicated.

Label this panel for what it is: **this is what a real referee is going to say.** It is the most valuable output of the whole run and the easiest to scroll past, so give it a heading that stops the author.

### 8. Run log

Newest first. One line per consequential change: round, track, level (`CLAIM`, `SUBSTANTIVE`), and what changed. Routine changes get a count at the bottom rather than a line each.

## Mechanics

Publish once at the start of the run, then republish to the same URL after every round. Same file path each time, so the author's open tab and their link both keep working.

The page is static HTML and reads nothing at runtime. Every republish is generated from the current state of `CLAIMS.md`, the ledger, the changelog, and the track state, so the page can never drift from the files. If a panel has nothing in it yet, say what it will hold rather than hiding it, because a panel that appears halfway through a run is a panel the author never learns to look at.

Follow the artifact design guidance for the page itself. It will be looked at many times over a long run, so it should be quiet, dense, and readable at a glance, and it must work in both light and dark.
