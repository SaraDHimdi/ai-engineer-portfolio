<p align="center">
  <img src="assets/logo.png" alt="DocumentLab.ai" width="80"/>
</p>
<p align="center">
  <img src="https://img.shields.io/github/last-commit/SaraDHimdi/ai-engineer-portfolio?color=1B2A4A&style=flat-square" alt="Last commit"/>
  <img src="https://img.shields.io/github/repo-size/SaraDHimdi/ai-engineer-portfolio?color=1B2A4A&style=flat-square" alt="Repo size"/>
  <img src="https://img.shields.io/github/languages/top/SaraDHimdi/ai-engineer-portfolio?color=C8960C&style=flat-square" alt="Top language"/>
  <img src="https://img.shields.io/github/issues/SaraDHimdi/ai-engineer-portfolio?color=1B2A4A&style=flat-square" alt="Issues"/>
</p>
<p align="center">
  <em>Built with intention. Shipped with evidence.</em>
</p>

# Sara Dhimdi — AI Engineer & Founder of DocumentLab.ai
Building RAG systems, LLM agents, and production pipelines for legal and financial document intelligence.






---

## About

I care about AI that is robust, interpretable, and genuinely useful — with a focus on RAG systems, LLM agents, and production pipelines that help organisations in legal and financial services unlock answers from their own documents.

**DocumentLab.ai** is my AI engineering studio, specialized in LLM-based document intelligence across research, analytics, automation, and customer service.

---

## Projects

| # | Project | Vertical | What it does | Key metric | Status |
|---|---------|----------|--------------|------------|--------|
| 1 | **Financial Client Intake Chatbot** | 🏦 Finance | Classifies client messages — loan enquiry, compliance question, fraud report. Drafts responses with cost tracking. | 18/20 manual tests · €0.002/conversation | 🧢 Live |
| 2 | **Legal Document RAG Pipeline** | ⚖️ Legal | Q&A over NDAs and commercial contracts (CUAD dataset). Source attribution on every answer. | Faithfulness 0.71 baseline · €0.006/query | 🧢 Live |
| 3 | **Financial Research Agent** | 🏦 Finance | Two-agent LangGraph system: Agent 1 searches financial news, Agent 2 synthesises a structured briefing. Wrapped in FastAPI, Dockerised, CI/CD, LangSmith traced. | 94% tool call success · p95 1.8s · 14 pytest tests, 100% pass | 🧢 Live |
| 4 | **RAG Evaluation Framework** | ⚖️ Legal | RAGAS harness across 4 RAG configurations on a 40-question golden dataset. Red-team and prompt injection tests. RAG vs LoRA fine-tuning comparison on the same test set. | Faithfulness 0.84 (RAG) vs 0.81 (LoRA rank 8) at 4x lower cost | 🧢 Live |
| 5 | **Legal & Financial Due Diligence Agent** | ⚖️ 🏦 Both | 3-agent orchestration. Agent 1 ingests documents. Agent 2 retrieves context + searches the web. Agent 3 writes a structured risk assessment memo. Works for law firms and banks. 3 ADRs documented. | Hallucination rate 31% → 12% · avg €0.023/document · 4.2s end-to-end | 🧢 Live |
| 6 | **Legal Intelligence Engine** | ⚖️ Legal | LoRA ablation study on Mistral 7B (3 rank configs, CUAD + EDGAR + EUR-Lex). Domain-adapted sentence transformer with hard negative mining. MCP server exposing the RAG pipeline as a composable tool — integrated into Project 5, tested with Claude Desktop. | Rank 8: 0.81 faithfulness at €0.002/query · Recall@3 0.71 → 0.83 vs OpenAI baseline · 2 models on HuggingFace Hub | 🧢 Live |

---

## Stack

| Layer | Tools |
|-------|-------|
| Language | Python 3.11+ |
| Orchestration | LangChain · LangGraph · LangSmith |
| LLM APIs | OpenAI API · Anthropic API |
| Vector DBs | Chroma · Pinecone |
| Evaluation | RAGAS · DeepEval · Guardrails AI |
| Fine-tuning | HuggingFace PEFT · LoRA · bitsandbytes · TRL |
| NLP | Sentence Transformers · Contrastive Learning |
| Infrastructure | MCP (Model Context Protocol) |
| Production | FastAPI · Docker · GitHub Actions · CI/CD |
| Monitoring | Helicone · LangSmith |
| Deployment | Vercel · Render · Streamlit Cloud · HuggingFace Hub |
| Tooling | pytest · ruff · pre-commit · python-dotenv · Git |

---

## Niche

**LLM-Based Document Intelligence for legal and financial services.**

- Contract analysis and clause retrieval
- Financial report Q&A and summarisation
- Compliance document search and retrieval
- Multi-agent due diligence and risk assessment
- Fine-tuning and evaluation for domain-specific accuracy
- Agentic workflows for research, analytics, and automation

---

## Repo Structure

```
ai-engineer-portfolio/
├── README.md                      ← You are here
├── financial-intake-chatbot/      ← Project 1 · Finance
├── legal-rag-pipeline/            ← Project 2 · Legal (CUAD dataset)
├── financial-research-agent/      ← Project 3 · Finance · LangGraph + FastAPI + Docker
├── rag-evaluation-framework/      ← Project 4 · RAGAS + LoRA comparison
├── due-diligence-agent/           ← Project 5 · Legal & Finance · 3-agent · FLAGSHIP
├── legal-intelligence-engine/     ← Project 6 · Fine-tuning · Embeddings · MCP server
└── demos/                         ← Loom video links
```

---

## Contact

- LinkedIn: [linkedin.com/in/sara-d-1a4795300](https://linkedin.com/in/sara-d-1a4795300)
- Company: [DocumentLab.ai](https://documentlab.ai)
- GitHub: [github.com/SaraDHimdi](https://github.com/SaraDHimdi)

---

*Built with intention. Shipped with evidence.*
