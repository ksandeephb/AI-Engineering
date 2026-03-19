# 📊 Data & Context Handling

## 📌 Overview
Data and context handling are foundational to Generative AI (GenAI) systems. Unlike traditional ML systems, LLM-based applications rely heavily on:
- Context quality and relevance
- Retrieval strategies
- Input structuring and preprocessing

Effective data handling directly impacts:
- Accuracy
- Hallucination rates
- Latency and cost

---

## 🧠 1. Types of Data in GenAI Systems

### Structured Data
- Tables, relational databases, CSV files
- Easily queryable and schema-defined
- Typically used with traditional ML or hybrid systems

---

### Unstructured Data
- Documents (PDFs, Word)
- Emails, chat logs
- Web pages, knowledge bases

Requires:
- Parsing
- Chunking
- Embedding

---

### Semi-Structured Data
- JSON, XML, logs
- Partially organized but may require normalization

---

## 📂 2. Data Sources

### Internal Sources
- Enterprise knowledge bases
- Databases and document repositories
- CRM, ERP systems

### External Sources
- Public datasets
- APIs
- Web scraping pipelines

### Real-time Inputs
- User queries
- Uploaded files (PDFs, images)

📚 References:
- https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/  
- https://cloud.google.com/architecture/ai-ml  
- https://learn.microsoft.com/en-us/azure/architecture/ai-ml/  

---

## 🔄 3. Data Ingestion Pipeline

A typical GenAI data pipeline consists of:

1. Data Collection  
2. Data Cleaning  
3. Data Transformation  
4. Chunking  
5. Embedding Generation  
6. Storage  

---
### Example Pipeline (RAG System)

Documents → Parsing → Chunking → Embeddings → Vector DB → Retrieval → LLM


---

### Framework Support

- LangChain: Document loaders, text splitters  
  https://python.langchain.com/docs/integrations/document_loaders/  

- LlamaIndex: Data connectors and indexing  
  https://docs.llamaindex.ai/  

---

## 📄 4. Document Processing (PDFs, Images, Text)

### Challenges
- Scanned vs digital PDFs
- Complex layouts (tables, multi-column)
- Noisy or inconsistent formatting

---

### Solutions

#### OCR (Optical Character Recognition)
- Extract text from scanned documents

Examples:
- https://cloud.google.com/document-ai  
- https://aws.amazon.com/textract/  
- https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/  

---

#### Layout-Aware Parsing
- Preserve document structure (tables, headings)

---

#### Structured Extraction
- Named Entity Recognition (NER)
- Prompt-based extraction

---

## ✂️ 5. Chunking Strategy (Critical for RAG)

### Why Chunking?
LLMs have limited context windows → large documents must be split.

---

### Common Chunking Strategies

#### Fixed-size Chunking
- Split by token/character length
- Simple but may break semantic meaning

---

#### Semantic Chunking
- Split by sentences/paragraphs
- Preserves meaning and improves retrieval

---

#### Recursive Chunking
- Hierarchical splitting (section → paragraph → sentence)

---

### Key Parameters

- Chunk size (e.g., 500–1000 tokens)
- Overlap (e.g., 10–20%)

---

### Tools

- https://python.langchain.com/docs/concepts/text_splitters/  
- https://docs.llamaindex.ai/en/stable/  

---

## 🧠 6. Context Window Management

### Problem
LLMs have token limits (context windows).

---

### Techniques

- Chunking large inputs
- Retrieval (RAG)
- Summarization
- Sliding window approach

---

### Example
Large Document → Chunking → Retrieve Relevant Chunks → Pass to LLM


---

## 🔎 7. Retrieval Strategies

### Semantic Search
- Uses embeddings similarity
- Captures meaning, not exact match

---

### Keyword Search
- Exact term matching (BM25)

---

### Hybrid Search
- Combines semantic + keyword search
- Improves recall and precision

---

### Re-ranking
- Post-retrieval ranking using models

---

📚 References:
- https://cloud.google.com/architecture/gen-ai-rag  
- https://www.pinecone.io/learn/hybrid-search/  

---

## 🧬 8. Embeddings

### Definition
Embeddings are vector representations of text used for similarity comparison.

---

### Use Cases
- Semantic search
- Clustering
- Retrieval (RAG)

---

### Embedding Models

- https://platform.openai.com/docs/guides/embeddings  
- https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/embeddings  
- https://cloud.google.com/vertex-ai/docs/generative-ai/embeddings  

---

## 🗄️ 9. Storage Systems

### Vector Databases

- FAISS (local, open-source)
- Pinecone (managed)
- Weaviate
- Chroma

---

### Traditional Databases

- SQL (PostgreSQL, MySQL)
- NoSQL (MongoDB, DynamoDB)

---

### Hybrid Storage

- Metadata → SQL/NoSQL  
- Embeddings → Vector DB  

---

📚 References:
- https://www.pinecone.io/learn/vector-database/  
- https://weaviate.io/developers/weaviate  

---

## ⚖️ 10. Trade-offs

| Decision | Trade-off |
|---------|----------|
| Large chunks | Better context, higher token cost |
| Small chunks | Faster retrieval, context loss |
| Semantic chunking | Higher accuracy, more compute |
| Fixed chunking | Simpler, less accurate |
| Hybrid search | Better accuracy, higher complexity |

---

## 🧱 11. Design Patterns

### 1. Retrieval-Augmented Generation (RAG)

- Retrieve relevant context  
- Generate response using LLM  

---

### 2. Preprocessing Pipelines

- Clean → Normalize → Structure → Store  

---

### 3. Metadata Enrichment

- Add tags, categories, timestamps  
- Improves filtering and retrieval  

---

### 4. Multi-stage Retrieval

- Retrieve → Re-rank → Generate  

---

## 🚨 12. Common Mistakes

- Poor chunking strategy
- Ignoring document structure
- Using raw PDFs without preprocessing
- Not validating extracted data
- Overloading context window
- Using only semantic search without keyword fallback

---

## 💡 Key Insight

> In GenAI systems, data quality, chunking strategy, and retrieval design have a greater impact than model selection.

---

## 📚 References

- https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/  
- https://cloud.google.com/architecture/ai-ml  
- https://learn.microsoft.com/en-us/azure/architecture/ai-ml/  

- https://cloud.google.com/document-ai  
- https://aws.amazon.com/textract/  
- https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/  

- https://platform.openai.com/docs/guides/embeddings  
- https://cloud.google.com/vertex-ai/docs/generative-ai/embeddings  

- https://docs.llamaindex.ai/  
- https://python.langchain.com/docs/  

- https://www.pinecone.io/learn/vector-database/  

### Example Pipeline (RAG System)
