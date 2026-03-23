# 🔎 Retrieval-Augmented Generation (RAG)

## 📌 Overview

Retrieval-Augmented Generation (RAG) is an architecture that combines:

- Information retrieval (search)
- Large Language Models (generation)

It allows LLMs to:
- Access external knowledge  
- Reduce hallucination  
- Provide context-aware responses  

---

## 🧠 Why RAG is Needed

### Problem with LLMs

LLMs:
- Are trained on static data  
- Do not have real-time knowledge  
- Can hallucinate  

---

### Solution: RAG

Instead of relying only on model memory:

```
Query → Retrieve relevant data → Provide to LLM → Generate answer
```

---

## 🎯 Benefits of RAG

- Reduces hallucination  
- Enables real-time knowledge  
- Improves accuracy  
- Avoids expensive fine-tuning  

---

## ⚙️ High-Level Architecture

```
User Query
   ↓
Retriever (Vector DB / Search)
   ↓
Relevant Documents (Top-K)
   ↓
LLM (Generation)
   ↓
Final Answer
```

---

## 🧩 Components of RAG

### 1. Data Ingestion
- Documents (PDFs, text, etc.)
- Chunking
- Embeddings

---

### 2. Retriever
- Vector search  
- Keyword search  
- Hybrid search  

---

### 3. Generator (LLM)
- Uses retrieved context  
- Produces final response  

---

### 4. Orchestration Layer
- Controls flow (LangChain / LangGraph)

---

📚 References

- https://cloud.google.com/architecture/gen-ai-rag  
- https://aws.amazon.com/what-is/retrieval-augmented-generation/  
- https://python.langchain.com/docs/

## 🧬 Embeddings in RAG

### 📌 What are Embeddings?

Embeddings are vector representations of text that capture semantic meaning.

---

### Why Embeddings are Used

Instead of keyword matching:

```
Query: "high blood sugar"
```

Embedding search can match:

```
"glucose levels are elevated"
```

---

### Workflow

```
Text → Embedding Model → Vector Representation → Store in Vector DB
```

---

### Query Flow

```
User Query → Embedding → Similarity Search → Top-K Results
```

---

### Embedding Models

- OpenAI Embeddings  
  https://platform.openai.com/docs/guides/embeddings  

- Google Vertex AI Embeddings  
  https://cloud.google.com/vertex-ai/docs/generative-ai/embeddings  

- Azure OpenAI Embeddings  
  https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/embeddings  

---

## 🗄️ Vector Databases

### 📌 What is a Vector DB?

A vector database stores embeddings and enables similarity search.

---

### Common Vector Databases

- FAISS (local, open-source)  
- Pinecone (managed service)  
- Weaviate  
- Chroma  

---

### Functionality

- Store vectors  
- Perform nearest neighbor search  
- Retrieve top-K similar results  

---

### Similarity Metrics

- Cosine similarity  
- Euclidean distance  
- Dot product  

---

📚 References

- https://www.pinecone.io/learn/vector-database/  
- https://weaviate.io/developers/weaviate  

---

## 🔎 Retrieval Strategies

---

### 1. Semantic Search

#### Description
- Uses embeddings similarity  
- Captures meaning, not exact match  

---

#### Example

```
Query: "high glucose"

Matches:
"elevated blood sugar"
```

---

#### Pros
- Handles synonyms  
- Context-aware  

---

#### Cons
- May miss exact keyword matches  

---

### 2. Keyword Search

#### Description
- Matches exact terms (e.g., BM25)

---

#### Example

```
Query: "glucose"

Matches only documents containing "glucose"
```

---

#### Pros
- Precise  
- Fast  

---

#### Cons
- Misses semantic meaning  

---

### 3. Hybrid Search (Best Practice)

#### Description
Combines:
- Semantic search  
- Keyword search  

---

#### Example

```
Final Score = α × semantic_score + β × keyword_score
```

---

#### Pros
- Best accuracy  
- Combines precision + recall  

---

#### Cons
- More complex  
- Requires tuning  

---

📚 References

- https://www.pinecone.io/learn/hybrid-search/  
- https://cloud.google.com/architecture/gen-ai-rag  

---

## ⚖️ Trade-offs

| Strategy | Pros | Cons |
|---------|------|------|
| Semantic | Context-aware | Misses exact terms |
| Keyword | Precise | Misses meaning |
| Hybrid | Best overall | Complex |

---

## 💡 Key Insight

> Retrieval quality (embeddings + search strategy) has a greater impact on system performance than the LLM itself.

## 🔄 End-to-End RAG Pipeline

### 📌 Full Flow

```
Documents
  → Parsing / OCR
  → Chunking
  → Embeddings
  → Vector DB Storage

User Query
  → Query Embedding
  → Retrieval (Top-K)
  → Re-ranking
  → Context Injection
  → LLM Generation
  → Final Answer
```

---

## 🎯 Retrieval → Re-ranking → Generation

### Why Retrieval Alone is Not Enough

Initial retrieval may:
- Include irrelevant chunks  
- Miss the most important context  
- Rank results incorrectly  

---

## 🔁 Re-ranking

### 📌 What is Re-ranking?

Re-ranking reorders retrieved results using a more powerful model.

---

### Workflow

```
Top-K Retrieved Documents
   → Re-ranker Model
   → Sorted by relevance
   → Top-N passed to LLM
```

---

### Types of Re-ranking

#### 1. Cross-Encoder Models
- Evaluate query + document together  
- High accuracy  

---

#### 2. LLM-based Re-ranking
- Use LLM to score relevance  

---

#### 3. Heuristic Re-ranking
- Based on metadata or rules  

---

### Benefits

- Improves ranking quality  
- Reduces noise  
- Boosts final answer accuracy  

---

📚 References

- https://www.pinecone.io/learn/re-ranking/  

---

## 📏 RAG Evaluation

### 📌 Why Evaluation is Critical

- Retrieval errors → wrong answers  
- LLM errors → hallucination  

---

### Evaluation Layers

#### 1. Retrieval Evaluation

- Hit@K  
- MRR  
- NDCG  
- Precision@K  

---

#### 2. Generation Evaluation

- Answer accuracy  
- Faithfulness  
- Relevance  

---

### Combined Evaluation

```
Good Retrieval + Good Generation → High Quality Output
```

---

## 🏭 Production Architecture

### Typical Architecture

```
Frontend
  ↓
API Layer (FastAPI / Backend)
  ↓
Orchestration (LangChain / LangGraph)
  ↓
Retriever (Vector DB + Hybrid Search)
  ↓
Re-ranker
  ↓
LLM (Generation)
  ↓
Response
```

---

### Supporting Components

- Cache layer (Redis)  
- Logging & monitoring  
- Feedback loop  

---

## ⚖️ Design Trade-offs

| Component | Trade-off |
|----------|----------|
| Top-K retrieval | More context vs higher cost |
| Re-ranking | Better accuracy vs latency |
| Large context | Better answers vs cost |
| Hybrid search | Accuracy vs complexity |

---

## 🚨 Common Mistakes

- Poor chunking strategy  
- No re-ranking  
- Using only semantic search  
- Passing too much context to LLM  
- No evaluation pipeline  
- Ignoring latency and cost  

---

## 🧠 Advanced Patterns

### 1. Multi-stage Retrieval

```
Initial Retrieval → Re-ranking → Final Selection
```

---

### 2. Query Expansion

- Expand user query for better retrieval  

---

### 3. Metadata Filtering

- Filter by:
  - Document type  
  - Date  
  - Source  

---

### 4. Conversational RAG

- Maintain chat history  
- Use previous context  

---

## 💡 Key Insight

> In RAG systems, retrieval quality + ranking strategy matter more than the LLM itself.

---

## 📚 References

- https://cloud.google.com/architecture/gen-ai-rag  
- https://aws.amazon.com/what-is/retrieval-augmented-generation/  
- https://python.langchain.com/docs/  
- https://www.pinecone.io/learn/  

