# 🤖 Customer Support Automation with CrewAI + Gemini

> **A production-grade multi-agent customer support system built with CrewAI + Gemini, capable of resolving real customer inquiries by scraping live documentation and running them through a QA review pipeline.**

<br>

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python)
![CrewAI](https://img.shields.io/badge/CrewAI-Multi--Agent-purple?style=for-the-badge)
![Gemini](https://img.shields.io/badge/Google-Gemini%202.5%20Pro-orange?style=for-the-badge&logo=google)
![Status](https://img.shields.io/badge/Status-Shipped%20✅-brightgreen?style=for-the-badge)

---

## 🧠 What This Project Does

This notebook builds a **two-agent customer support crew** that:

1. **Resolves customer inquiries** by scraping live product documentation (Stripe docs) in real-time
2. **QA reviews every response** before it goes out — ensuring accuracy, tone, and completeness
3. **Handles multiple inquiry types** in a loop — subscriptions, refunds, going live — all in one run

The system is modeled after a real SaaS support workflow for **Stripe**, a fintech company, with a fictional customer **Arjun Mehta from TechFlow India** asking real-world developer questions.

---

## 🏗️ System Architecture

```
Customer Inquiry (Input)
        │
        ▼
┌──────────────────────────────────────┐
│   Senior Support Representative      │
│   ├── Role: Resolve customer inquiry │
│   ├── Tool: ScrapeWebsiteTool        │  ◄── Scrapes docs.stripe.com live
│   └── delegation: False              │
└──────────────────┬───────────────────┘
                   │  hands off draft
                   ▼
┌──────────────────────────────────────┐
│  Support Quality Assurance Specialist│
│   ├── Role: Review & refine response │
│   ├── No tools — review only         │
│   └── Can delegate back to Agent 1   │
└──────────────────┬───────────────────┘
                   │
                   ▼
         Final Response to Customer
```

---

## ✨ Key Concepts Demonstrated

| Concept | Implementation |
|---|---|
| **Role Playing** | Both agents have dedicated roles, goals, and backstories |
| **Focus** | `allow_delegation=False` on Agent 1 prevents task-drifting |
| **Cooperation** | QA Agent can delegate back to Support Agent for corrections |
| **Live Tool Use** | `ScrapeWebsiteTool` fetches Stripe docs dynamically at runtime |
| **Memory** | Crew memory configured (toggle via `memory=True/False`) |
| **Guardrails** | CrewAI tracing enabled for observability |
| **Multi-Query Loop** | Crew handles 3 different customer questions in a single run |

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Agent Framework** | CrewAI |
| **LLM** | Google Gemini 2.5 Pro Preview |
| **Tools** | `ScrapeWebsiteTool`, `SerperDevTool`, `WebsiteSearchTool` |
| **API Key Management** | `python-dotenv` (recommended) |
| **Environment** | Jupyter Notebook / Google Colab |

---

## 📁 Project Structure

```
CUSTOMER-SUPPORT-RAG-WITH-CREWAI-GEMINI/
├── CUSTOMER_SUPPORT_RAG.ipynb   # Main notebook
├── .gitignore                   # Excludes .env and cache files
└── README.md                    # This file
```

---

## 🚀 Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/SESHANKCH7171/CUSTOMER-SUPPORT-RAG-WITH-CREWAI-GEMINI.git
cd CUSTOMER-SUPPORT-RAG-WITH-CREWAI-GEMINI
```

### 2. Install Dependencies
```bash
pip install crewai crewai-tools google-generativeai python-dotenv
```

### 3. Set Up Your API Key

**Option A — .env file (Recommended):**
```env
GEMINI_API_KEY=your_gemini_api_key_here
SERPER_API_KEY=your_serper_api_key_here
```
Then load it in the notebook:
```python
from dotenv import load_dotenv
load_dotenv()
```

**Option B — Set directly in notebook:**
```python
import os
os.environ["GEMINI_API_KEY"] = "your_key_here"
```
> ⚠️ If using Option B, **never commit your key to GitHub.**

> 🔑 Get your Gemini API key from [Google AI Studio](https://aistudio.google.com/app/apikey)

### 4. Run the Notebook
Open `CUSTOMER_SUPPORT_RAG.ipynb` in Jupyter or Google Colab and run all cells.

---

## 🔍 Customer Inquiries Handled

The crew processes the following real-world questions from **Arjun Mehta @ TechFlow India**:

```python
customer_questions = [
    "How do I set up subscriptions?",
    "How do I handle refunds?",
    "How do I go live?",
]
```

Each question triggers a full two-agent pipeline — scrape → respond → QA review → final answer.

---

## 📊 Sample Output Flow

```
🟢 Crew Execution Started
  └── 🟡 Task Started: inquiry_resolution
        └── 🟣 Agent: Senior Support Representative
              └── 🔧 Tool: read_website_content (docs.stripe.com)
              └── ✅ Tool Completed
        └── 🟢 Task Completed
  └── 🟡 Task Started: quality_assurance_review
        └── 🟣 Agent: Support QA Specialist
              └── ✅ Agent Final Answer delivered
  └── 🟢 Crew Execution Completed
```

---

## ⚙️ Configuration

```python
crew = Crew(
    agents=[support_agent, support_quality_assurance_agent],
    tasks=[inquiry_resolution, quality_assurance_review],
    verbose=True,
    memory=False,        # Set True to enable cross-run memory
    llm=gemini_llm
)
```

---

## 🔒 Security Note

> ⚠️ **Never commit API keys to GitHub.**  
> Replace any hardcoded keys with `os.getenv("GEMINI_API_KEY")` before pushing.  
> Use a `.env` file locally and add it to `.gitignore`.

---

## 🗺️ Part of My Agentic AI Roadmap

| # | Project | Stack | Status |
|---|---|---|---|
| 1 | Multi-Agent Content Engine | CrewAI, Gemini | ✅ Shipped |
| **2** | **Customer Support Automation** | **CrewAI, Gemini, ScrapeWebsiteTool** | **✅ Shipped** |
| 3 | Production RAG System | LangChain, ChromaDB | 🔄 In Progress |
| 4 | Multi-Agent Research System | LangGraph, LangSmith | 🔜 Coming |
| 5 | B2B Agentic Pipeline | n8n, LangGraph, FastAPI | 🔜 Coming |

---

## 👤 Author

**Seshank CH** — Agentic AI Engineer  
📍 Nashik, Maharashtra, India  
🔗 [LinkedIn](https://www.linkedin.com/in/seshankch/) | 💻 [GitHub](https://github.com/SESHANKCH7171)

---

*Building production-grade multi-agent AI systems — one agent at a time. 🚀*
