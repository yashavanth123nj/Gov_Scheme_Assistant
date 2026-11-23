# # Government Scheme Assistant (Multilingual RAG with FastAPI Backend)

This project implements a complete End-to-End **Retrieval-Augmented Generation (RAG)** pipeline designed to ingest multilingual Government Scheme PDF documents and answer user queries with precise context and metadata citations. It also includes a robust **FastAPI** backend integrated with **Ngrok** to allow direct connections from a frontend application.

---

## 🚀 Features
- **Multilingual OCR & Extraction:** Integrated with **Docling** utilizing rapid OCR engine support for Indian Regional Languages (`en`, `hi`, `kn`, `te`, `ta`, `mr`).
- **Efficient Chunking:** Employs LangChain's `RecursiveCharacterTextSplitter` to handle complex document layouts.
- **Dense Embeddings:** Utilizes the highly-ranked `BAAI/bge-small-en-v1.5` sentence transformer for producing dense semantic embeddings.
- **Vector Database:** Uses **ChromaDB** as an in-memory local vector store for fast, reliable document segment retrieval.
- **Local LLM Integration:** Employs **Microsoft's Phi-3-mini-4k-instruct** optimized for local execution using `torch.float16` precision.
- **Full-featured Web Server:** Includes a **FastAPI** backend with endpoints supporting real-time document uploading, semantic chat querying, eligibility checks, and scheme indexing.
- **Public Tunneling:** Streamlines frontend testing via a direct public tunnel powered by **Ngrok**.

---

## 🛠️ Tech Stack
- **Inference & LLM:** `transformers` (Hugging Face), `PyTorch` (Float16 device-mapped)
- **Embeddings:** `sentence-transformers`
- **Vector DB:** `chromadb`
- **Document Parser:** `docling` (with `RapidOCR` configuration)
- **Backend Web Server:** `fastapi`, `uvicorn`, `pydantic`
- **Tunneling:** `pyngrok`

---

## 📋 API Endpoints
Once the backend is up and running, the following endpoints are available at the exposed server URL:

### 1. `GET /schemes`
*   **Description:** Fetch current indexed documents and active schemes.

### 2. `POST /upload`
*   **Description:** Upload a PDF scheme file to automatically convert, chunk, embed, and index it into ChromaDB.
*   **Payload:** Multipart Form Data (`file`, `session_id`, `permanent`).

### 3. `POST /chat`
*   **Description:** Ask a scheme-related question. The pipeline retrieves corresponding chunks from ChromaDB, formats the Phi-3 prompt, and outputs a context-bounded answer with metadata citations.
*   **Payload:** 
    ```json
    {
      "session_id": "string",
      "question": "What is the eligibility criteria?"
    }
    ```

### 4. `POST /eligibility`
*   **Description:** Evaluates a user profile against current criteria requirements.

### 5. `DELETE /uploads/{session_id}`
*   **Description:** Clears session storage and uploaded documents.

---
