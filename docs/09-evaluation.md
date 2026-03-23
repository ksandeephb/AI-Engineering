# 📊 Evaluation in GenAI Systems

## 📌 Overview

Evaluation in GenAI systems measures the quality, accuracy, and reliability of outputs.

It is essential for:
- Improving system performance  
- Comparing models and prompts  
- Ensuring production reliability  

---

## 🧠 Why Evaluation Matters

Without evaluation:
- You cannot measure improvement  
- Failures go unnoticed  
- Systems degrade over time  

> Evaluation is the backbone of reliable GenAI systems.

---

## 🧩 Types of Evaluation

---

### 1. Retrieval Evaluation

Measures how well the system retrieves relevant data.

---

#### Metrics

- Hit@K  
- MRR  
- NDCG  
- Precision@K  
- Recall@K  

---

### 2. Generation Evaluation

Measures quality of LLM outputs.

---

#### Metrics

- Accuracy  
- Relevance  
- Faithfulness  
- Coherence  

---

### 3. End-to-End Evaluation

Measures overall system performance.

---

#### Example

```
Query → Retrieval → LLM → Final Answer
```

Evaluate:
- Was answer correct?  
- Was it grounded?  
- Was it useful?  

---

## ⚖️ Offline vs Online Evaluation

---

### 🧪 Offline Evaluation

#### 📌 Definition

Evaluation using pre-defined datasets.

---

#### Characteristics

- Controlled environment  
- Repeatable  
- Used during development  

---

#### Example

```
Dataset:
Query → Expected Answer

Compare model output vs ground truth
```

---

### 🌐 Online Evaluation

#### 📌 Definition

Evaluation using real user interactions.

---

#### Characteristics

- Real-world data  
- Continuous feedback  
- Used in production  

---

#### Example

- User ratings  
- Click-through rates  
- Feedback loops  

---

## ⚖️ Comparison

| Type | Pros | Cons |
|------|------|------|
| Offline | Controlled | May not reflect real usage |
| Online | Real-world | Harder to control |

---

## 💡 Key Insight

> Both offline and online evaluation are required for a complete evaluation strategy.

