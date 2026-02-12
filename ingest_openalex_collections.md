# Issue: Ingest OpenAlex Collections into ChromaDB

## Context
We need to ingest two datasets from the `OpenAlex_collections` directory into ChromaDB to enable vector search in the RAG pipeline.

- `firm_performance_ESG.csv` (~4,000 records)
- `obesity_diabetes.csv` (~62,000 records)

## Proposed Solution
Implement a Python script `src/ingest_collections.py` that:
1. Connects to the ChromaDB instance.
2. Reads the CSV files using pandas.
3. Batch-inserts documents into two separate collections.
4. Uses `id` as the primary key and includes metadata (title, abstract, year, etc.).

## Task List
- [ ] Create `src/ingest_collections.py`
- [ ] Ingest `firm_performance_ESG` collection
- [ ] Ingest `obesity_diabetes` collection
- [ ] Verify counts and perform test search
