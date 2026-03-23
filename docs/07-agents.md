# 🤖 Agents in GenAI Systems

## 📌 Overview

Agents are systems that use Large Language Models (LLMs) to:
- Make decisions  
- Plan actions  
- Use tools  
- Execute multi-step workflows  

---

## 🧠 What is an Agent?

An agent is an LLM-powered system that can:

- Understand a goal  
- Break it into steps  
- Execute actions using tools  
- Iterate until completion  

---

### Example

```
User Query:
"Find my latest lab report and summarize glucose levels"

Agent Workflow:
1. Search document
2. Extract data
3. Summarize results
4. Return answer
```

---

## 🎯 Why Agents are Needed

Traditional pipelines:
- Fixed workflow  
- No adaptability  

---

Agents:
- Dynamic decision-making  
- Multi-step reasoning  
- Tool integration  

---

## ⚙️ Agent Architecture

```
User Input
   ↓
LLM (Planner)
   ↓
Tool Selection
   ↓
Tool Execution
   ↓
Observation
   ↓
LLM (Next Step)
   ↓
Final Output
```

---

## 🧩 Core Components

### 1. LLM (Brain)
- Reasoning  
- Planning  
- Decision-making  

---

### 2. Tools

Examples:
- Search APIs  
- Databases  
- Calculators  
- External services  

---

### 3. Memory

- Stores previous interactions  
- Maintains context  

---

### 4. Orchestration

- Controls execution flow  
- Frameworks: LangChain, LangGraph  

---

📚 References

- https://python.langchain.com/docs/  
- https://www.anthropic.com/index/building-effective-agents

