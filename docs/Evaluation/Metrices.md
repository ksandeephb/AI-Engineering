# 📊 Evaluation Cheat Sheet — Overview & Core Metrics

## 🧠 Introduction

Evaluation is critical in modern AI systems such as:

- RAG (Retrieval-Augmented Generation)
- Summarization
- Translation
- Agent systems

Each system requires different evaluation strategies, but they share common foundations.

---

# 🧩 Types of Evaluation

## 1. Retrieval Evaluation (RAG)

Measures how well relevant documents are retrieved.

## 2. Generation Evaluation

Measures quality of generated text.

## 3. End-to-End Evaluation

Measures full pipeline performance.

## 4. Agent Evaluation

Measures reasoning, tool usage, and planning.

---

# 📏 Core Evaluation Metrics

## 🔹 Precision@K

Measures how many retrieved items are relevant.

```
Precision@K = (Relevant items in top K) / K
```

### Example

```python
def precision_at_k(relevant, retrieved, k):
    retrieved_k = retrieved[:k]
    return len(set(relevant) & set(retrieved_k)) / k
```

---

## 🔹 Recall@K

Measures how many relevant items are retrieved.

```
Recall@K = (Relevant items in top K) / (Total relevant items)
```

```python
def recall_at_k(relevant, retrieved, k):
    retrieved_k = retrieved[:k]
    return len(set(relevant) & set(retrieved_k)) / len(relevant)
```

---

## 🔹 F1 Score

Balances precision and recall.

```
F1 = 2 * (Precision * Recall) / (Precision + Recall)
```

```python
def f1_score(p, r):
    return 2 * (p * r) / (p + r + 1e-8)
```

---

## 🔹 Mean Reciprocal Rank (MRR)

Measures ranking quality.

```
MRR = 1 / rank of first relevant item
```

```python
def mrr(relevant, retrieved):
    for i, item in enumerate(retrieved):
        if item in relevant:
            return 1 / (i + 1)
    return 0
```

---

## 🔹 Normalized Discounted Cumulative Gain (nDCG)

Measures ranking quality with position importance.

```
nDCG = DCG / IDCG
```

```python
import numpy as np

def dcg(scores):
    return sum(score / np.log2(i + 2) for i, score in enumerate(scores))

def ndcg(scores):
    ideal = sorted(scores, reverse=True)
    return dcg(scores) / dcg(ideal)
```

---

# 📚 Libraries for Evaluation

## 🔹 1. Hugging Face Evaluate

👉 https://github.com/huggingface/evaluate

```python
import evaluate

metric = evaluate.load("accuracy")
metric.compute(predictions=[1,0,1], references=[1,1,1])
```

---

## 🔹 2. Scikit-learn

👉 https://scikit-learn.org/

```python
from sklearn.metrics import precision_score

precision_score([1,0,1], [1,1,1])
```

---

## 🔹 3. NumPy / Custom

Useful for custom metrics and experimentation.

---

# 🧠 Key Insight

Evaluation is not one-size-fits-all:

```
RAG → retrieval + generation
Summarization → semantic + compression
Translation → linguistic accuracy
Agents → reasoning + correctness
```

---

# 🏁 Summary

- Precision / Recall → retrieval quality  
- MRR / nDCG → ranking quality  
- F1 → balance metric  
- Libraries → automate evaluation  

---
