---
name: phase-1-literature-mapping
description: Build an evidence-backed Phase 1 literature map for an AI or computer-science research topic. Use when Codex needs to define a research scope, collect and classify foundational and recent papers, analyze method evolution, summarize benchmarks and trends, create a paper database, or produce a bounded problem pool before research-gap selection. Do not use to choose a single gap, propose a new method, design experiments, or write a paper.
---

# Phase 1 Literature Mapping

Create a navigable field map, not a pile of papers and not a novelty verdict. Read `../README.md` before work. Read `references/deliverables-and-validation.md` before creating output, and read `references/artifact-templates.md` when creating an artifact.

## Scope And Safety

- Keep this work in Phase 1: record observed limitations as problem candidates; do not rank a gap, propose an innovation, estimate an MVP, or recommend an experiment.
- Ask for a topic only when the supplied topic cannot be expressed as `object + task + scenario + constraints`. Do not ask for unpublished method details to search the web.
- Separate source-backed facts from synthesis. Never claim exhaustive coverage or novelty proof.
- Prefer official proceedings, publisher pages, ACL Anthology, CVF, PMLR, OpenReview, arXiv, DBLP, Semantic Scholar, OpenAlex, Crossref, and project pages. Verify material claims against a stable paper or proceedings URL.

## Tool Routing

Use the smallest available toolset that can produce traceable evidence.

| Need | Preferred local resource | Rule |
| --- | --- | --- |
| Multi-source paper collection and BibTeX | `../academic-research-plugin/literature-survey/` | Use its search and BibTeX utilities; inspect records before trusting metadata. |
| Citation, author, institution, and publication-count analysis | `../claude-scholar/openalex/` | Use for bibliometrics and trend counts, not as the only evidence for a paper claim. |
| Quality-screened search report | `../CCFA-Skills/ccf-literature-searcher/` | Use only after confirming its required `ccf-common` dependencies exist. Otherwise apply its source-quality and traceability principles manually. |
| Recent-paper or venue snapshot | `../CCFA-Skills/ccf-literature-monitor/` | Treat as a point-in-time scan unless a scheduler and persisted watch state are configured. |

Do not install packages, enable MCP servers, or run networked searches without the user's authorization or an available approved tool path. Record every source, query, date range, and exclusion in the output.

## Workflow

### 1. Define The Scope Card

Write `scope.md` first. Specify the object, task, scenario, constraints, inclusion/exclusion rules, target community, date windows, and intended map boundary. Split an over-broad topic before searching.

### 2. Plan A Layered Search

Create 3-5 reproducible queries per layer. Collect papers in four layers:

1. surveys and tutorials;
2. foundational or milestone papers;
3. representative and state-of-the-art methods;
4. recent work in an explicit window.

Use backward and forward citation traversal for seminal papers. A one-year default is acceptable only for the recent layer, never for the full map.

### 3. Build The Paper Database

Deduplicate by DOI, arXiv identifier, and normalized title. Retain the preferred stable URL and the discovery source. Populate every required column in `papers.csv`; do not invent missing abstracts, venues, citation counts, datasets, metrics, or results. Export verified citations to `references.bib`.

### 4. Construct The Taxonomy

Classify papers by problem, method family, model or mechanism, assumptions, data regime, compute regime, evidence type, and stated limitation. Create categories from the corpus rather than forcing a predetermined taxonomy. Explain each category with representative papers and counterexamples.

### 5. Analyze Evolution, Benchmarks, And Trends

For each major method family, describe the chain `problem -> prior solution -> limitation -> subsequent response`. Summarize datasets, metrics, baselines, protocol differences, and benchmark limitations separately from method performance. Use publication counts or citation data only with their query and date range recorded.

### 6. Create A Bounded Problem Pool

Record 5-10 observed problems with evidence, affected setting, and uncertainty. Phrase them as observations, for example: "Evaluation of X is inconsistent across Y settings." Do not select the best problem or attach a proposed solution; hand that decision to Phase 2.

### 7. Validate And Hand Off

Complete `phase1-validation.md` against the acceptance checks in `references/deliverables-and-validation.md`. A missing required artifact, unsupported claim, unrecorded query, or absent benchmark review means Phase 1 is incomplete. End with a short handoff note listing only the problem candidates and evidence boundaries for Phase 2.

## Output Location

Unless the user supplies a different destination, write a single dated folder:

```text
literature-mapping-YYYYMMDD-<topic-slug>/
```

Do not overwrite an earlier mapping. Create a new version or ask before merging artifacts.
