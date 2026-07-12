# Validation Checklist

Reference for Phase 5 SKILL.md Step 8.
Run all 7 checks before declaring the methodology ready for Phase 6.

---

## Check 1: Method-Gap Alignment Test

**Question**: Does the method objective directly correspond to the research
gap identified in Phase 2?

**Pass condition**:
- The method objective statement names the same root cause as the
  Phase 2 gap document
- The core mechanism modifies the exact intervention point identified
  in Phase 4 Step 1
- No gap from Phase 2 is left unaddressed by the objective

**Fail signals**:
- The method objective is "improve performance" without specifying what
  failure mode it addresses
- The Phase 2 gap is about efficiency but the objective adds computation
- The method addresses a different gap than what was validated in Phase 3

**Action if fail**: Return to Step 1 and restate the method objective.

---

## Check 2: Mechanism Justification Test

**Question**: Is there a clear causal argument for why the mechanism works?

**Pass condition**:
- The core mechanism has a written causal chain: existing behavior →
  failure mode → mechanism change → failure mode prevented
- The argument makes a falsifiable prediction

**Fail signals**:
- The mechanism is justified only empirically ("we tried it and it worked")
- The causal argument is circular ("component X improves Y because Y improves")
- The mechanism is described at the architecture level without explaining
  the computational change

**Action if fail**: Return to Step 3 and rewrite the causal argument.

---

## Check 3: Component Necessity Test

**Question**: Is every component in the framework individually necessary?

**Pass condition**:
- For every module: there is a stated prediction of what happens without it
- The prediction is falsifiable and would be tested in Phase 6

**Fail signals**:
- A module's removal would "probably" reduce performance without a
  specific mechanism for why
- Modules exist for "robustness" or "completeness" without a causal role

**Action if fail**: Remove modules that do not pass necessity justification.
If a module is needed but its necessity is unclear, add it to the Phase 6
ablation plan with the hypothesis to be tested.

---

## Check 4: Novelty Test

**Question**: Is the core mechanism sufficiently distinct from prior work?

**Pass condition**:
- The closest prior work is named and cited
- A specific difference between the proposed mechanism and the closest
  work is documented
- Novelty status is `partial` or `searched` (never just `unsearched`)

**Fail signals**:
- No closest work identified — novelty untested
- The stated difference is "we apply X to domain Y" without a
  mechanism-level distinction
- Novelty status is still `unsearched` at this stage

**Action if fail**: Search for closest work and document specific difference.
If search reveals prior art: either reframe the contribution or return to
Phase 4 for a different idea.

---

## Check 5: Experimental Testability Test

**Question**: Can every claim be tested with the experiments in the
evaluation plan?

**Pass condition**:
- Every contribution claim in the methodology has a corresponding
  experiment in the evaluation plan
- The experiment would produce direct (not proxy) evidence for the claim
- Ablation targets cover every key design decision

**Fail signals**:
- A contribution claim has no corresponding experiment
- The primary metric does not measure what the gap refers to
- An important design decision has no ablation

**Action if fail**: Add the missing experiments to the evaluation plan.
If an experiment is infeasible, qualify or remove the corresponding claim.

---

## Check 6: Complexity / Resource Test

**Question**: Is the computational overhead acceptable and justified?

**Pass condition**:
- Time and space complexity is documented vs. baseline
- If overhead is worse: a justification is written (bounded / asymptotic
  win / explicit tradeoff)
- The method fits within a standard academic compute budget (≤ 8 GPUs
  per main run, ≤ 3 days per run)

**Fail signals**:
- Complexity analysis is missing
- Method is >10× more expensive than baseline without justification
- Implementation requires proprietary hardware or data

**Action if fail**: Redesign the mechanism to reduce overhead, or document
the explicit tradeoff and its justification.

---

## Check 7: Failure Prediction Test

**Question**: Have the main failure modes been identified and mitigated?

**Pass condition**:
- Risk register has ≥ 3 risks with probability, impact, mitigation, and
  detection experiment
- At least one "blocks-all" risk has a mitigation or a go/no-go test
  scheduled early in Phase 6
- No risk listed as "high probability + blocks-all" without a mitigation

**Fail signals**:
- Risk register is empty or has only "minor" risks
- The main failure mode from Phase 4 is not addressed in the risk register
- No detection experiment for high-probability risks

**Action if fail**: Expand the risk register and add early sanity-check
experiments to the evaluation plan.

---

## Phase 6 Handoff Statement

After all 7 checks pass, write this statement in `phase5-validation.md`:

```
Phase 5 Validation — [Date]
Checks passed: [list check numbers]
Checks failed: [list check numbers and blocking reason, if any]

This methodology is ready for Phase 6 experiments.

Top idea: [P4-IDEA-N] — [title]
Method objective: [1-sentence statement]
Core mechanism: [1-sentence statement]
Primary claim to test: [1-sentence]
Highest-risk item: [Risk-N from risk register]
```

If any check fails, write "NOT READY for Phase 6" and list what must
be resolved before proceeding.
