# Phase 1 Exit Validation Checklist

Used at the end of SKILL.md to determine whether Phase 1 is complete.
All five criteria must pass before advancing to Phase 2.

---

## How to Use This Checklist

For each criterion, attempt the described task WITHOUT consulting your
notes or output files. The goal is to test internalized understanding,
not document lookup ability.

Mark each item: PASS / PARTIAL / FAIL

If any item is PARTIAL or FAIL, identify which Step in the skill needs
more depth, iterate that step, and re-run the validation.

---

## V1: Field Map Recall

**Test**: Close all documents. Draw the field's top-level structure from memory.

Required elements (all must be present):
- [ ] At least 2 Problem Categories from the taxonomy
- [ ] At least 2 Method Families per problem category
- [ ] At least 2 Benchmark names
- [ ] At least 2 Open Challenges / unsolved problems

**Pass criterion**: A colleague unfamiliar with the field could use your
drawing to understand the field's structure in 5 minutes.

**Fails if**: You can only list paper names without showing their relationships,
or you cannot identify any open challenges.

**Remediation**: Return to Step 3 (Taxonomy) and Step 4 (Evolution chains).
The map is probably a flat list of papers rather than a structured hierarchy.

---

## V2: Paper Positioning Speed

**Test**: Take any paper abstract from your T4 (Recent) collection that you
have NOT specifically analyzed yet. Without reading the full paper, answer:

- [ ] Which Problem Category does it address?
- [ ] Which Method Family does it belong to?
- [ ] Which prior paper does it most likely build on?
- [ ] What limitation of prior work does it claim to address?

**Pass criterion**: You can answer all four questions within 60 seconds,
and your answers are consistent with the paper's stated contributions.

**Fails if**: You cannot place the paper in the taxonomy, or you need to
re-read your notes to answer.

**Remediation**: Your taxonomy (Step 3) is not internalized. Rebuild the
Problem Map and Method Families sections of `literature_map.md` in your own
words without copying from `taxonomy.md`.

---

## V3: Method Comparison Table

**Test**: Without consulting notes, produce a comparison table for any 3
methods from the same Method Family, covering at least 4 attributes.

Required format:

| Method | Year | Core Idea | Strength | Weakness | Benchmark Score |
|---|---|---|---|---|---|
| A | | | | | |
| B | | | | | |
| C | | | | | |

**Pass criterion**: Table is complete, Weakness entries are specific
(not "worse performance"), and Benchmark Score column references a real
benchmark from your `benchmark_summary.md`.

**Fails if**: You can only recall paper names and years, or cannot state
concrete weaknesses.

**Remediation**: Return to Step 3. The Strength/Weakness column in the
taxonomy was not filled in with sufficient specificity.

---

## V4: Field History Narration

**Test**: Narrate the development of the field's primary method family
out loud (or in writing) in 5 minutes. The narration must:

- [ ] Start from the earliest relevant approach (T2 Foundation)
- [ ] Explain what problem each transition solved
- [ ] Explain *why* each transition happened (the insight, not just the date)
- [ ] End at the current state of the art
- [ ] Identify at least one unresolved limitation at the end

**Pass criterion**: A listener who knows the field could follow the logic
of why each method superseded the previous one, without it sounding like
a timeline of paper releases.

**Fails if**: The narration is a chronological list of papers without causal
explanation ("then in 2020 they proposed X, then in 2022 they proposed Y...").

**Remediation**: Return to Step 4. The evolution chains were constructed as
timelines rather than causal sequences. Re-read the evolution chain and
explicitly write the "Insight" node for each transition.

---

## V5: Problem Pool Completeness

**Test**: Review `problem_pool.md` against these criteria:

- [ ] At least 5 entries, no more than 10
- [ ] Each entry has a Severity rating (High/Medium/Low) with justification
- [ ] Each entry cites at least 2 papers as evidence
- [ ] Problems come from at least 3 different Origins
  (taxonomy gap, evolution open end, benchmark blind spot, trend shift)
- [ ] No entry proposes a solution or method design
- [ ] Problems span at least 2 different Problem Categories from the taxonomy

**Pass criterion**: All boxes checked.

**Fails if**: Fewer than 5 problems, problems all come from one source type,
or any entry contains a proposed solution.

**Remediation**:
- < 5 problems: return to Steps 3, 4, 5 and look for Open Nodes, Open Ends,
  benchmark blind spots
- Problems lack evidence: return to the relevant step and add citations
- Entries contain solutions: remove solution text; a Problem Pool entry ends
  at "what is unsolved", not "how to solve it"

---

## Phase 1 Completion Decision

| Criterion | Status | Remediation needed |
|---|---|---|
| V1: Field Map Recall | | |
| V2: Paper Positioning Speed | | |
| V3: Method Comparison Table | | |
| V4: Field History Narration | | |
| V5: Problem Pool Completeness | | |

**Decision**:
- All PASS → Advance to Phase 2 with `problem_pool.md` and `taxonomy.md`
- Any PARTIAL or FAIL → Iterate identified steps; re-validate before advancing

---

## What Phase 2 Needs From Phase 1

When handing off to Phase 2 (Identify Research Gap), confirm these files
exist and are complete:

| File | Required by Phase 2 | Status |
|---|---|---|
| `problem_pool.md` | Primary input — the candidate problems to evaluate | |
| `taxonomy.md` | Context for gap classification | |
| `evolution_chains.md` | Evidence for "why a gap exists" arguments | |
| `benchmark_summary.md` | Evaluation context for gap assessment | |
| `literature_map.md` | Navigation reference during gap analysis | |

Phase 2 will evaluate each problem in `problem_pool.md` for research value,
feasibility, and novelty. It will not revisit literature collection unless
a specific gap requires new evidence — that would be a targeted call to
`ccf-literature-searcher`, not a restart of Phase 1.
