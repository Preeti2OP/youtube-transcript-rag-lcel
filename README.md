# YouTube Video Transcript RAG System

An end-to-end Retrieval-Augmented Generation (RAG) system built with **LangChain (LCEL)**, **FAISS**, and **HuggingFace Transformers**. This application automatically extracts YouTube video transcripts, indexes them into a local vector database, and performs context-grounded Question Answering (QA) using open-source Large Language Models.

---

## 📌 Architecture Overview

1. **Data Ingestion:** Fetches video transcripts directly using `youtube-transcript-api`.
2. **Text Chunking:** Splits full transcripts into overlapping chunks using `RecursiveCharacterTextSplitter` to preserve context boundaries.
3. **Vector Embeddings & Storage:** Generates dense vector representations using `sentence-transformers/all-MiniLM-L6-v2` and indexes them in an in-memory **FAISS** vector store.
4. **Context Retrieval:** Uses similarity search (`k=4`) to retrieve the top relevant context snippets for a user query.
5. **Chain Execution (LCEL):** Constructs a declarative pipeline via `RunnableParallel` and `RunnablePassthrough` to format context and generate grounded responses via `google/flan-t5-large`.

---

## 🏗️ System Architecture & Workflow

```text
[ YouTube Video URL ] 
       │
       ▼ (youtube-transcript-api)
[ Raw Transcript Text ] 
       │
       ▼ (RecursiveCharacterTextSplitter)
[ Overlapping Text Chunks ] 
       │
       ▼ (HuggingFace Embeddings)
[ FAISS Vector Database Index ] 
       │
       ▼ (Similarity Retrieval k=4)
[ LCEL Parallel Chain Context ] 
       │
       ▼ (google/flan-t5-large LLM)
[ Grounded Answer Synthesis ]
```

## 🚀 Tech Stack

* **Language:** Python 3.10+
* **Framework:** LangChain (LCEL core & community modules)
* **Vector Store:** FAISS (Facebook AI Similarity Search)
* **Embedding Model:** HuggingFace `all-MiniLM-L6-v2`
* **LLM Engine:** HuggingFace `google/flan-t5-large`
* **Data Source:** YouTube Transcript API

---

## Create and activate a virtual environment:
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

## Install dependencies:
pip install youtube-transcript-api langchain-community langchain-huggingface faiss-cpu tiktoken python-dotenv

