Got it 👍 — here is clean GitHub-compatible Markdown with ZERO content outside the code block.

# 📘 Part 1: RAG (Retrieval-Augmented Generation) — Evaluation Metrics & Tools

---

## 🧠 What is RAG?

Retrieval-Augmented Generation combines:
- Retriever (vector DB / search)
- Generator (LLM)


Query → Retriever → Context → LLM → Response


---

# 📊 1. Evaluation Metrics for RAG

## 🔹 Retrieval Metrics

| Metric        | Description                     | Formula / Idea                  |
|--------------|---------------------------------|----------------------------------|
| Precision@K  | Relevant docs in top K           | relevant@K / K                  |
| Recall@K     | Coverage of relevant docs        | relevant@K / total relevant     |
| MRR          | Rank of first relevant result    | 1 / rank                        |
| nDCG         | Ranking quality                 | position-weighted relevance     |

### ✅ Code Example (Retrieval Metrics)

```python
def precision_at_k(relevant_docs, retrieved_docs, k):
    retrieved_k = retrieved_docs[:k]
    relevant = set(relevant_docs)
    return len([doc for doc in retrieved_k if doc in relevant]) / k

def recall_at_k(relevant_docs, retrieved_docs, k):
    retrieved_k = retrieved_docs[:k]
    relevant = set(relevant_docs)
    return len([doc for doc in retrieved_k if doc in relevant]) / len(relevant)
🔹 Generation Metrics
Metric	Description
Faithfulness	Answer grounded in context
Relevance	Answer matches query
Answer Correctness	Matches ground truth
Hallucination Rate	% incorrect facts
🔹 LLM-based Evaluation (Modern Standard)

Use LLM-as-a-judge:

Input: Question + Context + Answer  
Output: Score (0–1) + reasoning
🧪 2. RAG Evaluation Frameworks (Tools)
🥇 Ragas
GitHub: https://github.com/explodinggradients/ragas
Docs: https://docs.ragas.io/
✅ Features
Faithfulness
Context precision/recall
Answer relevance
💻 Code Example
from ragas import evaluate
from datasets import Dataset
from ragas.metrics import faithfulness, answer_relevancy

data = {
    "question": ["What is AI?"],
    "answer": ["AI is artificial intelligence"],
    "contexts": [["AI stands for artificial intelligence"]],
}

dataset = Dataset.from_dict(data)

result = evaluate(
    dataset,
    metrics=[faithfulness, answer_relevancy],
)

print(result)
🥈 TruLens
GitHub: https://github.com/truera/trulens
Docs: https://www.trulens.org/
✅ Features
Feedback functions
Hallucination detection
Observability dashboard
💻 Code Example
from trulens_eval import Tru
from trulens_eval.feedback import Feedback

tru = Tru()

f_relevance = Feedback.openai_relevance()

# attach to your pipeline
🥉 DeepEval
GitHub: https://github.com/confident-ai/deepeval
💻 Code Example
from deepeval.metrics import AnswerRelevancyMetric
from deepeval.test_case import LLMTestCase

metric = AnswerRelevancyMetric()

test_case = LLMTestCase(
    input="What is AI?",
    actual_output="AI is artificial intelligence"
)

metric.measure(test_case)
print(metric.score)
🧰 3. RAG Frameworks
LangChain
https://github.com/langchain-ai/langchain
LlamaIndex
https://github.com/jerryjliu/llama_index
💻 Example: Simple RAG (LlamaIndex)
from llama_index.core import VectorStoreIndex
from llama_index.core import SimpleDirectoryReader

docs = SimpleDirectoryReader("./data").load_data()

index = VectorStoreIndex.from_documents(docs)
query_engine = index.as_query_engine()

response = query_engine.query("What is AI?")
print(response)
🗄️ 4. Vector Databases
Tool	Type	Link
FAISS	Local	https://github.com/facebookresearch/faiss

Chroma	Open source	https://github.com/chroma-core/chroma

Weaviate	Hybrid	https://github.com/weaviate/weaviate

Pinecone	SaaS	https://www.pinecone.io
💻 Example: FAISS
from langchain.vectorstores import FAISS
from langchain.embeddings import OpenAIEmbeddings

db = FAISS.from_texts(
    ["AI is cool", "ML is subset of AI"],
    OpenAIEmbeddings()
)

docs = db.similarity_search("What is AI?")
print(docs)
🧪 5. End-to-End RAG Evaluation Pipeline
Dataset → Retrieval Eval → Generation Eval → LLM Judge → Dashboard
⚠️ Common Pitfalls
❌ Evaluating only LLM output (ignore retrieval)
❌ No ground truth dataset
❌ Using BLEU/ROUGE for RAG (not ideal)
❌ No hallucination detection

---

