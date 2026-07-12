---
name: phase1-literature-mapping
description: >
  Build a navigable research field map for AI/CS literature mapping (Phase 1).
  Covers research scope definition, tiered literature collection, taxonomy
  construction, method evolution analysis, benchmark understanding, trend
  analysis, and problem pool generation. Use when the user wants to map a
  research field, build a literature overview, understand field structure, or
  prepare for research gap identification (Phase 2). Also triggers on:
  "文献地图", "领域综述", "literature mapping", "field survey", "research
  landscape", "domain overview", "文献整理", "构建知识地图".
  DO NOT use for: finding innovation ideas (Phase 4/5), writing papers (Phase 8),
  or novelty checking of a specific idea (use ccf-literature-searcher instead).
user-invocable: true
argument-hint: "<research_topic> [--scope broad|narrow] [--date-range 1y|2y|3y|5y] [--max-papers 50] [--venues NeurIPS,ICML,CVPR,AAAI]"
---

# Phase 1: Literature Mapping Skill

## Purpose

Build a **structured, navigable research field map** that enables the
researcher to answer: *"What problems exist in this field, what methods have
been tried, why did they evolve, and where might new opportunities lie?"*

The output is not a paper list. It is a cognitive model of the field.

**Phase boundary**: This skill ends at Problem Pool construction. It does
NOT produce innovation proposals or method designs — those belong to
Phase 4/5. Any step that generates novel ideas is explicitly out of scope here.

## Arguments

- **research_topic** (required): The field or topic to map. Can be broad
  ("vision-language models") or narrow ("VLA for autonomous driving").
- **--scope** (optional): `broad` for a panoramic survey; `narrow` for a
  focused sub-field deep dive. Default: `broad`.
- **--date-range** (optional): Time window for recent papers. `1y` / `2y` /
  `3y` / `5y`. Default: `3y`. Use `5y` only for fast-moving fields where
  seminal works are recent.
- **--max-papers** (optional): Max papers per search query. Default: `50`.
- **--venues** (optional): Comma-separated venue filter. If omitted, all
  high-quality venues are included.

## Setup

Install required Python dependencies once:

```bash
pip install requests arxiv bibtexparser pandas semanticscholar
```

Scripts in `../academic-research-plugin/lib/` can be used directly:

```bash
python ../academic-research-plugin/lib/paper_search.py --query "<query>" --max-results 30 --output json
python ../academic-research-plugin/lib/bibtex_utils.py fetch --title "<title>"
```

---

## Workflow

Follow all 7 steps in order. Each step has a defined output; do not proceed
to the next step until the current output is complete.

---

### Step 1: Research Scope Definition（界定研究空间）

**Goal**: Convert the user's topic into a precise, bounded research space
before touching any papers.

Load `references/scope-definition-guide.md` and follow the narrowing process:

1. Start with the user's raw topic.
2. Identify the four dimensions:
   - **Object**: What system/model/algorithm is studied?
   - **Task**: What capability or problem is being solved?
   - **Scenario**: In what environment or domain?
   - **Constraint**: Under what real-world limitations?
3. If `--scope broad`, keep Object + Task as primary axes; Scenario and
   Constraint are secondary.
4. If `--scope narrow`, all four dimensions must be pinned.
5. Produce one Research Scope Statement in the form:
   > "How to improve [Task] of [Object] in [Scenario] under [Constraint]?"

**Output**: `scope_statement.md` — one paragraph defining the research space,
listing what is IN scope and what is explicitly OUT of scope.

**Do not move to Step 2 until the scope statement is confirmed.**

---

### Step 2: Tiered Literature Collection（分层级文献收集）

**Goal**: Collect a representative, quality-filtered paper set organized by
epistemic role, not publication date.

#### 2a. Define the four tiers

| Tier | Role | Target count |
|---|---|---|
| T1 Survey | Review papers, field overviews | 3–8 |
| T2 Foundation | Seminal/landmark papers (cited 500+) | 5–15 |
| T3 SOTA | State-of-the-art methods in the last 2–3 years | 15–30 |
| T4 Recent | Preprints and conference papers in the last year | 10–20 |

#### 2b. Generate search queries

Decompose the scope into 4–6 queries covering:
- Core terminology and acronyms
- Related sub-problems
- Adjacent method families
- Application-specific terms

Document all queries for reproducibility.

#### 2c. Execute searches

For each query:

```bash
python ../academic-research-plugin/lib/paper_search.py \
  --query "<query>" \
  --max-results 30 \
  --output json
```

- Prioritize: NeurIPS, ICML, ICLR, CVPR, ICCV, ECCV, ACL, EMNLP, AAAI,
  IJCAI, arXiv (credible groups), DBLP
- Apply source-quality filter: exclude predatory journals, anonymous preprints
  without institutional affiliation, and low-citation workshop papers unless
  very recent
- Deduplicate by title/arXiv ID

#### 2d. Assign tiers

For each paper, assign a tier based on citation count, publication year, and
community recognition. Mark papers that span multiple tiers (e.g., a 2023
paper that is already seminal) with the higher tier.

**Output**: `papers_tiered.json` — JSON array with fields:
`title`, `authors`, `year`, `venue`, `citations`, `tier`, `url`, `abstract`

---

### Step 3: Taxonomy Construction（文献分类与编码）

**Goal**: Build a hierarchical classification of *problems* and *methods*,
not merely a flat theme list.

Load `references/taxonomy-template.md`.

#### 3a. Problem taxonomy

Group papers by the **problem they address**, not by technique. Each problem
node must answer: "What limitation of prior work does this address?"

```
Research Area
├── Problem Category A
│   ├── Sub-problem A1
│   └── Sub-problem A2
└── Problem Category B
    └── Sub-problem B1
```

#### 3b. Method taxonomy

For each problem node, map the methods that address it:

```
Problem A
├── Method Family α  (e.g., attention-based)
│   ├── Paper X (Year): core idea, strength, weakness
│   └── Paper Y (Year): core idea, strength, weakness
└── Method Family β  (e.g., graph-based)
    └── Paper Z (Year): core idea, strength, weakness
```

#### 3c. Cross-reference

For each leaf node (individual paper), record:
- **Problem addressed**: which node above
- **Core idea**: one sentence
- **Strength**: one sentence
- **Weakness/Limitation**: one sentence (this feeds Step 4)

**Output**: `taxonomy.md` — full hierarchical map using the structure in
`references/taxonomy-template.md`

---

### Step 4: Method Evolution Analysis（方法演化分析）

**Goal**: Explain *why* methods evolved, not just *when*.

For each major method family identified in Step 3, construct one or more
evolution chains:

```
Problem identified
        ↓
Existing solution (Method A)
        ↓
Limitation of A
        ↓
New insight / idea
        ↓
New solution (Method B)
        ↓
Residual limitation of B  →  (next chain link)
```

Load `references/evolution-analysis-guide.md` for chain construction rules.

Requirements:
- At least one evolution chain per major method family
- Each chain must have a minimum of 3 links
- Limitations must be grounded in paper text or citations, not inferred
- Mark "open ends" — chains where the latest limitation has no known solution
  yet (these become candidates for Step 7)

**Output**: `evolution_chains.md` — one section per method family, with
labeled chain diagrams and explanatory text.

---

### Step 5: Benchmark & Evaluation System（Benchmark与评价体系理解）

**Goal**: Understand how the field measures progress, and identify
evaluation blind spots.

For each major benchmark or evaluation protocol in the field, document:

| Benchmark | Dataset | Primary Metrics | What it measures | Known limitations |
|---|---|---|---|---|
| Name | Source/size | Acc / F1 / BLEU / ... | Capability being tested | What it does NOT test |

Also answer:
1. Which benchmarks are considered standard / required by top venues?
2. Are there competing evaluation standards? Why?
3. What real-world capabilities are *not* covered by any existing benchmark?
4. Are any benchmarks known to be saturated (SOTA ≈ human-level)?

Use `ccf-literature-searcher` (in quick mode) if deep benchmark retrieval
is needed.

**Output**: `benchmark_summary.md` — table + analysis paragraph per benchmark.

---

### Step 6: Trend Analysis（研究趋势分析）

**Goal**: Identify which directions are growing, which are plateauing, and
where community attention is shifting.

#### 6a. Temporal trend

Bin papers in `papers_tiered.json` by year. Identify:
- Topics with accelerating publication volume (last 2 years > prior 2 years)
- Topics with decelerating volume (possibly solved or abandoned)

#### 6b. Method shift

Using the taxonomy from Step 3, identify transitions where one method family
is being systematically replaced by another, and explain why.

#### 6c. Community focus shift

Identify keywords/themes that have appeared or disappeared in titles/abstracts
over the date range. Examples of questions to answer:
- What did the field care about 3 years ago that it no longer emphasizes?
- What new concerns have emerged (e.g., efficiency, alignment, safety)?

#### 6d. Cross-domain signals

For the core methodology in the field, check if it has been adopted in
adjacent domains (or if adjacent methods are being imported). This is a
signal for either new application opportunities (for Problem Pool) or
competitive saturation.

Use `ccf-literature-monitor` (trend-scouting mode) for live arXiv signal if
available.

**Output**: `trend_analysis.md` — sections for temporal trend, method shift,
community focus, and cross-domain signals. Each section ends with one
"signal sentence" summarizing the implication.

---

### Step 7: Problem Pool Construction（初步问题池建立）

**Goal**: Produce 5–10 candidate research problems for Phase 2 evaluation.
This is NOT a gap analysis and NOT innovation proposals.

A Problem Pool entry is a *question the field has not answered yet*, grounded
in evidence from Steps 3–6. It is not a proposed solution.

For each candidate problem:

```
Problem ID: P-N
Title: [Short descriptive name]
Origin: [Which step revealed this — taxonomy gap / evolution open end /
         benchmark blind spot / trend shift]
Description: [2-3 sentences: what is the unsolved question?]
Evidence: [cite 2-3 papers that show the problem exists or is acknowledged]
Severity: High / Medium / Low
  (High = blocks a key application or is acknowledged by multiple papers;
   Medium = mentioned as limitation but not central;
   Low = speculative or single-paper observation)
Phase 2 relevance: [One sentence on why this is worth evaluating as a
                    research gap in Phase 2]
```

**Constraints**:
- Do NOT propose a solution or method design for any problem
- Do NOT score or prioritize problems here — that is Phase 2's job
- Aim for diversity: cover different problem categories from the taxonomy
- Minimum 5 entries; maximum 10

**Output**: `problem_pool.md`

---

## Output Package

All outputs are written to:

```
./output/phase1-<topic-slug>-<YYYYMMDD>/
  scope_statement.md
  papers_tiered.json
  taxonomy.md
  evolution_chains.md
  benchmark_summary.md
  trend_analysis.md
  problem_pool.md
  literature_map.md          ← synthesized navigable map (see below)
  references.bib
  search_log.json
```

### literature_map.md (synthesis)

After all 7 steps, produce one synthesized navigation document using the
template in `references/report-template.md`. This is the primary deliverable
— the "research map" a reader can use to orient themselves in the field in
under 30 minutes.

---

## Phase 1 Exit Validation

Before declaring Phase 1 complete, verify all five criteria in
`references/validation-checklist.md`:

- **V1** Can you draw the field's Problem + Method tree from memory?
- **V2** Given a new paper abstract, can you place it in the taxonomy within
  60 seconds?
- **V3** Can you produce a Method Comparison table (3+ methods, 4+ attributes)
  without consulting notes?
- **V4** Can you narrate the field's development history in 5 minutes,
  explaining *why* each transition happened?
- **V5** Do you have 5–10 candidate problems in the Problem Pool with evidence?

If any criterion fails, identify which step needs more depth and iterate.
Do not advance to Phase 2 until all five pass.

---

## Skill Linkage

- **Upstream**: Phase 0 Foundation Preparation (domain basics, reading ability)
- **Downstream**: `phase2-identify-research-gap` uses `problem_pool.md` and
  `taxonomy.md` as primary inputs
- **Parallel tools**:
  - `ccf-literature-searcher` — invoke for deep retrieval in Step 2 or
    benchmark deep-dive in Step 5
  - `ccf-literature-monitor` — invoke for trend-scouting in Step 6 or
    ongoing monitoring after Phase 1 completes

## Phase Boundary Reminder

The following outputs are **explicitly out of scope** for Phase 1:

| Out-of-scope output | Belongs to |
|---|---|
| Innovation proposals / novel method designs | Phase 4 |
| Feasibility assessment of new ideas | Phase 4/5 |
| Experiment design | Phase 6 |
| Hypothesis scoring or prioritization | Phase 2/3 |
| Paper writing or Related Work section | Phase 8 |
