# 🩺 Chronic Care RAG: Diabetes & Hypertension Question Answering

A **Retrieval-Augmented Generation (RAG)** system for answering clinical questions related to **Diabetes** and **Hypertension**, using **MiniLM embeddings**, **FAISS retrieval**, and **GPT-2 family language models**.

This project evaluates how retrieval-based grounding improves answer **correctness**, **groundedness**, and **hallucination reduction** across different model sizes.

---

## 1. System Overview

This project implements a **lightweight medical question-answering system** using the RAG paradigm.

The system compares **baseline generation** versus **RAG-enhanced generation** across three GPT-2 family models to analyze:
- Factual accuracy  
- Context grounding  
- Hallucination behavior  

The focus is on chronic care domains where hallucination risks are high and reliability is critical.

---

## 2. Architecture

**RAG System Workflow**

1. User submits a medical question  
2. Query is embedded using **MiniLM-L6-v2**
3. Relevant document chunks are retrieved using a **FAISS vector index**
4. Retrieved context is prepended to the prompt
5. A GPT-2 family model generates a grounded response

This architecture ensures that generation is conditioned on verified medical context rather than relying solely on parametric knowledge.

---

## 3. Dataset & Corpus Processing

**Corpus Composition**

The dataset consists of **9 curated medical documents** across three categories:
- **Diabetes**
- **Hypertension**
- **Common / Overlapping conditions**

**Preprocessing Pipeline**
- Text cleaning & normalization  
- Chunking into **200-word windows** with **40-word overlap**
- Embedding using **MiniLM-L6-v2**
- FAISS index construction for efficient similarity search  

This design balances retrieval accuracy with computational efficiency.

---

## 4. Retrieval Example

For each user query:
- The top-k most relevant chunks are retrieved from the FAISS index
- Retrieved evidence is injected into the prompt
- Generation becomes context-aware and medically grounded  

This step significantly improves answer relevance and reduces unsupported claims.

---

## 5. Baseline vs RAG Comparison

| Setting | Behavior |
|-------|---------|
| **Baseline (No Retrieval)** | Higher hallucination, vague or incorrect answers |
| **RAG Enabled** | Improved grounding, higher factual alignment, reduced off-topic output |

RAG consistently improves reliability across all evaluated models.

---

## 6. Model Evaluations

Three GPT-2 family models were evaluated under **Baseline** and **RAG** settings using domain-specific medical questions.

### 6.1 DistilGPT-2 (Smallest Model)

- Struggles under baseline conditions
- Frequently hallucinates or produces incomplete answers
- RAG improves relevance but medical depth remains limited

### 6.2 GPT-2 Medium

- Better fluency and structure
- More stable outputs
- RAG significantly reduces off-topic and unsupported content

### 6.3 GPT-2 Large

- Best performance across all metrics
- More coherent and context-aware answers
- RAG improves grounding, though clinical reasoning is still limited

---

## 6.4 Combined Evaluation Summary

**Key Observations**
- RAG improves correctness and grounding across all models
- Larger models benefit more from retrieval context
- Smaller models rely heavily on RAG to reduce hallucinations

---

## 7. Key Insights

- ✅ Retrieval-Augmented Generation improves factual grounding  
- 📈 Larger models produce more coherent and stable responses  
- ⚠️ Smaller models hallucinate frequently without retrieval support  
- 🏥 Medical QA still requires domain-specific LLMs for high reliability  

RAG provides a strong middle-ground by improving safety without heavy computational costs.

---

## 8. Conclusion

This project demonstrates how **Retrieval-Augmented Generation (RAG)** can substantially improve the quality and reliability of GPT-2 family models for **medical question answering**.

By grounding responses in a curated corpus on **diabetes and hypertension**, the system:
- Reduces hallucinations
- Improves factual alignment
- Makes smaller models more usable in sensitive domains

While larger models perform better overall, limitations in clinical reasoning remain—highlighting the importance of **domain-specific medical LLMs**.

This repository includes all code, figures, and documentation required to **reproduce, evaluate, or extend** the system.

---

## 📌 Technologies Used

- Python  
- Hugging Face Transformers  
- MiniLM-L6-v2  
- FAISS  
- GPT-2 / DistilGPT-2 / GPT-2 Medium / GPT-2 Large  

---

## 🚀 Future Work

- Integration with domain-specific medical LLMs
- Clinical guideline alignment (ADA, AHA)
- Evaluation using medical QA benchmarks
- Explainable retrieval visualization
