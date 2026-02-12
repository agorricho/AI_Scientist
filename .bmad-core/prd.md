# GRA AI Scientist - Demo Prototype PRD

**Version:** 1.0
**Status:** DRAFT
**Created:** 2026-01-30
**Demo Target:** 2026-01-31

---

## 1. Introduction and Project Context

### 1.1 Analysis Source

- **Project Brief**: `docs/brief.md` (created by Mary, Analyst Agent)
- **Gap Analysis**: `docs/rag_prototype_evaluation.md`
- **Existing Codebase**: `rag_prototype/` (MVP complete)

### 1.2 Current Project State

**GRA AI Scientist** is a Causal AI Scientist—a research system designed to autonomously identify impactful academic studies by performing causal inference rather than relying on hardcoded heuristics.

**Existing Assets (Production-Ready):**
| Component | Location | Status |
|-----------|----------|--------|
| OpenAlex Pipeline | `src/open_alex_pipeline/` | ✅ Production-ready |
| Scalable Fetcher | `scalable_fetcher.py` | ✅ Working |
| RAG Pipeline | `src/rag_pipeline/` | ✅ MVP complete |
| Stroke Rehab Filters | `stroke_rehabilitation/` | ✅ Pre-configured |
| Online Health Filters | `online_health_services/` | ✅ Pre-configured |
| Ollama Integration | qwen2.5:14b-instruct | ✅ Working |
| ChromaDB Vector Store | Built-in | ✅ Working |

**Current Output Format:** `FACTOR | EFFECT | SIGNIFICANCE`

**Required Output Format:** `Aims | Data | Analysis | Methods | Findings`

### 1.3 Enhancement Scope Definition

**Enhancement Type:**
- [x] Major Feature Modification
- [x] Integration with New Systems

**Enhancement Description:**
Transform the existing RAG prototype from a simple causal extraction tool (X→Y relationships) into a framework-educated Research & Analysis Agent that produces structured scholarly output following the Research Comparison Framework format, with causal inference capabilities to explain *why* studies are impactful.

**Impact Assessment:**
- [x] Moderate Impact (some existing code changes)

**Rationale:** The core pipeline exists. We're changing the *output format* and *prompt structure*, not the fundamental architecture.

---

## 2. Goals and Success Metrics

### 2.1 Demo Goals (Tomorrow)

| Goal | Success Metric |
|------|----------------|
| **End-to-end pipeline** | OpenAlex scrape → Agent analysis → Structured CSV output |
| **Framework-educated agent** | Agent produces Aims \| Data \| Analysis \| Methods \| Findings columns |
| **Correct metadata parsing** | Each column contains relevant info extracted from abstract metadata |
| **Output scale** | 20-60 relevant studies from 100-500 input abstracts |
| **Configurable topic** | Demonstrate with at least ONE topic (stroke rehabilitation OR online health) |
| **Causal reasoning visible** | Output includes "why" explanations based on causal variables |

### 2.2 Background Context

Graduate research assistants face an overwhelming volume of academic literature (10,000+ papers per topic). Existing AI tools use hardcoded metrics (citation counts, keyword matching) that cannot explain *why* certain studies are impactful.

This demo prototype proves that an LLM can be "educated" on research frameworks and statistical methodology, then independently synthesize structured outputs that replicate how a human scientist evaluates literature—through understanding rather than pattern matching.

---

## 3. Functional Requirements

### 3.1 Core Functional Requirements

- **FR1:** The system shall accept a configurable academic topic (e.g., "stroke rehabilitation") as input
- **FR2:** The system shall retrieve 100-500 abstracts from OpenAlex API using existing `scalable_fetcher.py`
- **FR3:** The system shall parse each abstract and extract structured columns:
  - **Aims**: Main objective of the study
  - **Data**: Data source, collection method, sample size
  - **Analysis**: Variable/disparity being studied (domain-configurable)
  - **Methods**: Statistical/ML method employed OR intervention/treatment applied
  - **Findings**: Key insights and causal relationships identified
- **FR4:** The system shall apply causal inference to identify studies demonstrating:
  - Treatment (T) → Outcome (Y) relationships
  - Covariate (X) adjustments
  - Statistical significance (p<0.05)
- **FR5:** The system shall output a structured CSV/JSON matching the Research Comparison Framework format
- **FR6:** The system shall reduce input corpus (100-500 abstracts) to 20-60 most relevant studies through causal ranking

### 3.2 Orchestration Interface Requirements (Placeholders)

> **Note:** These interfaces will be implemented by the user. The system provides hooks.

- **FR7:** [PLACEHOLDER] The system shall expose an `OrchestratorInterface` for external workflow control
  ```python
  class OrchestratorInterface:
      def inject_framework_education(self, framework_docs: List[str]) -> None:
          """User-provided: Inject research framework documents into agent context"""
          pass

      def configure_causal_queries(self, query_templates: Dict[str, str]) -> None:
          """User-provided: Configure statistical formula queries"""
          pass

      def on_study_processed(self, callback: Callable[[StudyResult], None]) -> None:
          """User-provided: Hook for orchestration layer to receive processed studies"""
          pass
  ```

- **FR8:** [PLACEHOLDER] The system shall accept statistical formula templates via configuration
  ```python
  # User-provided statistical formulas
  CAUSAL_FORMULAS = {
      "ATE": "τATE = E[Y(1) − Y(0)]",
      "RCT_ESTIMATION": "τ̂ATE = (1/N₁) Σᵢ:Tᵢ=1 Yᵢ − (1/N₀) Σᵢ:Tᵢ=0 Yᵢ",
      "CONDITIONAL_IGNORABILITY": "(Y(1), Y(0)) ⊥⊥ T | X",
      "LINEAR_STRUCTURAL": "Y = α + X^T β + τT + ϵ",
      "SMD": "SMD = (X̄_treated - X̄_control) / √((s²_treated + s²_control) / 2)"
  }
  ```

- **FR9:** [PLACEHOLDER] The system shall expose a decision tree interface for method selection
  ```python
  class DecisionTreeInterface:
      def select_causal_method(self, study_metadata: Dict) -> str:
          """
          User-provided: Implement CAIS decision tree logic
          Returns: "DiD" | "RDD" | "IV" | "Backdoor" | "Frontdoor" | "OLS"
          """
          pass
  ```

---

## 4. Non-Functional Requirements

- **NFR1:** Demo execution shall complete within 30 minutes for 500 abstracts (local Ollama)
- **NFR2:** System shall run entirely offline using local Ollama (qwen2.5:14b-instruct)
- **NFR3:** No user interface required—CLI output + CSV/JSON files only
- **NFR4:** System shall not hallucinate data—extract only from provided abstract metadata
- **NFR5:** System shall maintain existing `open_alex_pipeline` functionality unchanged
- **NFR6:** System shall be configurable for different academic topics without code changes

---

## 5. Compatibility Requirements

- **CR1:** Existing OpenAlex pipeline (`client.py`, `filters.py`, `scalable_fetcher.py`) must remain functional
- **CR2:** Existing RAG pipeline architecture must be preserved; changes only to prompts and output formatting
- **CR3:** Ollama model configuration must remain compatible with current `qwen2.5:14b-instruct` setup
- **CR4:** Output format must be compatible with CSV import into Excel/Google Sheets

---

## 6. Technical Constraints and Integration

### 6.1 Existing Technology Stack

| Category | Technology | Version | Notes |
|----------|------------|---------|-------|
| Runtime | Python | 3.10+ | Required |
| RAG Framework | LlamaIndex | Latest | Document indexing |
| Vector Store | ChromaDB | Embedded | Lightweight |
| LLM Provider | Ollama | Local | qwen2.5:14b-instruct |
| Embeddings | nomic-embed-text | Ollama | Local embeddings |
| Data Source | OpenAlex API | REST | No LLM involved in scraping |

### 6.2 Integration Approach

**Database Integration:** N/A for demo (file-based output)

**API Integration:**
- OpenAlex API → `scalable_fetcher.py` → JSON/CSV corpus
- Corpus → RAG Pipeline → Structured output

**Pipeline Integration:**
```
┌─────────────────────────────────────────────────────────────────────────┐
│                     GRA AI SCIENTIST - DEMO PROTOTYPE                    │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  ┌──────────────────┐    ┌────────────────────────────────────────────┐ │
│  │ OPENEX PIPELINE  │    │  RESEARCH & ANALYSIS AGENT                 │ │
│  │ (Existing)       │───>│  (Modified RAG Pipeline)                   │ │
│  │                  │    │                                            │ │
│  │ - scalable_      │    │  1. Framework Education (context inject)   │ │
│  │   fetcher.py     │    │  2. Structured Extraction Prompt           │ │
│  │ - filters.py     │    │  3. Causal Inference Prompt                │ │
│  │ - client.py      │    │  4. Output Formatter                       │ │
│  └──────────────────┘    └────────────────────────────────────────────┘ │
│           │                              │                               │
│           │                              ▼                               │
│           │              ┌────────────────────────────────────────────┐ │
│           │              │  USER-PROVIDED ORCHESTRATION               │ │
│           │              │  [PLACEHOLDER]                             │ │
│           │              │                                            │ │
│           │              │  - OrchestratorInterface                   │ │
│           │              │  - Statistical Formula Queries             │ │
│           │              │  - Decision Tree Logic                     │ │
│           │              └────────────────────────────────────────────┘ │
│           │                              │                               │
│           ▼                              ▼                               │
│  ┌──────────────────────────────────────────────────────────────────┐   │
│  │                    STRUCTURED CSV OUTPUT                          │   │
│  │   Aims | Data | Analysis | Methods | Findings                     │   │
│  └──────────────────────────────────────────────────────────────────┘   │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

### 6.3 Code Organization

**File Structure (Changes Only):**
```
rag_prototype/
├── src/
│   ├── rag_pipeline/
│   │   ├── causal_extractor.py      # MODIFY: New extraction prompt
│   │   ├── framework_educator.py    # NEW: Framework context injection
│   │   ├── output_formatter.py      # NEW: CSV/JSON output formatting
│   │   └── aggregator.py            # MODIFY: New aggregation logic
│   └── orchestration/               # NEW: User-provided orchestration
│       ├── __init__.py
│       ├── interfaces.py            # PLACEHOLDER: Interface definitions
│       └── config.py                # PLACEHOLDER: Formula/decision tree config
├── prompts/                         # NEW: Prompt templates
│   ├── framework_education.txt
│   ├── structured_extraction.txt
│   └── causal_inference.txt
└── output/                          # NEW: Demo outputs
    └── {topic}_{timestamp}.csv
```

### 6.4 Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| LLM extraction quality varies | Medium | High | Use structured prompts with examples |
| 500 abstracts may timeout | Low | Medium | Batch processing already implemented |
| Framework education too verbose | Medium | Medium | Summarize framework, use key examples |
| Output format inconsistent | Medium | Medium | Post-processing validation |

---

## 7. Epic and Story Structure

### 7.1 Epic Approach

**Epic Structure Decision:** Single Epic

**Rationale:** This is a focused enhancement to existing infrastructure. All stories contribute to one deliverable: the demo prototype. Sequential execution minimizes risk.

---

## 8. Epic 1: Demo Prototype Delivery

**Epic Goal:** Deliver a working end-to-end pipeline demonstrating framework-educated causal inference by tomorrow.

**Integration Requirements:**
- Must use existing OpenAlex pipeline unchanged
- Must output CSV compatible with Research Comparison Framework format
- Must include placeholder interfaces for user-provided orchestration

### Story 1.1: Create Framework Education Module

**As a** Research & Analysis Agent,
**I want** to receive research framework documentation as context,
**so that** I can learn the structured output format (Aims, Data, Analysis, Methods, Findings) before processing studies.

**Acceptance Criteria:**
1. New `framework_educator.py` module created
2. Module loads `.bmad-core/Example_Research_Framework.md` as context
3. Module loads example outputs (`.bmad-core/Example_Research_Framework_Output_*.csv`) as few-shot examples
4. Module exposes `get_framework_context()` function returning formatted prompt section

**Integration Verification:**
- IV1: Existing RAG pipeline still functions when module not used
- IV2: Module output integrates with LlamaIndex prompt templates
- IV3: Context injection does not exceed Ollama context window (4096 tokens budget)

---

### Story 1.2: Create Structured Extraction Prompt

**As a** Research & Analysis Agent,
**I want** a new extraction prompt template,
**so that** I extract Aims | Data | Analysis | Methods | Findings from each abstract instead of FACTOR | EFFECT | SIGNIFICANCE.

**Acceptance Criteria:**
1. New prompt template created at `prompts/structured_extraction.txt`
2. Prompt instructs LLM to extract exactly 5 columns per study
3. Prompt includes 2-3 few-shot examples from existing framework outputs
4. Prompt explicitly instructs: "Extract only from provided text. Do not infer or hallucinate."
5. `causal_extractor.py` modified to use new prompt template

**Integration Verification:**
- IV1: Output format matches `Example_Research_Framework_Output_*.csv` structure
- IV2: Extraction runs within 5 seconds per abstract on local Ollama
- IV3: Existing `paper_retriever.py` and `query_rephraser.py` unchanged

---

### Story 1.3: Create Causal Inference Prompt

**As a** Research & Analysis Agent,
**I want** a causal inference prompt that identifies treatment effects,
**so that** I can explain *why* a study is impactful based on T→Y relationships.

**Acceptance Criteria:**
1. New prompt template created at `prompts/causal_inference.txt`
2. Prompt defines causal variables: T (treatment), Y (outcome), X (covariates)
3. Prompt asks LLM to identify:
   - What intervention/treatment was applied?
   - What outcome was measured?
   - What confounders were controlled?
   - What is the statistical significance?
4. Prompt includes decision tree heuristics (simplified for demo):
   - Is this an RCT? → Report direct effect
   - Is this observational? → Report adjusted effect
5. Output includes "Causal Justification" field explaining the T→Y mechanism

**Integration Verification:**
- IV1: Causal inference runs after structured extraction (chained)
- IV2: Justification text is parseable and can be appended to CSV output
- IV3: Statistical significance filter (p<0.05) applied correctly

---

### Story 1.4: Create Output Formatter Module

**As a** researcher,
**I want** the system to output a properly formatted CSV,
**so that** I can import results into Excel or review tools.

**Acceptance Criteria:**
1. New `output_formatter.py` module created
2. Module accepts list of extracted study records
3. Module outputs CSV with columns: `Citation | Aims | Data | Analysis | Methods | Findings | Causal_Justification`
4. CSV saved to `output/{topic}_{timestamp}.csv`
5. JSON output also available for programmatic use

**Integration Verification:**
- IV1: CSV opens correctly in Excel/Google Sheets
- IV2: Special characters (quotes, newlines) properly escaped
- IV3: Output directory created if not exists

---

### Story 1.5: Create Orchestration Interface Placeholders

**As a** developer (user),
**I want** placeholder interfaces for orchestration and formula injection,
**so that** I can plug in my own logic for decision trees and statistical queries.

**Acceptance Criteria:**
1. New `src/orchestration/` package created
2. `interfaces.py` contains abstract base classes:
   - `OrchestratorInterface` (workflow control)
   - `DecisionTreeInterface` (method selection)
   - `FormulaConfigInterface` (statistical formulas)
3. `config.py` contains default placeholder implementations
4. Main pipeline accepts optional orchestrator injection
5. If no orchestrator provided, system uses simple heuristics

**Integration Verification:**
- IV1: Demo runs successfully without custom orchestrator
- IV2: Interface contracts documented with docstrings
- IV3: Placeholder implementations pass basic smoke tests

---

### Story 1.6: Wire End-to-End Pipeline

**As a** researcher,
**I want** to run a single command that executes the full pipeline,
**so that** I can demonstrate the system with one action.

**Acceptance Criteria:**
1. Modified `app.py` (or new `demo.py`) that:
   - Accepts topic parameter (default: "stroke rehabilitation")
   - Accepts abstract count parameter (default: 500)
   - Calls OpenAlex fetcher → Framework educator → Extractor → Formatter
2. CLI interface: `python demo.py --topic "stroke rehabilitation" --count 500`
3. Progress indicator shows: fetching → processing → complete
4. Final output path printed to console

**Integration Verification:**
- IV1: Pipeline completes in <30 minutes for 500 abstracts
- IV2: Output contains 20-60 ranked studies
- IV3: No crashes or unhandled exceptions during demo run

---

### Story 1.7: Validation Run with Stroke Rehabilitation Topic

**As a** stakeholder,
**I want** a successful demo run with real data,
**so that** I can verify the system works before the presentation.

**Acceptance Criteria:**
1. Execute full pipeline with stroke rehabilitation topic
2. Retrieve 300-500 abstracts from OpenAlex
3. Process all abstracts through framework-educated agent
4. Output CSV with 20-60 selected studies
5. Spot-check 5 random studies for:
   - Aims correctly extracted
   - Methods correctly identified
   - Causal justification makes sense

**Integration Verification:**
- IV1: Results comparable to manual expert review (sanity check)
- IV2: No hallucinated data in output
- IV3: Processing time acceptable for live demo

---

## 9. Causal Inference Framework Reference

> Included for developer reference when implementing prompts.

### Key Variables
- **T** = Treatment (intervention applied)
- **Y** = Outcome (target variable)
- **X** = Covariates (confounders)
- **Yi(1)** = Outcome if treatment applied
- **Yi(0)** = Outcome if no treatment

### Core Equations

**Average Treatment Effect (ATE):**
```
τATE = E[Y(1) − Y(0)]
```

**RCT Estimation:**
```
τ̂ATE = (1/N₁) Σᵢ:Tᵢ=1 Yᵢ − (1/N₀) Σᵢ:Tᵢ=0 Yᵢ
```

**Conditional Ignorability (Observational Data):**
```
(Y(1), Y(0)) ⊥⊥ T | X
```

**Linear Structural Model:**
```
Y = α + X^T β + τT + ϵ
```

**SMD (Covariate Balance):**
```
SMD = (X̄_treated - X̄_control) / √((s²_treated + s²_control) / 2)
```
If SMD < 0.1 → use IPW; else → use Matching

### Decision Tree (Simplified for Demo)

```
Is this an RCT?
├── YES → Report difference in means
└── NO (Observational)
    ├── Binary treatment + temporal data?
    │   └── YES → DiD or RDD
    └── Binary treatment, no temporal?
        └── Backdoor adjustment (IPW or Matching)
```

---

## 10. CAIS Pipeline Architecture

This section defines the Causal AI Scientist (CAIS) methodology adapted for GRA AI Scientist. The system operates in **4 sequential stages** with **8 micro-tools** that read/write a **shared typed state**.

### 10.1 Shared Typed State

All micro-tools read from and write to a shared state object containing:

```python
class CAISState:
    dataset_profile: DatasetProfile       # From dataset_analyzer
    normalized_query: NormalizedQuery     # From input_parser
    analysis_plan: AnalysisPlan           # From query_interpreter
    selected_method: MethodSelection      # From method_selector (with assumptions)
    diagnostics: ValidationDiagnostics    # From method_validator
    estimates: CausalEstimates            # From method_executor
    final_report: FinalReport             # From output_formatter
```

### 10.2 Stage 1: Data Preprocessing & Query Decomposition

**Purpose:** Parse user query and dataset to extract causal inference components.

**Micro-Tools:** `input_parser` → `dataset_analyzer` → `query_interpreter`

---

#### 10.2.1 Input Parser (`input_parser`)

**Function:** Analyze user-specified causal queries and extract three key components.

**Extracted Components:**
1. **Query Type** - Classification of the causal question
2. **Relevant Variables** - Treatment, outcome, covariates, instruments
3. **Explicit Constraints** - Filters, conditions, subgroups

**Strategy:** Hybrid approach combining:
- **Regex-based heuristics** - Pattern matching for dataset paths, variable names
- **LLM-driven structured parsing** - Semantic understanding of query intent

**Query Type Classification:**

| Query Type | Keywords/Patterns | Example |
|------------|-------------------|---------|
| `EFFECT_ESTIMATION` | "effect", "impact", "influence", "cause", "affect" | "Does robotic therapy improve motor recovery?" |
| `COUNTERFACTUAL` | "what if", "if X had been", "would Y have changed" | "What if the patient had received standard therapy instead?" |
| `CORRELATION` | "correlation", "association", "relationship", "linked to" | "Is therapy duration associated with recovery rate?" |
| `DESCRIPTIVE` | "summarize", "describe", "average", "trend" | "What is the average recovery time?" |
| `OTHER` | None of the above | Fallback category |

**Schema-Enforced Variable Roles:**

```json
{
  "query_type": "EFFECT_ESTIMATION",
  "variables": {
    "treatment": ["intervention_type"],
    "outcome": ["recovery_score"],
    "covariates_mentioned": ["age", "severity"],
    "grouping_vars": ["hospital_id"],
    "instruments_mentioned": []
  },
  "constraints": ["post_stroke_patients", "age > 18"],
  "dataset_path_mentioned": "stroke_rehab_data.csv"
}
```

**Validation:**
- LLM output validated for logical consistency (e.g., EFFECT_ESTIMATION requires both treatment AND outcome)
- Variable names validated against dataset columns when available
- Regex fallback for dataset path extraction

---

#### 10.2.2 Dataset Analyzer (`dataset_analyzer`)

**Function:** Profile the dataset to identify characteristics relevant for causal inference.

**Analysis Components:**

| Component | Description | Output |
|-----------|-------------|--------|
| **Basic Metadata** | Rows, columns, file name, data types | `{rows: 4500, cols: 12, types: {...}}` |
| **Temporal Structures** | Time-based patterns, panel data | `{has_temporal: true, time_col: "visit_date"}` |
| **Discontinuities** | Threshold-based treatment assignments | `{running_var: "distance", cutoff: 40}` |
| **Correlations** | Numeric variable correlations | `{corr_matrix: [...]}` |
| **Treatment/Outcome Candidates** | Heuristic + LLM identification | `{treatments: [...], outcomes: [...]}` |
| **Instrumental Variables** | Candidate instruments | `{instruments: ["distance_to_clinic"]}` |

**Binary Treatment Analysis:**

For binary treatment candidates, compute per-group summary statistics to facilitate balance checks:

```python
{
  "treatment_var": "robotic_therapy",
  "group_stats": {
    "treated": {"n": 2250, "age_mean": 62.3, "age_std": 12.1},
    "control": {"n": 2250, "age_mean": 61.8, "age_std": 11.9}
  },
  "smd_age": 0.04  # Standardized Mean Difference
}
```

**LLM Prompts:** Lightweight, framed as direct questions:

```
You are an expert causal inference data scientist. Identify potential treatment
and outcome variables from this dataset.

Dataset Description: {description_text}
Dataset Columns: {columns_list}
Binary Columns (good treatment candidates): {binary_cols}

Output: ONLY a valid JSON object with two lists:
{"potential_treatments": [...], "potential_outcomes": [...]}
```

**Final Output:** Comprehensive dictionary consolidating:
- Dataset information (metadata, types, missing values)
- Candidate causal variables (treatments, outcomes, instruments)
- Detected structures (temporal, panel, discontinuities)
- Diagnostic statistics (correlations, balance checks)

---

#### 10.2.3 Query Interpreter (`query_interpreter`)

**Function:** Reconcile the normalized query with the dataset profile to materialize the formal analysis plan.

**Materialized Variables:**

| Variable | Symbol | Description | Example |
|----------|--------|-------------|---------|
| Treatment | **T** | Intervention being studied | `robotic_therapy` (binary) |
| Outcome | **Y** | Result being measured | `motor_recovery_score` (continuous) |
| Covariates | **X** | Pre-treatment confounders | `[age, severity, prior_function]` |
| Instruments | **Z** | Variables for IV analysis | `[distance_to_clinic]` |
| Running Variable | **R** | For RDD, with cutoff **c** | `age` with `c=21` |
| Time Indicator | **t** | For DiD analysis | `post_policy` (binary) |
| Group Indicator | **g** | For DiD analysis | `treatment_state` (binary) |

**Targeted LLM Prompts:**

The system issues specific prompts for each variable type (from CAIS Appendix H.3):

1. **Treatment Identification Prompt** → Identify which column is the treatment
2. **Outcome Identification Prompt** → Identify which column is the outcome
3. **Covariates Identification Prompt** → Identify pre-treatment control variables
4. **Instrumental Variable Identification Prompt** → Assess if valid IV exists
5. **RDD Identification Prompt** → Check for running variable + cutoff
6. **RCT Identification Prompt** → Determine if data is from randomized trial
7. **DiD Term Identification Prompt** → Check for temporal treatment indicator

**Validation:**
- Responses aggregated across all prompts
- Validated for coherence with dataset schema
- Validated against causal design assumptions (e.g., IV requires relevance + exclusion)

**Final Output:** Structured Analysis Plan

```python
class AnalysisPlan:
    treatment: str                    # Column name for T
    outcome: str                      # Column name for Y
    covariates: List[str]             # Column names for X
    estimand: str                     # "ATE" | "ATT" | "LATE" | "RDD" | "DiD"

    # Design-specific fields (optional)
    instrument: Optional[str]         # Z for IV analysis
    running_variable: Optional[str]   # R for RDD
    cutoff: Optional[float]           # c for RDD
    time_indicator: Optional[str]     # t for DiD
    group_indicator: Optional[str]    # g for DiD

    # Encoding details
    treatment_reference: Optional[str]  # Reference level for categorical T
    interaction_term: Optional[str]     # For heterogeneous treatment effects
```

---

#### 10.2.4 Stage 1 Flow Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    STAGE 1: DATA PREPROCESSING & QUERY DECOMPOSITION         │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  USER INPUT                                                                  │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐              │
│  │ Natural Language│  │ Dataset (CSV)   │  │ Dataset         │              │
│  │ Query           │  │                 │  │ Description     │              │
│  └────────┬────────┘  └────────┬────────┘  └────────┬────────┘              │
│           │                    │                    │                        │
│           ▼                    ▼                    ▼                        │
│  ┌─────────────────────────────────────────────────────────────────┐        │
│  │                      input_parser                                │        │
│  │  • Regex heuristics + LLM parsing                               │        │
│  │  • Classify query type                                          │        │
│  │  • Extract variable roles                                       │        │
│  │  • Validate logical consistency                                 │        │
│  └─────────────────────────────┬───────────────────────────────────┘        │
│                                │                                             │
│                                ▼                                             │
│  ┌─────────────────────────────────────────────────────────────────┐        │
│  │                     dataset_analyzer                             │        │
│  │  • Basic metadata (rows, cols, types)                           │        │
│  │  • Temporal/panel/discontinuity detection                       │        │
│  │  • Treatment/outcome candidate identification                   │        │
│  │  • Binary treatment balance statistics                          │        │
│  │  • Instrumental variable assessment                             │        │
│  └─────────────────────────────┬───────────────────────────────────┘        │
│                                │                                             │
│                                ▼                                             │
│  ┌─────────────────────────────────────────────────────────────────┐        │
│  │                     query_interpreter                            │        │
│  │  • Issue targeted prompts for T, Y, X, Z, R, t, g               │        │
│  │  • Aggregate LLM responses                                      │        │
│  │  • Validate against dataset schema                              │        │
│  │  • Validate causal design assumptions                           │        │
│  │  • Output: Formal Analysis Plan                                 │        │
│  └─────────────────────────────┬───────────────────────────────────┘        │
│                                │                                             │
│                                ▼                                             │
│                    ┌───────────────────────┐                                 │
│                    │   SHARED STATE        │                                 │
│                    │   - dataset_profile   │                                 │
│                    │   - normalized_query  │                                 │
│                    │   - analysis_plan     │                                 │
│                    └───────────────────────┘                                 │
│                                │                                             │
│                                ▼                                             │
│                         TO STAGE 2                                           │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### 10.3 Stage 2: Method Selection

**Purpose:** Select the appropriate causal inference method based on the analysis plan.

**Micro-Tool:** `method_selector`

**Critical Design Principle:** This stage is **completely deterministic** and requires **NO LLM involvement**. The decision tree encodes standard causal design logic derived from established econometric and statistical methodology.

---

#### 10.3.1 Method Selector (`method_selector`)

**Function:** Given the analysis plan from Stage 1, traverse a rule-based decision tree to select a candidate estimator.

**Inputs (from Stage 1):**
- `analysis_plan.treatment` - Treatment variable T
- `analysis_plan.outcome` - Outcome variable Y
- `analysis_plan.covariates` - Covariate set X
- `analysis_plan.instrument` - Instrumental variable Z (if any)
- `analysis_plan.running_variable` - Running variable R with cutoff c (if any)
- `analysis_plan.time_indicator` - Temporal indicator t (if any)
- `dataset_profile.is_rct` - Whether data is from RCT
- `dataset_profile.has_temporal` - Whether temporal structure exists
- `dataset_profile.smd_values` - Covariate balance statistics

**Outputs:**
1. **Selected Method** - The chosen causal inference method
2. **Assumption Checklist** - List of assumptions to validate in Stage 3
3. **Fallback List** - Ordered list of alternative methods if validation fails

---

#### 10.3.2 Decision Tree Logic

The decision tree logic is fully specified in Section 9 (simplified) and the Project Brief (full). The complete tree is reproduced here for implementation reference:

```
                            ┌─────────────────────────┐
                            │  Is this a Randomized   │
                            │  Controlled Trial?      │
                            └───────────┬─────────────┘
                                        │
                    ┌───────────────────┴───────────────────┐
                    │ YES                                   │ NO
                    ▼                                       ▼
        ┌───────────────────────┐               ┌───────────────────────┐
        │ Is this an            │               │ Is treatment binary?  │
        │ Encouragement Design? │               │                       │
        │ (T ≠ D)               │               └───────────┬───────────┘
        └───────────┬───────────┘                           │
                    │                       ┌───────────────┴───────────────┐
        ┌───────────┴───────────┐           │ YES                           │ NO
        │ YES           │ NO    │           ▼                               ▼
        ▼               ▼       │   ┌───────────────────┐       ┌───────────────────┐
  ┌───────────┐  ┌───────────┐  │   │ Is temporal       │       │ Generalized       │
  │    IV     │  │ Pre-treat │  │   │ information       │       │ Propensity Scores │
  │           │  │ vars?     │  │   │ available?        │       │ (GPS)             │
  └───────────┘  └─────┬─────┘  │   └─────────┬─────────┘       └───────────────────┘
                       │        │             │
               ┌───────┴───────┐│     ┌───────┴───────┐
               │ YES       │ NO││     │ YES       │ NO │
               ▼           ▼   ││     ▼           ▼    │
        ┌───────────┐ ┌─────────┐│ ┌─────────┐ ┌───────────────────┐
        │ OLS with  │ │Diff in  ││ │ DiD or  │ │ Valid backdoor    │
        │ pre-treat │ │ Means   ││ │ RDD?    │ │ adjustment set?   │
        │ variables │ │         ││ └────┬────┘ └─────────┬─────────┘
        └───────────┘ └─────────┘│      │               │
                                 │      │       ┌───────┴───────┐
                                 │      │       │ YES       │ NO │
                                 │      │       ▼           ▼    │
                                 │      │ ┌───────────┐ ┌───────────────┐
                                 │      │ │ Covariates│ │ Valid         │
                                 │      │ │ balanced? │ │ Instrument?   │
                                 │      │ │ SMD<0.1?  │ └───────┬───────┘
                                 │      │ └─────┬─────┘         │
                                 │      │       │       ┌───────┴───────┐
                                 │      │ ┌─────┴─────┐ │ YES       │ NO │
                                 │      │ │YES    │ NO│ ▼           ▼    │
                                 │      │ ▼       ▼   │┌─────┐ ┌─────────────┐
                                 │      │┌─────┐┌─────┐││ IV  │ │ Frontdoor   │
                                 │      ││ IPW ││Match│││     │ │ Criterion?  │
                                 │      │└─────┘└─────┘│└─────┘ └──────┬──────┘
                                 │      │             │               │
                                 │      │             │       ┌───────┴───────┐
                                 │      │             │       │ YES       │ NO │
                                 │      │             │       ▼           ▼    │
                                 │      │             │ ┌───────────┐ ┌───────┐
                                 │      │             │ │ Frontdoor │ │ FAIL  │
                                 │      │             │ │ Adjustment│ │       │
                                 │      │             │ └───────────┘ └───────┘
```

---

#### 10.3.3 Decision Node Specifications

**E.2 Randomized Controlled Trials (RCTs)**

| Node | Question | Logic |
|------|----------|-------|
| **RCT Check** | Is the data from a randomized controlled trial? | Check `dataset_profile.is_rct` or `analysis_plan` metadata |
| **Encouragement Design** | Is treatment assignment ≠ treatment uptake (T ≠ D)? | If compliance data exists and some units didn't follow assignment |
| **Pre-treatment Variables** | Are there valid pre-treatment covariates? | Check if `analysis_plan.covariates` is non-empty |

**RCT Method Outputs:**

| Condition | Method | Estimand |
|-----------|--------|----------|
| Encouragement Design | **Instrumental Variables (IV)** | LATE (Local Average Treatment Effect) |
| Standard RCT + Pre-treatment vars | **OLS with pre-treatment variables** | ATE |
| Standard RCT, no pre-treatment vars | **Difference in Means** | ATE |

---

**E.3 Observational Studies**

| Node | Question | Logic |
|------|----------|-------|
| **Binary Treatment** | Is treatment variable binary? | Check `dataset_profile.treatment_type == "binary"` |
| **Temporal Info** | Is temporal information available? | Check `analysis_plan.time_indicator` is not null |
| **Running Variable** | Is there a running variable with cutoff? | Check `analysis_plan.running_variable` and `cutoff` |
| **Backdoor Set** | Is there a valid backdoor adjustment set? | Check `analysis_plan.covariates` blocks all backdoor paths |
| **Covariate Balance** | Are covariates balanced (SMD < 0.1)? | Check `dataset_profile.smd_values` |
| **Valid Instrument** | Is there a valid instrumental variable? | Check `analysis_plan.instrument` with relevance + exclusion |
| **Frontdoor Criterion** | Is there a valid mediator satisfying frontdoor? | Check for mediator M that intercepts T→Y path |

**Observational Method Outputs:**

| Condition | Method | Assumptions |
|-----------|--------|-------------|
| Binary + Temporal | **Difference-in-Differences (DiD)** | Parallel trends |
| Binary + Running var + Cutoff | **Regression Discontinuity (RDD)** | Continuity at cutoff |
| Binary + Backdoor + SMD < 0.1 | **Inverse Probability Weighting (IPW)** | Positivity, no unmeasured confounding |
| Binary + Backdoor + SMD ≥ 0.1 | **Matching** | Positivity, no unmeasured confounding |
| Valid Instrument | **Instrumental Variables (IV)** | Relevance, exclusion restriction |
| Frontdoor Criterion | **Frontdoor Adjustment** | Mediator intercepts all T→Y paths |
| Non-binary treatment | **Generalized Propensity Scores (GPS)** | Weak unconfoundedness |

---

#### 10.3.4 Method Hierarchy

When multiple methods are applicable, prefer in this order:

```
1. Instrumental Variables (IV)     ← Handles unmeasured confounding
2. Frontdoor Adjustment            ← Handles unmeasured confounding
3. Difference-in-Differences (DiD) ← Exploits temporal structure
4. Regression Discontinuity (RDD)  ← Exploits threshold assignment
5. Backdoor Adjustment (IPW/Match) ← Requires all confounders observed
```

**Rationale:** IV and Frontdoor can handle unobserved confounders; Backdoor methods require the strong assumption that all confounders are measured.

---

#### 10.3.5 Assumption Checklist Generation

For each selected method, `method_selector` generates an assumption checklist for Stage 3 validation:

| Method | Assumptions to Validate |
|--------|------------------------|
| **Difference in Means** | Random assignment, SUTVA |
| **OLS with pre-treatment** | Random assignment, SUTVA, linearity |
| **IV** | Relevance (Cov(Z,T) ≠ 0), Exclusion restriction, Independence |
| **DiD** | Parallel trends, No anticipation, SUTVA |
| **RDD** | Continuity at cutoff, No manipulation, Local randomization |
| **IPW** | Positivity, No unmeasured confounding, Correct propensity model |
| **Matching** | Positivity, No unmeasured confounding, Common support |
| **Frontdoor** | Mediator intercepts all paths, No T→M confounding, T blocks M→Y confounding |
| **GPS** | Weak unconfoundedness, Correct GPS model |

---

#### 10.3.6 Fallback List Generation

The `method_selector` also emits an **ordered fallback list** based on the decision tree path. If Stage 3 validation fails, the system backtracks to the next method in this list.

**Example Fallback Generation:**

```python
# If selected method is DiD but parallel trends fails:
fallback_list = [
    "RDD",           # Try RDD if running variable exists
    "IPW",           # Fall back to backdoor adjustment
    "Matching",      # If IPW positivity fails
    "IV",            # If instrument exists
]
```

---

#### 10.3.7 Stage 2 Output Structure

```python
class MethodSelection:
    selected_method: str                    # "DiD" | "RDD" | "IV" | "IPW" | "Matching" | etc.
    estimand: str                           # "ATE" | "ATT" | "LATE" | "RDD_effect" | "DiD_effect"
    assumptions: List[Assumption]           # Checklist for Stage 3
    fallback_list: List[str]                # Ordered alternatives
    decision_path: List[DecisionNode]       # Trace of tree traversal (for explainability)

class Assumption:
    name: str                               # "parallel_trends"
    description: str                        # "Treatment and control groups would have..."
    testable: bool                          # True if can be statistically tested
    test_method: Optional[str]              # "pre_trend_test" | "mccrary_test" | etc.
```

---

#### 10.3.8 Stage 2 Flow Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         STAGE 2: METHOD SELECTION                            │
│                         (DETERMINISTIC - NO LLM)                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  FROM STAGE 1                                                                │
│  ┌───────────────────────┐                                                   │
│  │   SHARED STATE        │                                                   │
│  │   - dataset_profile   │                                                   │
│  │   - analysis_plan     │                                                   │
│  └───────────┬───────────┘                                                   │
│              │                                                               │
│              ▼                                                               │
│  ┌─────────────────────────────────────────────────────────────────┐        │
│  │                      method_selector                             │        │
│  │                                                                  │        │
│  │  ┌─────────────────────────────────────────────────────────┐    │        │
│  │  │              DECISION TREE TRAVERSAL                     │    │        │
│  │  │                                                          │    │        │
│  │  │  1. Check: Is RCT?                                       │    │        │
│  │  │     ├─ YES → Check encouragement design                  │    │        │
│  │  │     └─ NO  → Check binary treatment                      │    │        │
│  │  │                                                          │    │        │
│  │  │  2. Follow tree path based on analysis_plan fields       │    │        │
│  │  │                                                          │    │        │
│  │  │  3. Reach leaf node → Selected Method                    │    │        │
│  │  │                                                          │    │        │
│  │  └─────────────────────────────────────────────────────────┘    │        │
│  │                                                                  │        │
│  │  OUTPUTS:                                                        │        │
│  │  • selected_method: "DiD" | "RDD" | "IV" | "IPW" | ...          │        │
│  │  • assumptions: [parallel_trends, no_anticipation, ...]         │        │
│  │  • fallback_list: ["RDD", "IPW", "Matching", ...]               │        │
│  │  • decision_path: [node1, node2, node3, ...]                    │        │
│  │                                                                  │        │
│  └─────────────────────────────────────────────────────────────────┘        │
│              │                                                               │
│              ▼                                                               │
│  ┌───────────────────────┐                                                   │
│  │   SHARED STATE        │                                                   │
│  │   + selected_method   │                                                   │
│  │   + assumptions       │                                                   │
│  │   + fallback_list     │                                                   │
│  └───────────┬───────────┘                                                   │
│              │                                                               │
│              ▼                                                               │
│        TO STAGE 3                                                            │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

#### 10.3.9 Cross-Reference

The statistical formulas and inference methods underlying this decision tree are documented in:

- **Section 9** of this PRD: Core equations (ATE, RCT Estimation, Conditional Ignorability, SMD)
- **Project Brief** (`docs/brief.md`): Full causal inference framework with E.2-E.3.5 specifications
- **CAIS Paper** (`.bmad-core/Causal_AI_Scientist_Research.md`): Appendix E decision tree explanation, Figure 3

### 10.4 Stage 3: Validation

**Purpose:** Verify that the assumptions required by the selected method hold in the given dataset. If validation fails, backtrack to select an alternative method.

**Micro-Tool:** `method_validator`

**Critical Design Principle:** This stage is **deterministic** and requires **NO LLM involvement**. Validation is performed through statistical diagnostics and schema consistency checks.

---

#### 10.4.1 Scientific Method Analogy

Stage 3 is designed to **imitate the scientific method**:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        THE SCIENTIFIC METHOD                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  1. HYPOTHESIS FORMULATION                                                   │
│     └─ Stage 1: Query decomposition, analysis plan                          │
│                                                                              │
│  2. EXPERIMENT DESIGN                                                        │
│     └─ Stage 2: Method selection (proposed estimator)                       │
│                                                                              │
│  3. EXPERIMENT EXECUTION & VALIDATION                                        │
│     └─ Stage 3: Test assumptions against data                               │
│                                                                              │
│  4. IF INEFFECTIVE → REVISE & RETRY                                         │
│     └─ Backtrack to Stage 2, select alternative method                      │
│                                                                              │
│  5. IF EFFECTIVE → PROCEED TO RESULTS                                        │
│     └─ Stage 4: Execute method, interpret results                           │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘

When a scientist's initial experiment fails to provide valid results, they don't
abandon the research question—they revise their methodology and try an alternative
approach that is compatible with the data at hand. Stage 3 automates this process.
```

---

#### 10.4.2 Method Validator (`method_validator`)

**Function:** Verify that the statistical assumptions required by the selected method hold in the dataset.

**Inputs (from Stages 1 & 2):**
- `analysis_plan` - Variable roles (T, Y, X, Z, R, etc.)
- `dataset_profile` - Dataset characteristics and statistics
- `selected_method` - Candidate estimator from Stage 2
- `assumptions` - Checklist of assumptions to validate

**Validation Components:**

1. **Statistical Diagnostics** - Method-specific assumption tests
2. **Schema Consistency Checks** - Variable roles match dataset columns
3. **Backtracking Trigger** - Failure detection and fallback activation

---

#### 10.4.3 Statistical Diagnostics by Method

| Method | Diagnostic Test | What It Checks | Failure Condition |
|--------|-----------------|----------------|-------------------|
| **IPW / Matching** | Overlap/Positivity Check | Treatment probability bounded away from 0 and 1 | P(T=1\|X) < 0.01 or > 0.99 for any stratum |
| **IPW / Matching** | Covariate Balance (SMD) | Covariates balanced after weighting/matching | SMD ≥ 0.1 for any covariate |
| **IV** | Relevance Test (First Stage F) | Instrument predicts treatment | F-statistic < 10 (weak instrument) |
| **IV** | Exogeneity Test | Instrument uncorrelated with error | Sargan/Hansen test p < 0.05 |
| **RDD** | Bandwidth Support | Sufficient observations near cutoff | < 30 observations in optimal bandwidth |
| **RDD** | McCrary Density Test | No manipulation of running variable | Discontinuity in density at cutoff (p < 0.05) |
| **RDD** | Covariate Continuity | Covariates smooth at cutoff | Significant jumps in covariates at cutoff |
| **DiD** | Parallel Trends Test | Pre-treatment trends are parallel | Significant interaction in pre-period |
| **DiD** | No Anticipation Check | No treatment effect before treatment | Significant effects in pre-treatment periods |
| **GPS** | Positivity Check | GPS bounded away from 0 | GPS < 0.01 for any observation |
| **All Methods** | Common Support | Overlap in covariate distributions | Non-overlapping regions in X space |

---

#### 10.4.4 Diagnostic Test Specifications

**Overlap/Positivity Check (IPW, Matching, GPS):**

```python
def check_positivity(propensity_scores: np.array, threshold: float = 0.01) -> ValidationResult:
    """
    Verify that propensity scores are bounded away from 0 and 1.
    Positivity assumption: 0 < P(T=1|X) < 1 for all X in support.
    """
    min_ps = propensity_scores.min()
    max_ps = propensity_scores.max()

    if min_ps < threshold or max_ps > (1 - threshold):
        return ValidationResult(
            passed=False,
            diagnostic="positivity_violation",
            message=f"Propensity scores outside [{threshold}, {1-threshold}]: min={min_ps:.4f}, max={max_ps:.4f}",
            suggestion="Consider trimming extreme propensity scores or using matching instead of IPW"
        )
    return ValidationResult(passed=True)
```

**Instrument Relevance Test (IV):**

```python
def check_instrument_relevance(Z: np.array, T: np.array, X: np.array, threshold: float = 10) -> ValidationResult:
    """
    Test first-stage F-statistic for instrument strength.
    Rule of thumb: F > 10 indicates strong instrument.
    """
    # Regress T on Z and X
    first_stage = OLS(T, add_constant(np.column_stack([Z, X]))).fit()
    f_stat = first_stage.fvalue

    if f_stat < threshold:
        return ValidationResult(
            passed=False,
            diagnostic="weak_instrument",
            message=f"First-stage F-statistic ({f_stat:.2f}) < {threshold}: weak instrument",
            suggestion="Instrument may be too weak for reliable IV estimation"
        )
    return ValidationResult(passed=True, f_statistic=f_stat)
```

**Parallel Trends Test (DiD):**

```python
def check_parallel_trends(df: pd.DataFrame, Y: str, T: str, time: str, group: str) -> ValidationResult:
    """
    Test for parallel pre-treatment trends between treatment and control groups.
    Regress Y on group × time interactions for pre-treatment periods.
    """
    pre_data = df[df[time] < treatment_time]

    # Test: coefficient on group × time should be insignificant
    model = OLS(Y ~ group * time, data=pre_data).fit()
    interaction_pval = model.pvalues['group:time']

    if interaction_pval < 0.05:
        return ValidationResult(
            passed=False,
            diagnostic="parallel_trends_violation",
            message=f"Pre-treatment trends not parallel (p={interaction_pval:.4f})",
            suggestion="Consider alternative identification strategy or control for trend differences"
        )
    return ValidationResult(passed=True, interaction_pvalue=interaction_pval)
```

**McCrary Density Test (RDD):**

```python
def check_mccrary_density(running_var: np.array, cutoff: float) -> ValidationResult:
    """
    Test for manipulation of the running variable at the cutoff.
    Discontinuity in density suggests sorting/manipulation.
    """
    # Estimate density on both sides of cutoff
    density_test = rdd_density_test(running_var, cutoff)

    if density_test.pvalue < 0.05:
        return ValidationResult(
            passed=False,
            diagnostic="manipulation_detected",
            message=f"Density discontinuity at cutoff (p={density_test.pvalue:.4f}): possible manipulation",
            suggestion="RDD assumptions may be violated; consider alternative methods"
        )
    return ValidationResult(passed=True, density_pvalue=density_test.pvalue)
```

---

#### 10.4.5 Schema Consistency Checks

Beyond statistical diagnostics, `method_validator` cross-checks variable roles against the dataset schema:

| Check | Description | Failure Condition |
|-------|-------------|-------------------|
| **Column Existence** | All specified variables exist in dataset | Column not found |
| **Type Compatibility** | Variables have expected types | Treatment not binary when required |
| **Missing Values** | Critical variables have no missing values | NaN in T, Y, or key covariates |
| **Cardinality** | Sufficient variation in variables | Treatment has only one level |
| **Temporal Ordering** | Time variables properly ordered | Post-treatment before pre-treatment |

```python
def validate_schema_consistency(analysis_plan: AnalysisPlan, dataset: pd.DataFrame) -> List[ValidationResult]:
    """
    Cross-check variable roles against dataset schema.
    """
    results = []

    # Check treatment variable
    if analysis_plan.treatment not in dataset.columns:
        results.append(ValidationResult(
            passed=False,
            diagnostic="missing_treatment",
            message=f"Treatment variable '{analysis_plan.treatment}' not found in dataset"
        ))
    elif dataset[analysis_plan.treatment].nunique() < 2:
        results.append(ValidationResult(
            passed=False,
            diagnostic="no_variation_treatment",
            message=f"Treatment variable '{analysis_plan.treatment}' has no variation"
        ))

    # Similar checks for outcome, covariates, instruments...
    return results
```

---

#### 10.4.6 Backtracking Mechanism

When any diagnostic test fails, the system triggers a **backtracking mechanism**:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        VALIDATION FEEDBACK LOOP                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  STAGE 2 OUTPUT                                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │  selected_method: "DiD"                                              │    │
│  │  fallback_list: ["RDD", "IPW", "Matching", "IV"]                    │    │
│  └─────────────────────────────────────────────────────────────────────┘    │
│                          │                                                   │
│                          ▼                                                   │
│              ┌───────────────────────┐                                       │
│              │   VALIDATE DiD        │                                       │
│              │   • Parallel trends   │                                       │
│              │   • No anticipation   │                                       │
│              └───────────┬───────────┘                                       │
│                          │                                                   │
│              ┌───────────┴───────────┐                                       │
│              │                       │                                       │
│         PASS ▼                  FAIL ▼                                       │
│    ┌─────────────┐         ┌─────────────────────┐                          │
│    │ TO STAGE 4  │         │ BACKTRACK           │                          │
│    └─────────────┘         │                     │                          │
│                            │ Pop from fallback:  │                          │
│                            │ next = "RDD"        │                          │
│                            └──────────┬──────────┘                          │
│                                       │                                      │
│                                       ▼                                      │
│                           ┌───────────────────────┐                          │
│                           │   VALIDATE RDD        │                          │
│                           │   • Bandwidth support │                          │
│                           │   • McCrary test      │                          │
│                           │   • Covariate cont.   │                          │
│                           └───────────┬───────────┘                          │
│                                       │                                      │
│                           ┌───────────┴───────────┐                          │
│                           │                       │                          │
│                      PASS ▼                  FAIL ▼                          │
│                 ┌─────────────┐         ┌─────────────────────┐             │
│                 │ TO STAGE 4  │         │ BACKTRACK           │             │
│                 └─────────────┘         │ next = "IPW"        │             │
│                                         └─────────────────────┘             │
│                                                   │                          │
│                                                   ▼                          │
│                                              ... continue ...                │
│                                                                              │
│  IF FALLBACK LIST EXHAUSTED:                                                 │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │  Return error: "No valid causal method found for this data"         │    │
│  │  Include: all attempted methods and their failure reasons           │    │
│  └─────────────────────────────────────────────────────────────────────┘    │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Backtracking Logic:**

```python
def validation_loop(selected_method: str, fallback_list: List[str],
                    analysis_plan: AnalysisPlan, dataset: pd.DataFrame) -> ValidationResult:
    """
    Validate selected method; if fails, iterate through fallback list.
    Guarantees every executed method is grounded in causal theory AND empirical feasibility.
    """
    methods_to_try = [selected_method] + fallback_list
    validation_history = []

    for method in methods_to_try:
        # Get assumptions for this method
        assumptions = get_method_assumptions(method)

        # Run all diagnostic tests
        results = run_diagnostics(method, assumptions, analysis_plan, dataset)
        validation_history.append((method, results))

        if all(r.passed for r in results):
            return ValidationResult(
                passed=True,
                validated_method=method,
                history=validation_history
            )

        # Log failure and continue to next method
        log_validation_failure(method, results)

    # All methods failed
    return ValidationResult(
        passed=False,
        error="No valid causal method found for this data",
        history=validation_history
    )
```

---

#### 10.4.7 Stage 3 Output Structure

```python
class ValidationDiagnostics:
    validated_method: str                   # Method that passed validation (or None)
    passed: bool                            # Overall validation success

    # Diagnostic results
    diagnostics: Dict[str, DiagnosticResult]  # {test_name: result}
    schema_checks: List[SchemaCheckResult]    # Schema consistency results

    # Backtracking history
    validation_history: List[ValidationAttempt]  # All methods tried

    # If failed
    error_message: Optional[str]            # Why no method worked
    failed_methods: List[FailedMethod]      # Methods tried and why they failed

class DiagnosticResult:
    test_name: str                          # "parallel_trends", "positivity", etc.
    passed: bool
    statistic: Optional[float]              # Test statistic value
    pvalue: Optional[float]                 # P-value if applicable
    threshold: Optional[float]              # Threshold used
    message: str                            # Human-readable result
    suggestion: Optional[str]               # What to do if failed

class ValidationAttempt:
    method: str
    diagnostics_run: List[str]
    all_passed: bool
    failure_reason: Optional[str]
```

---

#### 10.4.8 Stage 3 Flow Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         STAGE 3: VALIDATION                                  │
│                         (DETERMINISTIC - NO LLM)                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  FROM STAGE 2                                                                │
│  ┌───────────────────────┐                                                   │
│  │   selected_method     │                                                   │
│  │   assumptions         │                                                   │
│  │   fallback_list       │                                                   │
│  └───────────┬───────────┘                                                   │
│              │                                                               │
│              ▼                                                               │
│  ┌─────────────────────────────────────────────────────────────────┐        │
│  │                      method_validator                            │        │
│  │                                                                  │        │
│  │  ┌─────────────────────────────────────────────────────────┐    │        │
│  │  │           STATISTICAL DIAGNOSTICS                        │    │        │
│  │  │                                                          │    │        │
│  │  │  • Overlap/Positivity checks (IPW, Matching, GPS)       │    │        │
│  │  │  • Relevance/Exogeneity tests (IV)                      │    │        │
│  │  │  • Bandwidth support, McCrary test (RDD)                │    │        │
│  │  │  • Parallel trends, no anticipation (DiD)               │    │        │
│  │  │  • Common support (all methods)                         │    │        │
│  │  │                                                          │    │        │
│  │  └─────────────────────────────────────────────────────────┘    │        │
│  │                                                                  │        │
│  │  ┌─────────────────────────────────────────────────────────┐    │        │
│  │  │           SCHEMA CONSISTENCY CHECKS                      │    │        │
│  │  │                                                          │    │        │
│  │  │  • Column existence                                     │    │        │
│  │  │  • Type compatibility                                   │    │        │
│  │  │  • Missing values                                       │    │        │
│  │  │  • Cardinality/variation                                │    │        │
│  │  │                                                          │    │        │
│  │  └─────────────────────────────────────────────────────────┘    │        │
│  │                                                                  │        │
│  └─────────────────────────────────────────────────────────────────┘        │
│              │                                                               │
│              ▼                                                               │
│      ┌───────────────┐                                                       │
│      │  ALL PASSED?  │                                                       │
│      └───────┬───────┘                                                       │
│              │                                                               │
│      ┌───────┴───────┐                                                       │
│      │               │                                                       │
│ YES  ▼          NO   ▼                                                       │
│ ┌─────────┐   ┌─────────────────────────────────────────┐                   │
│ │   TO    │   │         BACKTRACKING MECHANISM          │                   │
│ │ STAGE 4 │   │                                         │                   │
│ └─────────┘   │  1. Pop next method from fallback_list  │                   │
│               │  2. Update selected_method              │                   │
│               │  3. Return to top of validation loop    │                   │
│               │                                         │                   │
│               │  IF fallback_list EMPTY:                │                   │
│               │  → Return error with validation_history │                   │
│               │                                         │                   │
│               └────────────────┬────────────────────────┘                   │
│                                │                                             │
│                                └──────────► (loop back to diagnostics)       │
│                                                                              │
│  ┌───────────────────────┐                                                   │
│  │   SHARED STATE        │                                                   │
│  │   + diagnostics       │                                                   │
│  │   + validated_method  │                                                   │
│  │   + validation_history│                                                   │
│  └───────────────────────┘                                                   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

#### 10.4.9 Validation Guarantees

The validation loop provides two critical guarantees:

| Guarantee | Description |
|-----------|-------------|
| **Causal Theory Grounding** | Every executed method has a valid causal identification strategy |
| **Empirical Feasibility** | Every executed method's assumptions are verified against the actual data |

This mimics how a scientist iteratively refines their experimental approach:

> *"When a scientist's initial experiment fails to provide valid results, they don't abandon the research question—they revise their methodology and try an alternative approach that is compatible with the data at hand."*

The validation loop automates this scientific process, ensuring that the final executed method is both theoretically sound and empirically supported.

---

#### 10.4.10 Worked Example: Method Validation Loop in Action

This example demonstrates the complete validation feedback loop using a real-world dataset from the CAIS evaluation.

---

**Query:** Does having access to electricity increase kerosene expenditures?

**Dataset:** `electrification_data.csv`

**Database:** All_Data Collection (Rural Electrification Survey)

**Description:** This household survey covers 686 households in 120 habitations across Uttar Pradesh, India. Using a geographic eligibility rule (households within 20–35 m vs. 45–60 m of a power pole), it records monthly expenditures on food, education, kerosene, total expenditure, appliance ownership, lighting usage, and satisfaction measures to assess the impact of electrification.

---

**Stage 1 Output (Analysis Plan):**

```json
{
  "query_type": "EFFECT_ESTIMATION",
  "treatment": "electricity_access",
  "outcome": "kerosene_expenditure",
  "covariates": ["total_expenditure", "household_size", "education_level"],
  "running_variable": "distance_to_pole",
  "cutoff": 40
}
```

---

**Stage 2 Output (Method Selection):**

The decision tree identifies:
- Binary treatment ✓
- Running variable with cutoff ✓ (distance to pole, 40m threshold)
- **Selected Method: RDD (Regression Discontinuity Design)**

```json
{
  "selected_method": "RDD",
  "assumptions": [
    {"name": "continuity_at_cutoff", "testable": true},
    {"name": "no_manipulation", "testable": true, "test": "mccrary_density"},
    {"name": "local_randomization", "testable": false}
  ],
  "fallback_list": ["PSM", "IPW", "Matching"]
}
```

---

**Stage 3: Validation Process**

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    VALIDATION LOOP - ELECTRIFICATION EXAMPLE                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ATTEMPT 1: RDD                                                              │
│  ─────────────────────────────────────────────────────────────────────────  │
│                                                                              │
│  Validation Test: Discontinuity at Cutoff                                    │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │  The pipeline fits local regressions on kerosene expenditure        │    │
│  │  immediately below and above the 40m cutoff to test for a sharp     │    │
│  │  discontinuity.                                                      │    │
│  │                                                                      │    │
│  │  Using lightweight model (gpt-4o-mini / qwen2.5:14b equivalent):    │    │
│  │  • Agent misidentified the "distance" variable                      │    │
│  │  • Effectively widened the window around 40m                        │    │
│  │  • Observed NO statistically significant jump (p > 0.05)            │    │
│  │                                                                      │    │
│  │  RESULT: ❌ FAILED                                                   │    │
│  │                                                                      │    │
│  │  Reason: A pronounced, localized shift at the cutoff is the         │    │
│  │  cornerstone of RDD. Absence of detectable discontinuity            │    │
│  │  constitutes a direct violation of RDD assumptions.                 │    │
│  └─────────────────────────────────────────────────────────────────────┘    │
│                                                                              │
│                          │                                                   │
│                          ▼                                                   │
│                 ┌─────────────────┐                                          │
│                 │   BACKTRACK     │                                          │
│                 │   Remove RDD    │                                          │
│                 │   from options  │                                          │
│                 └────────┬────────┘                                          │
│                          │                                                   │
│                          ▼                                                   │
│  ATTEMPT 2: PSM (Propensity Score Matching)                                  │
│  ─────────────────────────────────────────────────────────────────────────  │
│                                                                              │
│  Rationale for Selection:                                                    │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │  • Observational nature of the data ✓                               │    │
│  │  • Rich set of covariates available ✓                               │    │
│  │  • Can create balanced treatment and control groups                 │    │
│  └─────────────────────────────────────────────────────────────────────┘    │
│                                                                              │
│  Validation Tests:                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │  1. Positivity Check: P(T=1|X) ∈ (0.01, 0.99) ✓                    │    │
│  │  2. Covariate Balance: SMD < 0.1 after matching ✓                  │    │
│  │  3. Common Support: Overlapping propensity distributions ✓         │    │
│  │                                                                      │    │
│  │  RESULT: ✅ PASSED                                                   │    │
│  └─────────────────────────────────────────────────────────────────────┘    │
│                                                                              │
│                          │                                                   │
│                          ▼                                                   │
│                 ┌─────────────────┐                                          │
│                 │   PROCEED TO    │                                          │
│                 │   STAGE 4       │                                          │
│                 │   Execute PSM   │                                          │
│                 └─────────────────┘                                          │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

**Validation History Log:**

```json
{
  "validation_history": [
    {
      "attempt": 1,
      "method": "RDD",
      "diagnostics": {
        "discontinuity_test": {
          "passed": false,
          "p_value": 0.23,
          "threshold": 0.05,
          "message": "No significant discontinuity at cutoff (p=0.23 > 0.05)"
        }
      },
      "result": "FAILED",
      "action": "BACKTRACK"
    },
    {
      "attempt": 2,
      "method": "PSM",
      "diagnostics": {
        "positivity": {"passed": true, "min_ps": 0.08, "max_ps": 0.91},
        "balance": {"passed": true, "max_smd": 0.07},
        "common_support": {"passed": true, "overlap_pct": 0.94}
      },
      "result": "PASSED",
      "action": "PROCEED_TO_EXECUTION"
    }
  ],
  "final_method": "PSM",
  "total_attempts": 2
}
```

---

**Key Lessons from This Example:**

| Lesson | Implication |
|--------|-------------|
| **Model sensitivity matters** | Lightweight models may misidentify variables; validation catches this |
| **Backtracking is automatic** | System doesn't fail—it tries alternatives |
| **Rich covariates enable fallback** | PSM viable because dataset has good confounders |
| **Assumptions are testable** | RDD's discontinuity requirement is empirically verifiable |
| **Scientific method in action** | Hypothesis → Test → Fail → Revise → Succeed |

---

**Analogy:**

> *Think of this as a flight navigator using a pre-flight checklist. Instead of just "guessing" the best route based on a glance at the sky (like a standard LLM), the navigator follows a structured decision tree to account for weather, fuel, and mechanical limits. If a mid-flight check (the validation loop) reveals an unexpected storm (an assumption violation), the navigator doesn't crash—they consult their fallback plans to find a safer, more accurate path to the destination.*

---

### 10.5 Stage 4: Method Execution & Interpretation

**Purpose:** Execute the validated causal method using pre-verified templates, generate explanations, and format final output identifying the most impactful studies.

**Micro-Tools:** `method_executor` → `explanation_generator` → `output_formatter`

**Design Principle:** Execution favors **templates over code-generation** for stability and speed. LLM involvement is minimal and constrained to strict JSON outputs with deterministic fallbacks.

---

#### 10.5.1 Method Executor (`method_executor`)

**Function:** Run the validated estimator using pre-verified code templates from established statistical libraries.

**Template Library:**

| Method | Template | Library | Description |
|--------|----------|---------|-------------|
| **Difference in Means** | `diff_in_means_template` | statsmodels | Simple mean comparison for RCTs |
| **OLS with Controls** | `ols_template` | statsmodels | Linear regression with pre-treatment variables |
| **2SLS (IV)** | `iv_2sls_template` | statsmodels/linearmodels | Two-stage least squares for instrumental variables |
| **DiD** | `did_template` | statsmodels | Difference-in-differences with appropriate fixed effects |
| **RDD** | `rdd_local_poly_template` | rdrobust/statsmodels | Local polynomial regression discontinuity |
| **PSM** | `psm_matching_template` | DoWhy/causalml | Propensity score matching |
| **IPW/PSW** | `ipw_weighting_template` | DoWhy/causalml | Inverse probability weighting |
| **GPS** | `gps_template` | DoWhy | Generalized propensity scores for continuous treatment |
| **Frontdoor** | `frontdoor_template` | DoWhy | Frontdoor adjustment via mediator |

**Why Templates Over Code Generation:**

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  TEMPLATES VS CODE GENERATION                                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  CODE GENERATION (Avoided)          TEMPLATES (Preferred)                    │
│  ┌─────────────────────┐            ┌─────────────────────┐                 │
│  │ • LLM writes code   │            │ • Pre-verified code │                 │
│  │ • Runtime errors    │            │ • Tested & stable   │                 │
│  │ • Inconsistent      │            │ • Reproducible      │                 │
│  │ • Slow execution    │            │ • Fast execution    │                 │
│  │ • Security risks    │            │ • Secure            │                 │
│  └─────────────────────┘            └─────────────────────┘                 │
│                                                                              │
│  CAIS Results: Templates reduced execution errors by 33.4%                   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

#### 10.5.2 Template Execution Examples

**2SLS Instrumental Variables Template:**

```python
def execute_iv_2sls(analysis_plan: AnalysisPlan, dataset: pd.DataFrame) -> EstimationResult:
    """
    Execute two-stage least squares for instrumental variable estimation.
    Template uses linearmodels IV2SLS for robust standard errors.
    """
    from linearmodels.iv import IV2SLS

    # Build formula from analysis plan
    formula = f"{analysis_plan.outcome} ~ 1 + [{analysis_plan.treatment} ~ {analysis_plan.instrument}]"
    if analysis_plan.covariates:
        formula += " + " + " + ".join(analysis_plan.covariates)

    # Execute pre-verified template
    model = IV2SLS.from_formula(formula, data=dataset)
    results = model.fit(cov_type='robust')

    return EstimationResult(
        method="IV_2SLS",
        estimate=results.params[analysis_plan.treatment],
        std_error=results.std_errors[analysis_plan.treatment],
        pvalue=results.pvalues[analysis_plan.treatment],
        conf_int=(results.conf_int().loc[analysis_plan.treatment, 'lower'],
                  results.conf_int().loc[analysis_plan.treatment, 'upper']),
        first_stage_f=results.first_stage.diagnostics['f.stat'].stat,
        raw_results=results
    )
```

**DiD with Fixed Effects Template:**

```python
def execute_did(analysis_plan: AnalysisPlan, dataset: pd.DataFrame) -> EstimationResult:
    """
    Execute difference-in-differences with two-way fixed effects.
    """
    import statsmodels.formula.api as smf

    # DiD interaction term
    formula = f"{analysis_plan.outcome} ~ {analysis_plan.group_indicator} * {analysis_plan.time_indicator}"

    # Add fixed effects if panel data
    if analysis_plan.unit_id:
        formula += f" + C({analysis_plan.unit_id})"

    model = smf.ols(formula, data=dataset).fit(cov_type='cluster',
                                                cov_kwds={'groups': dataset[analysis_plan.unit_id]})

    # DiD coefficient is the interaction term
    did_coef = f"{analysis_plan.group_indicator}:{analysis_plan.time_indicator}"

    return EstimationResult(
        method="DiD",
        estimate=model.params[did_coef],
        std_error=model.bse[did_coef],
        pvalue=model.pvalues[did_coef],
        conf_int=(model.conf_int().loc[did_coef, 0],
                  model.conf_int().loc[did_coef, 1]),
        raw_results=model
    )
```

---

#### 10.5.3 LLM-Assisted Parameter Selection

While execution uses templates, **minimal LLM assistance** is used for parameter suggestions and coefficient identification. These assists are:

1. **Constrained to strict JSON output**
2. **Backed by deterministic fallbacks**
3. **Function-local** (scoped to specific tasks)

**Cross-Cutting Prompt: `STATSMODELS_PARAMS_IDENTIFICATION_PROMPT_TEMPLATE`**

This prompt helps select the correct coefficient(s) to report when formulas include encodings or interactions:

```python
STATSMODELS_PARAMS_IDENTIFICATION_PROMPT_TEMPLATE = """
You are a statistician identifying the correct coefficient to report from regression output.

Model Formula: {formula}
Treatment Variable: {treatment}
Parameter Names in Output: {param_names}

Task: Identify which parameter name(s) correspond to the treatment effect.

Consider:
- Categorical encodings (e.g., "C(treatment)[T.1]" for treatment=1)
- Interaction terms (e.g., "treatment:time" for DiD)
- Reference level encoding

Output: ONLY a valid JSON object:
{{"treatment_coefficient": "PARAM_NAME", "reasoning": "brief explanation"}}
"""
```

**Method-Specific LLM Helpers:**

| Method | LLM Helper | Purpose | Fallback |
|--------|------------|---------|----------|
| **IV** | `iv_param_helper` | Identify endogenous/instrument coefficients | Use first instrument column |
| **RDD** | `rdd_bandwidth_helper` | Suggest optimal bandwidth if not computed | Use IK optimal bandwidth |
| **DiD** | `did_interaction_helper` | Identify correct interaction term | Use `group:time` pattern |
| **GPS/Backdoor** | `covariate_selection_helper` | Suggest confounders if ambiguous | Use all pre-treatment variables |
| **Linear Regression** | `coefficient_interpreter` | Explain coefficient meaning | Report raw coefficient |

**Fallback Guarantee:**

```python
def llm_assisted_param_selection(prompt: str, fallback_value: str) -> str:
    """
    LLM-assisted parameter selection with deterministic fallback.
    """
    try:
        response = llm.generate(prompt, max_tokens=100, temperature=0)
        parsed = json.loads(response)

        if validate_json_schema(parsed, PARAM_SELECTION_SCHEMA):
            return parsed["treatment_coefficient"]
        else:
            return fallback_value  # Deterministic fallback

    except (JSONDecodeError, LLMError, TimeoutError):
        return fallback_value  # Deterministic fallback
```

---

#### 10.5.4 Explanation Generator (`explanation_generator`)

**Function:** Convert structured estimation artifacts into dataset-specific justification and interpretation for each study entry.

**Input:** `EstimationResult` from method_executor

**Output:** Natural language explanation with:
- Method justification (why this method was chosen)
- Effect interpretation (what the estimate means)
- Statistical significance assessment
- Causal mechanism explanation (T → Y relationship)

**Explanation Template:**

```python
def generate_explanation(result: EstimationResult, analysis_plan: AnalysisPlan,
                         validation_history: List[ValidationAttempt]) -> Explanation:
    """
    Generate dataset-specific justification and interpretation.
    """

    # Method justification
    method_justification = f"""
    Selected Method: {result.method}

    Justification: {get_method_rationale(result.method, validation_history)}

    This method was chosen because:
    - {list_method_assumptions_met(result.method, validation_history)}

    Alternative methods considered:
    - {list_alternatives_and_why_rejected(validation_history)}
    """

    # Effect interpretation
    effect_interpretation = f"""
    Treatment Effect Estimate: {result.estimate:.4f}
    Standard Error: {result.std_error:.4f}
    95% Confidence Interval: [{result.conf_int[0]:.4f}, {result.conf_int[1]:.4f}]
    P-value: {result.pvalue:.4f}

    Interpretation:
    {interpret_effect(result, analysis_plan)}

    Statistical Significance:
    {"Statistically significant at α=0.05" if result.pvalue < 0.05 else "Not statistically significant at α=0.05"}
    """

    # Causal mechanism
    causal_mechanism = f"""
    Causal Relationship: {analysis_plan.treatment} → {analysis_plan.outcome}

    The analysis suggests that {analysis_plan.treatment}
    {"increases" if result.estimate > 0 else "decreases"} {analysis_plan.outcome}
    by {abs(result.estimate):.4f} units, on average.

    Confounders Controlled: {', '.join(analysis_plan.covariates) or 'None specified'}
    """

    return Explanation(
        method_justification=method_justification,
        effect_interpretation=effect_interpretation,
        causal_mechanism=causal_mechanism,
        summary=generate_one_sentence_summary(result, analysis_plan)
    )
```

---

#### 10.5.5 Output Formatter (`output_formatter`)

**Function:** Assemble the final response object and return the most impactful studies across the research field as extracted from the causal inference analysis.

**GRA AI Scientist Integration:**

This is where the CAIS pipeline connects to the GRA AI Scientist's primary objective: **identifying the most impactful studies through causal inference**.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  FROM CAUSAL INFERENCE TO STUDY IMPACT RANKING                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  CAIS Pipeline Output                    GRA AI Scientist Output             │
│  ┌─────────────────────┐                ┌─────────────────────────────────┐ │
│  │ • Causal estimate   │                │ • Most impactful studies        │ │
│  │ • Statistical sig.  │  ──────────►   │ • Ranked by causal effect size  │ │
│  │ • Method used       │                │ • With justifications           │ │
│  │ • Assumptions met   │                │ • Research framework columns    │ │
│  └─────────────────────┘                └─────────────────────────────────┘ │
│                                                                              │
│  For each study in corpus:                                                   │
│  1. Extract T (intervention), Y (outcome), X (confounders)                   │
│  2. Apply causal inference to estimate effect size                          │
│  3. Rank studies by effect magnitude and significance                        │
│  4. Output structured table (Aims | Data | Analysis | Methods | Findings)   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Final Output Structure:**

```python
class FinalReport:
    # Study-level outputs (for each analyzed study)
    study_results: List[StudyResult]

    # Aggregated rankings
    impact_ranking: List[RankedStudy]        # Studies ranked by causal effect
    top_studies: List[StudyResult]           # Top N most impactful

    # Methodology summary
    methods_used: Dict[str, int]             # Count of methods applied
    validation_summary: ValidationSummary     # Overall validation statistics

    # Export formats
    csv_output: str                          # Path to CSV file
    json_output: str                         # Path to JSON file

class StudyResult:
    # Study identification
    citation: str                            # Study citation/reference
    title: str                               # Study title
    authors: List[str]                       # Author list

    # Research Framework Columns (Aims | Data | Analysis | Methods | Findings)
    aims: str                                # Main objective of the study
    data: str                                # Data source and collection method
    analysis: str                            # Variable/disparity being studied
    methods: str                             # Statistical/ML method employed
    findings: str                            # Key insights and causal relationships

    # Causal Inference Results
    causal_estimate: float                   # Effect size
    std_error: float                         # Standard error
    pvalue: float                            # Statistical significance
    conf_interval: Tuple[float, float]       # Confidence interval
    method_used: str                         # Causal method applied

    # Justification
    causal_justification: str                # Why this study is impactful (T→Y explanation)
    method_rationale: str                    # Why this method was selected

class RankedStudy:
    study: StudyResult
    rank: int
    impact_score: float                      # Composite score based on effect + significance
    ranking_rationale: str                   # Why this study ranks here

class OutputFormatter:
    def format_final_output(self, study_results: List[StudyResult]) -> FinalReport:
        """
        Assemble final response object with most impactful studies.
        """
        # Rank studies by impact
        ranked = self.rank_by_impact(study_results)

        # Select top studies (configurable, default 20-60)
        top_n = self.config.output_count  # From FR6: 20-60 studies
        top_studies = ranked[:top_n]

        # Generate exports
        csv_path = self.export_csv(top_studies)
        json_path = self.export_json(top_studies)

        return FinalReport(
            study_results=study_results,
            impact_ranking=ranked,
            top_studies=top_studies,
            methods_used=self.count_methods(study_results),
            validation_summary=self.summarize_validation(),
            csv_output=csv_path,
            json_output=json_path
        )

    def rank_by_impact(self, studies: List[StudyResult]) -> List[RankedStudy]:
        """
        Rank studies by causal impact using effect size and significance.
        """
        scored = []
        for study in studies:
            # Impact score: larger effects with higher significance rank higher
            # Penalize non-significant results
            if study.pvalue < 0.05:
                impact_score = abs(study.causal_estimate) * (1 - study.pvalue)
            else:
                impact_score = abs(study.causal_estimate) * 0.1  # Heavily penalized

            scored.append((study, impact_score))

        # Sort by impact score descending
        scored.sort(key=lambda x: x[1], reverse=True)

        return [
            RankedStudy(
                study=s,
                rank=i+1,
                impact_score=score,
                ranking_rationale=self.generate_ranking_rationale(s, score, i+1)
            )
            for i, (s, score) in enumerate(scored)
        ]
```

---

#### 10.5.6 CSV Output Format

The final CSV matches the Research Comparison Framework format:

```csv
Citation,Aims,Data,Analysis,Methods,Findings,Causal_Estimate,P_Value,Causal_Justification,Impact_Rank
"Smith et al. 2024","Evaluate motor recovery outcomes post-stroke using robotic therapy","EHR data from 12 rehab centers (n=4500), 2018-2023","Recovery rate variation by intervention type","Mixed-effects regression with PSM","Robotic therapy: 23% improvement (p<0.01)",0.23,0.008,"Robotic therapy (T) directly increases motor function (Y) by enabling high-intensity repetitive practice",1
"Jones et al. 2023","Compare standard vs intensive rehabilitation protocols","RCT data from 3 hospitals (n=890)","Protocol intensity effect on functional independence","DiD with hospital fixed effects","Intensive protocol: 15% faster recovery",0.15,0.023,"Treatment intensity (T) accelerates recovery (Y) through increased neuroplasticity stimulation",2
...
```

---

#### 10.5.7 Stage 4 Flow Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                  STAGE 4: METHOD EXECUTION & INTERPRETATION                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  FROM STAGE 3                                                                │
│  ┌───────────────────────┐                                                   │
│  │   validated_method    │                                                   │
│  │   analysis_plan       │                                                   │
│  │   validation_history  │                                                   │
│  └───────────┬───────────┘                                                   │
│              │                                                               │
│              ▼                                                               │
│  ┌─────────────────────────────────────────────────────────────────┐        │
│  │                      method_executor                             │        │
│  │                                                                  │        │
│  │  ┌─────────────────────────────────────────────────────────┐    │        │
│  │  │           PRE-VERIFIED TEMPLATES                         │    │        │
│  │  │                                                          │    │        │
│  │  │  • statsmodels/2SLS (IV)                                │    │        │
│  │  │  • DiD with fixed effects                               │    │        │
│  │  │  • Local polynomial RDD                                 │    │        │
│  │  │  • PSM/IPW matching/weighting                           │    │        │
│  │  │  • GPS, diff-in-means                                   │    │        │
│  │  │                                                          │    │        │
│  │  └─────────────────────────────────────────────────────────┘    │        │
│  │                                                                  │        │
│  │  ┌─────────────────────────────────────────────────────────┐    │        │
│  │  │           MINIMAL LLM ASSISTS (JSON + Fallbacks)         │    │        │
│  │  │                                                          │    │        │
│  │  │  • STATSMODELS_PARAMS_IDENTIFICATION_PROMPT              │    │        │
│  │  │  • Method-specific helpers (IV, RDD, DiD, etc.)         │    │        │
│  │  │                                                          │    │        │
│  │  └─────────────────────────────────────────────────────────┘    │        │
│  │                                                                  │        │
│  │  OUTPUT: EstimationResult (estimate, std_error, pvalue, CI)     │        │
│  └─────────────────────────────────────────────────────────────────┘        │
│              │                                                               │
│              ▼                                                               │
│  ┌─────────────────────────────────────────────────────────────────┐        │
│  │                   explanation_generator                          │        │
│  │                                                                  │        │
│  │  • Method justification (why this method)                       │        │
│  │  • Effect interpretation (what the estimate means)              │        │
│  │  • Statistical significance assessment                          │        │
│  │  • Causal mechanism explanation (T → Y)                         │        │
│  │                                                                  │        │
│  │  OUTPUT: Explanation (per study)                                │        │
│  └─────────────────────────────────────────────────────────────────┘        │
│              │                                                               │
│              ▼                                                               │
│  ┌─────────────────────────────────────────────────────────────────┐        │
│  │                     output_formatter                             │        │
│  │                                                                  │        │
│  │  • Assemble StudyResult objects                                 │        │
│  │  • Rank studies by causal impact                                │        │
│  │  • Select top 20-60 most impactful studies                      │        │
│  │  • Format Research Framework columns                            │        │
│  │    (Aims | Data | Analysis | Methods | Findings)                │        │
│  │  • Export CSV and JSON                                          │        │
│  │                                                                  │        │
│  │  OUTPUT: FinalReport with impact_ranking                        │        │
│  └─────────────────────────────────────────────────────────────────┘        │
│              │                                                               │
│              ▼                                                               │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │                         FINAL OUTPUT                                   │  │
│  │                                                                        │  │
│  │  ┌────────────────────────────────────────────────────────────────┐   │  │
│  │  │  CSV: output/{topic}_{timestamp}.csv                           │   │  │
│  │  │                                                                 │   │  │
│  │  │  Citation | Aims | Data | Analysis | Methods | Findings |      │   │  │
│  │  │  Causal_Estimate | P_Value | Causal_Justification | Rank       │   │  │
│  │  └────────────────────────────────────────────────────────────────┘   │  │
│  │                                                                        │  │
│  │  20-60 most impactful studies across the research field               │  │
│  │  Ranked by causal effect size and statistical significance            │  │
│  │                                                                        │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

#### 10.5.8 Integration with GRA AI Scientist Goals

Stage 4 directly fulfills the GRA AI Scientist's primary value proposition:

| Project Goal | Stage 4 Fulfillment |
|--------------|---------------------|
| **Identify impactful studies** | `output_formatter` ranks studies by causal effect size |
| **Explain WHY studies matter** | `explanation_generator` provides T→Y causal justifications |
| **Structured output** | Research Framework columns (Aims, Data, Analysis, Methods, Findings) |
| **Statistical rigor** | Effect estimates with confidence intervals and p-values |
| **Reproducibility** | Template-based execution ensures consistent results |
| **Domain-agnostic** | Same pipeline works for any academic topic |

The final output answers the core question: **"Which studies demonstrate the strongest causal relationships between interventions and outcomes?"**

---

### 10.6 Methodology Prompts: Query-to-Output Synthesis

This section documents the key prompts that synthesize natural language queries into structured causal analysis outputs.

#### 10.6.1 Causal Query Parsing Prompt (H.1)

**Purpose:** Parse a natural language causal query into a structured JSON object that maps directly to the Research Framework output columns.

**Full Prompt Template:**

```
Analyze the following causal query strictly in the context of the provided dataset
information (if available). Identify the query type, key variables (mapping query
terms to actual column names when possible), constraints, and any explicitly
mentioned dataset path.

User Query: "{query}"
{dataset_context}

Guidance for Identifying Query Type:

• EFFECT_ESTIMATION: Look for keywords like "effect", "impact", "influence",
  "cause", "affect", "consequence". Also consider questions asking "how does X
  affect Y?" or comparing outcomes between groups based on an intervention.

• COUNTERFACTUAL: Look for hypothetical scenarios, often using phrases like
  "what if", "if X had been", "would Y have changed", "imagine if", "counterfactual".

• CORRELATION: Look for keywords like "correlation", "association", "relationship",
  "linked to", "related to". These queries ask about statistical relationships
  without necessarily implying causality.

• DESCRIPTIVE: Queries that ask for summaries, descriptions, trends, or statistics
  about the data without investigating causal links (e.g., "Show sales over time",
  "What is the average age?").

• OTHER: Use if the query does not fit any of the above categories.

Choose the most appropriate type from: EFFECT_ESTIMATION, COUNTERFACTUAL,
CORRELATION, DESCRIPTIVE, OTHER.

Variable Roles to Identify:
• treatment: The intervention or variable whose effect is being studied.
• outcome: The result or variable being measured.
• covariates_mentioned: Variables explicitly mentioned to control for or adjust for.
• grouping_vars: Variables identifying specific subgroups for analysis (e.g., "for men",
  "in the sales department").
• instruments_mentioned: Variables explicitly mentioned as potential instruments.

Constraints: Conditions applied to the analysis (e.g., filters on columns, specific time
periods).

Dataset Path Mentioned: Extract the file path or URL if explicitly stated in the query.

Output: ONLY a valid JSON object matching this schema (no explanations or surrounding
text):

{
  "query_type": "<Identified Query Type>",
  "variables": {
    "treatment": ["<Treatment Variable(s) Mentioned>"],
    "outcome": ["<Outcome Variable(s) Mentioned>"],
    "covariates_mentioned": ["<Covariate(s) Mentioned>"],
    "grouping_vars": ["<Grouping Variable(s) Mentioned>"],
    "instruments_mentioned": ["<Instrument(s) Mentioned>"]
  },
  "constraints": ["<Constraint 1>", "<Constraint 2>"],
  "dataset_path_mentioned": "<Path Mentioned or null>"
}

Respond with only the JSON object.
```

---

#### 10.6.2 JSON-to-Research-Framework Mapping

The JSON output from the Causal Query Parsing Prompt is then organized into the Research Framework columns:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│           JSON OUTPUT → RESEARCH FRAMEWORK COLUMN MAPPING                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  JSON Field                    →    Research Framework Column                │
│  ─────────────────────────────────────────────────────────────────────────  │
│                                                                              │
│  query_type                    →    AIMS                                     │
│  + treatment                        (What the study investigates)            │
│  + outcome                                                                   │
│                                                                              │
│  dataset_context               →    DATA                                     │
│  + dataset_path                     (Data source, collection method,         │
│  + constraints                       sample size, time period)               │
│                                                                              │
│  treatment                     →    ANALYSIS                                 │
│  + outcome                          (Variable/disparity being studied,       │
│  + grouping_vars                     subgroup analysis)                      │
│                                                                              │
│  [From Stage 2/3]              →    METHODS                                  │
│  selected_method                    (Statistical/ML method employed,         │
│  + covariates_mentioned              causal inference approach)              │
│  + instruments_mentioned                                                     │
│                                                                              │
│  [From Stage 4]                →    FINDINGS                                 │
│  causal_estimate                    (Key insights, causal relationships,     │
│  + pvalue                            effect sizes, significance)             │
│  + causal_justification                                                      │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Detailed Mapping Table:**

| JSON Field | Maps To | Research Framework Column | Example |
|------------|---------|---------------------------|---------|
| `query_type` | Study objective classification | **Aims** | "EFFECT_ESTIMATION" → "Evaluate the causal effect of..." |
| `variables.treatment` | Intervention studied | **Aims** + **Analysis** | "robotic_therapy" → "...robotic-assisted therapy on motor recovery" |
| `variables.outcome` | Result measured | **Aims** + **Analysis** | "motor_recovery_score" → "...outcomes in stroke patients" |
| `dataset_context` | Data description | **Data** | "EHR data from 12 rehab centers (n=4,500), 2018-2023" |
| `constraints` | Filters/conditions | **Data** | "post_stroke_patients, age > 18" → "Adult stroke patients only" |
| `variables.covariates_mentioned` | Confounders controlled | **Methods** | "age, severity" → "Adjusted for patient age and stroke severity" |
| `variables.instruments_mentioned` | IV if applicable | **Methods** | "distance_to_clinic" → "Using distance as instrument" |
| `selected_method` (Stage 2) | Causal method | **Methods** | "PSM" → "Propensity score matching" |
| `causal_estimate` (Stage 4) | Effect size | **Findings** | "0.23" → "23% improvement in motor function" |
| `pvalue` (Stage 4) | Significance | **Findings** | "0.008" → "(p<0.01, statistically significant)" |
| `causal_justification` (Stage 4) | Why impactful | **Findings** | "Robotic therapy (T) enables high-intensity practice → improved motor function (Y)" |

---

#### 10.6.3 End-to-End Synthesis Example

**Input:** Study abstract about stroke rehabilitation

**Step 1: Causal Query Parsing** → JSON output:

```json
{
  "query_type": "EFFECT_ESTIMATION",
  "variables": {
    "treatment": ["robotic_assisted_therapy"],
    "outcome": ["motor_function_score", "recovery_time"],
    "covariates_mentioned": ["age", "stroke_severity", "time_since_stroke"],
    "grouping_vars": ["therapy_center"],
    "instruments_mentioned": []
  },
  "constraints": ["adult_patients", "ischemic_stroke_only"],
  "dataset_path_mentioned": null
}
```

**Step 2: Stage 2-4 Processing** → Causal analysis results:

```json
{
  "selected_method": "PSM",
  "causal_estimate": 0.23,
  "std_error": 0.045,
  "pvalue": 0.008,
  "conf_interval": [0.14, 0.32],
  "causal_justification": "Robotic-assisted therapy provides high-intensity, repetitive motor practice that stimulates neuroplasticity, directly causing improved motor function recovery."
}
```

**Step 3: Research Framework Output:**

| Column | Synthesized Content |
|--------|---------------------|
| **Citation** | Smith et al., 2024, Journal of Rehabilitation Medicine |
| **Aims** | Evaluate the causal effect of robotic-assisted therapy on motor recovery outcomes in adult ischemic stroke patients |
| **Data** | Multi-center EHR data from rehabilitation facilities; adult patients with ischemic stroke; controlled for age, stroke severity, and time since stroke |
| **Analysis** | Treatment effect of robotic-assisted therapy (T) on motor function score and recovery time (Y); subgroup analysis by therapy center |
| **Methods** | Propensity Score Matching (PSM) to balance treatment and control groups on observed confounders; robust standard errors |
| **Findings** | Robotic-assisted therapy caused 23% improvement in motor function (95% CI: 14-32%, p=0.008). High-intensity repetitive practice stimulates neuroplasticity, directly improving motor recovery. |
| **Causal_Justification** | Treatment (robotic therapy) → Mechanism (neuroplasticity stimulation via repetitive practice) → Outcome (improved motor function) |
| **Impact_Rank** | 1 |

---

#### 10.6.4 Synthesis Pipeline Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│              QUERY-TO-OUTPUT SYNTHESIS PIPELINE                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  STUDY ABSTRACT                                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │ "This study evaluated robotic-assisted therapy for motor recovery    │    │
│  │  in stroke patients. We analyzed data from 12 rehab centers..."      │    │
│  └─────────────────────────────────────────────────────────────────────┘    │
│                          │                                                   │
│                          ▼                                                   │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │           CAUSAL QUERY PARSING PROMPT (H.1)                          │    │
│  │           LLM extracts structured JSON                               │    │
│  └─────────────────────────────────────────────────────────────────────┘    │
│                          │                                                   │
│                          ▼                                                   │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │  JSON OUTPUT                                                         │    │
│  │  {                                                                   │    │
│  │    "query_type": "EFFECT_ESTIMATION",                               │    │
│  │    "variables": {                                                    │    │
│  │      "treatment": ["robotic_assisted_therapy"],                     │    │
│  │      "outcome": ["motor_function_score"],                           │    │
│  │      "covariates": ["age", "severity"]                              │    │
│  │    }                                                                 │    │
│  │  }                                                                   │    │
│  └─────────────────────────────────────────────────────────────────────┘    │
│                          │                                                   │
│          ┌───────────────┼───────────────┐                                  │
│          ▼               ▼               ▼                                  │
│     ┌─────────┐    ┌─────────┐    ┌─────────┐                              │
│     │ Stage 2 │    │ Stage 3 │    │ Stage 4 │                              │
│     │ Method  │───►│ Valid.  │───►│ Execute │                              │
│     │ Select  │    │         │    │         │                              │
│     └─────────┘    └─────────┘    └─────────┘                              │
│          │               │               │                                  │
│          └───────────────┴───────────────┘                                  │
│                          │                                                   │
│                          ▼                                                   │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │           RESEARCH FRAMEWORK OUTPUT                                  │    │
│  │                                                                      │    │
│  │  ┌─────────┬─────────┬──────────┬─────────┬──────────┐              │    │
│  │  │  AIMS   │  DATA   │ ANALYSIS │ METHODS │ FINDINGS │              │    │
│  │  ├─────────┼─────────┼──────────┼─────────┼──────────┤              │    │
│  │  │ From    │ From    │ From     │ From    │ From     │              │    │
│  │  │ query_  │ dataset │ treat-   │ Stage 2 │ Stage 4  │              │    │
│  │  │ type +  │ context │ ment +   │ method  │ estimate │              │    │
│  │  │ T + Y   │ + const │ outcome  │ + covar │ + p-val  │              │    │
│  │  └─────────┴─────────┴──────────┴─────────┴──────────┘              │    │
│  │                                                                      │    │
│  └─────────────────────────────────────────────────────────────────────┘    │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

#### 10.6.5 Lightweight Inline Prompts for Dataset Analysis (H.2)

**Purpose:** Quick, focused prompts used by `dataset_analyzer` to identify causal variables from dataset metadata. These prompts are lightweight and framed as direct questions to minimize token usage while maintaining accuracy.

**Treatment & Outcome Identification Prompt:**

```
You are an expert causal inference data scientist. Identify potential treatment and
outcome variables from this dataset.

Dataset Description: {description_text}
Dataset Columns: {columns_list}
Column Types: {column_types}
Binary Columns (good treatment candidates): {binary_cols}

Instructions:
1. Identify TREATMENT variables: interventions, treatments, programs, policies,
   or binary state changes. Look for binary variables or names with "treatment",
   "intervention", "program", "policy", etc.

2. Identify OUTCOME variables: results, effects, or responses to treatments. Look
   for numeric variables (especially non-binary) or names with "outcome", "result",
   "effect", "score", etc.

Output: ONLY a valid JSON object with two lists:
{
  "potential_treatments": ["treatment_a", "program_b"],
  "potential_outcomes": ["result_score", "outcome_measure"]
}
```

**Design Principles for Lightweight Prompts:**

| Principle | Implementation |
|-----------|----------------|
| **Minimal Context** | Only essential dataset metadata provided |
| **Direct Questions** | Single-purpose queries, not multi-step reasoning |
| **Strict JSON Output** | Constrained response format for parsing reliability |
| **Keyword Hints** | Explicit patterns to look for (treatment, outcome, etc.) |
| **Fallback-Ready** | Deterministic fallback if LLM fails to respond correctly |

**Additional Lightweight Prompts Used by `dataset_analyzer`:**

| Prompt | Purpose | Output Format |
|--------|---------|---------------|
| **Temporal Structure Detection** | Identify time-based columns | `{"time_column": "...", "panel_id": "..."}` |
| **Instrument Candidate Assessment** | Find potential IVs | `{"instrument_candidates": [...]}` |
| **Discontinuity Detection** | Find threshold-based assignments | `{"running_var": "...", "cutoff": ...}` |
| **Covariate Classification** | Categorize pre/post treatment vars | `{"pre_treatment": [...], "post_treatment": [...]}` |

**Example: Instrument Candidate Assessment Prompt:**

```
You are a causal inference assistant. Identify potential instrumental variables
from this dataset that could be used for IV estimation.

A valid instrument must:
1. Be correlated with the treatment (relevance)
2. Affect outcome ONLY through treatment (exclusion restriction)
3. Be as-good-as-random with respect to confounders

Dataset Columns: {columns_list}
Treatment Variable: {treatment}
Outcome Variable: {outcome}

Output: ONLY a valid JSON object:
{
  "instrument_candidates": ["column_name_1", "column_name_2"],
  "reasoning": "brief explanation for each candidate"
}
```

---

#### 10.6.6 Query Interpretation Prompts (H.3)

**Purpose:** These prompts are used by `query_interpreter` in Stage 1 to reconcile the parsed query with the dataset profile and materialize specific causal design elements (T, Y, X, Z, R, etc.).

---

**Instrumental Variable Identification Prompt:**

```
You are a causal inference assistant tasked with assessing whether a valid Instrumental
Variable (IV) exists in the dataset. A valid IV must satisfy all of the following conditions:

1. Relevance: It must causally influence the Treatment.

2. Exclusion Restriction: It must affect the Outcome only through the Treatment —
   not directly or indirectly via other paths.

3. Independence: It must be as good as randomly assigned with respect to any
   unobserved confounders affecting the Outcome.

4. Compliance (for RCTs): If the dataset comes from a randomized controlled trial
   or experiment, IVs are only valid if compliance data is available i.e., if some units
   did not follow their assigned treatment. In this case, the random assignment may be
   a valid IV, and compliance is the actual treatment variable. If compliance related
   variable is not available, do not select IV.

5. The instrument must be one of the listed dataset columns (not the treatment itself),
   and must not be assumed or invented.

You should only suggest an IV if you are confident that all the conditions are satisfied.
Otherwise, return "NULL".

Information Provided:
• User Query: {query}
• Dataset Description: {description}
• Treatment: {treatment}
• Outcome: {outcome}
• Available Columns: {column_info}

Output: Return a JSON object with the following structure:
{ "instrument_variable": "COLUMN_NAME_OR_NULL" }
```

**IV Validity Conditions Summary:**

| Condition | Test | Failure Handling |
|-----------|------|------------------|
| **Relevance** | Cov(Z, T) ≠ 0 | First-stage F-statistic > 10 |
| **Exclusion** | Z → Y only through T | Domain knowledge required |
| **Independence** | Z ⊥⊥ U | As-good-as-random assignment |
| **Compliance** | Some units don't follow assignment | Check for compliance column |
| **Column Exists** | Z ∈ dataset columns | Must be actual column, not invented |

---

**RDD Identification Prompt:**

```
You are an expert causal inference assistant helping to determine if Regression
Discontinuity Design (RDD) is applicable for quasi-experimental analysis.

Information Provided:
• User Query: {query}
• Dataset Description: {description}
• Identified Treatment (tentative): {treatment}
• Identified Outcome (tentative): {outcome}
• Available Columns: {column_info}

Task: Your goal is to check if there is a Running Variable, i.e., a variable that
determines treatment/control.

• If the variable is above a certain cutoff, the unit is categorized as treated;
  if below, it is control.
• The running variable must be numeric and continuous. Do not use categorical
  or low-cardinality variables.
• The treatment variable must be binary. If not, RDD is not valid.

Output: Respond ONLY with a valid JSON object. If RDD is not suggested by the
context, return null for both fields.

{ "running_variable": "COLUMN_NAME_OR_NULL", "cutoff_value": NUMERIC_VALUE_OR_NULL }

Examples:
{ "running_variable": "test_score", "cutoff_value": 70 }
{ "running_variable": null, "cutoff_value": null }
```

---

**RCT Identification Prompt:**

```
You are an expert causal inference assistant helping to determine if the data comes
from a Randomized Controlled Trial (RCT). Your goal is to assess if the treatment
assignment mechanism described or implied was random.

Information Provided:
• User Query: {query}
• Dataset Description: {description}
• Identified Treatment (tentative): {treatment}
• Identified Outcome (tentative): {outcome}
• Available Columns: {column_info}

Output: Respond ONLY with a valid JSON object matching the required schema.

{ "is_rct": BOOLEAN_OR_NULL }

Examples:
{ "is_rct": true }   # RCT likely
{ "is_rct": false }  # Observational likely
{ "is_rct": null }   # Unsure
```

---

**DiD Term Identification Prompt:**

```
You are a causal inference assistant tasked with determining whether a valid
Difference-in-Differences (DiD) interaction term already exists in the dataset.

This DiD term should be a binary variable indicating whether a unit belongs to
the treatment group after treatment was applied.

For example, if a policy was enacted in 2020 for a particular state, then the DiD
term would equal 1 for units from that state in years after 2020, and 0 otherwise.

Information Provided:
• User Query: {query}
• Time Variable: {time_variable}
• Group Variable: {group_variable}
• Dataset Description: {description}
• Available Columns: {column_info}
• Column Types: {column_types}

Output: Return your answer as a valid JSON object with the following format:

{ "did_term": "COLUMN_NAME_OR_NULL" }
```

---

**Treatment Variable Identification Prompt:**

```
You are an expert in causal inference. Your task is to identify the treatment
variable in a dataset in order to perform a causal analysis that answers the
user's query.

Information Provided:
• User Query: {query}
• Dataset Description: {description}
• List of Available Variables: {column_info}

Task: Based on the query, dataset description, and available variables, determine
which variable is most likely to serve as the treatment variable.

If a clear treatment variable cannot be determined, return null.

Output Schema:
{ "treatment": "COLUMN_NAME_OR_NULL" }
```

---

**Outcome Variable Identification Prompt:**

```
You are an expert in causal inference. Your task is to identify the outcome
variable in a dataset in order to perform a causal analysis that answers the
user's query.

Information Provided:
• User Query: {query}
• Dataset Description: {description}
• Available Variables: {column_info}

Task: Based on the query, dataset description, and available variables, determine
which variable is most likely to serve as the outcome variable in the causal analysis.

Do not speculate. If a clear outcome variable cannot be identified, return null.

Output Schema:
{ "outcome": "COLUMN_NAME_OR_NULL" }
```

---

**Covariates Identification Prompt:**

```
You are an expert in causal inference. Your task is to identify the pre-treatment
variables in a dataset that can be used as controls in a causal estimation model
to answer the user's query.

Information Provided:
• User Query: {query}
• Dataset Description: {description}
• Available Variables: {column_info}
• Treatment Variable: {treatment}
• Outcome Variable: {outcome}

Task: Pre-treatment variables are those that are measured before the treatment is
applied and are not affected by the treatment. These variables can be used as
controls in the causal model.

For example, in an RCT with outcome Y, treatment T, and pre-treatment variables
X1, X2, X3, we can perform a regression of the form:

Y ~ T + X1 + X2 + X3

Based on the information above, return a list of variables that qualify as
pre-treatment variables from the available columns. If no suitable pre-treatment
variables can be identified, return an empty list.

Output Schema:
{ "covariates": ["LIST_OF_COLUMN_NAMES_OR_EMPTY_LIST"] }
```

---

**Confounder Identification Prompt:**

```
You are an expert in causal inference. Your task is to identify potential
confounders in a dataset that should be adjusted for when estimating the causal
effect described in the user query.

Information Provided:
• User Query: {query}
• Dataset Description: {description}
• Available Variables: {column_info}
• Treatment Variable: {treatment}
• Outcome Variable: {outcome}

Definition of Confounder: A confounder is a variable that:
1. Affects the treatment (influences who receives the treatment),
2. Affects the outcome,
3. Is not caused by the treatment (must be a pre-treatment variable),
4. Is not a mediator between treatment and outcome.

These variables can create spurious associations between treatment and outcome
if not adjusted for.

Task: Based on the user query and the dataset description, identify which variables
are likely to be confounders. Only include variables that you believe causally affect
both treatment and outcome. If uncertain, only include variables where the
justification is clear from the query or description.

Output Schema:
{ "confounders": ["LIST_OF_COLUMN_NAMES_OR_EMPTY_LIST"] }
```

---

**Query Interpretation Prompts Summary:**

| Prompt | Purpose | Decision Tree Node |
|--------|---------|-------------------|
| **IV Identification** | Find valid instrumental variables | E.3.3 Unmeasured Confounding |
| **RDD Identification** | Find running variable + cutoff | E.3.1 Binary + Temporal |
| **RCT Identification** | Determine if randomized trial | E.2 Root node |
| **DiD Term** | Find treatment × time interaction | E.3.1 Binary + Temporal |
| **Treatment Variable** | Identify T | Stage 1 Analysis Plan |
| **Outcome Variable** | Identify Y | Stage 1 Analysis Plan |
| **Covariates** | Identify X (controls) | Stage 1 Analysis Plan |
| **Confounders** | Identify backdoor variables | E.3.2 Backdoor Adjustment |

---

## 11. Experimental Setup

This section defines the experimental configuration for evaluating and running the GRA AI Scientist system, adapted from the CAIS methodology.

### 11.1 Dataset

**Primary Data Source:** Full extracted abstracts from OpenAlex API

| Parameter | Value | Notes |
|-----------|-------|-------|
| **Data Source** | OpenAlex API | Deterministic scraping, no LLM involvement |
| **Data Format** | Full abstract metadata | Title, authors, abstract, publication date, citations, etc. |
| **Initial Corpus** | 10,000 - 56,000 abstracts | Configurable per topic |
| **Output Target** | 20-60 studies | Most impactful studies after causal analysis |
| **Pilot Topics** | Stroke Rehabilitation, Online Health Communities | Domain-agnostic after validation |

**Data Pipeline:**
```
OpenAlex API → scalable_fetcher.py → JSON/CSV corpus → CAIS Pipeline → Ranked Studies
```

### 11.2 Baseline Comparisons

Given the lack of LLM-based tools for fully automated causal inference, we compare GRA AI Scientist (CAIS-based) against three strong prompting strategies:

| Baseline | Description | Reference |
|----------|-------------|-----------|
| **ReAct Prompting** | Reasoning + Acting interleaved; shown highly effective for causal inference | Yao et al., 2023 |
| **Program of Thoughts (PoT)** | Code generation for quantitative reasoning | Chen et al., 2022 |
| **Veridical Data Science** | Rigorous scientific framework with checklists | Yu, 2020 |

---

#### 11.2.1 ReAct Prompt Template

```
You are working with a pandas DataFrame in Python. The name of the DataFrame is df.

You should use the tools below to answer the question posed to you:
python_repl_ast: A Python shell. Use this to execute Python commands.

Use the following format:
• Question: the input question you must answer
• Thought: what you should do next
• Action: the action to take (e.g., python_repl_ast)
• Action Input: the input to the action (code to execute)
• Observation: the result of the action
(This Thought/Action/Action Input/Observation can repeat N times.)

Final Answer: The final answer to the original input question. Please provide a structured
response including the following:
• Method
• Causal Effect
• Standard Deviation
• Treatment Variable
• Outcome Variable
• Covariates
• Instrument / Running Variable / Temporal Variable
• Results of Statistical Test
• Explanation for Model Choice
• Regression Equation

Instructions:
• Import libraries as needed.
• Do not create any plots.
• Use the print() function for all code outputs.
```

---

#### 11.2.2 Program of Thoughts (PoT) Prompt Template

```
You are a data analyst with strong quantitative reasoning skills. Your task is to
answer a data-driven causal question using the provided dataset.

You should analyze the first 10 rows of the dataset and then write Python code to
generalize the analysis to the full table. You may use any Python libraries.

The returned value of the program should be the final answer. Please follow this format:
def solution():
    # import libraries if needed
    # load data from {dataset_path}
    # write code to get the answer
    # return answer
print(solution())

Dataset Description: {dataset_description}
Dataset Path: {dataset_path}
First 10 rows of data: {df.head(10)}
Question: {query}

Example Methods (choose one if applicable):
• propensity_score_weighting: output the ATE
• propensity_score_matching_treatment_to_control: output the ATT
• linear_regression: output coefficient of variable of interest
• instrumental_variable: output coefficient
• matching: output the ATE
• difference_in_differences: output coefficient
• regression_discontinuity_design: output coefficient
• linear_regression / difference_in_means: output coefficient / DiM

Response: Final answer should include structured summary:
Method, Causal Effect, Standard Deviation, Treatment/Outcome Variables,
Covariates, Instruments, Statistical Test Results, Model Choice Explanation
```

---

#### 11.2.3 Veridical Data Science Prompt Template

```
You are an expert in statistics and causal reasoning. You will use a rigorous scientific
framework to answer a causal question using a structured, step-by-step process with checklists.

Problem Statement: {query}

Step 1: Domain Understanding
- What is the real-world question? Why is it important?
- Could alternate formulations impact the final result?

Step 2: Dataset Overview
- Dataset Path: {dataset_path}
- Description: {dataset_description}
- Dataset Summary, Types, Missing Values, Preview Rows

Checklist:
- How was data collected? Design principles?
- What are the variables, types, and units?
- Are there errors or pre-processing artifacts?

Step 3: Exploratory Analysis
- Identify confounders, mediators, biases
- Suspect endogeneity? What instruments might be relevant?
- Are strong correlations present?

Step 4: Modeling Strategy
- Choose 3 candidate methods (e.g., matching, regression, IV)
- State assumptions and reasons for each method
- Discuss software libraries to be used and potential pitfalls
- Outline key outputs and steps in analysis

Step 5: Post Hoc Analysis
- Are relationships or outcomes unexpected?
- Assess result stability and robustness

Step 6: Interpretation and Reporting
Final Answer: Report Method, Causal Effect, Standard Deviation, Treatment/Outcome
Variables, Covariates, Instruments, Statistical Tests, Model Choice Justification
```

---

### 11.3 Implementation Details

#### 11.3.1 Statistical Libraries

| Library | Version | Purpose |
|---------|---------|---------|
| **DoWhy** | Latest | Causal inference framework (effect estimation, refutation) |
| **statsmodels** | Latest | Statistical modeling (OLS, 2SLS, GLM) |
| **linearmodels** | Latest | Panel data, IV estimation |
| **scikit-learn** | Latest | Propensity score models, preprocessing |
| **pandas** | Latest | Data manipulation |
| **numpy** | Latest | Numerical operations |

#### 11.3.2 LLM Configuration

**Ollama Model Mapping** (from CAIS paper models to local equivalents):

| CAIS Paper Model | Ollama Equivalent | Parameters | Use Case |
|------------------|-------------------|------------|----------|
| GPT-4o | `qwen2.5:72b` | 72B | Complex reasoning, primary backbone |
| GPT-4o-mini | `qwen2.5:14b-instruct` | 14B | **Current default**, good balance |
| o3-mini | `qwen2.5:7b` or `phi3:14b` | 7-14B | Fast inference, simple tasks |
| Gemini 2.5 Pro | `qwen2.5:32b` or `mixtral:8x7b` | 32-56B | Alternative backbone |
| Llama-3.3-70B | `llama3.3:70b-instruct` | 70B | Direct equivalent, strong reasoning |

**Recommended Configuration for Demo:**

```python
OLLAMA_CONFIG = {
    "primary_model": "qwen2.5:14b-instruct",   # Current working model
    "fallback_model": "qwen2.5:7b",            # Faster fallback
    "temperature": 0,                           # Greedy decoding for reproducibility
    "num_ctx": 8192,                           # Context window
    "num_predict": 2048,                       # Max output tokens
}
```

**Temperature Setting:**

```python
# CRITICAL: Temperature = 0 for reproducibility
# Greedy decoding ensures same input → same output
temperature = 0
```

**Rationale:** Setting temperature to 0 ensures reproducibility across experiments. All models use greedy decoding so that the same input query produces the same output, enabling fair comparison between methods.

---

### 11.4 Evaluation Metrics

| Metric | Definition | Formula |
|--------|------------|---------|
| **Method Selection Accuracy (MSA)** | Percentage of queries where selected method matches reference | `MSA = (Σ 1[m̂ᵢ = mᵢ]) / N × 100%` |
| **Mean Relative Error (MRE)** | Average relative error between predicted and reference causal effects | `MRE = (1/N) Σ min(|τ̂ᵢ - τᵢ| / |τᵢ|, 1) × 100%` |

**CAIS Benchmark Performance (Reference Targets):**

| Metric | Baseline (ReAct) | CAIS | Improvement |
|--------|------------------|------|-------------|
| Method Selection Accuracy | 52.08% | 76.20% | +46.3% |
| Retries per Query | 59.96% | 27.18% | -54.69% |
| Execution Errors | 34.39% | 22.91% | -33.4% |
| Data Loading Failures | 3.10% | 0.00% | -100% |

---

### 11.5 Experimental Protocol

**For Demo (Tomorrow):**

```
1. SETUP
   ├─ Verify Ollama running with qwen2.5:14b-instruct
   ├─ Verify OpenAlex API accessible
   └─ Verify DoWhy/statsmodels installed

2. DATA COLLECTION
   ├─ Run scalable_fetcher.py for "stroke rehabilitation"
   ├─ Retrieve 300-500 abstracts
   └─ Store as JSON/CSV corpus

3. PIPELINE EXECUTION
   ├─ Stage 1: Parse abstracts, extract T/Y/X
   ├─ Stage 2: Select causal method per study
   ├─ Stage 3: Validate assumptions
   └─ Stage 4: Execute, explain, format output

4. OUTPUT VALIDATION
   ├─ Verify CSV format matches Research Framework
   ├─ Spot-check 5 random studies for accuracy
   └─ Confirm 20-60 studies in final output

5. BASELINE COMPARISON (Post-Demo)
   ├─ Run same corpus through ReAct prompt
   ├─ Run same corpus through PoT prompt
   ├─ Run same corpus through Veridical prompt
   └─ Compare MSA and MRE
```

---

### 11.6 Reproducibility Checklist

| Item | Requirement | Status |
|------|-------------|--------|
| Temperature | Set to 0 | ☐ |
| Random Seed | Fixed for any stochastic operations | ☐ |
| Model Version | Document exact Ollama model tag | ☐ |
| Library Versions | Pin in requirements.txt | ☐ |
| Data Snapshot | Save corpus with timestamp | ☐ |
| Output Logging | Log all intermediate artifacts | ☐ |

---

## 12. Reference Documents

| Document | Location | Purpose |
|----------|----------|---------|
| Project Brief | `docs/brief.md` | Full context |
| Gap Analysis | `docs/rag_prototype_evaluation.md` | What to change |
| Research Framework | `.bmad-core/Example_Research_Framework.md` | Framework structure |
| Framework Outputs | `.bmad-core/Example_Research_Framework_Output_*.csv` | Example outputs |
| CAIS Methodology | `.bmad-core/Causal_AI_Scientist_Research_Summarized.md` | Causal inference approach |
| Current MVP Spec | `rag_prototype/docs/MVP_SPEC.md` | Existing architecture |

---

## 13. Change Log

| Change | Date | Version | Description | Author |
|--------|------|---------|-------------|--------|
| Initial Draft | 2026-01-30 | 1.0 | PRD created from project brief synthesis | BMad Master |
| CAIS Stage 1 | 2026-01-30 | 1.1 | Added CAIS Pipeline Architecture Section 10, detailed Stage 1 (Data Preprocessing & Query Decomposition) with input_parser, dataset_analyzer, query_interpreter specifications | BMad Master |
| CAIS Stage 2 | 2026-01-30 | 1.2 | Added Stage 2 (Method Selection) - deterministic decision tree, method_selector tool, assumption checklist, fallback list generation, cross-reference to Section 9 and Brief | BMad Master |
| CAIS Stage 3 | 2026-01-30 | 1.3 | Added Stage 3 (Validation) - method_validator, statistical diagnostics by method, schema consistency checks, backtracking mechanism, scientific method analogy | BMad Master |
| CAIS Stage 4 | 2026-01-30 | 1.4 | Added Stage 4 (Method Execution & Interpretation) - method_executor templates, LLM-assisted param selection, explanation_generator, output_formatter with study impact ranking | BMad Master |
| Experimental Setup | 2026-01-30 | 1.5 | Added Section 11 (Experimental Setup) - dataset config, baseline prompts (ReAct/PoT/Veridical), Ollama model mapping, evaluation metrics, reproducibility checklist | BMad Master |
| Query-to-Output Synthesis | 2026-01-30 | 1.6 | Added Section 10.6 (Methodology Prompts) - Causal Query Parsing Prompt (H.1), JSON-to-Research-Framework column mapping, end-to-end synthesis example | BMad Master |
| Lightweight Prompts | 2026-01-30 | 1.7 | Added Section 10.6.5 (Lightweight Inline Prompts H.2) - Treatment/outcome identification, instrument candidate assessment, design principles for minimal prompts | BMad Master |
| Query Interpretation | 2026-01-30 | 1.8 | Added Section 10.6.6 (Query Interpretation Prompts H.3) - IV identification, RDD identification, RCT identification, DiD term, treatment/outcome/covariates/confounders prompts | BMad Master |
| Validation Worked Example | 2026-01-30 | 1.9 | Added Section 10.4.10 (Worked Example: Method Validation Loop) - Electrification dataset, RDD→PSM backtrack, validation history log, key lessons | BMad Master |
| Brownfield Architecture | 2026-01-30 | 2.0 | Created docs/brownfield-architecture.md - Full codebase analysis, tech stack, module documentation, technical debt, enhancement impact areas | BMad Master |

---

*This PRD is a working document focused on tomorrow's demo delivery. Post-MVP enhancements (full CAIS decision tree, Qdrant integration, multi-domain generalization) are documented in the Project Brief.*
