# Research Offline Intelligences (RI)

**A Local AI-Powered Research Assistant for PDF Documents**

Research Offline Intelligences (RI) is a document-based AI research assistant designed to help users upload PDF documents, retrieve relevant information, and ask questions using a locally running language model.

The application combines document processing, vector search, and AI-powered question answering to provide answers grounded in selected PDF content, along with source citations.

##  Key Features

-  **PDF Upload:** Upload PDF documents for analysis.
-  **Text Extraction:** Extract text from PDFs and divide it into smaller chunks.
-  **Semantic Search:** Use embeddings and FAISS vector search to find relevant document content.
-  **Local AI Question Answering:** Generate answers using an Ollama-powered language model.
-  **Source Citations:** Return document names, page numbers, and relevant text snippets with answers.
-  **Document Management:** Retrieve a list of uploaded documents.
-  **Database Integration:** Store document metadata, text chunks, and question history.
-  **REST API:** Expose endpoints for document upload, listing, question answering, and health checks.

##  Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core application logic |
| FastAPI | Backend REST API |
| SQLAlchemy | Database operations and ORM |
| FAISS | Vector similarity search |
| Embeddings | Convert text and questions into vectors |
| Ollama | Run a local language model |
| PDF Processing | Extract and process PDF content |
| Uvicorn | Local ASGI application server |

## ⚙️ How It Works

1. **Upload:** The user uploads a PDF document.
2. **Extract:** The application extracts text and divides it into chunks.
3. **Embed:** Text chunks are converted into embeddings.
4. **Index:** FAISS indexes the vectors for retrieval.
5. **Ask:** The user submits a question about a selected document.
6. **Retrieve:** Relevant chunks belonging to that document are retrieved.
7. **Generate:** The local Ollama model generates an answer using the retrieved evidence.
8. **Cite:** The API returns the answer with source document names, page numbers, and snippets.

##  Project Structure

```text
offline-research-ai/
├── app/
│   ├── faiss_data/
│   ├── uploads/
│   ├── __init__.py
│   ├── database.py
│   ├── embeddings.py
│   ├── faiss_store.py
│   ├── main.py
│   ├── models.py
│   ├── ollama_client.py
│   ├── pdf_utils.py
│   └── schemas.py
├── .env.example
├── .gitignore
├── README.md
└── requirements.txt
```

*This structure is based on the current project files. Update it if your repository contains additional folders, such as a frontend directory.*

##  Getting Started

### Prerequisites

Install the following before running the application:

- Python 3.10 or a compatible version for your dependencies
- pip
- Ollama
- A compatible Ollama language model
- A compatible embedding model

### 1. Clone the repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd offline-research-ai
```

Replace `YOUR_GITHUB_REPOSITORY_URL` with your actual repository URL.

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on Windows:

```bash
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set up Ollama

Install Ollama from its official website:

https://ollama.com/

Start Ollama and download the model configured in `app/ollama_client.py`.

For example, if your application is configured to use the `llama3.2` model:

```bash
ollama pull llama3.2
```

**Important:** Use the actual model name configured in your project. Check `app/ollama_client.py` before running this command.

Also ensure that the embedding model configured in `app/embeddings.py` is available locally.

### 5. Configure environment variables

Review `.env.example` and `app/database.py` to identify the configuration required by your application.

Configure the relevant settings, including the upload directory and database connection if needed. Never commit passwords, API keys, or private credentials to GitHub.

### 6. Run the application

From the project root, run:

```bash
uvicorn app.main:app --reload
```

Once the server starts, open:

- **API:** http://127.0.0.1:8000
- **Interactive API documentation:** http://127.0.0.1:8000/docs
- **Health check:** http://127.0.0.1:8000/health

The interactive API documentation lets you test the available endpoints.

## 🔗 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/health` | Check API status |
| POST | `/upload` | Upload and process a PDF |
| GET | `/documents` | List uploaded documents |
| POST | `/ask` | Ask a question about a selected document |

For `/ask`, provide a valid document ID and a question in the request body, following the schema defined in `app/schemas.py`.

## 🔒 Privacy and Offline Processing

RI is designed to use a locally running Ollama language model and local document retrieval components.

The intention is to process research documents locally rather than rely on a cloud-based language model API. However, complete offline operation depends on the model setup, dependencies, and any external services used by the application.

##  Future Improvements

- Improve document indexing and retrieval accuracy.
- Add a more polished user interface.
- Improve persistent storage and index recovery.
- Add document deletion and re-indexing functionality.
- Strengthen file validation and API security.
- Expand automated testing and error handling.
- Improve installation and offline setup documentation.

##  Developer

**Shanmugapriya MK**

GitHub: https://github.com/shanmugapriya-MK

##  Project Status

**In Progress **

RI is an ongoing project exploring local language models, document retrieval, semantic search, and AI-assisted research workflows.

---

 If you find this project interesting, feel free to explore the repository and its implementation.
