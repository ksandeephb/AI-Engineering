# 🧾 Prompt Engineering

## 📌 Overview

Prompt engineering is the process of designing inputs (prompts) to guide Large Language Models (LLMs) to produce desired outputs.

It is one of the most effective ways to:
- Improve accuracy  
- Control output format  
- Reduce hallucination  
- Avoid unnecessary fine-tuning  

---

## 🧠 Why Prompt Engineering Matters

LLMs are highly sensitive to input phrasing.

Small changes in prompts can lead to:
- Better responses  
- Different reasoning paths  
- Improved consistency  

> Prompt engineering is often the fastest way to improve system performance.

---

## 🧩 Prompt Structure

A typical prompt consists of:

---

### 1. System Prompt

Defines:
- Role  
- Behavior  
- Constraints  

---

#### Example

```
"You are a medical assistant. Provide accurate and concise answers."
```

---

### 2. User Prompt

The actual query or task.

---

#### Example

```
"What is the normal glucose level?"
```

---

### 3. Context (Optional)

Additional information provided to the model.

---

#### Example

```
Context:
"Glucose normal range: 70–100 mg/dL"
```

---

### 4. Output Format Instructions

Defines structure of output.

---

#### Example

```
Return output in JSON format:
{
  "biomarker": "",
  "value": "",
  "status": ""
}
```

---

## 🎯 Basic Prompting Techniques

---

### 1. Zero-shot Prompting

No examples provided.

---

#### Example

```
Extract biomarkers from the following text:
"Glucose: 180 mg/dL"
```

---

### 2. Few-shot Prompting

Provide examples to guide the model.

---

#### Example

```
Example:
Input: "Glucose: 180 mg/dL"
Output: {"biomarker": "Glucose", "value": 180}

Now process:
"HbA1c: 8.2%"
```

---

### 3. Instruction-based Prompting

Explicit instructions for the task.

---

#### Example

```
Extract all biomarkers and return them as structured JSON.
```

---

## ⚖️ Prompt Design Principles

- Be clear and specific  
- Provide context when needed  
- Define output format  
- Avoid ambiguity  

---

## 💡 Key Insight

> Better prompts can outperform model upgrades in many cases.

