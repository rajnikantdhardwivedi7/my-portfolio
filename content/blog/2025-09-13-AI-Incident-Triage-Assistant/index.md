+++
title = "Building AI Incident Triage Assistant: My Journey + Technical Deep Dive"
description = "How I built an AI-powered incident triage assistant with Streamlit, Docker, and ML. A mix of story, architecture, and code snippets."
date = 2025-09-13
+++

# Building AI Incident Triage Assistant: My Journey + Technical Deep Dive

Debugging is messy. Incidents pile up, logs get noisy, and finding solutions often feels like déjà vu. As a DevOps engineer passionate about AI, I wanted to build something that cuts through this chaos — an assistant that doesn’t just *store* logs but actively *understands* them.

That’s how the **AI Incident Triage Assistant** was born.

---

## Why I Built This

I’ve spent years juggling between DevOps tasks and experimenting with AI/ML. One recurring frustration was how much time went into repetitive troubleshooting — sifting through the same classes of errors, searching for past resolutions, and trying to predict what might break next.

So, I asked myself: *What if AI could take the first pass at incidents?* Auto-classify them, suggest fixes, and even predict potential issues. That was the seed of this project.

---

## What It Does

The dashboard is built to be sleek, simple, and functional. Here’s what it offers:

* **AI Classification 🤖** — Uses ML to automatically categorize incidents (timeouts, config errors, infra failures, syntax bugs, etc.) with \~92% accuracy.
* **Similarity Search 🔍** — Finds past incidents and matches them to current ones using NLP-based embeddings.
* **Knowledge Base 📚** — Surfaces solutions and best practices from 150+ curated cases.
* **Real-time Analytics ⚡** — Tracks health, success rate, and resolution times to keep teams proactive.

---

## Tech Stack

* **Streamlit** → Interactive dashboard & UI
* **Python (scikit-learn, FAISS, transformers)** → ML models & similarity search
* **Docker** → Containerized for reproducibility and deployment
* **Zola** → This blog, documenting the journey

---

## Architecture

```text
                ┌──────────────────────┐
                │      Streamlit UI    │
                │ (Dashboard + Inputs) │
                └──────────┬───────────┘
                           │
                           ▼
                ┌──────────────────────┐
                │   AI/ML Engine       │
                │ - Log Classification │
                │ - Similarity Search  │
                │ - Knowledge Base     │
                └──────────┬───────────┘
                           │
                           ▼
                ┌──────────────────────┐
                │   Docker Container   │
                │  (Runs everything)   │
                └──────────────────────┘
```

---

## File Structure

```text
AI-Triage-Assistant/
│
├── app.py               # Streamlit entry point
├── models/              # Trained ML models (classification, embeddings)
├── data/                # Historical incident data, logs
├── utils/               # Helper functions (parsing, preprocessing)
├── requirements.txt     # Dependencies
├── Dockerfile           # Container setup
└── README.md            # Documentation
```

---

## Core Code Examples

**Classification Snippet:**

```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.linear_model import LogisticRegression

vectorizer = TfidfVectorizer()
X = vectorizer.fit_transform(log_messages)
clf = LogisticRegression()
clf.fit(X, labels)

prediction = clf.predict(vectorizer.transform(["Timeout error: DB connection failed"]))
print(prediction)
```

**Similarity Search Snippet:**

```python
import faiss
import numpy as np

index = faiss.IndexFlatL2(768)  # 768-d embeddings
index.add(embeddings)

query_vec = embed(["Kubernetes pod crashlooping"])
D, I = index.search(np.array(query_vec), 5)
print("Top 5 similar incidents:", I)
```

---

## How It Works in Action

1. User enters a log or error in the dashboard.
2. Log gets vectorized and classified into categories.
3. System searches embeddings for similar past incidents.
4. Matching cases + curated fixes are displayed instantly.
5. Dashboard updates real-time analytics.

---

## What’s Next

I want this to evolve beyond incident triage — into a full **AI-powered ops assistant** that not only reacts but *prevents* failures by spotting patterns ahead of time. Imagine predictive incident alerts before a system even crashes.

---

## Contact

👨‍💻 **Rajnikant Dhar Dwivedi**
✉️ [rajnikantdhardwivedi@gmail.com](mailto:rajnikantdhardwivedi@gmail.com)
👉 [My Portfolio](https://rajnikantdhardwivedi-mu.vercel.app/)

---

### Final Thought

This project is a mix of **passion + problem solving**. It’s not about replacing DevOps engineers but augmenting them — cutting down noise, surfacing insights, and letting humans focus on what really matters.
