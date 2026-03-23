# 🎯 Fine-Tuning in LLMs

## 📌 Overview

Fine-tuning is the process of adapting a pre-trained model to a specific task or domain using additional training data.

---

## 🧠 Why Fine-Tuning is Needed

LLMs are general-purpose, but real-world systems require:

- Domain-specific knowledge  
- Consistent output format  
- Custom behavior  

---

> Fine-tuning specializes a model beyond prompting and RAG.

---

## ⚖️ Fine-Tuning vs Instruction Tuning

---

### Instruction Tuning

#### 📌 Definition

Training a model to follow instructions using a dataset of prompts and responses.

---

#### Example

```
Input: "Translate to French: Hello"
Output: "Bonjour"
```

---

#### Goal

- Improve instruction-following ability  

---

---

### Fine-Tuning (Task-Specific)

#### 📌 Definition

Training a model on domain-specific data for a particular task.

---

#### Example

```
Input: "Glucose: 180 mg/dL"
Output: {"biomarker": "Glucose", "value": 180}
```

---

#### Goal

- Improve performance on a specific task  

---

---

## 🧩 Types of Fine-Tuning

---

### 1. Supervised Fine-Tuning (SFT)

- Train on input-output pairs  
- Most common approach  

---

### 2. Instruction Fine-Tuning

- Improve general instruction following  

---

### 3. Preference Optimization (Advanced)

- RLHF (Reinforcement Learning from Human Feedback)  
- DPO (Direct Preference Optimization)  

---

## 🎯 When to Use Fine-Tuning

- Consistent structured output required  
- Domain-specific language (medical, legal)  
- High-volume repetitive tasks  

---

## 🚫 When NOT to Use Fine-Tuning

- Data changes frequently → use RAG  
- Small dataset → use prompting  
- Early-stage system → start with prompting  

---

## ⚖️ Fine-Tuning vs RAG vs Prompting

| Approach | Use Case |
|---------|---------|
| Prompting | Quick setup |
| RAG | Dynamic knowledge |
| Fine-tuning | Consistent behavior |

---

## 💡 Key Insight

> Start with prompting → add RAG → fine-tune only if necessary.

