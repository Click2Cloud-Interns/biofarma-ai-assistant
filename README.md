# 🏢 PT Bio Farma AI Assistant - Unified Dual-Agent System

<div align="center">

![Python Version](https://img.shields.io/badge/python-3.9%2B-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-0.111.0-green)
![Streamlit](https://img.shields.io/badge/Streamlit-1.36.0-red)
![Azure OpenAI](https://img.shields.io/badge/Azure-OpenAI-purple)
![License](https://img.shields.io/badge/license-MIT-yellow)

**A production-ready RAG system with dual specialized AI agents for SOP compliance and Human Capital management**

[Features](#-features) • [Demo](#-demo) • [Quick Start](#-quick-start) • [Documentation](#-documentation) • [API](#-api-documentation)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Architecture](#-architecture)
- [Agents](#-agents)
- [Tech Stack](#-tech-stack)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [API Documentation](#-api-documentation)
- [Project Structure](#-project-structure)
- [Development](#-development)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Overview

PT Bio Farma AI Assistant is a unified dual-agent system powered by Azure OpenAI that provides intelligent assistance for two critical business functions:

1. **SOP & Work Procedure Assistant** - Helps employees quickly find and understand Standard Operating Procedures
2. **Human Capital Assistant** - Provides instant answers to HR policy questions and employee benefits

Built with LangChain, FastAPI, and Streamlit, this system uses Retrieval-Augmented Generation (RAG) to deliver accurate, source-cited answers from your organization's documents.

---

## ✨ Features

### 🤖 Dual-Agent System
- **Two Specialized Agents** with different personas and expertise areas
- **Separate Vector Stores** for optimal retrieval performance
- **Independent Chat Histories** for each agent
- **Unified Interface** with seamless agent switching

### 🎨 Modern UI
- **Intuitive Streamlit Interface** with gradient designs
- **Real-time Chat Experience** with source citations
- **Example Questions** for quick onboarding
- **Document Upload** for HR documents
- **Responsive Design** for desktop and mobile

### 🔧 Production-Ready API
- **RESTful FastAPI Backend** with automatic documentation
- **Separate Endpoints** for each agent
- **CORS Support** for frontend integration
- **Health Check** and status monitoring
- **Error Handling** and validation

### 📚 Advanced RAG
- **FAISS Vector Store** for fast similarity search
- **Azure OpenAI Embeddings** (text-embedding-ada-002)
- **GPT-4.1 Mini** for intelligent responses
- **Chunk Optimization** (800 tokens, 120 overlap)
- **Top-K Retrieval** (4 most relevant chunks)

### 🔒 Enterprise Security
- **Environment Variables** for credential management
- **.env File Support** with python-dotenv
- **No Hardcoded Secrets** in codebase
- **API Key Validation** on startup

---

## 🏗 Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Streamlit Frontend                       │
│                    (app_final.py)                            │
└────────────────────────┬────────────────────────────────────┘
                         │ HTTP/REST
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                   FastAPI Backend (api.py)                   │
├─────────────────────────────────────────────────────────────┤
│  ┌──────────────────────┐    ┌──────────────────────┐       │
│  │   SOP Agent          │    │   HC Agent           │       │
│  │   /sop/ask           │    │   /hc/upload         │       │
│  │                      │    │   /hc/ask            │       │
│  └──────────┬───────────┘    └──────────┬───────────┘       │
└─────────────┼──────────────────────────┼─────────────────────┘
              │                          │
              ▼                          ▼
   ┌──────────────────┐      ┌──────────────────┐
   │  SOP FAISS Index │      │  HC FAISS Index  │
   │  (Markdown SOPs) │      │  (PDF/DOCX HRs)  │
   └──────────────────┘      └──────────────────┘
              │                          │
              └──────────┬───────────────┘
                         ▼
              ┌─────────────────────┐
              │   Azure OpenAI      │
              │  - Embeddings       │
              │  - GPT-4.1 Mini     │
              └─────────────────────┘
```

---

## 👥 Agents

### Agent 1: SOP Assistant 📋
**Persona:** Filman Galuh Purnawidjaya (AVP Kepatuhan)

**Specialized In:**
- Standard Operating Procedures (SOPs)
- Work Instructions (WIs)
- Quality Assurance Documents
- Compliance Procedures
- Manufacturing Protocols

**Response Style:**
- Numbered procedural steps
- Direct and concise
- SOP-style formatting
- Real-world pharma tone

**Example Questions:**
- "What is the temperature for aseptic filling?"
- "How do I perform LAL endotoxin testing?"
- "What are the gowning requirements for Grade A?"

### Agent 2: Human Capital Assistant 👥
**Persona:** Ditya Handayani (VP Layanan Human Capital)

**Specialized In:**
- HR Policies & Regulations
- Leave Policies (sick, annual, maternity)
- Employee Benefits
- Notice Periods & Exit Formalities
- Reimbursement Policies
- Working Hours & Attendance

**Response Style:**
- Professional HR tone
- Empathetic and helpful
- Policy citations
- Clear explanations

**Example Questions:**
- "What is the notice period?"
- "How many sick leaves do I get?"
- "What is the reimbursement policy?"

---

## 🛠 Tech Stack

| Component | Technology | Version |
|-----------|-----------|---------|
| **LLM** | Azure OpenAI GPT-4.1 Mini | Latest |
| **Embeddings** | Azure OpenAI text-embedding-ada-002 | Latest |
| **Vector DB** | FAISS (CPU) | 1.8.0 |
| **Framework** | LangChain | 0.2.6 |
| **Backend** | FastAPI | 0.111.0 |
| **Frontend** | Streamlit | 1.36.0 |
| **Language** | Python | 3.9+ |
| **Doc Processing** | PyPDF, python-docx | Latest |

---

## 📥 Installation

### Prerequisites
- Python 3.9 or higher
- Azure OpenAI account with:
  - text-embedding-ada-002 deployment
  - gpt-4.1-mini deployment
- Git (for cloning)

### Step 1: Clone Repository
```bash
git clone https://github.com/yourusername/biofarma-ai-assistant.git
cd biofarma-ai-assistant
```

### Step 2: Create Virtual Environment
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Mac/Linux
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 4: Create .env File
Create a `.env` file in the root directory:

```env
# Azure OpenAI Configuration
AZURE_OPENAI_ENDPOINT=https://your-resource.openai.azure.com/
AZURE_OPENAI_KEY=your-api-key-here
AZURE_OPENAI_API_VERSION=2024-02-01

# Deployment Names
AZURE_EMBEDDING_DEPLOYMENT=text-embedding-ada-002
AZURE_CHAT_DEPLOYMENT=gpt-4.1-mini
```

**Important:** Replace `your-resource` and `your-api-key-here` with your actual Azure OpenAI credentials.

### Step 5: Create Directory Structure
```bash
mkdir -p data/sop_documents
mkdir -p data/hc_documents
mkdir -p data/vectorstore
mkdir -p uploads/hc
```

---

## ⚙️ Configuration

### Azure OpenAI Setup

1. **Create Azure OpenAI Resource:**
   - Go to [Azure Portal](https://portal.azure.com)
   - Create a new Azure OpenAI resource
   - Note your endpoint URL

2. **Deploy Models:**
   - Deploy `text-embedding-ada-002` (for embeddings)
   - Deploy `gpt-4` or `gpt-4.1-mini` (for chat)
   - Note the exact deployment names

3. **Get API Key:**
   - Navigate to Keys and Endpoint
   - Copy one of the keys

4. **Update .env:**
   ```env
   AZURE_OPENAI_ENDPOINT=https://your-actual-resource.openai.azure.com/
   AZURE_OPENAI_KEY=your-actual-api-key
   AZURE_EMBEDDING_DEPLOYMENT=your-embedding-deployment-name
   AZURE_CHAT_DEPLOYMENT=your-chat-deployment-name
   ```

### Document Preparation

#### SOP Documents (Markdown Format)
Place `.md` files in `data/sop_documents/` with this structure:

```markdown
Document ID: SOP-MFG-2024-018
Title: Aseptic Filling Operations
Version: 1.0
Effective Date: 2024-01-15

## 1. Purpose
...

## 2. Scope
...
```

#### HC Documents (PDF/DOCX)
- Place PDF or DOCX files in `data/hc_documents/`
- OR upload via the web interface

---

## 🚀 Usage

### Option 1: Run Everything with Scripts

#### 1. Ingest Documents
```bash
# Process SOP documents
python ingest_unified.py sop

# Process HC documents (optional - can upload via UI)
python ingest_unified.py hc
```

#### 2. Start Backend API
```bash
python api.py
```
API will be available at: `http://localhost:8000`

#### 3. Start Frontend (New Terminal)
```bash
streamlit run app_final.py
```
Web UI will open at: `http://localhost:8501`

### Option 2: Use API Directly

#### Ask SOP Question
```bash
curl -X POST "http://localhost:8000/sop/ask" \
  -H "Content-Type: application/json" \
  -d '{"question": "What is the temperature for aseptic filling?"}'
```

#### Upload HC Document
```bash
curl -X POST "http://localhost:8000/hc/upload" \
  -F "file=@employee_manual.pdf"
```

#### Ask HC Question
```bash
curl -X POST "http://localhost:8000/hc/ask" \
  -H "Content-Type: application/json" \
  -d '{"question": "What is the notice period?"}'
```

#### Check System Status
```bash
curl http://localhost:8000/status
```

---

## 📚 API Documentation

### Base URL
```
http://localhost:8000
```

### Endpoints

#### 🔵 SOP Agent

**POST /sop/ask**

Ask questions about SOPs and work procedures.

```json
Request:
{
  "question": "What is the temperature for aseptic filling?"
}

Response:
{
  "answer": "The aseptic filling area must maintain...",
  "sources": [
    {
      "document_id": "SOP-MFG-2024-018",
      "title": "Aseptic Filling Operations",
      "doc_type": "Standard Operating Procedure",
      "filename": "SOP-MFG-2024-018.md"
    }
  ],
  "chunks": 4,
  "agent": "SOP Assistant"
}
```

#### 🟢 HC Agent

**POST /hc/upload**

Upload and process HR documents (PDF/DOCX).

```
Content-Type: multipart/form-data
file: <binary file data>

Response:
{
  "status": "success",
  "message": "Document processed successfully. Created 127 chunks.",
  "chunks_created": 127
}
```

**POST /hc/ask**

Ask questions about HR policies and benefits.

```json
Request:
{
  "question": "What is the notice period?"
}

Response:
{
  "answer": "The notice period is one month...",
  "sources": [...],
  "chunks": 4,
  "agent": "Human Capital Assistant"
}
```

#### ⚙️ System

**GET /status**

Check system health and agent status.

```json
Response:
{
  "sop_agent_ready": true,
  "hc_agent_ready": true,
  "sop_index_exists": true,
  "hc_index_exists": true,
  "env_loaded": true,
  "azure_endpoint": "https://your-resource.openai.azure.com/",
  "embedding_model": "text-embedding-ada-002",
  "chat_model": "gpt-4.1-mini"
}
```

**GET /**

Get API information and available endpoints.

**GET /docs**

Interactive Swagger UI documentation.

---

## 📁 Project Structure

```
biofarma-ai-assistant/
├── .env                      # Environment variables (not in repo)
├── .gitignore               # Git ignore file
├── README.md                # This file
├── requirements.txt         # Python dependencies
├── config.py                # Configuration settings
├── prompts.py               # System prompts for agents
├── agents.py                # Agent class implementations
├── ingest_unified.py        # Document ingestion script
├── api.py                   # FastAPI backend
├── app_final.py             # Streamlit frontend
├── data/
│   ├── sop_documents/       # SOP markdown files
│   │   ├── SOP-MFG-2024-018.md
│   │   ├── WI-QC-2024-042.md
│   │   └── QA-PROC-2024-025.md
│   ├── hc_documents/        # HR PDF/DOCX files
│   │   └── employee_manual.pdf
│   └── vectorstore/
│       ├── sop_faiss_index/ # SOP vector store
│       └── hc_faiss_index/  # HC vector store
└── uploads/
    └── hc/                  # Temporary HC uploads
```

---

## 👨‍💻 Development

### Running Tests
```bash
# Install dev dependencies
pip install pytest pytest-cov

# Run tests
pytest tests/ -v

# With coverage
pytest tests/ --cov=. --cov-report=html
```

### Code Quality
```bash
# Format code
black .

# Lint code
flake8 .

# Type checking
mypy .
```

### Adding New Agents

1. **Create Agent Class** in `agents.py`:
```python
class NewAgent(BaseAgent):
    def __init__(self):
        super().__init__("NEW")
        # Your initialization
```

2. **Add Prompts** in `prompts.py`:
```python
NEW_SYSTEM_PROMPT = """Your prompt here"""
NEW_RESPONSE_TEMPLATE = """Your template here"""
```

3. **Add Endpoints** in `api.py`:
```python
@app.post("/new/ask")
async def ask_new_question(question: Question):
    # Your endpoint logic
```

4. **Update UI** in `app_final.py`:
```python
AGENT_CONFIGS["New Agent"] = {
    "key": "new",
    # Your config
}
```

---

## 🐛 Troubleshooting

### Common Issues

#### 1. ImportError: cannot import name 'RetrievalQA'

**Solution:**
```bash
pip uninstall langchain langchain-openai langchain-community -y
pip cache purge
pip install -r requirements.txt
```

#### 2. FileNotFoundError: Vector store not found

**Solution:**
```bash
# For SOP
python ingest_unified.py sop

# For HC
python ingest_unified.py hc
# OR upload via web interface
```

#### 3. Connection refused (Backend API not running)

**Solution:**
```bash
# Make sure API is running
python api.py

# Check if port 8000 is available
netstat -an | grep 8000
```

#### 4. Azure OpenAI 401 Unauthorized

**Solution:**
- Verify API key in `.env` file
- Check endpoint URL (no trailing `/openai/deployments/...`)
- Ensure deployment names match exactly
- Verify API key hasn't expired

#### 5. Streamlit connection error

**Solution:**
```bash
# Make sure both servers are running
# Terminal 1
python api.py

# Terminal 2
streamlit run app_final.py
```

### Debug Mode

Enable verbose logging:

```python
# In api.py
import logging
logging.basicConfig(level=logging.DEBUG)
```

Check agent status:
```bash
curl http://localhost:8000/status | jq
```

---

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. **Fork the Repository**
2. **Create a Feature Branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit Your Changes**
   ```bash
   git commit -m 'Add amazing feature'
   ```
4. **Push to Branch**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open a Pull Request**

### Contribution Guidelines

- Follow PEP 8 style guide
- Add tests for new features
- Update documentation
- Keep commits atomic and meaningful
- Add docstrings to functions

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **Azure OpenAI** for powerful language models
- **LangChain** for RAG framework
- **FastAPI** for modern API development
- **Streamlit** for rapid UI prototyping
- **PT Bio Farma** for the use case and requirements

---

## 📞 Support

- **Documentation:** [Wiki](https://github.com/yourusername/biofarma-ai-assistant/wiki)
- **Issues:** [GitHub Issues](https://github.com/yourusername/biofarma-ai-assistant/issues)
- **Discussions:** [GitHub Discussions](https://github.com/yourusername/biofarma-ai-assistant/discussions)

---

## 🗺 Roadmap

- [ ] Add support for more document formats
- [ ] Implement conversation memory
- [ ] Add user authentication
- [ ] Multi-language support
- [ ] Advanced analytics dashboard
- [ ] Mobile app
- [ ] Integration with Microsoft Teams
- [ ] Batch document processing
- [ ] Fine-tuned models for specific domains

---

<div align="center">

**Built with ❤️ for PT Bio Farma**

⭐ Star this repo if you find it helpful!

</div>