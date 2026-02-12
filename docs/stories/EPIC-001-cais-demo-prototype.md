# EPIC-001: CAIS Demo Prototype

**Version:** 1.0
**Created:** 2026-01-30
**Demo Target:** 2026-01-31
**Epic Type:** Brownfield Enhancement

---

## Epic Summary

Transform the existing RAG prototype into a framework-educated Research & Analysis Agent that outputs structured scholarly data in Research Framework format (Aims | Data | Analysis | Methods | Findings).

## Epic Context

**Existing System:** Working RAG pipeline with OpenAlex and arXiv integration, Ollama LLM, ChromaDB vector store.

**Enhancement Goal:** Change output format from `FACTOR | EFFECT | SIGNIFICANCE` to `Citation | Aims | Data | Analysis | Methods | Findings` while maintaining all existing functionality.

**Brownfield Architecture Reference:** `docs/brownfield-architecture.md`

---

## Stories in Epic

| Story | Title | Priority | Effort | Dependencies |
|-------|-------|----------|--------|--------------|
| STORY-001 | Create CAIS Prompt Templates | P0 | 2h | None |
| STORY-002 | Modify CausalExtractor for Research Framework Output | P0 | 2h | STORY-001 |
| STORY-003 | Update Aggregator and Output Formatter | P0 | 2h | STORY-002 |
| STORY-004 | Wire End-to-End Demo Pipeline | P0 | 1h | STORY-003 |

**Total Estimated Effort:** ~7 hours focused development

---

## Success Criteria (Epic Level)

1. Pipeline accepts topic input (stroke rehabilitation)
2. Pipeline retrieves abstracts from OpenAlex (100-500)
3. Pipeline outputs CSV with Research Framework columns
4. Output contains 20-60 relevant studies
5. Each study has populated Aims, Data, Analysis, Methods, Findings columns

---

## Risk Assessment

| Risk | Impact | Mitigation |
|------|--------|------------|
| Prompt changes break extraction | High | Keep existing prompts as fallback |
| Output format parsing fails | Medium | Add robust error handling |
| Demo data insufficient | Low | Use pre-fetched OpenAlex data |

