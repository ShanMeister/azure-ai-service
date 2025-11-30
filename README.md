# Azure AI Service - AI-Powered Document Processing System: Architecture & Capability Showcase

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-Latest-green.svg)](https://fastapi.tiangolo.com/)

This document serves as an **Architecture Design and Technical Capability Summary** for an Enterprise-Level AI Intelligent Document Processing System. The core objective of this project is to demonstrate the implementation of **Clean Architecture** principles, integrating multiple **Azure AI Services** (including Azure OpenAI and Azure AI Search) to build a **highly scalable, maintainable, and performant** backend system.

This system provides an all-in-one document solution covering parsing, content extraction, intelligent summarization, multi-language translation, and content Q&A functionalities. **To protect intellectual property, this document focuses solely on the system design and technical implementation details, and does not include proprietary source code.**

## 🌟 Key Features (Architectural Highlights)

The system design emphasizes the architecture and efficiency required for enterprise-level applications:

-   **🏗️ Clean Architecture Implementation**: Strict separation of business logic (Use Cases), data access (Repositories), and external interfaces (Controllers) ensures modularity, testability, and long-term maintainability.
-   **🤖 AI-Driven Data Processing**: Leverages **Azure OpenAI GPT-5** for advanced intelligent analysis, including complex document summarization and multi-language Q&A generation.
-   **⚡ High-Performance Asynchronous Architecture**: Built on **FastAPI** to achieve fully asynchronous processing, optimizing the speed and concurrency of I/O-intensive tasks like file uploads and AI service calls.
-   **🔍 Intelligent Search Integration**: Deep integration with **Azure AI Search** enables semantic search of document content and efficient RAG (Retrieval-Augmented Generation) workflows.
-   **🌐 Multi-Language/Multi-Format Support**: Natively supports various document formats including PDF, DOCX, and DOC, offering summarization and translation in multiple languages (Chinese, English, Japanese, etc.).

## 🚀 Core Functions (Functional Modules)

The system organizes functionalities into distinct service or module boundaries:

### 1. AI Document Service (`/ai_service`)
-   Asynchronous document parsing and structured content extraction.
-   Generation of document-level intelligent summaries and multi-language Q&A data preparation.
-   Automated creation of Azure AI Search indexes from document content.

### 2. Contract Search Service (`/contract_search`)
-   Semantic search against specific document sets (e.g., contracts).
-   Similarity matching and configurable search thresholds.

### 3. Real-Time AI Service (`/real_time_ai_service`)
-   Supports instant summarization and translation of document content.
-   Document-based interactive chat conversations (RAG Chat).
-   Built-in conversation history management.

### 4. Document Lifecycle Management
-   CRUD (Create, Read, Update, Delete) operations for document records.
-   Synchronization with the AI Search index to ensure data consistency.

## 🛠️ Technical Architecture (In-Depth Technical Stack)

### Core Technology Stack
-   **Web Framework**: FastAPI (for high-performance asynchronous APIs)
-   **AI Services**: Azure OpenAI (GPT-5), Azure Document Intelligence
-   **Search Engine**: Azure AI Search (for semantic search)
-   **Database**: SQLite/SQL Server (Designed for a configurable data access layer)
-   **File Processing**: PyMuPDF, python-docx (underlying document parsing libraries)
-   **Asynchronous Processing**: AsyncIO, APScheduler

### System Architecture (Clean Architecture Layering)

This diagram clearly illustrates the layering of the **Clean Architecture**, ensuring that core business logic remains independent of external frameworks and databases.


```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   FastAPI Web  │    │   Use Cases      │    │  Repositories   │
│   Controllers  │───▶│   (Business      │───▶│   (Data         │
│                 │    │    Logic)        │    │    Access)      │
└─────────────────┘    └──────────────────┘    └─────────────────┘
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Models &      │    │   Pipeline       │    │   Database      │
│   Schemas       │    │   Processing     │    │   (SQLite/      │
│                 │    │                  │    │    SQL Server)  │
└─────────────────┘    └──────────────────┘    └─────────────────┘
         │                       │
         ▼                       ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Azure AI Services                           │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │
│  │ Azure OpenAI│  │ Document    │  │ AI Search   │           │
│  │   (GPT-5)  │  │ Intelligence│  │             │           │
│  └─────────────┘  └─────────────┘  └─────────────┘           │
└─────────────────────────────────────────────────────────────────┘
```

## 📦 Project Structure (Design Structure)

The project structure reflects the principle of separation of concerns inherent in Clean Architecture:

```
azure_ai_service/
├── app/                          # Application core
│   ├── conf/                     # Configuration files
│   ├── enums/                    # Enumeration definitions
│   ├── msg_format/              # Message format definitions
│   ├── repository/              # Data access layer
│   ├── use_case/                # Business logic layer
│   └── utils/                   # Utility classes
├── src/doc2rag/                 # Document processing core
│   ├── cli/                     # Command line tools
│   ├── db_utils/                # Database utilities
│   ├── pipeline/                # Processing pipeline
│   └── ...                      # Other processing modules
├── configuration/               # System configuration
├── scripts/                     # Script files
├── logs/                        # Log directory
├── result/                      # Processing results
├── main.py                      # FastAPI application entry point
├── run.py                      # Run FastAPI application
├── pipeline.py                  # Processing pipeline
└── pyproject.toml              # Project configuration
```

## 🔧 Installation and Setup (Configuration Demonstration)

**Note: This section demonstrates the required environment and configuration structure. All values are placeholders for a proof-of-concept design.**

### System Requirements
- Python 3.9+
- Sufficient memory for processing large documents

### Installation Steps (Design Flow)

1.  **Clone the Project (Code omitted for IP protection)**
    ```bash
    # The source code is omitted; this is to show the setup flow.
    # git clone [Repository URL Omitted for IP Protection]
    # cd azure_ai_service
    ```

2.  **Install Dependencies**
    ```bash
    pip install -e .
    ```

3.  **Setup Environment Variables (Placeholders)**
    
    Create a `.env` file in the `app/conf/` directory. The following are required configurations (**all values are placeholders**):
    ```env
    # Azure OpenAI Configuration
    AOAI_API_KEY=your_azure_openai_key_PLACEHOLDER
    AOAI_ENDPOINT=your_azure_openai_endpoint_PLACEHOLDER
    AOAI_MODEL=gpt-5
    
    # Azure Document Intelligence
    DI_ENDPOINT=your_document_intelligence_endpoint_PLACEHOLDER
    DI_API_KEY=your_document_intelligence_key_PLACEHOLDER
    
    # Azure AI Search
    AIS_ENDPOINT=your_ai_search_endpoint_PLACEHOLDER
    AIS_API_KEY=your_ai_search_key_PLACEHOLDER
    AIS_INDEX_NAME=your_index_name
    
    # Other Configurations
    SAVE_API_FILE_PATH=./uploaded_files
    ```

4.  **Initialize System**
    ```bash
    # Initialize directory structure and base data
    digest-cli initialize
    ```

## 🚀 Usage (API and Endpoint Design)

### Starting the Service (Startup Demonstration)

1.  **Direct FastAPI Service Launch**
    ```bash
    python run.py
    ```

2.  **Using uvicorn (Standard Runtime)**
    ```bash
    uvicorn run:app --host 0.0.0.0 --port 8000 --reload
    ```

### Main API Endpoints (API Interface Design)

#### 1. AI Document Processing Service
```http
POST /ai_service
Content-Type: multipart/form-data

{
  "system_name": "AIService",
  "account_id": "user123",
  "document_id": "doc456",
  "response_language": "Traditional Chinese",
  "file": [document file] // Document upload
}
```


#### 2. Contract Search
```http
POST /contract_search
Content-Type: multipart/form-data

{
  "system_name": "AIService",
  "message_request": "Search related contracts", // Search query
  "document_count": 10
}
```

#### 3. Real-Time AI Service
```http
POST /real_time_ai_service
Content-Type: multipart/form-data

{
  "system_name": "AIService",
  "action": "summarize",
  "account_id": "user123",
  "response_language": "Traditional Chinese",
  "file": [document file]
}
```

## 🔍 Processing Flow

### Document Processing Pipeline

1. **File Upload and Validation**
   - File format checking (PDF, DOCX, DOC)
   - File size limitation (10MB)
   - File content preprocessing

2. **Azure Document Intelligence Analysis**
   - Document structure parsing
   - Text content extraction
   - Table and image recognition

3. **Content Processing and Integration**
   - Markdown format conversion
   - Image description generation (GPT-5)
   - Table content organization

4. **AI Service Processing**
   - Intelligent summary generation
   - Multi-language translation
   - Q&A content generation

5. **Indexing and Storage**
   - Azure AI Search index creation
   - Database record storage
   - Processing result caching

## 🧪 Testing

### Running Tests
```bash
# Run all tests
pytest

# Run specific test files
pytest unittest/test_specific.py

# Run tests with coverage report
pytest --cov=app
```

### Health Checks
```bash
# Service health check
curl http://localhost:8000/health_check

# Azure OpenAI health check
curl http://localhost:8000/health_check/aoai
```

## 📊 Monitoring and Logging

### Log Configuration
The system uses `loguru` for log management, with log files located in the `logs/` directory.

### Monitoring Metrics
- API response time
- Document processing success rate
- Azure AI service usage
- System resource utilization
