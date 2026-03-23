# 🔍 Observability in GenAI Systems

## 📌 Overview

Observability is the ability to monitor, trace, and debug GenAI systems in production.

It helps answer:
- Why did the model give this output?  
- Where did the system fail?  
- How is performance changing over time?  

---

## 🧠 Why Observability Matters

GenAI systems are:
- Non-deterministic  
- Multi-component (RAG, LLM, tools)  
- Hard to debug  

---

> Without observability, debugging GenAI systems becomes guesswork.

---

## 🧩 What to Observe

---

### 1. Inputs

- User queries  
- Prompt structure  
- Context provided  

---

### 2. Retrieval

- Retrieved documents  
- Relevance scores  
- Top-K results  

---

### 3. LLM Outputs

- Generated responses  
- Token usage  
- Latency  

---

### 4. System Metrics

- API latency  
- Error rates  
- Throughput  

---

### 5. Cost Metrics

- Token usage  
- Cost per request  

---

## 🧱 Observability Layers

```
User Input
  → Prompt Logs
  → Retrieval Logs
  → LLM Logs
  → Output Logs
  → Metrics & Monitoring
```

---

## ☁️ Azure Observability Setup

---

### 1. Application Insights (Core Tool)

Tracks:
- Requests  
- Dependencies  
- Exceptions  

---

### Python Integration Example

```python
from opencensus.ext.azure.log_exporter import AzureLogHandler
import logging

logger = logging.getLogger(__name__)
logger.addHandler(AzureLogHandler(connection_string="YOUR_CONNECTION_STRING"))

logger.warning("LLM request started")
```

---

### 2. Azure Monitor

- Collects metrics  
- Dashboards  
- Alerts  

---

## 🧰 Open-source Observability Tools

---

### 1. LangSmith (LangChain)

- Trace LLM calls  
- Debug chains  

```python
import os
os.environ["LANGCHAIN_TRACING_V2"] = "true"
os.environ["LANGCHAIN_API_KEY"] = "your_api_key"
```

---

### 2. OpenTelemetry (Standard)

- Distributed tracing  

```python
from opentelemetry import trace

tracer = trace.get_tracer(__name__)

with tracer.start_as_current_span("llm_call"):
    response = llm.invoke(prompt)
```

---

### 3. Weights & Biases (W&B)

- Experiment tracking  
- Metrics logging  

---

## 📊 Logging Example (End-to-End)

```python
def process_query(query):
    logger.info(f"User Query: {query}")

    docs = retrieve_documents(query)
    logger.info(f"Retrieved Docs: {docs}")

    response = llm.invoke(query)
    logger.info(f"LLM Response: {response}")

    return response
```

---

## 💡 Key Insight

> Observability is not just logging — it is structured tracking of every step in the GenAI pipeline.

## 🔁 LLM Tracing (Deep Dive)

### 📌 What is LLM Tracing?

LLM tracing tracks:
- Input prompt  
- Context provided  
- Model response  
- Latency and tokens  

---

### Why It Matters

- Debug incorrect outputs  
- Analyze prompt effectiveness  
- Track hallucinations  

---

## 🧪 Basic LLM Trace Example

```python
def trace_llm_call(prompt):
    start_time = time.time()

    response = llm.invoke(prompt)

    end_time = time.time()

    logger.info({
        "prompt": prompt,
        "response": response,
        "latency": end_time - start_time
    })

    return response
```

---

## 🔎 Retrieval Tracing (RAG Debugging)

### 📌 What to Track

- Query embedding  
- Retrieved documents  
- Similarity scores  
- Final selected context  

---

### Example

```python
def retrieve_with_trace(query):
    embedding = embed_model.encode(query)

    docs = vector_db.search(embedding, top_k=5)

    logger.info({
        "query": query,
        "retrieved_docs": docs
    })

    return docs
```

---

## 🧰 LangSmith (Open-source / LangChain Ecosystem)

### 📌 Features

- Full chain tracing  
- Prompt inspection  
- Debugging tools  

---

### Setup

```python
import os

os.environ["LANGCHAIN_TRACING_V2"] = "true"
os.environ["LANGCHAIN_API_KEY"] = "your_api_key"
os.environ["LANGCHAIN_PROJECT"] = "genai-app"
```

---

### Example

```python
from langchain.chat_models import ChatOpenAI

llm = ChatOpenAI()

response = llm.invoke("What is glucose?")
```

👉 Automatically traced in LangSmith dashboard

---

## ☁️ Azure + OpenTelemetry Integration

### 📌 Goal

Combine:
- OpenTelemetry (tracing standard)  
- Azure Monitor (visualization)  

---

### Setup Example

```python
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.exporter.azure.monitor import AzureMonitorTraceExporter
from opentelemetry.sdk.trace.export import BatchSpanProcessor

trace.set_tracer_provider(TracerProvider())

exporter = AzureMonitorTraceExporter(
    connection_string="YOUR_CONNECTION_STRING"
)

span_processor = BatchSpanProcessor(exporter)
trace.get_tracer_provider().add_span_processor(span_processor)

tracer = trace.get_tracer(__name__)
```

---

### Usage

```python
with tracer.start_as_current_span("rag_pipeline"):
    docs = retrieve_documents(query)

    with tracer.start_as_current_span("llm_call"):
        response = llm.invoke(query)
```

---

## 🔗 Combined Trace (Best Practice)

```
User Query
  → Retrieval Trace
  → Context Trace
  → LLM Trace
  → Output Trace
```

---

## 🧠 Debugging RAG Example

### Problem: Wrong Answer

---

### Debug Steps

1. Check retrieved documents  
2. Verify relevance  
3. Inspect prompt  
4. Analyze LLM output  

---

### Example

```python
logger.info("Query:", query)
logger.info("Docs:", docs)
logger.info("Prompt:", prompt)
logger.info("Response:", response)
```

---

## ⚖️ Tool Comparison

| Tool | Use Case |
|-----|--------|
| Azure Monitor | Production monitoring |
| OpenTelemetry | Distributed tracing |
| LangSmith | LLM debugging |
| W&B | Experiment tracking |

---

## 💡 Key Insight

> Observability in GenAI requires tracing across multiple layers — retrieval, prompts, and generation — not just system logs.

## 📊 Metrics Dashboards

### 📌 Why Dashboards Matter

Dashboards provide:
- Real-time visibility  
- Trend analysis  
- Performance insights  

---

## ☁️ Azure Dashboards

---

### Azure Monitor + Application Insights

Track:

- Request latency  
- Error rates  
- Dependency calls (LLM, DB)  
- Throughput  

---

### Example Metrics

| Metric | Description |
|-------|------------|
| Request Duration | API latency |
| Failed Requests | Error rate |
| Dependency Duration | LLM / DB latency |

---

### Query Example (Kusto - Azure)

```
requests
| summarize avg(duration), count() by bin(timestamp, 5m)
```

---

## 🧰 Open-source Dashboards

---

### 1. Grafana + Prometheus

- Real-time monitoring  
- Custom dashboards  

---

### Example Metrics to Track

- LLM latency  
- Token usage  
- Retrieval time  

---

---

### 2. Weights & Biases (W&B)

- Experiment tracking  
- Model performance  

---

## 🚨 Alerting Strategies

### 📌 Why Alerts?

- Detect failures early  
- Prevent system degradation  

---

### Azure Alerts

Trigger alerts on:

- High latency  
- Error spikes  
- Cost thresholds  

---

### Example

```
Alert: Latency > 2 seconds for 5 minutes
```

---

### Open-source Alerts

- Prometheus AlertManager  
- Custom webhook alerts  

---

## 💰 Cost & Performance Tracking

---

### What to Track

#### 1. Token Usage

- Input tokens  
- Output tokens  

---

#### 2. Cost per Request

```
Cost = tokens × price
```

---

#### 3. Model Usage

- Which models are used  
- Frequency  

---

---

### Example Logging

```python
logger.info({
    "tokens_input": 500,
    "tokens_output": 200,
    "cost": 0.02
})
```

---

## ⚡ Performance Metrics

- End-to-end latency  
- Retrieval latency  
- LLM response time  

---

## 🏭 Production Observability Patterns

---

### 1. End-to-End Tracing

```
User → API → Retrieval → LLM → Response
```

---

### 2. Layered Monitoring

- System metrics  
- Model metrics  
- Business metrics  

---

### 3. Feedback Loop

```
User Feedback → Logs → Analysis → Improvements
```

---

### 4. Cost Monitoring

- Track usage per user  
- Detect anomalies  

---

## ⚖️ Trade-offs

| Factor | Trade-off |
|-------|----------|
| Monitoring depth | Overhead |
| Logging detail | Storage cost |
| Alert sensitivity | Noise vs missed issues |

---

## 🚨 Common Mistakes

- No dashboards  
- No alerting  
- Ignoring cost tracking  
- Logging without structure  
- No correlation between components  

---

## 🧠 Design Principles

- Monitor everything  
- Trace end-to-end  
- Alert on critical issues  
- Optimize continuously  

---

## 💡 Key Insight

> Observability is not optional — it is essential for debugging, scaling, and optimizing GenAI systems in production.

---

## 📚 References

- https://learn.microsoft.com/en-us/azure/monitor/  
- https://opentelemetry.io/  
- https://grafana.com/  
- https://wandb.ai/  
