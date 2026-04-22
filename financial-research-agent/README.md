# Financial Research Agent

Two-agent LangGraph system: Agent 1 searches financial news and regulatory updates, Agent 2 synthesises a structured briefing. Wrapped in FastAPI, Dockerised, CI/CD pipeline, and fully traced in LangSmith.

**94% tool call success rate · p95 latency 1.8s · 14 pytest tests, 100% pass · error rate 0.3%**

🔗 [Live Demo](#) <!-- replace with your deployed URL -->

---

## What It Solves

Financial analysts spend hours aggregating news and regulatory updates before they can write a briefing. This system does it in under 10 seconds — two agents working in sequence, with every step traceable in LangSmith and every failure handled gracefully.

---

## Architecture

```
User input: topic
     ↓
Agent 1 — Research
  └── Serper web search (financial news + regulatory sources)
  └── Returns: structured research notes
     ↓
Shared LangGraph state (AgentState TypedDict)
     ↓
Agent 2 — Synthesis
  └── Reads research notes from state
  └── Writes domain-specific financial briefing
     ↓
FastAPI endpoint → Streamlit UI
     ↓
LangSmith trace · Helicone cost/latency monitoring
```

---

## LangSmith Trace

<!-- embed your LangSmith trace screenshot here -->
![LangSmith trace showing both agents](demos/langsmith-trace.png)

---

## Results

| Metric | Value |
|--------|-------|
| Tool call success rate | 94% |
| p95 latency | 1.8s |
| Avg briefing generation time | 8s |
| Agent 1 avg tool calls per run | 3.2 |
| pytest tests | 14, 100% pass |
| Error rate | 0.3% |
| Cost per briefing | €0.009 |

---

## Stack

- Python 3.11
- LangGraph (multi-agent state machine)
- LangSmith (tracing)
- Serper API (web search)
- FastAPI + Pydantic
- Docker
- GitHub Actions (CI/CD)
- Helicone (cost + latency monitoring)
- pytest + ruff
- Streamlit (UI)
- Render (deployment)

---

## CI/CD Pipeline

Every push runs:
1. `ruff check .` — linting
2. `pytest tests/ -v` — 14 tests, LLM calls mocked
3. Auto-deploy to Render on merge to main

---

## How to Run

```bash
git clone https://github.com/SaraDHimdi/ai-engineer-portfolio
cd financial-research-agent

cp .env.example .env
# Add OPENAI_API_KEY, SERPER_API_KEY, LANGSMITH_API_KEY

# Run with Docker
docker build -t financial-research-agent .
docker run --env-file .env -p 8000:8000 financial-research-agent

# Or run locally
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn app:app --reload
```

---

## Design Decision

**Why LangGraph over CrewAI or AutoGen?** LangGraph gives explicit control over state transitions — you define exactly what each agent reads and writes. When Agent 2 produces wrong output, the bug is always traceable to a specific state field. With CrewAI the failure modes are harder to isolate in production.

---

*DocumentLab.ai — LLM-based document intelligence for legal and financial services*
