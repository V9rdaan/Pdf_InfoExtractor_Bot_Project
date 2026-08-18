# AI-Powered PDF Question Answering System

An AI-powered document question-answering system that allows users to upload large PDF documents and ask natural-language questions about their contents.

The system uses a multi-stage Retrieval-Augmented Generation (RAG) pipeline combining semantic search, keyword matching, fuzzy retrieval, reranking, and conversational memory to retrieve relevant document context before generating an answer.

## Features

* Upload and process PDF documents
* Clean and chunk large documents for retrieval
* Generate semantic embeddings using BGE embeddings
* Store document vectors using FAISS
* Maintain both L2 and cosine-similarity indices
* Combine semantic, keyword, and fuzzy retrieval
* Rerank retrieved chunks before answer generation
* Maintain multi-turn conversational context
* Generate answers grounded in retrieved PDF content
* FastAPI backend for document upload and question answering
* Streamlit interface for interacting with the system

## Tech Stack

**Programming:** Python

**API:** FastAPI

**Interface:** Streamlit

**Vector Search:** FAISS

**Embeddings:** BAAI/bge-large-en-v1.5

**Reranking:** BAAI/bge-reranker-v2-m3

**LLM Integration:** OpenAI API

**Memory:** LangChain ConversationBufferMemory

**Text Matching:** RapidFuzz

## System Workflow

```text
PDF Upload
    ↓
Text Extraction & Cleaning
    ↓
Document Chunking
    ↓
BGE Embeddings
    ↓
FAISS Vector Indices
    ↓
User Question
    ↓
Semantic + Keyword + Fuzzy Retrieval
    ↓
Chunk Reranking
    ↓
Relevant Context Selection
    ↓
LLM Answer Generation
    ↓
Conversational Response
```

## Project Structure

```text
Pdf_InfoExtractor_Bot_Project/
│
├── main.py
│
├── chatbot/
│   ├── __init__.py
│   └── logic.py
│
├── pipeline/
│   ├── __init__.py
│   ├── cleaner.py
│   ├── embed_and_index.py
│   ├── eda_tools.py
│   └── run.py
│
├── streamlit_app.py
├── requirements.txt
├── .env.example
├── .gitignore
└── README.md
```

## API Endpoints

### Upload PDF

```text
POST /upload
```

Uploads a PDF and triggers the document-processing and indexing pipeline.

### Ask Question

```text
POST /ask
```

Accepts a natural-language question and returns an answer generated using relevant context retrieved from the processed document.

### Health Check

```text
GET /health
```

Checks whether the API service is running.

### System Statistics

```text
GET /stats
```

Returns document and system-related statistics.

## Setup

Clone the repository:

```bash
git clone https://github.com/V9rdaan/Pdf_InfoExtractor_Bot_Project.git
cd Pdf_InfoExtractor_Bot_Project
```

Create a virtual environment:

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Create a `.env` file:

```env
OPENAI_API_KEY=your_openai_api_key
```

## Run the API

```bash
uvicorn main:app --reload
```

FastAPI documentation will then be available through the local API documentation page.

## Run the Streamlit Interface

```bash
streamlit run streamlit_app.py
```

## Retrieval Pipeline

The system does not rely on a single similarity search.

It combines multiple retrieval techniques to improve the probability of identifying relevant information from large documents:

* Semantic vector retrieval
* Cosine and L2 FAISS search
* Keyword matching
* Fuzzy text matching
* Cross-encoder reranking

The highest-ranking document chunks are then supplied as context to the language model for answer generation.

## Conversational Memory

LangChain conversational memory is used to preserve context between consecutive questions, allowing users to ask follow-up questions without repeating the entire context.


## Future Improvements

* Support multiple PDFs within a single session
* Add source-page citations to generated answers
* Add persistent conversation history
* Improve document-table extraction
* Add automated evaluation for retrieval and answer quality
* Deploy the application for public demonstration

## Author

**Vardaan Talwar**

GitHub: [V9rdaan](https://github.com/V9rdaan)

LinkedIn: [vardaantalwar](https://www.linkedin.com/in/vardaantalwar)
