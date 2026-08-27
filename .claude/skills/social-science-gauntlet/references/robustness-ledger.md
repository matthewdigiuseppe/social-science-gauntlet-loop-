# The robustness ledger

The loop is allowed to run robustness checks. The ledger is what keeps that from being specification search.

The logic is simple: a robustness check is only evidence if it could have come out badly and you would have reported it anyway. Declaring the check before running it, and reporting it after, is what makes that true. Everything below is machinery for enforcing those two facts.

## Rules

1. **Append-only.** Entries are never edited after their result is filled in, and never deleted. If an entry is wrong, add a correcting entry below it that references it.
2. **Declare before running.** Fields 1 through 5 of an entry are written and committed *before* the code runs. Field 6 is filled in after. A builder that writes the whole entry at once has not run a robustness check.
3. **The failure criterion is written in advance.** "What result would make me say this check failed" is field 5, and it is written before the result exists. This field is the load-bearing one — it is what the auditor reads to detect after-the-fact declarations.
4. **Every declared check is reported.** In the paper or the appendix, with its actual result. A declared check that appears nowhere in the manuscript is a hard gate failure and blocks the loop from exiting.
5. **One preferred variant per family.** Declare the form of the check you would defend to a referee, then run it. Running further variants is allowed, but each one is its own ledger entry with its own result. The count of variants tried is visible by construction.
6. **A failure is bounded, not buried.** When a check fails, the two permitted responses are to narrow the paper's claim to the range where it holds, or to diagnose the failure and report the diagnosis. Searching for a variant that passes is the thing this file exists to prevent.
7. **The frozen spec never changes.** A check that overturns the headline result is reported and discussed in the paper. It does not become the new headline. If it convinces you the paper is wrong, stop the loop and talk to the author — that is a finding, not a task.

## Entry template

Copy this block for each check. Fields 1–5 before running, field 6 after.

```markdown
### [YYYY-MM-DD] Check N: <short name>

1. **Objection it answers.** Which referee objection, from which round, demands
   this check. If no referee asked for it, say why you are running it anyway.

2. **Family.** The check family this belongs to (e.g. "alternative estimators
   for staggered treatment", "sample restrictions", "alternative operation-
   alizations of the DV"). Say whether this is the preferred variant for the
   family or an additional one, and if additional, why.

3. **Specification.** Exactly what changes from FROZEN.md. Estimator, sample,
   variables, fixed effects, clustering. Precise enough that someone else
   could run it from this description alone.

4. **Script.** Path to the script that runs it, and the commit at which it was
   added.

5. **Failure criterion, written before running.** What result would make this
   check a failure. Be specific about sign, significance, and magnitude — "the
   coefficient loses significance" is weak; "the coefficient falls below half
   the frozen estimate, or flips sign, or its CI covers zero" is a criterion.

6. **Result.** *(after running)* The actual estimate, its uncertainty, and a
   one-line verdict: passed, failed, or ambiguous against the criterion in
   field 5. Then where in the manuscript it is reported — section or appendix
   table number. This is filled in whether or not you like the answer.
```

## Worked example

```markdown
### [2026-03-04] Check 3: Callaway–Sant'Anna estimator

1. **Objection it answers.** Round 2, methodologist referee: "TWFE with
   staggered adoption is hard to justify with a causal target; the estimate
   may be contaminated by already-treated comparisons."

2. **Family.** Alternative estimators for staggered treatment. Preferred
   variant for this family.

3. **Specification.** Same sample, DV, and treatment as FROZEN.md. Replace
   TWFE with Callaway–Sant'Anna group-time ATT, never-treated as comparison
   group, aggregated to a simple overall ATT. Country clustering retained.

4. **Script.** analysis/robustness/03_callaway_santanna.R, commit a1b2c3d.

5. **Failure criterion, written before running.** Failure if the aggregated
   ATT falls below half the frozen TWFE estimate, or flips sign, or its 95%
   CI covers zero.

6. **Result.** ATT = 0.31 (95% CI 0.09–0.53), against frozen TWFE estimate of
   0.44. Above half, same sign, CI excludes zero. **Passed.** Reported in
   Appendix Table A4 and referenced in Section 5.2.
```

## Failed-check example

A failure is reported the same way, and the paper changes to accommodate it rather than the ledger changing to hide it.

```markdown
### [2026-03-06] Check 5: Excluding post-2008 observations

1. **Objection it answers.** Round 3, area referee: "The relationship may be
   driven entirely by the financial crisis period."

2. **Family.** Sample restrictions. Preferred variant for this family.

3. **Specification.** FROZEN.md specification, sample restricted to 1990–2007.

4. **Script.** analysis/robustness/05_pre_crisis.R, commit e4f5g6h.

5. **Failure criterion, written before running.** Failure if the estimate falls
   below half the frozen estimate, flips sign, or its 95% CI covers zero.

6. **Result.** Estimate = 0.11 (95% CI −0.04–0.26). Below half, CI covers zero.
   **Failed.** Reported in Appendix Table A6 and discussed in Section 5.3,
   where the paper's claim is now bounded to the post-crisis period and the
   scope condition is stated in the theory section. Not re-run in other forms.
```

That last sentence — "not re-run in other forms" — is the one the auditor is looking for.
