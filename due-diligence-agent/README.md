# Legal & Financial Due Diligence Agent

3-agent orchestration system for document intelligence. Agent 1 ingests documents, Agent 2 retrieves relevant clauses and researches external context, Agent 3 writes a structured risk assessment memo. Works for a law firm reviewing an NDA and a bank reviewing a loan application.

**Hallucination rate 31% → 12% with source-grounding · avg €0.023/document · 4.2s end-to-end · 3 ADRs documented**

🔗 [Live Demo](#) <!-- replace with your deployed URL -->

---

## What It Solves

Due diligence on a contract or loan application typically takes hours of manual review. This system produces a structured risk memo in under 5 seconds — with every claim traced to a source clause, hallucination actively mitigated, and the full decision trail logged in LangSmith.

---

## Architecture

```
Input: PDF document (NDA, contract, loan application)
     ↓
Agent 1 — Ingestion
  └── UnstructuredPDFLoader (scanned + digital PDFs)
  └── Chunk → embed → store in vector DB
     ↓
Agent 2 — Research
  └── Vector retrieval (relevant clauses)
  └── Serper web search (external context)
  └── Merges both into unified context field
     ↓
Agent 3 — Memo Writer
  └── Executive Summary
  └── Key Risks
  └── Clause Analysis
  └── Recommendation
     ↓
Guardrails AI (hallucination checks)
LangSmith (full trace)
Helicone (cost + latency)
```

---

## Sample Output Structure

```
RISK ASSESSMENT MEMO
════════════════════
Executive Summary
  [2–3 sentence overview of document and risk level]

Key Risks
  1. [Risk] — Source: [Clause reference]
  2. [Risk] — Source: [Clause reference]

Clause Analysis
  [Clause name]: [Finding] — [Recommendation]

Recommendation
  [Approve / Flag for review / Reject] — [Rationale]
```

---

## Results

| Metric | Value |
|--------|-------|
| Hallucination rate (baseline) | 31% |
| Hallucination rate (with mitigation) | 12% |
| Avg cost per document | €0.023 |
| End-to-end latency | 4.2s |
| Adversarial inputs tested | 20 |

---

## Architecture Decision Records

Three ADRs document the key technical decisions with evidence:

- **ADR-001:** Chunking strategy — semantic chunking chosen over fixed-size (Faithfulness 0.84 vs 0.71)
- **ADR-002:** Embedding model — large embedding chosen for legal domain precision vs latency trade-off
- **ADR-003:** Retrieval method — semantic + reranking chosen over hybrid BM25 for this document type

---

## Stack

- Python 3.11
- LangGraph (3-agent state machine)
- LangSmith (tracing)
- Guardrails AI (hallucination mitigation)
- Helicone (monitoring)
- UnstructuredPDFLoader
- OpenAI Embeddings + GPT-4o
- Chroma / Pinecone
- Serper API
- FastAPI
- Streamlit (UI)
- GitHub Actions (CI/CD)

---

## How to Run

```bash
git clone https://github.com/SaraDHimdi/ai-engineer-portfolio
cd due-diligence-agent

cp .env.example .env
# Add OPENAI_API_KEY, SERPER_API_KEY, LANGSMITH_API_KEY

# Run with Docker
docker build -t due-diligence-agent .
docker run --env-file .env -p 8000:8000 due-diligence-agent

# Or run locally
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn app:app --reload
```

---

## Known Limitations

| Failure case | Why it happens | Mitigation |
|---|---|---|
| Scanned PDFs with poor OCR quality | UnstructuredPDFLoader degrades on low-res scans | Pre-processing quality check at ingestion |
| Highly technical financial instruments | Domain knowledge gaps in base model | Flagged for human review in memo |
| Documents over 100 pages | Context window and cost constraints | Chunked processing with section summarisation |
| Ambiguous clause language | LLM interprets rather than extracts | Confidence score surfaced to user |
| Out-of-scope document types | Agent 1 has no document type classifier | Returns explicit unsupported format message |

---

*DocumentLab.ai — LLM-based document intelligence for legal and financial services*
