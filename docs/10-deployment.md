# 🚀 Deployment in GenAI Systems

## 📌 Overview

Deployment in GenAI involves making models and pipelines available in a scalable, secure, and production-ready environment.

Key goals:
- Reliability  
- Scalability  
- Low latency  
- Cost efficiency  

---

## 🧠 Deployment Architecture (High-Level)

```
Frontend (UI / Streamlit / Web App)
   ↓
API Layer (FastAPI / Backend)
   ↓
Orchestration Layer (LangChain / LangGraph)
   ↓
Core Components:
   - RAG Pipeline
   - LLM (Azure OpenAI / Others)
   - Agents / Tools
   ↓
Data Layer:
   - Vector DB
   - Storage
   ↓
Monitoring & Logging
```

---

## ☁️ Azure-Based Deployment Architecture

### Core Azure Services

---

### 1. Azure OpenAI Service

- Provides GPT models  
- Embeddings  
- Function calling  

📚 https://learn.microsoft.com/en-us/azure/ai-services/openai/  

---

### 2. Azure App Service / Azure Container Apps

- Hosts FastAPI backend  
- Handles API requests  

---

### 3. Azure Functions

- Serverless execution  
- Event-driven workflows  

---

### 4. Azure AI Search (Vector DB)

- Vector search + keyword search  
- Hybrid retrieval support  

📚 https://learn.microsoft.com/en-us/azure/search/  

---

### 5. Azure Blob Storage

- Stores documents (PDFs, images)  

---

### 6. Azure Cosmos DB / SQL

- Stores structured data  
- Metadata storage  

---

### 7. Azure Monitor & Application Insights

- Logging  
- Metrics  
- Observability  

---

## 🔄 Azure Deployment Flow

```
User → Frontend (Streamlit / Web App)
     → FastAPI (App Service / Container Apps)
     → Azure OpenAI (LLM)
     → Azure AI Search (Retrieval)
     → Response
```

---

## 🧩 Component Mapping (Your Use Case)

| Component | Azure Service |
|----------|-------------|
| LLM | Azure OpenAI |
| Embeddings | Azure OpenAI |
| Vector DB | Azure AI Search |
| Backend | Azure App Service |
| Storage | Azure Blob Storage |
| Monitoring | Azure Monitor |

---

## 💡 Key Insight

> A strong deployment architecture maps each GenAI component to a scalable cloud service while optimizing for cost, latency, and reliability.
>
> ## ⚙️ Backend Deployment (FastAPI on Azure)

### 📌 Option 1: Azure App Service (Simple)

#### Steps

1. Create FastAPI app  

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "GenAI API running"}
```

---

2. Create `requirements.txt`

```
fastapi
uvicorn
```

---

3. Deploy using Azure App Service

- Create App Service  
- Select Python runtime  
- Deploy via:
  - GitHub integration  
  - Zip deployment  

---

### 📌 Option 2: Azure Container Apps (Recommended)

#### Why?

- Better scalability  
- Container-based  
- More control  

---

## 🐳 Dockerization

### Dockerfile Example

```
FROM python:3.10

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]
```

---

### Build & Push

```
docker build -t genai-app .
docker push <azure-container-registry>/genai-app
```

---

### Deploy to Azure Container Apps

- Create Container App  
- Connect to Azure Container Registry  
- Deploy image  

---

## 🔄 CI/CD Pipeline

---

### Option 1: GitHub Actions

#### Example Workflow

```
name: Deploy FastAPI to Azure

on:
  push:
    branches: [main]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2

    - name: Build Docker image
      run: docker build -t genai-app .

    - name: Push to Azure
      run: docker push <acr>/genai-app
```

---

### Option 2: Azure DevOps

- Build pipeline  
- Release pipeline  
- Integrated with Azure services  

---

## 🔐 Secrets Management

### Use Azure Key Vault

Store:
- API keys  
- Database credentials  
- Secrets  

---

### Access Example

```
Azure Key Vault → Fetch secret → Use in app
```

---

## ⚙️ Environment Configuration

Use environment variables:

```
AZURE_OPENAI_KEY=xxx
AZURE_SEARCH_KEY=xxx
```

---

## ⚖️ Deployment Options Comparison

| Option | Pros | Cons |
|-------|------|------|
| App Service | Simple | Less flexible |
| Container Apps | Scalable | Slightly complex |
| AKS (Kubernetes) | Full control | High complexity |

---

## 💡 Key Insight

> Container-based deployment (Azure Container Apps) is the most flexible and scalable approach for GenAI systems.
