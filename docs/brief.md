# Project Brief: GRA AI Scientist

**Status:** DRAFT - In Progress
**Created:** 2026-01-29
**Mode:** Interactive

---

## Executive Summary

**GRA AI Scientist** is a Causal AI Scientist—a multi-agent research system designed to autonomously identify the most impactful academic studies by performing causal inference rather than relying on pre-programmed heuristics or correlation-based filtering.

**Primary Problem:** Researchers face an overwhelming volume of academic literature, but the deeper challenge is that existing AI tools rely on hardcoded metrics (citation counts, keyword matching) or correlation-based ML models that drift toward memorization. These approaches cannot answer *why* certain studies are impactful—they can only point to surface-level patterns.

**Target Market:** Academic researchers, graduate research assistants, and systematic review teams across any scientific domain who need to conduct comprehensive literature reviews with genuine understanding of research impact and causality.

**Key Value Proposition:** Unlike traditional ML-based research tools, GRA AI Scientist is "educated" on research comparison frameworks, statistical formulas, and scientific methodology—then independently synthesizes the relevant metrics from study abstracts. The agent performs causal inference to determine the independent actual effect of variables, moving beyond correlation to understand *why* certain research succeeds. This replicates how a human scientist, after learning a framework, identifies the most significant studies through understanding rather than pattern matching.

**Core Innovation:** A domain-agnostic, multi-agent system that can be assigned any academic topic (public health, stroke rehabilitation, or any field), apply its learned research frameworks, and discover the same causal relationships a trained scientist would identify—without requiring domain-specific hardcoding.

---

## What is a Causal AI Scientist?

A Causal AI Scientist is an AI workflow framework that:

1. **Receives Education** - Is provided text, frameworks, mathematical/statistical/scientific formulas
2. **Analyzes Assigned Topics** - Studies abstracts and research papers
3. **Performs Causal Inference** - Determines the Independent Actual Effect of One Variable on Another

Rather than being specified the relationships to look for, the AI performs causal inference—moving beyond pointing to mere correlation to understanding "WHY" something happens.

### Causal AI vs Traditional ML

| Traditional ML/AI Research Tools | GRA AI Scientist (Causal AI) |
|----------------------------------|------------------------------|
| Hardcoded metrics (citations, keywords) | Synthesizes metrics from learned frameworks |
| Correlation-based filtering | Causal inference—asks "why" |
| Domain-specific training required | Domain-agnostic after framework education |
| Pattern memorization over time | Reasoning from principles |
| Static rules | Adaptive understanding |
| Points to relationships | Explains relationships |

---

## Assumptions & Design Philosophy

### 1. "Education" Over Hardcoding

The agent receives research frameworks, mathematical/statistical formulas, and scientific text as context—not as rules but as knowledge to reason from.

**Research Comparison Framework Structure:**

The agent learns to extract structured information from studies:

| Column | Description | Example (Stroke Rehabilitation) |
|--------|-------------|--------------------------------|
| **Aims** | Main objective of the study | "Evaluate motor recovery outcomes post-stroke using robotic-assisted therapy" |
| **Data** | Data source and collection method | "EHR data from 12 rehabilitation centers (n=4,500 patients), 2018-2023" |
| **Analysis** | Variable being studied (configurable per domain) | "Recovery rate variation by intervention type and patient demographics" (THIS IS JUST AN EXAMPLE, SPECIFICS CHANGE PER TOPIC AND STUDY ENTRY) |
| **Method Used** | Statistical/ML method employed Or alternatively implementation or treatment applied to test group or test data. Changes with each entry | "Mixed-effects regression with propensity score matching" |
| **Findings** | Key insights and causal relationships | "Robotic-assisted therapy showed 23% improvement in motor function (p<0.01)" |

**Framework Education Process:**

- Phase 1: Framework Ingestion (receive documentation and examples)
- Phase 2: Pattern Recognition (learn structure without hardcoded column names)
- Phase 3: Application (synthesize columns from raw abstracts)

### 2. Single-Agent Prototype Architecture

**Current Scope (Phase 1):** Focus on ONE agent—the Research & Analysis Agent.

```
┌─────────────────────────────────────────────────────────────────┐
│                    GRA AI SCIENTIST - PROTOTYPE                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────────────┐    ┌──────────────────────────────────┐  │
│  │  TRADITIONAL     │    │  RESEARCH & ANALYSIS AGENT       │  │
│  │  SCRAPERS        │───>│  (Ollama LLM - qwen2.5:14b)      │  │
│  │                  │    │                                  │  │
│  │  - OpenAlex API  │    │  - Framework-educated            │  │
│  │  - Selenium      │    │  - Synthesizes metrics           │  │
│  │  - CSV exports   │    │  - Performs causal inference     │  │
│  │                  │    │  - Outputs structured tables     │  │
│  └──────────────────┘    └──────────────────────────────────┘  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

**Why Separate Scraping from Inference:**

| Concern | Solution |
|---------|----------|
| **LLM Hallucination Risk** | Scrapers use deterministic APIs—no LLM involvement in data collection |
| **Data Integrity** | Literature is "definite and unchangeable"—scientists learn it, not infer it |
| **Reproducibility** | Same query → same dataset every time |

### 3. Configurable Study Target (100-300)

| Parameter | Default | Notes |
|-----------|---------|-------|
| **Initial Corpus** | 10^4 (~10,000) | OpenAlex API practical limit |
| **Maximum Corpus** | 10^4.75 (~56,000) | Upper bound for comprehensive topics |
| **Post-Filter Target** | 100-300 | "Essential" studies for human review |
| **Topic-Specific Override** | Configurable | Narrow topics may need 50; broad may need 500 |

**Critical Design Principle:** Configuration parameters do NOT influence causal inference. The configuration layer acts as a pre-filter (traditional criteria), while the inference layer performs causal selection (framework-based reasoning).

### 4. "Why" Over "What" — Causal Inference

The agent must understand causal mechanisms, not just identify correlations.

**Based on CAIS Methodology (Verma et al., NeurIPS 2025):**

| CAIS Component | Application to GRA AI Scientist |
|----------------|--------------------------------|
| **Decision Tree Method Selection** | Structured decision process for analysis approach |
| **Validation Feedback Loop** | Self-correction if assumptions fail |
| **Template Execution** | DoWhy/statsmodels for rigorous statistical analysis |

**Recommended Literature:**

- Causal AI Scientist (CAIS) - Verma et al., 2025
- CauSciBench - Acharya et al., 2025
- DoWhy - Sharma & Kiciman, 2020
- ReAct Prompting - Yao et al., 2023

---

## Pilot Topics

1. **Stroke Rehabilitation** (Primary)
2. **Online Health Communities** (Secondary)

These topics serve as proof of concept. The system should be domain-agnostic after validation.

---

## Existing Prototype

Located at: `rag_prototype/`

**Current Capabilities:**
- RAG pipeline for causal extraction from arXiv papers (MVP complete)
- OpenAlex pipeline for large-scale paper discovery (production-ready)
- Scalable fetching with progress tracking and checkpoints
- CSV/JSON export

**Needs Improvement:**
- Qdrant integration (not yet implemented)
- Research comparison framework application
- CAIS-style decision tree for method selection
- Multi-domain generalization

---

## Key Reference Documents

| Document | Location | Purpose |
|----------|----------|---------|
| Example Research Framework | `.bmad-core/Example_Research_Framework.md` | Framework structure and methodology |
| Framework Outputs | `.bmad-core/Example_Research_Framework_Output_*.csv` | Example structured outputs |
| Causal AI Scientist Research | `.bmad-core/Causal_AI_Scientist_Research.md` | CAIS methodology details |
| Causal AI Summary | `.bmad-core/Causal_AI_Scientist_Research_Summarized.md` | Quick reference |

---

## Problem Statement

**Volume Overwhelm:** A search on any academic topic yields 50,000+ papers (up to 10^4.75 ~56,000 studies). Manual review is impossible.

**Surface-Level Filtering Fails:** Current tools filter by citations/keywords—but these don't identify *why* a study matters.

**Correlation ≠ Causation:** Traditional ML tools can't determine if an intervention *caused* outcomes or just correlated.

**Domain Lock-In:** Tools require domain-specific training; can't transfer between topics without retraining.

**Scale Challenge:** The agent must reduce 10^4.75 studies to 100-300 essential papers through causal reasoning, not arbitrary cutoffs.

**Prototype Examples:** Stroke Rehabilitation, Online Health Communities

---

## Target Users

| User Type | Need |
|-----------|------|
| **Graduate Research Assistants** | Conduct literature reviews with reproducible, structured outputs |
| **Systematic Review Teams** | Comprehensive reviews that any researcher can independently reproduce |
| **Principal Investigators** | Both quick landscape assessment AND deep identification of evidence-based interventions |
| **Academic Researchers (Any Domain)** | Apply the agent to their own research and reproduce results independently |

**Key Emphasis:**

- **Reproducibility:** Any academic researcher can take this agent, apply it to their own topic, and independently reproduce the same structured results.
- **Dual Capability:** Quick landscape overview + deep causal analysis identifying the most impactful studies/interventions (central to causal reasoning).

---

## Proposed Solution

**GRA AI Scientist** - A Causal AI Scientist that:

### Core Pipeline

1. **Scrapes literature deterministically** via OpenAlex API (full abstract metadata, no LLM hallucination risk)
2. **Ingests research comparison frameworks** as "education" (not hardcoded rules)
3. **Parses full abstract metadata** and divides into structured columns:
   - **Aims** - Study objective
   - **Data** - Data source, collection method, sample size
   - **Analysis** - Variable/disparity being studied (domain-configurable)
   - **Methods** - Statistical/ML method or intervention applied
   - **Findings** - Key insights and causal relationships
4. **Performs causal inference** to identify *why* studies are impactful
5. **Outputs structured CSV tables** matching `Example_Research_Framework_Output.csv` format

### Prototype Scope

- **Input:** ~10,000 abstracts from OpenAlex
- **Output:** 20-60 most relevant studies (scaled for testing phase)
- **Agent:** Single Research & Analysis Agent built on existing `rag_prototype`

### How the Agent Learns the Framework

**Step 1: Framework Education (from CAIS methodology)**
- Agent receives the Research Comparison Framework documentation
- Agent receives example outputs (`Example_Research_Framework_Output_*.csv`)
- Agent learns the structure: what constitutes Aims vs Data vs Analysis vs Methods vs Findings

**Step 2: Causal Reasoning Education (from Causal AI Scientist paper)**
- Agent learns to perform causal inference, not correlation matching
- Agent uses decision-tree approach for method selection
- Agent applies validation feedback loop for self-correction
- Agent determines "why" a study is impactful (Independent Actual Effect of variables)

**Step 3: Application**
- Given full abstract metadata, agent synthesizes each column
- Agent does NOT hallucinate—extracts from provided metadata only
- Agent outputs structured table with causal justifications

---

## Goals & Success Metrics

### Prototype Goals (Tomorrow's Demo)

| Goal | Success Metric |
|------|----------------|
| **End-to-end pipeline** | OpenAlex scrape → Agent analysis → Structured CSV output |
| **Framework-educated agent** | Agent produces structured table (Aims, Data, Analysis, Methods, Findings) |
| **Correct metadata parsing** | Each column contains relevant info extracted from full abstract metadata |
| **Output scale** | 20-60 relevant studies from ~10,000 input abstracts |
| **Configurable topic** | Demonstrate with stroke rehabilitation AND online health communities |
| **Causal reasoning visible** | Output includes "why" explanations, not just rankings |

### Causal Inference Framework

**Key Variables:**
- **T** = Treatment (intervention applied)
- **Y** = Outcome (target variable)
- **X** = Covariates (confounders)
- **Yi(1)** = Outcome if treatment applied
- **Yi(0)** = Outcome if no treatment
- **Ti** = 1 (treatment group) or 0 (control group)

**Core Equations:**

1. **Average Treatment Effect (ATE):**
   ```
   τATE = E[Y(1) − Y(0)]
   ```

2. **RCT Estimation:**
   ```
   τ̂ATE = (1/N₁) Σᵢ:Tᵢ=1 Yᵢ − (1/N₀) Σᵢ:Tᵢ=0 Yᵢ
   ```

3. **Conditional Ignorability (Observational Data):**
   ```
   (Y(1), Y(0)) ⊥⊥ T | X
   ```

4. **ATE with Covariate Adjustment:**
   ```
   τATE = EX[E[Y | T = 1, X] − E[Y | T = 0, X]]
   ```

5. **Linear Structural Model:**
   ```
   Y = α + X^T β + τT + ϵ
   ```
   - α = intercept
   - β = vector of coefficients for covariates X
   - τ = treatment effect parameter (directly corresponds to ATE)
   - ϵ = unobserved error term

**Statistical Significance Threshold:** p<0.05 (probability of random chance <5% assuming null hypothesis)

**SUTVA:** Stable Unit Treatment Value Assumption (no interference between units, consistency of treatment)

### Decision Tree Method Selection

**E.2 RCTs:**
- Encouragement Designs → Use IV
- Standard RCT → Difference in means (or OLS with pre-treatment variables)

**E.3 Observational Studies:**
- E.3.1 Binary + Temporal → **DiD** or **RDD**
- E.3.2 General Binary → **Backdoor adjustment** (IPW or Matching based on SMD < 0.1)
- E.3.3 Unmeasured Confounding → **IV** (Relevance + Exclusion) or **Frontdoor**
- E.3.4 Method Hierarchy: **IV > Frontdoor > Backdoor**
- E.3.5 Nonbinary → Generalized Propensity Scores

**SMD Formula (Covariate Balance):**
```
SMD = (X̄_treated - X̄_control) / √((s²_treated + s²_control) / 2)
```
If SMD < 0.1 → use IPW; else → use Matching

### Baseline vs CAIS Performance (Reference Targets)

| Metric | Baseline | CAIS | Change |
|--------|----------|------|--------|
| Total Queries | 1551 | 585 | — |
| Successful Queries | 1476 | 512 | — |
| Retries per Query | 59.96% | 27.18% | ↓ 54.69% |
| Method Match Rate | 52.08% | 76.20% | ↑ 46.3% |
| Mean Error | 35.38% | 37.66% | ↑ 6.4% |

**Error Breakdown:**

| Error Type | Baseline | CAIS | Change |
|------------|----------|------|--------|
| Execution & Runtime Error | 34.39% | 22.91% | ↓ 33.4% |
| Method Mismatch | 29.77% | 21.20% | ↓ 28.8% |
| Data Loading Failure | 3.10% | 0.00% | ↓ 100.0% |
| Missing Result | 0.76% | 6.84% | ↑ 800.0% |

### Role of LLM: Supplying Domain Expertise

The entire causal inference process hinges on the validity of the conditional ignorability assumption, which cannot be verified from data alone. Justifying this assumption requires domain knowledge to argue that the set of measured covariates X is sufficient to account for all major confounders.

The LLM acts as **proxy for human domain expert** to:
1. **Propose plausible causal relationships** between variables
2. **Identify most likely confounders** (set X)
3. **Justify conditional ignorability assumption**

---

## Next Sections (To Be Completed)

- [x] Problem Statement
- [x] Proposed Solution
- [x] Target Users
- [ ] Goals & Success Metrics (in progress)
- [ ] MVP Scope
- [ ] Post-MVP Vision
- [ ] Technical Considerations
- [ ] Constraints & Assumptions
- [ ] Risks & Open Questions
- [ ] Next Steps

---

*This Project Brief is a working document created during an interactive session with Mary (Business Analyst persona).*
