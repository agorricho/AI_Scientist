# Dev Agent Handoff: STORY-001

**Task:** Implement CAIS Prompt Templates
**Priority:** P0 - Critical Path
**Story File:** `docs/stories/STORY-001-cais-prompt-templates.md`

---

## Quick Context

You are enhancing an existing RAG prototype to produce Research Framework output instead of simple causal extraction.

**Current Output:** `FACTOR | EFFECT | SIGNIFICANCE`
**Required Output:** `CITATION | AIMS | DATA | ANALYSIS | METHODS | FINDINGS`

---

## Files to Create

```
rag_prototype/prompts/
├── __init__.py                    # Empty init
├── structured_extraction.txt      # Main extraction prompt
└── loader.py                      # Prompt loading utility
```

---

## Files to Modify

| File | Change |
|------|--------|
| `rag_prototype/src/rag_pipeline/causal_extractor.py` | Add method to load new prompt, keep existing as fallback |

---

## Key Reference Files (READ THESE)

1. **Story Details:** `docs/stories/STORY-001-cais-prompt-templates.md`
2. **Current Prompt:** `rag_prototype/src/rag_pipeline/causal_extractor.py:47-67`
3. **PRD Section 10.6:** `docs/prd.md` (search for "H.1", "H.2", "H.3" prompts)
4. **Example Output Format:** `.bmad-core/Example_Research_Framework_Output_Stroke_Rehab.csv`

---

## Prompt Requirements

The `structured_extraction.txt` prompt must:

1. Extract 6 columns: Citation, Aims, Data, Analysis, Methods, Findings
2. Include 1-2 few-shot examples (stroke rehabilitation domain)
3. Use LlamaIndex template variables: `{context_str}` and `{query_str}`
4. Output pipe-delimited format for easy parsing
5. Instruct LLM to extract only from provided text (no hallucination)

---

## Integration Pattern

```python
# Add to causal_extractor.py
from pathlib import Path

def _load_research_framework_prompt(self) -> PromptTemplate:
    prompt_path = Path(__file__).parent.parent.parent / "prompts" / "structured_extraction.txt"
    if prompt_path.exists():
        return PromptTemplate(prompt_path.read_text())
    return self._create_extraction_prompt()  # fallback to existing
```

---

## Definition of Done

- [ ] `rag_prototype/prompts/` directory created
- [ ] `structured_extraction.txt` with Research Framework format
- [ ] Few-shot examples included in prompt
- [ ] Integration method added to `causal_extractor.py`
- [ ] Existing `EXTRACTION_TEMPLATE` preserved as fallback

---

## Test Command

After implementation, test with:
```bash
cd rag_prototype
python -c "from src.rag_pipeline.causal_extractor import CausalExtractor; print('Prompt loads OK')"
```

---

## Do NOT Modify

- `src/open_alex_pipeline/*` (production-ready, preserve unchanged)
- `src/rag_pipeline/paper_retriever.py`
- `src/rag_pipeline/query_rephraser.py`
