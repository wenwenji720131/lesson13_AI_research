# Response Letter Guide

Reference for Phase 9 SKILL.md Step 6.

---

## Structure and Tone

A response letter serves two goals:
1. Show reviewers that each concern was understood and addressed
2. Document every change so reviewers can verify without re-reading the whole paper

Tone: professional, direct, and collegial. Never defensive or dismissive.
If a reviewer is wrong, the manuscript was unclear — fix the manuscript first,
then explain the clarification in the response.

---

## Letter Template

```
Dear Reviewers and Area Chair,

We thank the reviewers for their careful reading and constructive feedback.
We have addressed all comments and summarize the key changes below.
The revised manuscript changes are marked in [blue / track-changes / diff].

─────────────────────────────────────────────────────────
REVIEWER 1
─────────────────────────────────────────────────────────

**R1-1**: [quote or close paraphrase of the comment]

**Response**: [your response — see patterns below]

**Manuscript change**: Section [N], paragraph [M], lines [X–Y].
[Quote the new text, or write "No change — see explanation below."]

─────────────────────────────────────────────────────────

**R1-2**: ...

─────────────────────────────────────────────────────────
REVIEWER 2
─────────────────────────────────────────────────────────
...

─────────────────────────────────────────────────────────
AREA CHAIR (if applicable)
─────────────────────────────────────────────────────────
...
```

---

## Response Patterns

### Pattern 1: Factual Correction (reviewer is right, you must change the paper)

```
Response: The reviewer is correct. [State what was wrong.] We have revised
Section X to [state what was changed]. The corrected text reads: "[new text]."
```

### Pattern 2: Clarity Revision (reviewer misunderstood due to unclear writing)

```
Response: We apologize for the lack of clarity. The reviewer's reading
was [natural / understandable] given the original phrasing. [Clarify
the intended meaning.] We have revised Section X to read: "[new text]."
```

Do NOT write: "The reviewer misunderstood our method." The manuscript was
unclear — own the clarification.

### Pattern 3: Evidence Gap (reviewer asks for more experiments)

```
Response: We agree this would strengthen the paper. We have [run / added]
[experiment type] on [dataset]. The results, shown in [Table/Figure N], show
[key finding]. [1–2 sentence interpretation.] We have added this to Section X.
```

If the experiment is outside the paper's scope or budget:

```
Response: We thank the reviewer for this suggestion. [This experiment is
outside the scope of this work because [reason] / This would require
[X compute / unavailable dataset] which we are unable to provide].
We have added a note in the Limitations section (Section X, paragraph Y)
acknowledging this as future work.
```

### Pattern 4: Design Concern (reviewer questions an architectural decision)

```
Response: We appreciate this concern. The design choice was motivated by
[original reason from methodology]. [Address the specific concern.]
[If you changed it: "We have revised the method to [change] and report
updated results in Table N."] [If you kept it: "We have added a clarifying
paragraph in Section X explaining the tradeoff."]
```

### Pattern 5: Scope Extension (reviewer asks to expand the paper)

```
Response: Thank you for the suggestion. [Acknowledge the value of the idea.]
This extension is outside the scope of the current submission because
[specific reason — e.g., would require a substantially different experimental
setup, or addresses a different research question]. We have added this
direction to the Future Work paragraph in Section X.
```

### Pattern 6: Formatting or Minor Issue

```
Response: Fixed. [One sentence on what was changed.] See Section X.
```

---

## Rules

**Address every comment.** Even minor ones. "Thank you — fixed" is
sufficient for typos. A comment without a response will flag the letter
as incomplete.

**Never argue that a reviewer is wrong without fixing the manuscript.**
If the paper was clear, the reviewer would not have raised the concern.
Fix the text, then explain.

**State exact manuscript locations.** "We revised the paper" is not
sufficient. Give section number, paragraph, and quote the new text.

**Keep explanations short.** 2–4 sentences per comment for minor items,
1–2 paragraphs for major changes. Reviewers read many response letters.

**Be consistent.** If the response letter says "we added Table 3 with
efficiency results," Table 3 must exist in the revised manuscript with
exactly those results.

---

## Common Mistakes to Avoid

| Mistake | Why it fails | Fix |
|---|---|---|
| "The reviewer misunderstood" | Defensive; still needs a fix | Fix the manuscript, then explain |
| Vague location ("we improved Section 3") | Reviewer cannot verify | Give paragraph and line range |
| New claims in the response not in the paper | Inconsistency | Add to paper or remove from response |
| Ignoring a comment | Signals the review was not read | Address every comment |
| Over-long explanations for minor issues | Wastes reviewer time | 1–2 sentences for minor items |
| Adding new experiments that change conclusions | Raises new questions | New experiments must support, not undermine, existing claims |
