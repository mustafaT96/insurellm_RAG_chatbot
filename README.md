# 🏢 Insurellm RAG Chatbot

A Retrieval-Augmented Generation (RAG) chatbot built to answer questions about **Insurellm** using a company knowledge base.  
The system uses LLM-driven document chunking, vector search with ChromaDB, reranking, and a Gradio web interface.

---

## ✨ Features

- LLM-based document chunking with summaries and overlap
- Vector search using OpenAI embeddings + ChromaDB
- Query rewriting for improved retrieval
- LLM-based reranking of retrieved chunks
- Context-aware answer generation
- Interactive Gradio chat UI with retrieved sources

---

## 🧠 Architecture Overview

**Ingestion (offline)**  
1. Load markdown documents from `knowledge-base/`  
2. Split documents into overlapping chunks using an LLM  
3. Generate embeddings for each chunk  
4. Store vectors and metadata in a persistent ChromaDB store  

**Query Time (online)**  
1. Rewrite the user query for better KB retrieval  
2. Retrieve relevant chunks using vector similarity  
3. Merge and rerank chunks using an LLM  
4. Generate a final answer grounded in retrieved context  
5. Display answer and sources in the UI  

---

## 🗂 Project Structure  
insurellm_RAG_chatbot/
├── app.py # Gradio web interface  
├── ingest.py # Knowledge base ingestion pipeline  
├── answer.py # RAG retrieval + answering logic  
├── knowledge-base/ # Markdown documents (input)  
├── preprocessed_db/ # ChromaDB vector store (generated)  
├── .gitignore  
└── README.md  

---

## 🧪 Tech Stack  
1. Python  
2. OpenAI (Embeddings)  
3. Groq / OpenAI-compatible LLMs (Generation & reranking)  
4. LiteLLM  
5. ChromaDB  
6. Gradio  
7. Pydantic

---

## 🔍 Design Choices  
1. LLM-based chunking improves semantic coverage compared to fixed splitters
2. Query rewriting boosts recall for ambiguous user questions
3. Reranking ensures the most relevant context is passed to the final LLM
4. Context display improves transparency and debuggability

---
