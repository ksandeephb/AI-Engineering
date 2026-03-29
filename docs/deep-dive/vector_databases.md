# 📄 Page 1 — Vector Search Algorithms & Techniques

## 🧠 Why Algorithms Matter

In vector search systems, every query is transformed into a high-dimensional vector using an embedding model. The system must then identify the most similar vectors from a large dataset. The efficiency and accuracy of this process depend entirely on the underlying nearest neighbor search algorithm.

As datasets grow, exact comparison becomes computationally infeasible. This is why modern systems rely on Approximate Nearest Neighbor (ANN) algorithms, which trade a small amount of accuracy for significant improvements in speed and scalability.

---

## 🔍 Exact Search (Flat Index)

Exact search computes similarity between the query vector and every stored vector. This guarantees perfect accuracy because no approximation is used.

However, the computational cost grows linearly with the number of vectors, making it impractical for large-scale systems.

### Characteristics

- Time Complexity: O(N)
- Accuracy: 100%
- Speed: Slow for large datasets
- Use Case: Benchmarking, small datasets

---

## 🔵 IVF (Inverted File Index)

IVF reduces search space by clustering vectors into partitions using algorithms such as k-means.

### How it works

1. During indexing, vectors are grouped into clusters.
2. At query time, the system identifies the nearest cluster(s).
3. Search is performed only within those clusters.

### Key Parameters

- `nlist`: number of clusters
- `nprobe`: number of clusters to search

### Trade-offs

- Faster than exact search
- May miss relevant vectors if clusters are not searched
- Tunable accuracy vs speed

---

## 🟣 HNSW (Hierarchical Navigable Small World Graph)

HNSW is a graph-based ANN algorithm where vectors are nodes connected by similarity edges.

### How it works

- Vectors are organized into multiple layers
- Higher layers provide a coarse view
- Lower layers provide fine-grained search
- Query navigates from top layer to bottom layer

### Characteristics

- Time Complexity: ~log(N)
- Accuracy: Very high (near exact)
- Speed: Very fast
- Memory: High (due to graph connections)

### Why it is popular

HNSW provides one of the best trade-offs between speed and accuracy and is widely used in production systems.

---

## 🟡 Product Quantization (PQ)

Product Quantization compresses vectors to reduce memory usage.

### How it works

- Vectors are split into sub-vectors
- Each sub-vector is quantized separately
- Stored using compact representations

### Benefits

- Reduces memory footprint significantly
- Enables faster distance computation

### Trade-offs

- Loss of precision
- Slight reduction in accuracy

---

## 🟠 IVF + PQ (Combined Approach)

Many systems combine IVF with PQ to achieve both speed and memory efficiency.

### Workflow

1. Cluster vectors (IVF)
2. Compress vectors (PQ)
3. Search within selected clusters

This combination is commonly used in large-scale systems where memory is a constraint.

---

## ⚙️ Distance Metrics

All algorithms rely on distance/similarity functions:

- Cosine Similarity (most common for text)
- Euclidean Distance (L2)
- Inner Product (used in some embedding spaces)

Choice of metric affects retrieval quality.

---

## 🧠 Techniques Used by Each System

| Technique / Algorithm | FAISS | Chroma | Azure AI Search |
|---------------------|------|--------|----------------|
| Flat (Exact) | Yes | No | No |
| IVF | Yes | No | No |
| HNSW | Yes | Yes | Yes |
| Product Quantization | Yes | No | No |
| IVF + PQ | Yes | No | No |
| Hybrid Search (BM25 + Vector) | No | No | Yes |

---

## 🧠 Key Insight

Vector search is not just about one algorithm. It is about choosing the right combination of:

- indexing strategy
- compression technique
- search parameters

---

## 🏁 Summary

- FAISS provides multiple algorithm choices and deep control  
- Chroma uses HNSW internally with simplified configuration  
- Azure AI Search uses HNSW but enhances retrieval with hybrid search  

---





## 💡 Core Trade-off


# 📄 Page 2 — System-Level Deep Dive (FAISS vs Chroma vs Azure AI Search)

## 🧠 What Happens Inside a Vector System

Every vector system follows the same high-level pipeline:

```
Document → Chunking → Embedding → Indexing → Storage → Query → Retrieval
```

However, the difference between systems lies in:

- how indexing is done  
- how data is stored  
- how queries are executed  
- how much control is exposed  

---

# 🔵 FAISS — Full Control Engine

## 🧠 Overview

FAISS is a low-level vector search library that provides direct access to indexing algorithms such as Flat, IVF, HNSW, and Product Quantization.

It does not behave like a database. Instead, it acts as a computational engine that you integrate into your own system.

---

## ⚙️ Indexing Flow in FAISS

1. Convert documents into embeddings  
2. Choose an index type (e.g., IVF, HNSW)  
3. Train index (required for IVF/PQ)  
4. Add vectors to index  
5. Store index in memory or disk  

Example workflow:

```
Embeddings → Index Selection → Training → Add Vectors → Search
```

---

## 🔍 Query Execution in FAISS

- Query is converted into a vector  
- Search is performed using selected index  
- Returns nearest vectors based on similarity  

---

## ⚠️ Key Characteristics

- Full control over algorithm selection  
- Requires manual tuning  
- No built-in metadata filtering (must be handled separately)  
- No API layer (you must build one)  

---

## 🧠 When Using FAISS

You are responsible for:

- choosing indexing strategy  
- tuning parameters  
- managing storage  
- handling updates and deletes  

---

# 🟢 Chroma — Lightweight Vector Database

## 🧠 Overview

Chroma abstracts away algorithm complexity and provides a database-like interface. Internally, it uses HNSW for vector search and SQLite for metadata storage.

---

## ⚙️ Indexing Flow in Chroma

1. Documents are converted into embeddings  
2. Vectors are inserted into HNSW index  
3. Metadata is stored alongside vectors  
4. Data is persisted automatically (if enabled)  

```
Documents → Embeddings → HNSW Index → SQLite Storage
```

---

## 🔍 Query Execution in Chroma

- Query is converted into embedding  
- HNSW graph is traversed to find nearest neighbors  
- Metadata filtering can be applied  
- Results returned as structured objects  

---

## ⚠️ Key Characteristics

- Uses HNSW internally (no algorithm selection)  
- Built-in metadata storage and filtering  
- Easy to use and integrate  
- Limited control over indexing parameters  

---

## 🧠 Trade-off

Chroma prioritizes simplicity over flexibility. It works well out-of-the-box but does not allow deep optimization.

---

# ☁️ Azure AI Search — Managed Vector + Hybrid System

## 🧠 Overview

Azure AI Search is a fully managed service that provides vector search capabilities along with keyword-based retrieval.

It uses HNSW internally but combines it with traditional search techniques such as BM25.

---

## ⚙️ Indexing Flow in Azure AI Search

1. Documents are ingested via API  
2. Embeddings are generated (externally or integrated)  
3. Data is indexed into:  
   - vector index (HNSW)  
   - inverted index (BM25 for keyword search)  

```
Documents → Embeddings → Vector Index + Keyword Index → Cloud Storage
```

---

## 🔍 Query Execution in Azure AI Search

- Query is converted into embedding  
- Vector similarity search is performed  
- Keyword search (BM25) is executed  
- Results are combined and ranked  

---

## ⚠️ Key Characteristics

- Fully managed (no infrastructure handling)  
- Hybrid search (vector + keyword)  
- Advanced filtering and ranking  
- No access to algorithm-level tuning  

---

## 🧠 Hybrid Retrieval Explained

Unlike FAISS and Chroma, Azure AI Search combines:

- semantic similarity (vector search)  
- keyword matching (BM25)  

This ensures:

- better handling of rare terms  
- improved precision for structured queries  
- higher real-world relevance  

---

# ⚖️ System-Level Comparison

| Feature | FAISS | Chroma | Azure AI Search |
|--------|------|--------|----------------|
| Type | Engine | Local DB | Managed Service |
| Indexing control | Full | Limited | None |
| Algorithm choice | Yes | No | No |
| Metadata storage | External | Built-in | Built-in |
| Filtering | Manual | Basic | Advanced |
| Hybrid search | No | No | Yes |
| API layer | No | Local | Cloud API |
| Scaling | Manual | Limited | Automatic |

---

# 🧠 Key Insight

The difference between these systems is not just algorithms but **who controls the system**:

- FAISS → developer controls everything  
- Chroma → system manages complexity locally  
- Azure → cloud manages everything  

---

# 🏁 Summary

- FAISS provides maximum flexibility and control  
- Chroma provides simplicity with reasonable performance  
- Azure AI Search provides scalability and hybrid retrieval  

---

## 💡 Mental Model

```
FAISS  → Engine  
Chroma → Lightweight DB  
Azure  → Full Search Platform  
```
