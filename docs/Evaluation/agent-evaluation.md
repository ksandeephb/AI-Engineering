# 🤖 Agent Evaluation — Metrics, Tools, and Code

## 🧠 Introduction

Agent systems are more complex than standard LLM tasks because they involve:

- reasoning
- planning
- tool usage
- multi-step execution

Evaluation must therefore go beyond simple text comparison and assess **behavior and correctness**.

---

# 🧩 Evaluation Dimensions

## 🔹 Task Success

Did the agent complete the task correctly?

## 🔹 Reasoning Quality

Was the reasoning process logical and coherent?

## 🔹 Tool Usage

Did the agent select the correct tools and use them properly?

## 🔹 Efficiency

How many steps were taken to complete the task?

## 🔹 Robustness

Can the agent handle edge cases and unexpected inputs?

---

# 📏 Key Metrics

---

## 🔵 Task Success Rate

```
Success Rate = Successful Tasks / Total Tasks
```

```python
def success_rate(successes, total):
    return successes / total
```

---

## 🟢 Step Efficiency

Measures number of steps taken.

```python
def step_efficiency(steps_taken):
    return sum(steps_taken) / len(steps_taken)
```

---

## 🟣 Tool Accuracy

Measures correctness of tool selection.

```python
def tool_accuracy(correct, total):
    return correct / total
```

---

## 🟡 Reasoning Score (LLM-based)

```python
def reasoning_score(trace):
    prompt = f"Evaluate reasoning quality:\n{trace}"
    # send to LLM for scoring
```

---

# 🧰 Agent Evaluation Tools

---

## 🔵 LangSmith

👉 https://smith.langchain.com/

### Features

- trace-based evaluation  
- debugging agent steps  
- dataset-based evaluation  

---

### Example

```python
from langsmith import Client

client = Client()

runs = client.list_runs(project_name="agent-project")

for run in runs:
    print(run.outputs)
```

---

## 🟢 AutoGen Evaluation

👉 https://github.com/microsoft/autogen

### Features

- multi-agent evaluation  
- conversation tracking  
- tool usage analysis  

---

### Example

```python
from autogen import AssistantAgent

agent = AssistantAgent(name="assistant")

response = agent.generate_reply(
    messages=[{"role": "user", "content": "Solve math problem"}]
)

print(response)
```

---

## 🟣 DeepEval (Agent Testing)

👉 https://github.com/confident-ai/deepeval

### Features

- unit tests for agents  
- reasoning evaluation  
- CI/CD integration  

---

### Example

```python
from deepeval.test_case import LLMTestCase

test_case = LLMTestCase(
    input="Book a flight",
    actual_output="Flight booked"
)

print(test_case)
```

---

## 🟡 OpenAI Evals

👉 https://github.com/openai/evals

### Features

- benchmark-style evaluation  
- customizable eval pipelines  
- supports agent workflows  

---

### Example

```python
# CLI usage
# evals run my_eval
```

---

# ⚖️ Tool Comparison

| Tool | Type | Strength | Use Case |
|------|-----|----------|----------|
| LangSmith | Monitoring | Trace analysis | Debugging |
| AutoGen | Multi-agent | Conversation eval | Agent systems |
| DeepEval | Testing | CI/CD | Production |
| OpenAI Evals | Benchmark | Custom evals | Research |

---

# 🧠 Evaluation Strategies

---

## 🔹 Trace-Based Evaluation

Analyze each step of agent execution:

- inputs  
- outputs  
- tool calls  

---

## 🔹 LLM-as-a-Judge

Use LLM to evaluate:

- reasoning quality  
- correctness  
- coherence  

---

## 🔹 Rule-Based Evaluation

Define rules:

- expected outputs  
- tool usage constraints  

---

## 🔹 Human Evaluation

Used for:

- high-stakes applications  
- subjective quality  

---

# 🧠 Key Insight

Agent evaluation is fundamentally different:

```
Not just "what was the answer?"
But "how was the answer produced?"
```

---

# 🏁 Summary

- Agents require multi-dimensional evaluation  
- Combine metrics + tracing + LLM judging  
- No single metric is sufficient  

---

## 💡 Final Takeaway

```
RAG → retrieval + generation  
Summarization → semantic accuracy  
Translation → linguistic correctness  
Agents → reasoning + behavior  
```

---
