# ⚡ Quantization in LLMs

## 📌 Overview

Quantization is a technique to reduce the memory and compute requirements of models by lowering the precision of weights.

---

## 🧠 What is Quantization?

LLMs normally use:

```
32-bit floating point (FP32)
```

Quantization reduces precision to:

- 16-bit (FP16)
- 8-bit (INT8)
- 4-bit (INT4)

---

## 🎯 Why Quantization is Needed

LLMs are:
- Large (GBs in size)  
- Expensive to run  
- Slow in inference  

---

### Benefits

- Reduced memory usage  
- Faster inference  
- Lower cost  
- Enables running on smaller hardware  

---

## 📊 Example

```
FP32 model → 28 GB  
INT8 model → ~14 GB  
INT4 model → ~7 GB  
```

---

## 🧩 Types of Quantization

---

### 1. FP16 (Half Precision)

- Common in GPUs  
- Good balance  

---

### 2. INT8 Quantization

- Moderate compression  
- Minimal accuracy loss  

---

### 3. INT4 Quantization

- High compression  
- Slight accuracy drop  

---

### Comparison

| Type | Memory | Speed | Accuracy |
|------|-------|------|---------|
| FP32 | High | Slow | Best |
| FP16 | Medium | Faster | Very good |
| INT8 | Low | Fast | Slight drop |
| INT4 | Very low | Very fast | Moderate drop |

---

## ⚖️ Trade-offs

| Factor | Trade-off |
|-------|----------|
| Lower precision | Faster, cheaper |
| Accuracy | Slight degradation |

---

## 💡 Key Insight

> Quantization is the most effective way to reduce cost and improve inference speed without retraining the model.

# ⚡ Quantization in LLMs

## 📌 Overview

Quantization is a technique to reduce the memory and compute requirements of models by lowering the precision of weights.

---

## 🧠 What is Quantization?

LLMs normally use:

```
32-bit floating point (FP32)
```

Quantization reduces precision to:

- 16-bit (FP16)
- 8-bit (INT8)
- 4-bit (INT4)

---

## 🎯 Why Quantization is Needed

LLMs are:
- Large (GBs in size)  
- Expensive to run  
- Slow in inference  

---

### Benefits

- Reduced memory usage  
- Faster inference  
- Lower cost  
- Enables running on smaller hardware  

---

## 📊 Example

```
FP32 model → 28 GB  
INT8 model → ~14 GB  
INT4 model → ~7 GB  
```

---

## 🧩 Types of Quantization

---

### 1. FP16 (Half Precision)

- Common in GPUs  
- Good balance  

---

### 2. INT8 Quantization

- Moderate compression  
- Minimal accuracy loss  

---

### 3. INT4 Quantization

- High compression  
- Slight accuracy drop  

---

### Comparison

| Type | Memory | Speed | Accuracy |
|------|-------|------|---------|
| FP32 | High | Slow | Best |
| FP16 | Medium | Faster | Very good |
| INT8 | Low | Fast | Slight drop |
| INT4 | Very low | Very fast | Moderate drop |

---

## ⚖️ Trade-offs

| Factor | Trade-off |
|-------|----------|
| Lower precision | Faster, cheaper |
| Accuracy | Slight degradation |

---

## 💡 Key Insight

> Quantization is the most effective way to reduce cost and improve inference speed without retraining the model.

## 🔥 QLoRA (Quantized LoRA)

### 📌 What is QLoRA?

QLoRA combines:
- 4-bit quantization  
- LoRA fine-tuning  

---

### Why It Matters

- Fine-tune large models on limited hardware  
- Reduce memory usage significantly  
- Maintain good performance  

---

### Architecture

```
Base Model (4-bit quantized)
   + LoRA adapters (trainable)
   → Fine-tuned model
```

---

### Benefits

- Train large models on a single GPU  
- Lower memory footprint  
- Faster training  

---

## 🧪 QLoRA Example

```python
from transformers import BitsAndBytesConfig

quant_config = BitsAndBytesConfig(
    load_in_4bit=True,
    bnb_4bit_quant_type="nf4",
    bnb_4bit_compute_dtype="bfloat16"
)
```

---

```python
from peft import LoraConfig, get_peft_model

lora_config = LoraConfig(
    r=8,
    lora_alpha=16,
    target_modules=["q_proj", "v_proj"],
    task_type="CAUSAL_LM"
)

model = get_peft_model(model, lora_config)
```

---

## 📊 Performance Benchmarks (Typical)

| Setup | Memory | Speed | Accuracy |
|------|-------|------|---------|
| FP32 | High | Slow | Best |
| FP16 | Medium | Faster | Very good |
| INT8 | Low | Fast | Slight drop |
| INT4 + LoRA | Very low | Fast | Good |

---

## 🏭 Real-world Architecture Decisions

---

### Scenario 1: Enterprise (Azure OpenAI)

- No need for quantization  
- Managed infrastructure  
- Focus on API usage  

---

### Scenario 2: Self-hosted LLM

- Use 4-bit quantization  
- Combine with LoRA  
- Optimize for cost  

---

### Scenario 3: High-scale System

```
User → Router → 
   Small Model (fast path)
   Large Model (complex tasks)
```

---

## ⚖️ Trade-offs

| Decision | Trade-off |
|---------|----------|
| Quantization | Speed vs accuracy |
| QLoRA | Efficiency vs flexibility |
| Self-hosting | Cost vs complexity |

---

## 🚨 Common Mistakes

- Over-quantizing critical models  
- Ignoring accuracy drop  
- Using quantization unnecessarily (API models)  
- Not benchmarking performance  

---

## 🧠 Best Practices

- Use FP16 for high-accuracy tasks  
- Use INT4 for cost-sensitive workloads  
- Combine quantization with LoRA  
- Always benchmark before production  

---

## 💡 Key Insight

> QLoRA enables efficient fine-tuning of large models, making advanced LLM customization accessible even with limited hardware.

---

## 📚 References

- https://huggingface.co/docs  
- https://arxiv.org/abs/2305.14314 (QLoRA paper)  
- https://github.com/TimDettmers/bitsandbytes  
