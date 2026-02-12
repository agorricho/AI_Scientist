# GRA AI Scientist - Brownfield Architecture Document

**Version:** 1.0
**Created:** 2026-01-30
**Purpose:** Document the ACTUAL state of the codebase for AI development agents

---

## Introduction

This document captures the CURRENT STATE of the GRA AI Scientist codebase, including technical debt, workarounds, and real-world patterns. It serves as a reference for AI agents working on the CAIS pipeline enhancement.

### Document Scope

**Focused on areas relevant to:** Transforming the existing RAG prototype into a framework-educated Research & Analysis Agent with CAIS (Causal AI Scientist) pipeline integration.

### Change Log

| Date | Version | Description | Author |
|------|---------|-------------|--------|
| 2026-01-30 | 1.0 | Initial brownfield analysis | BMad Master |

---

## Quick Reference - Key Files and Entry Points

### Critical Files for Understanding the System

| Category | File | Purpose |
|----------|------|---------|
| **Main Entry** | `rag_prototype/app.py` | CLI orchestrator, RAGPipeline class |
| **OpenAlex Client** | `src/open_alex_pipeline/client.py` | API communication with OpenAlex |
| **Scalable Fetcher** | `src/open_alex_pipeline/scalable_fetcher.py` | Batch processing with checkpoints |
| **Filter Config** | `src/open_alex_pipeline/filters.py` | FilterConfig dataclass for queries |
| **Causal Extractor** | `src/rag_pipeline/causal_extractor.py` | LlamaIndex RAG extraction |
| **Aggregator** | `src/rag_pipeline/aggregator.py` | Results compilation and formatting |
| **Query Rephraser** | `src/rag_pipeline/query_rephraser.py` | Query optimization for retrieval |
| **Paper Retriever** | `src/rag_pipeline/paper_retriever.py` | arXiv paper download |

### Enhancement Impact Areas

For the CAIS pipeline enhancement, these files will be affected:

| File | Change Type | Description |
|------|-------------|-------------|
| `causal_extractor.py` | **MODIFY** | Replace extraction prompt with CAIS prompts |
| `aggregator.py` | **MODIFY** | Change output format to Research Framework columns |
| `app.py` | **MODIFY** | Add CAIS pipeline stages, new CLI options |
| `src/orchestration/` | **NEW** | CAIS 4-stage pipeline orchestration |
| `prompts/` | **NEW** | CAIS prompt templates (H.1, H.2, H.3) |
| `output/` | **NEW** | Structured CSV/JSON output |

---

## High Level Architecture

### Technical Summary

The system is a CLI-based RAG pipeline that:
1. Fetches academic papers from OpenAlex (production-ready) or arXiv (MVP)
2. Indexes papers using LlamaIndex with ChromaDB vector store
3. Extracts causal relationships using Ollama LLM
4. Aggregates and formats results as tables

### Actual Tech Stack (from requirements.txt)

| Category | Technology | Version | Notes |
|----------|------------|---------|-------|
| **Runtime** | Python | 3.10+ | Required |
| **RAG Framework** | LlamaIndex | 0.14.12 | Core indexing and retrieval |
| **Vector Store** | ChromaDB | 1.4.1 | Embedded, lightweight |
| **LLM Provider** | Ollama | 0.6.1 | Local inference |
| **LLM Model** | qwen2.5:14b-instruct | - | Default generation model |
| **Embeddings** | nomic-embed-text | - | Via Ollama |
| **Data Source** | OpenAlex API | REST | Production data source |
| **Data Source (MVP)** | arXiv API | REST | MVP paper source |
| **PDF Processing** | pdfplumber | 0.11.9 | PDF text extraction |
| **Tables** | tabulate | 0.9.0 | Output formatting |
| **HTTP** | requests | 2.32.5 | API calls |

### Repository Structure

- **Type:** Single repository with submodule (`rag_prototype/`)
- **Package Manager:** pip with requirements.txt
- **Notable:** Two parallel pipelines exist (OpenAlex production, arXiv MVP)

---

## Source Tree and Module Organization

### Project Structure (Actual)

```
GRA_AI_Scientist/
├── .bmad-core/                      # BMad methodology resources
│   ├── Example_Research_Framework.md
│   ├── Example_Research_Framework_Output_*.csv
│   ├── Causal_AI_Scientist_Research.md
│   └── Causal_AI_Scientist_Research_Summarized.md
├── .claude/                         # Claude Code configuration
├── docs/                            # Project documentation
│   ├── brief.md                     # Project brief (by Analyst)
│   ├── prd.md                       # Product Requirements Document
│   ├── rag_prototype_evaluation.md  # Gap analysis
│   └── brownfield-architecture.md   # This document
└── rag_prototype/                   # Main codebase
    ├── app.py                       # Main CLI orchestrator
    ├── requirements.txt             # Python dependencies
    ├── Containerfile                # Container build
    ├── podman-compose.yml           # Container orchestration
    ├── docs/
    │   ├── MVP_SPEC.md              # Original MVP specification
    │   └── TEST_RESULTS.md          # Test documentation
    └── src/
        ├── __init__.py
        ├── rag_pipeline/            # RAG extraction pipeline
        │   ├── __init__.py
        │   ├── causal_extractor.py  # LlamaIndex extraction
        │   ├── query_rephraser.py   # Query optimization
        │   ├── paper_retriever.py   # arXiv paper download
        │   └── aggregator.py        # Results compilation
        └── open_alex_pipeline/      # OpenAlex data pipeline
            ├── __init__.py
            ├── client.py            # OpenAlex API client
            ├── filters.py           # Filter configuration
            ├── pipeline.py          # Pipeline orchestration
            ├── scalable_fetcher.py  # Batch processing
            ├── batch_processor.py   # Batch utilities
            ├── find_topic_id.py     # Topic discovery
            ├── stroke_rehabilitation/  # Pre-configured filters
            └── online_health_services/ # Pre-configured filters
```

### Key Modules and Their Purpose

| Module | Location | Purpose | Status |
|--------|----------|---------|--------|
| **RAGPipeline** | `app.py:25` | Main orchestrator class | Working |
| **QueryRephraser** | `query_rephraser.py` | Optimizes queries for retrieval | Working |
| **PaperRetriever** | `paper_retriever.py` | Downloads papers from arXiv | Working |
| **CausalExtractor** | `causal_extractor.py` | RAG-based relationship extraction | Working, **needs modification** |
| **ResultsAggregator** | `aggregator.py` | Compiles and formats results | Working, **needs modification** |
| **OpenAlexClient** | `client.py` | API communication | Production-ready |
| **ScalableFetcher** | `scalable_fetcher.py` | Batch processing with checkpoints | Production-ready |
| **FilterConfig** | `filters.py` | Query filter configuration | Production-ready |

---

## Current Pipeline Flow

### Existing RAG Pipeline (app.py)

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    CURRENT RAG PIPELINE (app.py)                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  1. USER INPUT                                                               │
│     └─ Research question: "What affects student performance?"               │
│                                                                              │
│  2. QUERY REPHRASER (QueryRephraser)                                        │
│     └─ Ollama LLM rephrases for academic search                             │
│     └─ Output: "factors influencing academic achievement"                   │
│                                                                              │
│  3. PAPER RETRIEVER (PaperRetriever)                                        │
│     └─ Downloads 5 papers from arXiv                                        │
│     └─ Stores PDFs in ./papers/                                             │
│                                                                              │
│  4. CAUSAL EXTRACTOR (CausalExtractor)                                      │
│     └─ LlamaIndex indexes papers (ChromaDB)                                 │
│     └─ Extracts "FACTOR | EFFECT | SIGNIFICANCE" format                     │
│     └─ Uses custom PromptTemplate                                           │
│                                                                              │
│  5. RESULTS AGGREGATOR (ResultsAggregator)                                  │
│     └─ Groups by factor (case-insensitive)                                  │
│     └─ Formats as table using tabulate                                      │
│                                                                              │
│  OUTPUT: Table with Factor | Effect | Significance | Papers                 │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Current Output Format

```
FACTOR: [factor name] | EFFECT: [positive/negative/mixed] | SIGNIFICANCE: [p-value]
```

### Required Output Format (CAIS Enhancement)

```
Citation | Aims | Data | Analysis | Methods | Findings | Causal_Justification
```

---

## Existing Assets to Reuse

### Production-Ready Components (DO NOT MODIFY)

| Component | Location | Why Preserve |
|-----------|----------|--------------|
| **OpenAlexClient** | `client.py` | Stable API communication |
| **ScalableFetcher** | `scalable_fetcher.py` | Progress tracking, checkpoints, resume |
| **FilterConfig** | `filters.py` | Flexible query filtering |
| **Stroke Rehab Filters** | `stroke_rehabilitation/` | Pre-configured for demo |
| **Online Health Filters** | `online_health_services/` | Pre-configured for demo |

### Components to Modify

| Component | Current State | Required Change |
|-----------|---------------|-----------------|
| **CausalExtractor** | Extracts FACTOR\|EFFECT\|SIGNIFICANCE | Add CAIS prompts, output Research Framework columns |
| **ResultsAggregator** | Groups by factor, table output | Rank by causal impact, CSV export |
| **app.py** | 4-step pipeline | Add CAIS 4-stage orchestration |

---

## Data Models and APIs

### Data Models

**Current Relationship Model:**
```python
relationship = {
    'factor': str,           # e.g., "study hours"
    'effect': str,           # "positive" | "negative" | "mixed" | "unclear"
    'significance': str,     # e.g., "p<0.01" | "not reported"
    'paper_title': str,
    'paper_id': str,
    'paper_url': str
}
```

**Required StudyResult Model (from PRD):**
```python
class StudyResult:
    citation: str
    title: str
    authors: List[str]
    aims: str                    # Research Framework column
    data: str                    # Research Framework column
    analysis: str                # Research Framework column
    methods: str                 # Research Framework column
    findings: str                # Research Framework column
    causal_estimate: float
    std_error: float
    pvalue: float
    conf_interval: Tuple[float, float]
    method_used: str
    causal_justification: str
```

### API Specifications

| API | Type | Documentation |
|-----|------|---------------|
| **OpenAlex** | REST | `src/open_alex_pipeline/SPEC.md` |
| **arXiv** | REST/Python | `arxiv` Python library |
| **Ollama** | REST | Default: `http://localhost:11435` |

---

## Technical Debt and Known Issues

### Critical Technical Debt

| Issue | Location | Impact | Priority |
|-------|----------|--------|----------|
| **arXiv vs OpenAlex mismatch** | Pipeline uses arXiv, but OpenAlex is production-ready | Demo may use wrong data source | HIGH |
| **Hardcoded Ollama port** | `causal_extractor.py:35` uses port 11435 (non-standard) | May fail on default Ollama installs | MEDIUM |
| **No structured output parsing** | LLM response parsed with string splits | Brittle, may break with format changes | MEDIUM |
| **ChromaDB not persisted** | Re-indexes on every run | Slow for large corpora | LOW |

### Workarounds and Gotchas

| Workaround | Location | Reason |
|------------|----------|--------|
| **Optional dotenv** | `app.py:10-15` | Graceful handling if dotenv not installed |
| **Import fallbacks** | `scalable_fetcher.py:20-27` | Allows running as script or module |
| **Case-insensitive grouping** | `aggregator.py:31` | Handles LLM output inconsistency |
| **Port 11435** | `causal_extractor.py:35` | Non-standard Ollama port (check env) |

---

## Integration Points and External Dependencies

### External Services

| Service | Purpose | Integration | Key Files |
|---------|---------|-------------|-----------|
| **OpenAlex API** | Paper metadata & abstracts | REST, no auth required | `client.py`, `scalable_fetcher.py` |
| **arXiv API** | Paper PDFs (MVP) | `arxiv` Python library | `paper_retriever.py` |
| **Ollama** | LLM inference | Local REST API | `causal_extractor.py`, `query_rephraser.py` |

### Ollama Configuration

```python
# Current configuration (causal_extractor.py)
base_url = os.getenv("OLLAMA_BASE_URL", "http://localhost:11435")
llm_model = "qwen2.5:14b-instruct"
embed_model = "nomic-embed-text"
request_timeout = 120.0
```

**Note:** Default Ollama port is 11434, but codebase uses 11435. Check `OLLAMA_BASE_URL` environment variable.

---

## Development and Deployment

### Local Development Setup

```bash
# 1. Clone and enter directory
cd GRA_AI_Scientist/rag_prototype

# 2. Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
# or: venv\Scripts\activate  # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Ensure Ollama is running
ollama serve  # Default port 11434

# 5. Pull required models
ollama pull qwen2.5:14b-instruct
ollama pull nomic-embed-text

# 6. Run pipeline
python app.py "What affects student performance?"
```

### CLI Options

```bash
python app.py [QUESTION] [OPTIONS]

Options:
  --papers INT      Maximum papers to retrieve (default: 5)
  --details         Show detailed breakdown
  --clear           Clear cached papers
  --llm MODEL       Ollama LLM model (default: qwen2.5:14b-instruct)
  --embed MODEL     Embedding model (default: nomic-embed-text)
```

### Container Deployment

```bash
# Build container
podman build -t rag-prototype -f Containerfile .

# Run with compose
podman-compose up
```

---

## Testing Reality

### Current Test Coverage

| Type | Coverage | Location |
|------|----------|----------|
| **Unit Tests** | Minimal | None found |
| **Integration Tests** | Manual | `test_stroke_filters.py` |
| **E2E Tests** | Manual | Run `app.py` manually |
| **Test Results** | Documented | `docs/TEST_RESULTS.md` |

### Running Tests

```bash
# No formal test suite - run manually:
python app.py "What affects stroke rehabilitation?"

# Test OpenAlex filters:
python src/open_alex_pipeline/test_stroke_filters.py
```

---

## Enhancement Impact Analysis

### Files That Will Need Modification

Based on the CAIS enhancement requirements:

| File | Changes Required |
|------|------------------|
| `causal_extractor.py` | New extraction prompts (H.1, H.2, H.3), CAIS variable extraction |
| `aggregator.py` | New output format (Aims\|Data\|Analysis\|Methods\|Findings), CSV export, impact ranking |
| `app.py` | CAIS 4-stage orchestration, new CLI options (--topic, --count) |

### New Files/Modules Needed

```
rag_prototype/
├── src/
│   ├── orchestration/              # NEW: CAIS pipeline
│   │   ├── __init__.py
│   │   ├── interfaces.py           # Abstract base classes
│   │   ├── cais_pipeline.py        # 4-stage orchestration
│   │   ├── method_selector.py      # Stage 2: Decision tree
│   │   ├── method_validator.py     # Stage 3: Assumption checks
│   │   └── config.py               # Formula/method config
│   └── rag_pipeline/
│       ├── framework_educator.py   # NEW: Framework context injection
│       └── output_formatter.py     # NEW: CSV/JSON formatting
├── prompts/                        # NEW: Prompt templates
│   ├── causal_query_parsing.txt    # H.1
│   ├── dataset_analysis.txt        # H.2
│   ├── iv_identification.txt       # H.3
│   ├── rdd_identification.txt      # H.3
│   └── structured_extraction.txt
└── output/                         # NEW: Demo outputs
    └── {topic}_{timestamp}.csv
```

### Integration Considerations

- Must use existing OpenAlex pipeline unchanged
- Must follow existing response format patterns
- Must maintain CLI interface compatibility
- Must work with current Ollama configuration

---

## Appendix - Useful Commands and Scripts

### Frequently Used Commands

```bash
# Start Ollama (if not running as service)
ollama serve

# Run demo pipeline
python app.py "What affects stroke rehabilitation outcomes?" --papers 10

# Fetch OpenAlex papers (scalable)
python src/open_alex_pipeline/scalable_fetcher.py

# Test stroke filters
python src/open_alex_pipeline/test_stroke_filters.py
```

### Environment Variables

```bash
# Ollama configuration
export OLLAMA_BASE_URL="http://localhost:11434"  # Note: code default is 11435

# OpenAlex polite pool (faster responses)
export OPENALEX_EMAIL="your-email@example.com"
```

### Debugging

- **Logs:** stdout (no log files)
- **Debug Mode:** Add `--details` flag for verbose output
- **Common Issues:**
  - Ollama not running → "Connection refused"
  - Wrong port → Check `OLLAMA_BASE_URL`
  - Model not pulled → Run `ollama pull qwen2.5:14b-instruct`

---

## Summary

This brownfield architecture document captures the actual state of the GRA AI Scientist codebase. Key findings:

1. **Production-ready:** OpenAlex pipeline (`client.py`, `scalable_fetcher.py`, `filters.py`)
2. **Needs modification:** RAG pipeline (`causal_extractor.py`, `aggregator.py`, `app.py`)
3. **New modules needed:** CAIS orchestration, prompt templates, output formatter
4. **Technical debt:** Port mismatch (11435 vs 11434), brittle parsing, no persistence

The enhancement should preserve the OpenAlex pipeline while transforming the RAG pipeline to use CAIS methodology and output Research Framework format.
