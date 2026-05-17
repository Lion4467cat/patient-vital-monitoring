# 🏥 Patient Vital Monitoring — RAG Pipeline

A Retrieval-Augmented Generation (RAG) system that enables natural language querying of patient vitals and medical history — making clinical data accessible without writing a single SQL query.

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-2.x-000000?style=flat&logo=flask&logoColor=white)
![RAG](https://img.shields.io/badge/RAG-Pipeline-FF6B6B?style=flat)
![LLM](https://img.shields.io/badge/LLM-Powered-8B5CF6?style=flat)

---

## 🔍 What It Does

Instead of writing queries like `SELECT * FROM vitals WHERE patient_id = 42 AND timestamp > ...`, a doctor or nurse can simply ask:

> *"What was the blood pressure trend for Patient 42 over the last 6 hours?"*
> *"Which patients had oxygen saturation below 95% this morning?"*
> *"Summarize the vitals history for Patient 17."*

The RAG pipeline retrieves the relevant records and generates a grounded, accurate response.

---

## 🏗️ Architecture

```
Patient Vital Data (CSV / DB)
        │
        ▼
  Document Chunking
  + Embedding Generation
        │
        ▼
   Vector Store (retrieval index)
        │
   User Query ──► Query Embedding
        │
        ▼
  Similarity Search → Relevant Records
        │
        ▼
  LLM (with retrieved context)
        │
        ▼
  Natural Language Response
        │
        ▼
  Flask UI Dashboard
```

---

## 🚀 Getting Started

### Prerequisites
- Python 3.10+
- LLM API key (Groq / OpenAI)

### Installation

```bash
git clone https://github.com/Lion4467cat/patient-vital-monitoring.git
cd patient-vital-monitoring
pip install -r requirements.txt
```

### Run

```bash
python app.py
```

Visit `http://localhost:5000`

---

## 🛠️ Tech Stack

- **RAG Framework** — LangChain
- **LLM** — Groq API / LLaMA 3.1
- **Embeddings** — Sentence Transformers
- **Backend** — Flask, Python
- **Data** — Patient vitals (structured CSV / JSON)

---

## 💡 Why RAG Over Fine-Tuning?

Fine-tuning an LLM on medical data is expensive and raises privacy concerns. RAG solves this by:
- Keeping patient data local — nothing leaves your server
- Retrieving only relevant records per query (no hallucination on unrelated data)
- Being updatable in real time as new vitals come in

---

## ⚠️ Disclaimer

This is an academic/research project. Not intended for clinical use. Always consult qualified medical professionals for healthcare decisions.

---

## 👤 Author

**S. S. Gokula Swamy** — [LinkedIn](https://www.linkedin.com/in/ssgokulaswamy) · [Portfolio](https://lion4467cat.github.io/raikabuilds)
