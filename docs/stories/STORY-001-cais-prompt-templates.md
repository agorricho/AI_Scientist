# STORY-001: Create CAIS Prompt Templates

**Epic:** EPIC-001 CAIS Demo Prototype
**Priority:** P0 - Critical Path
**Effort:** 2 hours

---

## User Story

As a **Research & Analysis Agent**,
I want **prompt templates that extract Research Framework columns from abstracts**,
So that **I can produce structured scholarly output in the required format**.

---

## Story Context

**Existing System Integration:**
- Integrates with: `causal_extractor.py` (uses LlamaIndex PromptTemplate)
- Technology: LlamaIndex 0.14.12, Ollama qwen2.5:14b-instruct
- Follows pattern: Existing `EXTRACTION_TEMPLATE` in `causal_extractor.py:47-67`
- Touch points: `CausalExtractor._create_extraction_prompt()` method

**Reference Files:**
- Current prompt: `rag_prototype/src/rag_pipeline/causal_extractor.py:47-67`
- PRD prompts: `docs/prd.md` Section 10.6 (H.1, H.2, H.3)

---

## Acceptance Criteria

### Functional Requirements:

1. **AC1:** Create `prompts/` directory with structured prompt template files
2. **AC2:** Create `structured_extraction.txt` prompt that extracts:
   - Citation (DOI, title, authors, year)
   - Aims (research objectives)
   - Data (data source, sample size, collection method)
   - Analysis (variables studied, treatment T, outcome Y)
   - Methods (statistical methods, interventions)
   - Findings (key results, effect sizes, p-values)
3. **AC3:** Prompt outputs valid parseable format (pipe-delimited or JSON)
4. **AC4:** Include few-shot examples in prompt for output consistency

### Integration Requirements:

5. **AC5:** Prompts are loadable by LlamaIndex PromptTemplate
6. **AC6:** Existing `EXTRACTION_TEMPLATE` preserved as fallback
7. **AC7:** Prompt templates are parameterized for different topics

### Quality Requirements:

8. **AC8:** Prompts tested manually with sample abstracts
9. **AC9:** Output format is consistent across multiple runs

---

## Technical Implementation

### Files to Create:

```
rag_prototype/
└── prompts/
    ├── __init__.py
    ├── structured_extraction.txt      # Main extraction prompt
    └── research_framework_examples.txt # Few-shot examples
```

### Prompt Structure (structured_extraction.txt):

```
You are a Research Framework Analyst. Given an academic abstract, extract structured information.

## Research Framework Columns

For each study, extract:
1. **Citation**: DOI, authors, title, publication year
2. **Aims**: The main research objective or hypothesis
3. **Data**: Data source, sample size (n=), data collection period, methodology
4. **Analysis**: The specific variable/factor being studied (e.g., "impact of X on Y")
5. **Methods**: Statistical methods used OR intervention/treatment applied
6. **Findings**: Key results including effect sizes, confidence intervals, p-values

## Output Format

Return EXACTLY this format (one line per study):
CITATION: [citation] | AIMS: [aims] | DATA: [data] | ANALYSIS: [analysis] | METHODS: [methods] | FINDINGS: [findings]

## Example

Abstract: "This randomized controlled trial evaluated the effectiveness of robot-assisted therapy on upper limb function in 120 stroke patients. Participants were randomly assigned to robot-assisted (n=60) or conventional therapy (n=60). After 6 weeks, the robot-assisted group showed significantly greater improvement in Fugl-Meyer scores (mean difference: 8.2 points, 95% CI: 5.1-11.3, p<0.001)."

Output:
CITATION: [DOI pending] | AIMS: Evaluate robot-assisted therapy effectiveness on upper limb function post-stroke | DATA: RCT, n=120 stroke patients, 6-week intervention | ANALYSIS: Impact of robot-assisted therapy (T) on Fugl-Meyer scores (Y) | METHODS: Randomized controlled trial, between-group comparison | FINDINGS: Robot-assisted therapy showed 8.2 point improvement (95% CI: 5.1-11.3, p<0.001)

## Abstract to Analyze

{context_str}

## Research Question

{query_str}

## Structured Output
```

### Integration Pattern:

```python
# In causal_extractor.py - add method to load new prompt
def _load_research_framework_prompt(self) -> PromptTemplate:
    prompt_path = Path(__file__).parent.parent.parent / "prompts" / "structured_extraction.txt"
    if prompt_path.exists():
        return PromptTemplate(prompt_path.read_text())
    return self._create_extraction_prompt()  # fallback
```

---

## Definition of Done

- [x] `prompts/` directory created
- [x] `structured_extraction.txt` created with Research Framework format
- [x] Prompt includes few-shot examples
- [x] Prompt outputs consistent parseable format
- [x] Manual test with 3 sample abstracts confirms output format
- [x] Existing extraction template preserved as fallback

---

## Rollback Plan

If prompts fail:
1. Revert to existing `EXTRACTION_TEMPLATE` (still in code)
2. No database or infrastructure changes to undo

---

## Dev Agent Record

### Status
Ready for Review

### Agent Model Used
Claude Opus 4 (claude-opus-4-5-20251101)

### File List
| File | Action | Description |
|------|--------|-------------|
| `rag_prototype/prompts/__init__.py` | Created | Package init with helper function |
| `rag_prototype/prompts/structured_extraction.txt` | Created | Main extraction prompt with 2 few-shot examples |
| `rag_prototype/prompts/loader.py` | Created | Prompt loading utility module |
| `rag_prototype/src/rag_pipeline/causal_extractor.py` | Modified | Added `use_research_framework` flag, `_load_research_framework_prompt()`, `_parse_research_framework_response()` |

### Change Log
| Date | Change |
|------|--------|
| 2026-01-30 | Created prompts/ directory with __init__.py, structured_extraction.txt, loader.py |
| 2026-01-30 | Modified causal_extractor.py to support both legacy and RF modes |
| 2026-01-30 | All parser tests passing |

### Debug Log References
None

### Completion Notes
- Prompt uses pipe-delimited format: `CITATION: | AIMS: | DATA: | ANALYSIS: | METHODS: | FINDINGS:`
- Two few-shot examples included (stroke rehab RCT, ML model performance study)
- Legacy template renamed to `_legacy_extraction_template` and preserved as fallback
- New `use_research_framework=True` flag enables Research Framework mode
- Created conda environment `gra-venv` with Python 3.12 and all dependencies

