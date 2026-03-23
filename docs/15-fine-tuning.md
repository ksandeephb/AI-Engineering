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

## 🧪 Dataset Preparation

### 📌 Format (Instruction Style)

Fine-tuning data is usually in JSON format:

---

### Example

```json
[
  {
    "instruction": "Extract biomarker information",
    "input": "Glucose: 180 mg/dL",
    "output": "{\"biomarker\": \"Glucose\", \"value\": 180}"
  }
]
```

---

### Alternative (Chat Format)

```json
{
  "messages": [
    {"role": "user", "content": "Glucose: 180 mg/dL"},
    {"role": "assistant", "content": "{\"biomarker\": \"Glucose\", \"value\": 180}"}
  ]
}
```

---

## ⚙️ Fine-Tuning with Hugging Face + LoRA

---

### 📌 Why LoRA?

- Reduces training cost  
- Requires less memory  
- Faster training  

---

## 📦 Install Dependencies

```bash
pip install transformers datasets peft accelerate bitsandbytes
```

---

## 🧠 Model Loading (4-bit Quantization + LoRA)

```python
from transformers import AutoModelForCausalLM, AutoTokenizer
from peft import LoraConfig, get_peft_model

model_name = "meta-llama/Llama-2-7b-hf"

tokenizer = AutoTokenizer.from_pretrained(model_name)

model = AutoModelForCausalLM.from_pretrained(
    model_name,
    load_in_4bit=True,
    device_map="auto"
)
```

---

## ⚙️ LoRA Configuration

```python
lora_config = LoraConfig(
    r=8,
    lora_alpha=16,
    target_modules=["q_proj", "v_proj"],
    lora_dropout=0.05,
    bias="none",
    task_type="CAUSAL_LM"
)

model = get_peft_model(model, lora_config)
```

---

## 📊 Dataset Loading

```python
from datasets import load_dataset

dataset = load_dataset("json", data_files="data.json")
```

---

## 🏋️ Training Setup

```python
from transformers import TrainingArguments, Trainer

training_args = TrainingArguments(
    output_dir="./results",
    per_device_train_batch_size=2,
    num_train_epochs=3,
    logging_steps=10,
    save_steps=100
)

trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=dataset["train"]
)

trainer.train()
```

---

## 💾 Save Model

```python
model.save_pretrained("./fine-tuned-model")
tokenizer.save_pretrained("./fine-tuned-model")
```

---

## 🚀 Inference

```python
from transformers import pipeline

pipe = pipeline("text-generation", model="./fine-tuned-model")

response = pipe("Glucose: 180 mg/dL")
print(response)
```

---

## ⚖️ Trade-offs

| Factor | Trade-off |
|-------|----------|
| LoRA | Efficient but limited capacity |
| Full fine-tuning | Better performance but expensive |
| Quantization | Lower memory vs slight accuracy loss |

---

## 💡 Key Insight

> LoRA + quantization is the most practical way to fine-tune LLMs in real-world systems.

## 📊 Evaluating Fine-Tuned Models

### 📌 Why Evaluation is Critical

Fine-tuning can:
- Improve performance  
- Or degrade general capability  

---

### Evaluation Metrics

---

#### 1. Task Accuracy

- Compare output with ground truth  

---

#### 2. Format Consistency

- Check structured output (JSON correctness)  

---

#### 3. Generalization

- Test on unseen data  

---

### Example

```python
def evaluate(model, dataset):
    correct = 0

    for sample in dataset:
        output = model(sample["input"])

        if output == sample["output"]:
            correct += 1

    return correct / len(dataset)
```

---

## 🚨 When Fine-Tuning Fails

---

### 1. Overfitting

- Model memorizes training data  
- Poor performance on new data  

---

### 2. Data Quality Issues

- Noisy or inconsistent dataset  

---

### 3. Insufficient Data

- Too few examples  

---

### 4. Wrong Use Case

- Dynamic knowledge → should use RAG  

---

## ☁️ Azure OpenAI Fine-Tuning

---

### 📌 When to Use

- Enterprise scenarios  
- Managed infrastructure  
- Compliance requirements  

---

### Workflow

```
Prepare dataset → Upload → Train → Deploy → Use endpoint
```

---

### Example (Conceptual)

```python
from openai import AzureOpenAI

client = AzureOpenAI(
    api_key="API_KEY",
    azure_endpoint="ENDPOINT",
    api_version="2024-02-01"
)

# Pseudo-code (Azure handles training internally)
response = client.fine_tuning.jobs.create(
    training_file="file-id",
    model="gpt-4"
)
```

---

📚 Reference  
https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/fine-tuning  

---

## 🏭 Production Considerations

---

### 1. Versioning

- Maintain model versions  
- Rollback capability  

---

### 2. Monitoring

- Track performance  
- Detect drift  

---

### 3. Cost

- Training cost  
- Inference cost  

---

### 4. Deployment Strategy

- A/B testing  
- Gradual rollout  

---

## ⚖️ Fine-Tuning vs RAG (Revisited)

| Factor | Fine-Tuning | RAG |
|-------|------------|-----|
| Knowledge updates | Hard | Easy |
| Cost | High upfront | Pay per query |
| Consistency | High | Medium |
| Flexibility | Low | High |

---

## 🧠 Best Practice Strategy

```
Start → Prompting
   → Add RAG
   → Fine-tune if necessary
```

---

## 🚨 Common Mistakes

- Fine-tuning too early  
- Poor dataset quality  
- Ignoring evaluation  
- No versioning  

---

## 💡 Key Insight

> Fine-tuning is powerful but expensive — it should be used only when simpler approaches cannot achieve the desired performance.

---

## 📚 References

- https://huggingface.co/docs  
- https://learn.microsoft.com/en-us/azure/ai-services/openai/  
- https://platform.openai.com/docs  
