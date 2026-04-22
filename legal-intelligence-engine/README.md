# Legal Intelligence Engine

Three components that make the DocumentLab.ai RAG system smarter and more composable: a LoRA fine-tuning ablation study on Mistral 7B, a domain-adapted legal embedding model trained with contrastive learning, and an MCP server exposing the full RAG pipeline as a callable tool for any MCP client.

**LoRA rank 8: 0.81 faithfulness at €0.002/query · Recall@3 0.71 → 0.83 vs OpenAI baseline · 2 models on HuggingFace Hub · integrated into Due Diligence Agent via MCP**

🔗 [HuggingFace Hub — Fine-tuned model](#) <!-- replace with HF link -->
🔗 [HuggingFace Hub — Embedding model](#) <!-- replace with HF link -->

---

## What It Solves

Three problems that sit above basic RAG: (1) at high query volumes, fine-tuning is more economical than calling OpenAI — this ablation study finds exactly where the crossover is. (2) generic embedding models don't understand legal terminology — a domain-adapted model measurably improves retrieval. (3) the RAG pipeline should be callable by any agent or tool, not just hardcoded into one system — MCP makes it composable.

---

## Component 1 — Legal Clause Fine-Tuning System

LoRA fine-tuning of Mistral 7B on CUAD + EDGAR + EUR-Lex legal data. Ablation study across 3 LoRA rank configurations evaluated against the PFE golden dataset.

### Dataset
- Sources: CUAD (contract clauses) + EDGAR (financial filings) + EUR-Lex (EU legal documents)
- Format: instruction-tuning pairs
- Split: 70% train / 15% validation / 15% test (stratified by clause type)

### Ablation Results

| Config | Faithfulness | Hallucination rate | Training time | Cost/query |
|--------|--------------|--------------------|---------------|------------|
| Base Mistral 7B | 0.61 | 31% | — | €0.002 |
| LoRA rank 4 | 0.74 | 19% | ~40 min A100 | €0.002 |
| **LoRA rank 8 ★** | **0.81** | **14%** | **~75 min A100** | **€0.002** |
| LoRA rank 16 | 0.83 | 13% | ~140 min A100 | €0.002 |
| RAG best config | 0.84 | 12% | — | €0.008 |

★ chosen: achieves 95% of rank 16 performance at 54% of training cost.

**Economic crossover:** fine-tuning at €0.002/query breaks even with RAG at €0.008/query at approximately 50,000 queries/month on a fixed corpus.

---

## Component 2 — Domain-Adapted Legal Embedding Model

Sentence transformer fine-tuned on CUAD legal clause pairs using contrastive learning with hard negative mining. Hard negatives are clauses that look semantically similar but belong to different legal categories — forcing the model to learn legal-domain precision, not just English similarity.

### Benchmark Results

| Model | Recall@3 | Recall@5 | MRR | Cost/1M tokens |
|-------|----------|----------|-----|----------------|
| text-embedding-3-small (baseline) | 0.71 | 0.79 | 0.68 | €0.02 |
| all-MiniLM-L6-v2 (off-shelf) | 0.74 | 0.81 | 0.71 | €0.00 |
| **DocumentLab legal model ★** | **0.83** | **0.89** | **0.79** | **€0.00** |

★ plugged into Due Diligence Agent — Faithfulness improved by 0.06 points vs OpenAI baseline embedding.

---

## Component 3 — DocumentLab MCP Server

Python MCP server exposing the legal RAG pipeline as a typed, composable tool. Any MCP client — Claude Desktop, another agent, a future DocumentLab product — can call legal clause retrieval without touching the underlying code.

### Tool Schema

```
Tool: legal_rag_query
Input:
  - query: str         — the question to answer
  - document_type: str — NDA | contract | loan_application
  - top_k: int         — number of chunks to retrieve (default: 5)
Output:
  - answer: str
  - source_chunks: list[str]
  - faithfulness_score: float
  - cost_usd: float
```

### Integration
- Integrated into Due Diligence Agent — Agent 2 calls RAG via MCP instead of a direct function
- Tested with Claude Desktop
- MCP primitives documented: tools · resources · prompts

---

## Stack

- Python 3.11
- HuggingFace PEFT (LoRA)
- bitsandbytes (4-bit quantisation)
- TRL (training)
- Accelerate
- SentenceTransformers
- MCP SDK
- Mistral 7B
- HuggingFace Hub

---

## How to Run

```bash
git clone https://github.com/SaraDHimdi/ai-engineer-portfolio
cd legal-intelligence-engine

cp .env.example .env
# Add OPENAI_API_KEY, HF_TOKEN

# Fine-tuning (requires GPU)
python finetune.py --rank 8

# Embedding model training
python train_embeddings.py

# MCP server
python mcp_server.py
```

---

## Design Decision

**Why combine three components in one project?** They share the same goal — making retrieval more accurate and more accessible — and the same evaluation dataset (the 40-question golden set from the RAG Evaluation Framework). Running them separately would mean three sets of boilerplate for one coherent system improvement.

---

*DocumentLab.ai — LLM-based document intelligence for legal and financial services*
