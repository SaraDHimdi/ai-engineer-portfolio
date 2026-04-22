# Financial Client Intake Chatbot

Classifies incoming client messages for a financial services firm — loan enquiries, compliance questions, fraud reports — and drafts responses with full cost tracking.

**18/20 manual test cases correct · €0.002/conversation · 4 message types classified**

🔗 [Live Demo](#) <!-- replace with your deployed URL -->

---

## What It Solves

Financial firms receive hundreds of client messages daily across multiple channels. Routing them manually to the right team wastes time and introduces errors. This chatbot classifies each message into one of four categories and drafts an appropriate response — instantly, at under half a cent per conversation.

---

## Architecture

```
User message
     ↓
System prompt (classification logic)
     ↓
OpenAI API (GPT-4o-mini)
     ↓
Classified response + draft reply
     ↓
Cost tracker (tokens in + tokens out → € per message)
```

---

## Message Categories

| Category | Example input |
|----------|--------------|
| Loan enquiry | "I'd like to apply for a mortgage" |
| Compliance question | "What documents do I need for KYC?" |
| Fraud report | "I didn't authorise this transaction" |
| General enquiry | "What are your opening hours?" |

---

## Results

| Metric | Value |
|--------|-------|
| Test cases correct | 18/20 (90%) |
| Cost per conversation | €0.002 |
| Avg response time | <2s |
| Message types handled | 4 |

---

## Stack

- Python 3.11
- OpenAI API (GPT-4o-mini)
- Flask
- python-dotenv

---

## How to Run

```bash
git clone https://github.com/SaraDHimdi/ai-engineer-portfolio
cd financial-intake-chatbot

python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

cp .env.example .env
# Add your OPENAI_API_KEY to .env

python app.py
```

---

## Design Decision

The system prompt classifies first, then drafts — two separate instructions in one call rather than two API calls. This keeps cost at €0.002/conversation. A two-call approach would double that with no accuracy gain for this task.

---

*DocumentLab.ai — LLM-based document intelligence for legal and financial services*
