# 📏 Retrieval Metrics Deep Dive

## 📌 Overview

Retrieval metrics evaluate how effectively a system retrieves relevant documents or passages for a given query.

They are critical in:
- Search systems  
- Recommendation systems  
- Retrieval-Augmented Generation (RAG)

---

## 🧠 Why Retrieval Metrics Matter

In GenAI systems:

- Poor retrieval → hallucination  
- Missing context → incomplete answers  
- Wrong ranking → degraded quality  

> Retrieval quality directly impacts LLM output quality.

---

## 🧩 Types of Retrieval Metrics

### 1. Rank-aware Metrics
These consider **position of results**:
- Mean Reciprocal Rank (MRR)
- Normalized Discounted Cumulative Gain (NDCG)

---

### 2. Rank-unaware Metrics
These consider only **presence of relevant results**:
- Precision@K
- Recall@K

---

📚 Reference:  
Rank-aware metrics consider both relevance and order, while others only count relevant items. :contentReference[oaicite:0]{index=0}  

---

## 🎯 Mean Reciprocal Rank (MRR)

### 📌 Definition

MRR measures how quickly the **first relevant result** appears in the ranking.

---

### Formula

\[
MRR = \frac{1}{|Q|} \sum_{i=1}^{|Q|} \frac{1}{rank_i}
\]

Where:
- \( rank_i \) = position of first relevant result
- \( Q \) = number of queries

---

### Intuition

- If correct answer is at rank 1 → score = 1  
- Rank 2 → score = 0.5  
- Rank 5 → score = 0.2  

---

### Example

```
Query: "What is HbA1c?"

Retrieved Results:
1. "HbA1c definition" ✅
2. "Glucose explanation"
3. "Cholesterol levels"

Reciprocal Rank = 1/1 = 1.0
```

---

```
Query: "Normal glucose level?"

Retrieved Results:
1. "Cholesterol"
2. "Blood pressure"
3. "Glucose levels" ✅

Reciprocal Rank = 1/3 ≈ 0.33
```

---

### Final MRR

```
MRR = (1 + 0.33) / 2 = 0.665
```

---

### When to Use MRR

- Question-answering systems  
- Search systems with **single correct answer**  
- Chatbots  

---

### Key Insight

- Focuses ONLY on first relevant result  
- Ignores rest of ranking  

📚 References:  
- MRR evaluates position of first relevant item :contentReference[oaicite:1]{index=1}  
- Reciprocal rank is inverse of position :contentReference[oaicite:2]{index=2}  

---

### Limitations

- Ignores multiple relevant results  
- Not suitable when multiple answers matter  

---

## 📊 Discounted Cumulative Gain (DCG)

### 📌 Definition

DCG measures the usefulness of a document based on:
- Its **relevance score**
- Its **position in the ranking**

Higher-ranked relevant items contribute more than lower-ranked ones.

---

### Formula

\[
DCG_k = \sum_{i=1}^{k} \frac{rel_i}{\log_2(i + 1)}
\]

Where:
- \( rel_i \) = relevance score at position \( i \)
- \( i \) = rank position
- \( k \) = cutoff rank

---

### Intuition

- Rank 1 → highest importance  
- Rank 2 → slightly less  
- Rank 10 → much less  

Logarithmic discount reduces importance of lower-ranked results.

---

### Example

```
Query: "Diabetes markers"

Results:
Rank 1 → Relevant (rel = 3)
Rank 2 → Relevant (rel = 2)
Rank 3 → Not relevant (rel = 0)
```

---

### DCG Calculation

```
DCG =
3 / log2(1+1) +
2 / log2(2+1) +
0 / log2(3+1)

= 3/1 + 2/1.58 + 0
≈ 3 + 1.26
≈ 4.26
```

---

## 📈 Ideal DCG (IDCG)

### 📌 Definition

IDCG is the **maximum possible DCG** for a perfect ranking.

---

### Example (Perfect Order)

```
Rank 1 → rel = 3
Rank 2 → rel = 2
Rank 3 → rel = 0
```

---

```
IDCG ≈ 4.26
```

---

## 📊 Normalized Discounted Cumulative Gain (NDCG)

### 📌 Definition

NDCG normalizes DCG by dividing by the ideal DCG.

---

### Formula

\[
NDCG_k = \frac{DCG_k}{IDCG_k}
\]

---

### Range

- 0 → worst ranking  
- 1 → perfect ranking  

---

### Example

```
DCG = 3.5
IDCG = 4.26

NDCG = 3.5 / 4.26 ≈ 0.82
```

---

### Intuition

- Measures **ranking quality**
- Rewards correct ordering
- Penalizes relevant results appearing lower

---

## 🎯 When to Use NDCG

- RAG systems (most important)
- Search engines
- Recommendation systems
- When multiple relevant results exist

---

## ⚖️ Why NDCG is Powerful

| Feature | Benefit |
|--------|--------|
| Rank-aware | Considers position |
| Multi-relevance | Handles graded relevance |
| Normalized | Comparable across queries |

---

## 🚨 Limitations

- Requires relevance scoring (not binary)
- Slightly complex to compute
- Depends on quality of ground truth labels

---

## 💡 Key Insight

> NDCG is the most reliable metric for evaluating retrieval quality when multiple relevant documents exist.

---

## 📚 References

- https://www.geeksforgeeks.org/machine-learning/normalized-discounted-cumulative-gain-multilabel-ranking-metrics-ml/  
- https://www.evidentlyai.com/ranking-metrics/ndcg-metric  

## 📊 Precision@K

### 📌 Definition

Precision@K measures how many of the top-K retrieved results are relevant.

---

### Formula

\[
Precision@K = \frac{\text{Number of relevant items in top K}}{K}
\]

---

### Example

```
Top 5 results:
[Relevant, Not Relevant, Relevant, Relevant, Not Relevant]

Precision@5 = 3 / 5 = 0.6
```

---

### When to Use

- When quality of top results matters  
- Search systems  
- RAG (top-k retrieval)  

---

## 📊 Recall@K

### 📌 Definition

Recall@K measures how many of the total relevant items are retrieved in top-K results.

---

### Formula

\[
Recall@K = \frac{\text{Relevant items retrieved}}{\text{Total relevant items}}
\]

---

### Example

```
Total relevant documents = 4

Retrieved top 5:
3 relevant

Recall@5 = 3 / 4 = 0.75
```

---

### Key Insight

- Precision → quality  
- Recall → coverage  

---

## 🎯 Keyword Coverage

### 📌 Definition

Keyword coverage measures whether retrieved documents contain important query terms.

---

### Example

```
Query: "high glucose level"

Retrieved document:
"Glucose levels are elevated"

Coverage:
- "glucose" → present
- "high" → implied
- "level" → present

High keyword coverage
```

---

### Use Cases

- Simple retrieval validation  
- Debugging retrieval systems  
- Baseline metric  

---

### Limitations

- Ignores semantic meaning  
- Cannot capture synonyms or context  

---

## 🎯 Hit Rate (Hit@K)

### 📌 Definition

Measures whether at least one relevant result appears in top-K.

---

### Formula

```
Hit@K = 1 if at least one relevant result exists, else 0
```

---

### Example

```
Top 5 results:
[Not Relevant, Not Relevant, Relevant, Not Relevant, Not Relevant]

Hit@5 = 1
```

---

### When to Use

- QA systems  
- Chatbots  
- First-result importance  

---

## ⚖️ Comparing Metrics

| Metric | Measures | Use Case |
|-------|--------|---------|
| MRR | First relevant result | QA systems |
| NDCG | Ranking quality | RAG, search |
| Precision@K | Top-K accuracy | Search |
| Recall@K | Coverage | Large datasets |
| Hit@K | Presence of answer | QA systems |
| Keyword Coverage | Term matching | Debugging |

---

## 🧠 How Metrics Work Together (Real Systems)

### Typical RAG Evaluation Stack

- Hit@K → Did we retrieve anything useful?  
- MRR → How early did we retrieve it?  
- NDCG → Was ranking correct?  
- Precision@K → Are top results good?  
- Recall@K → Did we miss anything?  

---

### Example Evaluation Pipeline

```
Query → Retrieve top-K documents
       → Compute metrics:
           - Hit@K
           - MRR
           - NDCG
           - Precision@K
           - Recall@K
```

---

## 🏭 Industry Practice

In production systems:

- Use multiple metrics together  
- Monitor trends over time  
- Combine with human evaluation  
- Use offline + online evaluation  

---

## 🚨 Common Mistakes

- Using only one metric  
- Ignoring ranking order  
- Not defining ground truth properly  
- Over-optimizing for precision but hurting recall  
- Ignoring semantic relevance  

---

## 💡 Key Insight

> No single metric is sufficient. A combination of ranking, accuracy, and coverage metrics is required to evaluate retrieval systems effectively.

---

## 📚 References

- https://www.evidentlyai.com/ranking-metrics/ndcg-metric  
- https://www.geeksforgeeks.org/machine-learning/normalized-discounted-cumulative-gain-multilabel-ranking-metrics-ml/  
- https://www.evidentlyai.com/ranking-metrics/mean-reciprocal-rank-mrr  
- Not suitable when multiple answers matter  

---
