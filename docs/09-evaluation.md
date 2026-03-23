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

## 📊 LLM Evaluation Metrics

### 📌 Why Special Metrics Are Needed

LLM outputs are:
- Open-ended  
- Non-deterministic  
- Context-dependent  

Traditional accuracy alone is not sufficient.

---

## 🔤 BLEU (Bilingual Evaluation Understudy)

### 📌 Definition

Measures overlap between generated text and reference text using n-grams.

---

### Example

```
Reference: "Glucose level is high"
Generated: "Glucose is high"
```

High overlap → high BLEU score

---

### Pros

- Simple  
- Fast  

---

### Cons

- Does not capture meaning  
- Sensitive to wording differences  

---

## 📝 ROUGE (Recall-Oriented Understudy for Gisting Evaluation)

### 📌 Definition

Measures recall of overlapping text between generated and reference outputs.

---

### Variants

- ROUGE-1 → unigram overlap  
- ROUGE-2 → bigram overlap  
- ROUGE-L → longest common subsequence  

---

### Pros

- Good for summarization  
- Captures recall  

---

### Cons

- Ignores semantics  
- Can reward verbose outputs  

---

## 🧠 Semantic Metrics (Modern Approach)

### Examples

- BERTScore  
- Embedding similarity  

---

### Advantages

- Capture meaning, not just words  
- Better for LLM outputs  

---

## 🎯 Faithfulness

### 📌 Definition

Measures whether the generated answer is supported by provided context.

---

### Example

```
Context: "Glucose normal range is 70–100 mg/dL"

Answer: "Normal glucose is 70–100 mg/dL" ✅ (Faithful)
```

---

```
Answer: "Normal glucose is 50 mg/dL" ❌ (Hallucination)
```

---

## 🚨 Hallucination Detection

### 📌 Definition

Detects when LLM generates:
- Incorrect  
- Unsupported  
- Fabricated information  

---

### Techniques

- Compare with source context  
- Use retrieval grounding  
- LLM-based validation  

---

## 🤖 LLM-as-a-Judge

### 📌 Definition

Use an LLM to evaluate another LLM’s output.

---

### Example

```
Prompt:
"Evaluate if the answer is correct and grounded in context. Score from 1–5."
```

---

### Benefits

- Scalable  
- Flexible  
- Handles complex evaluation  

---

### Risks

- Bias  
- Inconsistency  

---

## ⚖️ Trade-offs

| Metric | Pros | Cons |
|-------|------|------|
| BLEU | Fast | Not semantic |
| ROUGE | Good for summarization | Limited meaning |
| Semantic | Accurate | More compute |
| LLM-as-judge | Flexible | Bias risk |

---

## 💡 Key Insight

> Traditional metrics measure text similarity, but modern evaluation focuses on meaning, faithfulness, and usefulness.

## 🔎 RAG Evaluation (End-to-End)

### 📌 Why RAG Evaluation is Different

RAG systems involve two components:
- Retrieval  
- Generation  

Failures can occur in either stage.

---

### Types of Errors

#### 1. Retrieval Error

- Relevant documents not retrieved  

---

#### 2. Ranking Error

- Relevant documents ranked too low  

---

#### 3. Generation Error

- Incorrect or hallucinated answer  

---

## 🧪 Evaluation Layers

---

### 1. Retrieval Evaluation

Metrics:
- Hit@K  
- MRR  
- NDCG  
- Precision@K  

---

### 2. Context Evaluation

Checks:
- Is retrieved context relevant?  
- Is it sufficient?  

---

### 3. Generation Evaluation

Metrics:
- Accuracy  
- Faithfulness  
- Relevance  

---

### 4. End-to-End Evaluation

```
Query → Retrieval → LLM → Answer
```

Evaluate:
- Final answer correctness  
- User satisfaction  

---

## 🧱 Evaluation Pipeline

### Example Workflow

```
Dataset:
Query → Ground Truth

Step 1: Retrieve documents  
Step 2: Evaluate retrieval metrics  
Step 3: Generate answer  
Step 4: Evaluate answer quality  
Step 5: Aggregate results  
```

---

## 📊 Production Monitoring

### 📌 What to Track

#### 1. System Metrics

- Latency  
- Error rates  
- Throughput  

---

#### 2. Model Metrics

- Token usage  
- Cost per request  

---

#### 3. Quality Metrics

- Accuracy  
- Hallucination rate  
- User feedback  

---

### Feedback Loop

```
User Feedback → Logging → Model Improvement
```

---

## 🏭 Real-world Evaluation Strategy

### 1. Offline Evaluation

- Benchmark datasets  
- Regression testing  

---

### 2. Online Evaluation

- A/B testing  
- User feedback  

---

### 3. Continuous Monitoring

- Track performance over time  
- Detect drift  

---

## ⚖️ Trade-offs

| Factor | Trade-off |
|-------|----------|
| Offline eval | Controlled vs unrealistic |
| Online eval | Real vs noisy |
| Automation | Scale vs accuracy |

---

## 🚨 Common Mistakes

- Evaluating only LLM, not retrieval  
- No ground truth dataset  
- Ignoring hallucination  
- No production monitoring  
- No feedback loop  

---

## 🧠 Advanced Techniques

### 1. Synthetic Data Generation

- Generate evaluation datasets using LLMs  

---

### 2. Human-in-the-Loop

- Manual review for critical systems  

---

### 3. Continuous Evaluation

- Automated pipelines for regular testing  

---

## 💡 Key Insight

> A GenAI system is only as good as its evaluation pipeline. Without evaluation, improvement is impossible.

---

## 📚 References

- https://www.evidentlyai.com/  
- https://cloud.google.com/architecture/gen-ai-rag  
- https://platform.openai.com/docs  
