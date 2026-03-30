# 📊 Summarization & Translation Evaluation — Metrics, Tools, and Code

## 🧠 Introduction

Summarization and translation tasks focus on **text quality, meaning preservation, and linguistic accuracy**.

Unlike RAG, these tasks do not involve retrieval. Instead, evaluation focuses on:

- correctness of meaning  
- fluency and readability  
- faithfulness to source  
- compression (for summarization)  

---

# 🧩 Evaluation Dimensions

## 🔹 Summarization

- Content coverage → Did we capture key points?
- Faithfulness → Is summary factually correct?
- Compression → Is it concise?

## 🔹 Translation

- Semantic equivalence → Same meaning?
- Fluency → Natural language?
- Adequacy → Completeness?

---

# 📏 Key Metrics

---

## 🔵 ROUGE (Summarization)

👉 https://huggingface.co/spaces/evaluate-metric/rouge

Measures overlap between generated summary and reference.

### Types

- ROUGE-1 → unigram overlap  
- ROUGE-2 → bigram overlap  
- ROUGE-L → longest common subsequence  

---

### Example

```python
import evaluate

rouge = evaluate.load("rouge")

results = rouge.compute(
    predictions=["AI is transforming industries"],
    references=["Artificial intelligence is changing industries"]
)

print(results)
```

---

## 🟢 BLEU (Translation)

👉 https://huggingface.co/spaces/evaluate-metric/bleu

Measures n-gram overlap between translation and reference.

---

### Example

```python
import evaluate

bleu = evaluate.load("bleu")

results = bleu.compute(
    predictions=[["the cat is on the mat"]],
    references=[[["the cat is on the mat"]]]
)

print(results)
```

---

## 🟣 METEOR

Measures alignment using synonyms and stemming.

👉 https://www.nltk.org/api/nltk.translate.meteor_score.html

---

### Example

```python
from nltk.translate.meteor_score import meteor_score

score = meteor_score(
    ["the cat is on the mat"],
    "the cat sits on the mat"
)

print(score)
```

---

## 🟡 BERTScore (Semantic Similarity)

👉 https://github.com/Tiiiger/bert_score

Uses embeddings to compare meaning instead of exact words.

---

### Example

```python
from bert_score import score

P, R, F1 = score(
    ["AI is powerful"],
    ["Artificial intelligence is powerful"],
    lang="en"
)

print(F1)
```

---

## 🔴 COMET (Advanced Translation Metric)

👉 https://github.com/Unbabel/COMET

Uses neural models trained on human judgments.

---

### Example

```python
from comet import download_model, load_from_checkpoint

model_path = download_model("Unbabel/wmt22-comet-da")
model = load_from_checkpoint(model_path)

data = [{
    "src": "AI is powerful",
    "mt": "AI is powerful",
    "ref": "Artificial intelligence is powerful"
}]

score = model.predict(data)
print(score)
```

---

# ⚖️ Metric Comparison

| Metric | Type | Use Case | Limitation |
|-------|-----|----------|-----------|
| ROUGE | Overlap | Summarization | ignores semantics |
| BLEU | Overlap | Translation | strict matching |
| METEOR | Linguistic | Translation | slower |
| BERTScore | Semantic | Both | heavier compute |
| COMET | Neural | Translation | requires model |

---

# 🧠 Key Insight

Traditional metrics (BLEU, ROUGE):

- rely on word overlap  
- fail on paraphrasing  

Modern metrics (BERTScore, COMET):

- capture semantic meaning  
- align better with human judgment  

---

# 🧰 Best Practice

Combine metrics:

```
ROUGE / BLEU → baseline
BERTScore → semantic check
COMET → production-grade evaluation
```

---

# 🏁 Summary

- Summarization → ROUGE + BERTScore  
- Translation → BLEU + COMET  
- Semantic metrics outperform lexical ones  

---
