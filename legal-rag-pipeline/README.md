# Legal Document RAG Pipeline

Answers questions over real legal contracts — NDAs, commercial agreements, CUAD dataset — with source attribution on every answer so you know exactly which clause it came from.

**Faithfulness 0.71 baseline · €0.006/query · 17/20 manual tests passed**

🔗 [Live Demo](#) <!-- replace with your deployed URL -->

---

## What It Solves

Lawyers and legal teams spend hours manually searching contracts for specific clauses. This pipeline lets you ask questions in plain English and get answers traced back to the exact document and clause — no hallucination without a source to back it up.

---

## Architecture

```
PDF contracts (CUAD dataset)
     ↓
UnstructuredPDFLoader → chunking (semantic, 512 tokens)
     ↓
OpenAI embeddings → Chroma vector store
     ↓
User query → similarity search (top 5 chunks)
     ↓
GPT-4o-mini → answer + source attribution
     ↓
FastAPI endpoint → cost per query logged
```

---

## Results

| Metric | Value |
|--------|-------|
| Faithfulness (RAGAS baseline) | 0.71 |
| Cost per query | €0.006 |
| Manual tests passed | 17/20 |
| Avg response time | <3s |
| Documents in corpus | 50 CUAD contracts |

---

## Stack

- Python 3.11
- LangChain
- Chroma (vector store)
- OpenAI Embeddings + GPT-4o-mini
- UnstructuredPDFLoader
- FastAPI
- Vercel (deployment)

---

## How to Run

```bash
git clone https://github.com/SaraDHimdi/ai-engineer-portfolio
cd legal-rag-pipeline

python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

cp .env.example .env
# Add your OPENAI_API_KEY to .env

# Ingest documents
python ingest.py

# Run the API
uvicorn app:app --reload
```

---

## Design Decisions

**Why UnstructuredPDFLoader over PyPDFLoader?** PyPDFLoader strips formatting and merges lines incorrectly on legal documents. UnstructuredPDFLoader preserves clause structure, which directly improves retrieval precision.

**Why chunk at 512 tokens?** Tested 512 vs 1024. At 1024, retrieved chunks frequently contained two separate clauses — the answer to a different question diluted the relevant one. 512 keeps each chunk focused on one clause.

---

*DocumentLab.ai — LLM-based document intelligence for legal and financial services*
