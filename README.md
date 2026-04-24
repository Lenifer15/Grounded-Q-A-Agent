# 🧠 Grounded Q&A Agent with LangChain, Granite 3 & RAG

> A production-ready, hallucination-resistant Q&A agent powered by IBM Granite 3, LangChain, and Retrieval-Augmented Generation (RAG) — delivering accurate, source-grounded answers from your own documents.

---

## 📌 Description

This project implements a **grounded Question-Answering (Q&A) Agent** that retrieves relevant context from a custom document corpus before generating answers. By combining **IBM Granite 3** as the LLM backbone with **LangChain's** RAG pipeline and a vector store, the agent avoids hallucinations and provides traceable, evidence-backed responses.

Ideal for enterprise knowledge bases, internal documentation Q&A, and research assistants.

---

## ✨ Features

- 🔍 **Retrieval-Augmented Generation (RAG)** — grounds every answer in retrieved document chunks
- 🤖 **IBM Granite 3 LLM** — enterprise-grade language model with strong instruction-following
- 🔗 **LangChain Orchestration** — modular pipeline for ingestion, retrieval, and generation
- 📄 **Custom Document Ingestion** — supports PDF, TXT, and Markdown sources
- 🗃️ **Vector Store Integration** — fast semantic search via FAISS or Chroma
- 📎 **Source Citation** — every answer is returned with the source document reference
- 🧩 **Modular Architecture** — easily swap LLMs, vector stores, or document loaders
- 🖥️ **CLI + API Interface** — run via terminal or expose as a REST endpoint

---

## 🛠️ Tech Stack

| Component        | Technology                           |
|------------------|--------------------------------------|
| LLM              | IBM Granite 3 (via WatsonX / Ollama) |
| Orchestration    | LangChain                            |
| Vector Store     | FAISS / Chroma                       |
| Embeddings       | HuggingFace / WatsonX Embeddings     |
| Document Loaders | LangChain Community Loaders          |
| API Layer        | FastAPI (optional)                   |
| Language         | Python 3.10+                         |
| Package Manager  | pip / Poetry                         |

---

## ⚙️ Installation

### Prerequisites

- Python 3.10 or higher
- An IBM WatsonX API key **or** Ollama running Granite 3 locally
- Git

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/your-username/granite-rag-agent.git
cd granite-rag-agent

# 2. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Configure environment variables
cp .env.example .env
# Edit .env and add your WatsonX credentials or Ollama endpoint
```

### Environment Variables (`.env`)

```env
WATSONX_API_KEY=your_api_key_here
WATSONX_PROJECT_ID=your_project_id
WATSONX_URL=https://us-south.ml.cloud.ibm.com

# Optional: Ollama local setup
OLLAMA_BASE_URL=http://localhost:11434
```

---

## 🚀 Usage

### 1. Ingest Your Documents

Place your source files (`.pdf`, `.txt`, `.md`) in the `docs/` folder, then run:

```bash
python ingest.py
```

### 2. Run the Q&A Agent (CLI)

```bash
python agent.py --query "What is the refund policy for enterprise plans?"
```

### 3. Launch the API Server (Optional)

```bash
uvicorn app.main:app --reload
```

Then POST a question:

```bash
curl -X POST http://localhost:8000/ask \
  -H "Content-Type: application/json" \
  -d '{"question": "What are the system requirements?"}'
```

---

## 💡 Example

**Input:**
```
Query: "What is Granite 3's context window size?"
```

**Output:**
```json
{
  "answer": "IBM Granite 3 supports a context window of up to 128,000 tokens, making it suitable for long-document reasoning tasks.",
  "sources": [
    "docs/granite3_technical_specs.pdf — Page 4"
  ]
}
```

---

## 📁 Folder Structure

```
granite-rag-agent/
│
├── docs/                   # Source documents for ingestion
├── vectorstore/            # Persisted FAISS/Chroma vector index
│
├── app/
│   ├── main.py             # FastAPI entry point
│   └── routes.py           # API route definitions
│
├── src/
│   ├── ingestor.py         # Document loading, chunking & embedding
│   ├── retriever.py        # Vector store retrieval logic
│   ├── agent.py            # LangChain RAG chain and agent logic
│   └── llm.py              # Granite 3 LLM wrapper (WatsonX/Ollama)
│
├── ingest.py               # CLI script to run ingestion
├── agent.py                # CLI script to query the agent
├── requirements.txt
├── .env.example
└── README.md
```

---

## 🤝 Contributing

1. Fork this repository
2. Create a new branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m "feat: add your feature"`
4. Push to your fork: `git push origin feature/your-feature-name`
5. Open a Pull Request

Please follow [Conventional Commits](https://www.conventionalcommits.org/) and ensure new features include documentation.

---

## 📄 License

Licensed under the **MIT License**. See [LICENSE](./LICENSE) for details.

---

## 👩‍💻 Author

**Jessica Lenifer R.**

---

> *"Ground your AI. Every answer should have a source."*
