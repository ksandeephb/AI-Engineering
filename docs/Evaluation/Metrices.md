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


# 📊 RAG Evaluation — Metrics, Tools, and Code

## 🧠 Introduction

RAG (Retrieval-Augmented Generation) systems require evaluation across two layers:

1. Retrieval Quality → Are the right documents fetched?
2. Generation Quality → Is the answer correct and grounded?

A good RAG system must perform well in both.

---

# 🔍 RAG Evaluation Dimensions

## 1. Context Relevance

Measures whether retrieved documents are relevant to the query.

## 2. Faithfulness (Groundedness)

Checks if the generated answer is supported by retrieved context.

## 3. Answer Relevance

Measures how well the answer addresses the question.

## 4. Context Recall

Measures whether all necessary information was retrieved.

---

# 📏 Key RAG Metrics

## 🔹 Context Precision

How much of retrieved context is relevant.

```python
def context_precision(relevant_docs, retrieved_docs):
    return len(set(relevant_docs) & set(retrieved_docs)) / len(retrieved_docs)
```

---

## 🔹 Context Recall

How much relevant information is retrieved.

```python
def context_recall(relevant_docs, retrieved_docs):
    return len(set(relevant_docs) & set(retrieved_docs)) / len(relevant_docs)
```

---

## 🔹 Faithfulness Score

Checks if answer is grounded in context (LLM-based evaluation).

```python
def faithfulness_score(answer, context):
    prompt = f"Is the answer supported by the context?\nAnswer: {answer}\nContext: {context}"
    # pass to LLM and evaluate
```

---

## 🔹 Answer Relevance

Measures how well the answer matches the question.

```python
def answer_relevance(question, answer):
    prompt = f"Rate relevance of answer to question:\nQ: {question}\nA: {answer}"
```

---

# 🧰 RAG Evaluation Tools

---

## 🔵 1. RAGAS

👉 https://github.com/explodinggradients/ragas

### Features

- Context precision
- Faithfulness
- Answer relevance
- Fully open-source

---

### Example

```python
from ragas import evaluate
from datasets import Dataset

data = Dataset.from_dict({
    "question": ["What is AI?"],
    "answer": ["AI is artificial intelligence"],
    "contexts": [["AI is the simulation of human intelligence"]]
})

result = evaluate(data)
print(result)
```

---

## 🟢 2. TruLens

👉 https://github.com/truera/trulens

### Features

- Feedback-based evaluation
- Groundedness scoring
- Monitoring

---

### Example

```python
from trulens_eval import Tru

tru = Tru()

# wrap your RAG app
# evaluate groundedness
```

---

## 🟣 3. DeepEval

👉 https://github.com/confident-ai/deepeval

### Features

- Unit testing for LLM apps
- RAG evaluation metrics
- CI/CD integration

---

### Example

```python
from deepeval.metrics import FaithfulnessMetric
from deepeval.test_case import LLMTestCase

metric = FaithfulnessMetric()

test_case = LLMTestCase(
    input="What is AI?",
    actual_output="AI is intelligence",
    retrieval_context=["AI simulates human intelligence"]
)

score = metric.measure(test_case)
print(score)
```

---

## 🟡 4. LangChain Evaluation

👉 https://python.langchain.com/docs/guides/evaluation/

### Features

- Built-in evaluators
- LLM-based scoring

---

### Example

```python
from langchain.evaluation import load_evaluator

evaluator = load_evaluator("qa")

evaluator.evaluate_strings(
    prediction="AI is intelligence",
    reference="AI is artificial intelligence"
)
```

---

# ⚖️ Tool Comparison

| Tool | Type | Open Source | Strength |
|------|-----|------------|----------|
| RAGAS | Metric-based | Yes | Best for RAG metrics |
| TruLens | Feedback-based | Yes | Monitoring + eval |
| DeepEval | Testing | Yes | CI/CD ready |
| LangChain Eval | LLM-based | Yes | Easy integration |

---

# 🧠 Best Practice

Use combination:

```
RAGAS → metrics
DeepEval → testing
TruLens → monitoring
```

---

# 🏁 Summary

- RAG requires both retrieval + generation evaluation  
- Use specialized tools (not generic metrics)  
- Combine multiple evaluation frameworks for production  

---
