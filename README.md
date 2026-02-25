---
title: AskMyDocs RAG Chatbot
emoji: 🤖📄
colorFrom: indigo
colorTo: blue
sdk: streamlit
sdk_version: "1.38.0"
app_file: app.py
pinned: false
license: mit
---

# RAG Pipeline with FAISS + Streamlit (Local LLM via Ollama)

A **Retrieval-Augmented Generation (RAG)** system using FAISS for vector storage, Streamlit for a ChatGPT-style interface, and a local LLM via Ollama (Mistral) for private, on-device inference.

---

## Tech Stack
- **LLM (generation):** Mistral via Ollama  
- **Embeddings:** `sentence-transformers/all-MiniLM-L6-v2` (HuggingFace)  
- **Vector DB:** FAISS (persisted locally)  
- **Frameworks:** LangChain (community + HuggingFace + Ollama integrations)  
- **UI:** Streamlit (chat interface + sidebar uploads)  
- **Loaders:** PyPDFLoader (PDF), TextLoader (TXT)  
- **Memory:** Session-level chat history (UI only, not passed to LLM for context)  

---

## Features
- Upload PDFs/TXTs → automatic embeddings → store in FAISS  
- Chat with your documents using a ChatGPT-style interface  
- Incremental knowledge growth; new uploads are added without overwriting  
- Local inference ensures privacy and no cloud dependency  
- Session-level chat history for UI continuity (each query is independent to the LLM)  

---

## Folder Structure

rag_project/
├─ data/ # Uploaded PDFs/TXTs
├─ index/ # FAISS vector DB (persistent)
├─ ingest.py # Ingestion pipeline (embed + store docs)
├─ query.py # Retrieval + generation
├─ app.py # Streamlit chat app
├─ requirements.txt # Dependencies
└─ Procfile # Deployment configuration


---

## Getting Started

### Setup
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Install Ollama
```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama serve
ollama pull mistral     # or: ollama pull gemma:2b
```

### Run the App
```bash
streamlit run app.py
```

## Usage

1. Open the Streamlit app URL (typically `http://localhost:8501`)
2. Use "Manage Documents" in the sidebar to upload PDFs/TXTs
3. Ask questions in the chat; answers are grounded in uploaded documents
4. Knowledge base grows incrementally as new documents are added

## Implementation Details

- **Ingestion:** PyPDFLoader & TextLoader → HuggingFace embeddings → FAISS
- **Retrieval + Generation:** FAISS retriever (top-3 chunks) → LangChain prompt → Ollama Mistral LLM
- **UI Memory:** Streamlit session state maintains chat history for display only

## Achievements

- ✅ Fully functional RAG pipeline with FAISS
- ✅ ChatGPT-style UI for Q&A over documents
- ✅ Incremental knowledge base growth (no reindexing required)
- ✅ Fully local inference (privacy-friendly, no cloud dependency)
- ✅ Support for both PDF and TXT documents
