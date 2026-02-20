# SanskritRAG – CPU-Based Sanskrit Retrieval Augmented Generation System

SanskritRAG is a Retrieval-Augmented Generation (RAG) system built for Sanskrit question answering.  
It retrieves relevant content from Sanskrit documents before generating answers, ensuring grounded and context-aware responses.  
The system is designed to run entirely on CPU without any GPU dependency.

---

## Project Overview

The objective of this project is to create a reliable Sanskrit question-answering system that avoids blind AI generation. Instead of letting a language model hallucinate answers, the system first retrieves semantically relevant content from uploaded Sanskrit PDFs and then generates answers strictly based on that retrieved context.

The entire pipeline is built using Python, ChromaDB, Sentence Transformers, and Google Gemini API.

---

## How the System Works

The workflow follows a structured RAG pipeline:

1. Sanskrit PDF documents are placed inside the `data/` directory.
2. The system extracts text from PDFs.
3. Extracted text is split into meaningful overlapping chunks.
4. Multilingual embeddings are generated for each chunk.
5. These embeddings are stored in a local ChromaDB vector database.
6. The user enters a Sanskrit query in the terminal.
7. Relevant text chunks are retrieved using semantic similarity search.
8. Gemini generates the final answer using ONLY the retrieved context.
9. If the answer is not present in the retrieved content, the system returns:  
   **"I don’t know"**

This ensures correctness, transparency, and reduced hallucination.

---

## Key Features

- Fully CPU-based execution
- Local persistent vector database using ChromaDB
- Multilingual embedding model supporting Sanskrit
- Controlled and grounded answer generation
- Clear modular architecture
- Safe fallback when answer is not found

---

## Technology Stack

Programming Language:
- Python 3.11+

Vector Database:
- ChromaDB (local persistent storage for embeddings)

Embedding Model:
- sentence-transformers/distiluse-base-multilingual-cased-v2  
  (Multilingual model supporting Sanskrit, runs on CPU)

Text Processing:
- langchain-community (document loading)
- langchain-text-splitters (chunking long text)
- pypdf (PDF extraction)

Large Language Model:
- Google Gemini API (google-genai)
  - Generates answers strictly using retrieved context
  - Avoids unsupported generation

Environment Management:
- python-dotenv (secure API key handling)

CPU Enforcement:
```python
os.environ["CUDA_VISIBLE_DEVICES"] = ""
