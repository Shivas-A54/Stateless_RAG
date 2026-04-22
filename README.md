# Stateless RAG 

> RAG without vector databases — uses tree-indexed PDF navigation + Gemini 2.0 Flash.

---

## What It Does

Most RAG systems chunk documents into vector embeddings and run similarity search. This project skips all that.

Instead:
1. PDF is uploaded to **PageIndex**, which builds a tree index (like a smart Table of Contents)
2. On each query, **Gemini navigates the tree** to find the right sections
3. Gemini then **generates a cited answer** from those sections

No embeddings. No vector store. Just two API calls per query.

---

## How It Works

```
PDF → PageIndex (tree index) → User Query
                                    ↓
                          Gemini: "Which nodes answer this?"
                                    ↓
                          Fetch those sections
                                    ↓
                          Gemini: Generate cited answer
```

---

## Tech Stack

| What | Tool |
|------|------|
| Document Indexing | [PageIndex API](https://dash.pageindex.ai) |
| Language Model | Gemini 2.0 Flash |
| Interface | Jupyter Notebook |
| Language | Python 3.11+ |

---

## Setup

**1. Clone**
```bash
git clone https://github.com/Shivas-A54/Stateless_RAG.git
cd Stateless_RAG
```

**2. Install**
```bash
pip install pageindex python-dotenv google-generativeai ipykernel
```

**3. Add API keys**
```env
PAGEINDEX_API_KEY="your_key"   # → dash.pageindex.ai/api-keys
GEMINI_API_KEY="your_key"      # → aistudio.google.com/app/apikey
```

**4. Run**
```bash
jupyter notebook PageIndex.ipynb
```

---

## Project Structure

```
Stateless_RAG/
├── PageIndex.ipynb        # Full pipeline
├── RAG.pdf                # Sample PDF for testing
├── workflow_diagram.png   # Architecture diagram
├── .env.example           # API key template
└── pyproject.toml
```

---

## Why "Stateless"?

No vector store is created or maintained locally. The document tree lives in PageIndex (external), and each query runs as a clean, self-contained pipeline. Nothing is written to disk between runs.

---

## Limitations

- PDF only (other formats untested)
- Requires a PageIndex API account
- Two Gemini calls per query (adds slight latency)
- Very large PDFs may increase token usage

---

## Acknowledgments

- [PageIndex](https://pageindex.ai) — tree indexing API
- [Google Gemini](https://ai.google.dev/) — language model

---

*Built by [Shivas-A54](https://github.com/Shivas-A54)*
