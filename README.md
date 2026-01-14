## 🎯 Problem Statement

Organisations often store critical information across internal documents such as
policies, FAQs, product notes, and operational guides. While this information exists,
it is often difficult for employees or users to quickly find accurate, up-to-date
answers using traditional keyword search.

This leads to:
- Time wasted searching through documents
- Inconsistent or incomplete answers
- Increased reliance on subject-matter experts for routine questions

Large Language Models (LLMs) can generate fluent answers, but **on their own they may
hallucinate or provide information that is not grounded in company-approved sources**.

### The Challenge

How can we build a conversational assistant that:
- Answers questions **only using trusted internal documents**
- Retrieves the most relevant information accurately
- Provides clear, context-aware answers
- Remains transparent about where the information comes from

### The Solution

This project implements a **Retrieval-Augmented Generation (RAG) chatbot** that combines:

- **Vector search** to retrieve relevant document chunks
- **LLM-based query rewriting and reranking** to improve retrieval quality
- **Context-grounded answer generation** to ensure responses are based strictly on the knowledge base
- **A user-friendly Gradio interface** for interactive querying

The result is a chatbot that delivers **accurate, explainable, and source-backed answers**
about the organisation (Insurellm), while reducing hallucinations and improving information accessibility.  

---

## 📁 Code Overview & Execution Flow

This project consists of three main Python files that together implement a complete
Retrieval-Augmented Generation (RAG) pipeline with a web-based user interface.

The workflow is **two-step**:
1. **Ingest the knowledge base**
2. **Run the Gradio UI to interact with the RAG system**

---

## 1️⃣ `ingest.py` — Knowledge Base Ingestion

This script is responsible for **preparing the knowledge base** and must be run **once before using the chatbot**.

### What it does
- Loads all markdown documents from the `knowledge-base/` directory
- Uses an LLM to split each document into **overlapping semantic chunks**
- Generates:
  - A short **headline**
  - A concise **summary**
  - The **original text** for each chunk
- Creates vector embeddings for every chunk using OpenAI embeddings
- Stores embeddings, text, and metadata in a **persistent ChromaDB vector store**

---

## 2️⃣ `answer.py` — RAG Pipeline Logic

This file contains the core Retrieval-Augmented Generation (RAG) logic used at query time.

### Responsibilities

- Rewrites the user query to improve retrieval accuracy  
- Retrieves relevant chunks from ChromaDB using vector similarity  
- Merges results from multiple retrieval strategies  
- Reranks retrieved chunks using an LLM  
- Injects the top-ranked context into a system prompt  
- Generates a final answer grounded strictly in retrieved knowledge  

### Key Techniques Used

- Query rewriting  
- Vector similarity search  
- LLM-based reranking  
- Context-grounded answer generation  

> **Note:** This file is not run directly. It is imported and used by `app.py`.

---

## 3️⃣ `app.py` — Gradio User Interface

This script launches the interactive web interface for the chatbot.

### What It Does

- Creates a Gradio-based chat UI  
- Accepts user questions  
- Passes conversation history to the RAG pipeline  
- Displays:
  - The chatbot’s answer  
  - The retrieved context and source documents side-by-side

---

## 📝 Summary

- `ingest.py` → prepares and stores knowledge for retrieval  
- `answer.py` → handles retrieval, reranking, and answer generation  
- `app.py` → provides a web interface to interact with the RAG system  

This separation keeps ingestion, reasoning, and UI concerns cleanly isolated.
