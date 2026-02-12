# RAG Prototype Evaluation vs Project Requirements

**Date:** 2026-01-30
**Purpose:** Gap analysis between existing rag_prototype (Baseline) and GRA AI Scientist requirements

---

## What EXISTS (Baseline - rag_prototype)

| Component | Current Implementation |
|-----------|----------------------|
| **Data Source** | arXiv API |
| **Output Format** | FACTOR \| EFFECT \| SIGNIFICANCE |
| **Extraction** | X → Y causal relationships |
| **Statistical Filter** | p<0.05 significance |
| **LLM** | Ollama qwen2.5:14b-instruct |
| **Embeddings** | nomic-embed-text |
| **Vector Store** | ChromaDB |
| **Scale Tested** | 2-5 papers |

---

## What's REQUIRED (GRA AI Scientist)

| Component | Required Implementation |
|-----------|------------------------|
| **Data Source** | **OpenAlex API** (NOT arXiv) |
| **Output Format** | **Aims \| Data \| Analysis \| Methods \| Findings** |
| **Extraction** | Framework-educated structured parsing |
| **Causal Inference** | Decision tree method selection + validation loop |
| **Input Scale** | ~10,000 abstracts |
| **Output Scale** | 20-60 relevant studies |
| **Topics** | Stroke Rehabilitation, Online Health Communities |

---

## REQUIRED CHANGES

| Priority | Change | Effort |
|----------|--------|--------|
| **CRITICAL** | Replace arXiv with OpenAlex API | Medium - OpenAlex pipeline already exists in `src/open_alex_pipeline/` |
| **CRITICAL** | Change output format from FACTOR\|EFFECT\|SIGNIFICANCE to Aims\|Data\|Analysis\|Methods\|Findings | Medium - New extraction prompt template |
| **HIGH** | Educate agent on Research Framework (ingest example outputs) | Medium - Prompt engineering |
| **HIGH** | Scale from 5 papers to 10,000 abstracts → 20-60 output | Low - Use existing `scalable_fetcher.py` |
| **MEDIUM** | Add decision tree for causal method selection | High - New module |
| **MEDIUM** | Add validation feedback loop | High - New module |
| **LOW** | Configure for stroke rehabilitation + online health topics | Low - Filter configuration |

---

## EXISTING ASSETS TO REUSE

| Asset | Location | Use For |
|-------|----------|---------|
| OpenAlex Client | `src/open_alex_pipeline/client.py` | Data scraping |
| Scalable Fetcher | `src/open_alex_pipeline/scalable_fetcher.py` | 10,000 abstract retrieval |
| Filter Config | `src/open_alex_pipeline/filters.py` | Topic filtering |
| Stroke Rehab Filters | `src/open_alex_pipeline/stroke_rehabilitation/` | Pre-configured filters |
| Online Health Filters | `src/open_alex_pipeline/online_health_services/` | Pre-configured filters |
| Causal Extractor | `src/rag_pipeline/causal_extractor.py` | Base for new framework extractor |
| Aggregator | `src/rag_pipeline/aggregator.py` | Results compilation |

---

## RECOMMENDED NEXT STEPS

### Agent to Summon: `/dev`

**Reason:** Development tasks required to modify/build code.

### Development Tasks:

1. **Integrate OpenAlex pipeline with RAG pipeline**
   - Connect `open_alex_pipeline/` output to `rag_pipeline/` input
   - Ensure full abstract metadata is passed through

2. **Create new extraction prompt template**
   - Replace FACTOR | EFFECT | SIGNIFICANCE format
   - New format: Aims | Data | Analysis | Methods | Findings
   - Match structure of `Example_Research_Framework_Output_*.csv`

3. **Add Research Framework education to agent context**
   - Ingest `.bmad-core/Example_Research_Framework.md`
   - Ingest `.bmad-core/Example_Research_Framework_Output_*.csv` as examples
   - Agent learns structure without hardcoded column names

4. **Wire end-to-end pipeline**
   - OpenAlex scrape → Agent analysis → Structured CSV output
   - Test with stroke rehabilitation topic
   - Test with online health communities topic

5. **Scale testing**
   - Input: ~10,000 abstracts
   - Output: 20-60 relevant studies

---

## KEY WARNINGS

1. **DO NOT USE arXiv** - Must use OpenAlex API only
2. **DO NOT HALLUCINATE DATA** - Agent extracts from provided metadata only
3. **PREVENT LLM HALLUCINATION** - Scraping is deterministic (no LLM involvement in data collection)

---

## REFERENCE DOCUMENTS

| Document | Location |
|----------|----------|
| Project Brief | `docs/brief.md` |
| Research Framework | `.bmad-core/Example_Research_Framework.md` |
| Framework Outputs | `.bmad-core/Example_Research_Framework_Output_*.csv` |
| Causal AI Scientist | `.bmad-core/Causal_AI_Scientist_Research.md` |
| CAIS Summary | `.bmad-core/Causal_AI_Scientist_Research_Summarized.md` |
| Baseline vs CAIS | `.bmad-core/Baseline_vs_CAIS.csv` |
| Current Test Results | `rag_prototype/docs/TEST_RESULTS.md` |
| Current MVP Spec | `rag_prototype/docs/MVP_SPEC.md` |
