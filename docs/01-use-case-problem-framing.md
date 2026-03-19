# 🎯 Use Case & Problem Framing

## 📌 Overview
This section defines how to identify, evaluate, and frame Generative AI (GenAI) use cases using vendor-neutral, industry-standard architecture principles.

It aligns with:
- Cloud AI/ML best practices (AWS, Azure, GCP)
- LLM application frameworks (LangChain, LlamaIndex)
- Responsible AI guidelines

---

## 🧠 1. When to Use GenAI vs Traditional ML

### ✅ Use GenAI When:
- Working with **unstructured or semi-structured data**
  - Text, PDFs, emails, chat logs
- Tasks require:
  - Natural Language Understanding (NLU)
  - Natural Language Generation (NLG)
- Contextual reasoning is required
- Output can tolerate **probabilistic variation**

### ❌ Avoid GenAI When:
- Deterministic outputs are required
- Problem is structured/tabular prediction
- Strict explainability or auditability is required
- Ultra-low latency systems (<100ms hard constraints)

📚 References:
- https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/ml-lens.html  
- https://cloud.google.com/architecture/ai-ml  
- https://learn.microsoft.com/en-us/azure/architecture/ai-ml/  

> LLMs are probabilistic systems and should not replace deterministic systems where precision is critical.

---

## 🧩 2. Identifying Strong GenAI Use Cases

### Key Characteristics:
- High language or semantic complexity
- Rules-based systems are hard to scale
- High manual effort or cognitive load
- Acceptable tolerance for approximate outputs

### Examples:

| Strong Candidates | Weak Candidates |
|------------------|----------------|
| Document Q&A (RAG) | Financial transaction validation |
| Summarization | Real-time control systems |
| Information extraction | Deterministic workflows |
| Conversational assistants | Exact numerical computation |

📚 References:
- https://aws.amazon.com/generative-ai/use-cases/  
- https://cloud.google.com/use-cases/generative-ai  
- https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/use-cases  

---

## 🚫 3. Common Anti-Patterns

- Using GenAI in real-time safety-critical systems
- Expecting zero hallucination tolerance
- Replacing simple rule-based systems unnecessarily
- Ignoring latency and cost constraints
- Over-reliance on LLM reasoning without validation

📚 References:
- https://aws.amazon.com/machine-learning/responsible-ai/  
- https://learn.microsoft.com/en-us/azure/ai-services/responsible-use-of-ai-overview  

---

## 📏 4. Defining Success Metrics

### Core Evaluation Dimensions:

| Category | Metrics |
|----------|--------|
| Quality | Accuracy, factual consistency, hallucination rate |
| Latency | P50, P95, P99 response time |
| Cost | Cost per request / per token |
| User Experience | Task success rate, user satisfaction |
| Reliability | Error rate, fallback success |

📚 References:
- https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/metrics.html  
- https://cloud.google.com/vertex-ai/docs/evaluation/overview  

---

## 🧠 5. Use Case Decomposition Framework

### Step 1: Problem Classification
- Generation
- Retrieval (RAG)
- Extraction
- Classification
- Transformation (summarization, translation)

---

### Step 2: Input / Output Definition

input: Unstructured documents (PDF, text, images)
output: Structured data or generated response

---

### Step 3: Constraint Identification

- Latency requirements  
- Accuracy thresholds  
- Cost limits  
- Data privacy (PII, HIPAA, GDPR)  

---

### Step 4: Approach Selection

| Scenario | Recommended Approach |
|----------|--------------------|
| Dynamic knowledge | Retrieval-Augmented Generation (RAG) |
| Static domain knowledge | Fine-tuning |
| Structured extraction | Prompt + schema / NER |
| Multi-step workflows | Agent-based systems |

📚 References:
- https://cloud.google.com/architecture/gen-ai-rag  
- https://aws.amazon.com/what-is/retrieval-augmented-generation/  
- https://docs.llamaindex.ai/en/stable/  

---

## ⚖️ 6. Key Trade-offs

### RAG vs Fine-tuning

| RAG | Fine-tuning |
|-----|------------|
| Works with dynamic data | Best for static knowledge |
| Lower cost | Higher cost |
| Faster iteration | Slower iteration |
| Easier updates | Requires retraining |

📚 References:
- https://aws.amazon.com/blogs/machine-learning/choosing-between-rag-and-fine-tuning/  

---

### Prompt Engineering vs Model Modification

> Always start with prompt engineering and retrieval improvements before modifying the model.

📚 References:
- https://www.promptingguide.ai/  

---

## 🧱 7. Industry Design Patterns

### 1. Retrieval-first Architecture
Prefer retrieval-based grounding over model retraining.

---

### 2. Human-in-the-loop Systems

Used in:
- Healthcare  
- Finance  
- Legal  

---

### 3. Hybrid AI Systems

Combine:
- LLMs  
- Traditional ML  
- Rule-based validation  

📚 References:
- https://cloud.google.com/architecture/ai-ml  
- https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/  

---

## 🚨 8. Common Mistakes

- Poor use case selection  
- Lack of evaluation strategy  
- Ignoring data quality  
- Overusing agent-based systems  
- Not optimizing cost and latency early  

---

## 🎯 9. Sample Interview Scenario

### Problem:
Design a system to extract insights from medical reports.

### Approach:

1. Problem Type: Extraction + reasoning  
2. Input: Unstructured PDFs  
3. Pipeline:
   - OCR (if required)  
   - Structured extraction (NER or prompt-based)  
   - Context enrichment (RAG)  
4. Constraints:
   - High accuracy  
   - Compliance (PII, healthcare regulations)  
5. Metrics:
   - Extraction accuracy  
   - Hallucination rate  

---

## 💡 10. Key Insight

> The primary failure point in GenAI systems is not model capability, but incorrect problem framing and lack of evaluation strategy.

---

## 📚 References

- https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/  
- https://cloud.google.com/architecture/ai-ml  
- https://learn.microsoft.com/en-us/azure/architecture/ai-ml/  

- https://aws.amazon.com/what-is/retrieval-augmented-generation/  
- https://cloud.google.com/architecture/gen-ai-rag  

- https://www.promptingguide.ai/  

- https://docs.llamaindex.ai/  
- https://python.langchain.com/docs/  

```yaml
input: Unstructured documents (PDF, text, images)
output: Structured data or generated response
