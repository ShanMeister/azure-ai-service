# Azure AI service - AI-Powered Document Processing System

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-Latest-green.svg)](https://fastapi.tiangolo.com/)
[![License](https://img.shields.io/badge/License-Proprietary-red.svg)](LICENSE)

This is an AI-based intelligent document processing system designed for enterprise-level applications. It integrates multiple Azure AI services to provide document parsing, content extraction, intelligent summarization, translation, and Q&A functionalities.

## 🌟 Key Features

- **🤖 AI-Driven Document Processing**: Intelligent document analysis based on Azure OpenAI GPT-4o model
- **📄 Multi-Format Support**: Supports PDF, DOCX, DOC and other document formats
- **🔍 Intelligent Search**: Integrates Azure AI Search for semantic search functionality
- **🌐 Multi-Language Support**: Supports Chinese, English, and Japanese summarization and translation
- **💬 Real-Time Chat**: Intelligent Q&A system based on document content
- **🏗️ Clean Architecture**: Adopts clean architecture design, modular and easy to maintain
- **⚡ High-Performance Processing**: Asynchronous processing architecture based on FastAPI

## 🚀 Core Functions

### 1. AI Document Service (`/ai_service`)
- Automatic document parsing and content extraction
- Intelligent summary generation
- Multi-language Q&A generation
- Azure AI Search index creation

### 2. Contract Search (`/contract_search`)
- Semantic search of contract documents
- Similarity matching
- Configurable search thresholds

### 3. Real-Time AI Service (`/real_time_ai_service`)
- Instant document summarization
- Multi-language translation
- Document-based chat conversations
- Conversation history management

### 4. Document Management
- CRUD operations for document records
- AI Search index synchronization
- Document lifecycle management

## 🛠️ Technical Architecture

### Core Technology Stack
- **Web Framework**: FastAPI
- **AI Services**: Azure OpenAI (GPT-4o), Azure Document Intelligence
- **Search Engine**: Azure AI Search
- **Database**: SQLite/SQL Server (configurable)
- **File Processing**: PyMuPDF, python-docx, mammoth
- **Asynchronous Processing**: AsyncIO, APScheduler

### System Architecture

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
│  │   (GPT-4o)  │  │ Intelligence│  │             │           │
│  └─────────────┘  └─────────────┘  └─────────────┘           │
└─────────────────────────────────────────────────────────────────┘
```

## 📦 Project Structure

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

## 🔧 Installation and Setup

### System Requirements
- Python 3.9+
- Sufficient memory for processing large documents

### Installation Steps

1. **Clone the Project**
   ```bash
   git clone https://github.com/ShanMeister/azure_ai_service.git
   cd azure_ai_service
   ```

2. **Install Dependencies**
   ```bash
   pip install -e .
   ```

3. **Setup Environment Variables**
   
   Create a `.env` file in the `app/conf/` directory:
   ```env
   # Azure OpenAI Configuration
   AOAI_API_KEY=your_azure_openai_key
   AOAI_ENDPOINT=your_azure_openai_endpoint
   AOAI_MODEL=gpt-4o
   AOAI_API_VERSION=2024-05-01-preview
   
   # Azure Document Intelligence
   DI_ENDPOINT=your_document_intelligence_endpoint
   DI_API_KEY=your_document_intelligence_key
   
   # Azure AI Search
   AIS_ENDPOINT=your_ai_search_endpoint
   AIS_API_KEY=your_ai_search_key
   AIS_INDEX_NAME=your_index_name
   
   # Other Configurations
   SAVE_API_FILE_PATH=./uploaded_files
   O200K_BASE=./tiktoken_cache
   ```

4. **Setup Configuration File**
   
   Edit the `configuration/config.yml` file and fill in the corresponding configuration information.

5. **Initialize System**
   ```bash
   # Initialize directory structure
   digest-cli initialize
   ```

## 🚀 Usage

### Starting the Service

1. **Direct FastAPI Service Launch**
   ```bash
   python run.py
   ```

2. **Using uvicorn**
   ```bash
   uvicorn run:app --host 0.0.0.0 --port 8000 --reload
   ```

3. **Using Batch File (Windows)**
   ```bash
   start_server.bat
   ```

### API Documentation

After starting the service, you can view API documentation at:
- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

### Main API Endpoints

#### 1. AI Document Processing Service
```http
POST /ai_service
Content-Type: multipart/form-data

{
  "system_name": "AIService",
  "account_id": "user123",
  "document_id": "doc456",
  "response_language": "Traditional Chinese",
  "file": [document file]
}
```

#### 2. Contract Search
```http
POST /contract_search
Content-Type: multipart/form-data

{
  "system_name": "AIService",
  "message_request": "Search related contracts",
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

### Command Line Tools

The system provides rich CLI tools:

```bash
# Document scanning
digest-cli scan-files

# Document analysis
digest-cli di-analyze

# Document pagination
digest-cli split-pages

# Image description generation
digest-cli fig-gen-desc

# Content integration
digest-cli bundle

# Database operations
sqldb-cli file list
sqldb-cli chunk change-status --file-id 1 --status "processing"
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
   - Image description generation (GPT-4o)
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
