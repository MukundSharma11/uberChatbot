# 🚀 First things first - How to Run This Project Using Docker
## Read howToRun.md file present in this repository

-------------------------------------------------------------------------------------------------------------------------------------------------

# 🚖 Agentic Uber Chatbot

A modular, LLM-driven conversational agent for simulating Uber-like ride operations—booking rides, cancellations with fee adjudication, active ride management, and query resolution. Built using LangGraph, LangChain, OpenAI LLMs, and a RAG pipeline.

---

## 📌 Project Overview

This project implements an **agentic framework** to automate ride management tasks using a **ReAct-based agent**, enabling:
- Ride booking
- Ride cancellations with automated fee decisions
- Listing active bookings
- Contextual question-answering using a Retrieval-Augmented Generation (RAG) pipeline

Multiple versions were designed:
- **Agentic V1**: ReAct agent with LangGraph orchestrating LLM-bound tools.
- **Agentic V2**: Manual tool triggering via LLM instructions (under development).
- **Workflow**: LangGraph nodes and edges define conversation flow and decision points.

---

## 🛠️ Tech Stack

| Category                | Libraries/Tools                              |
|-------------------------|----------------------------------------------|
| Language Models         | OpenAI GPT models                            |
| Agent Orchestration     | LangGraph, LangChain                         |
| Vector Database         | FAISS                                        |
| Embeddings              | HuggingFace Transformers                     |
| Data Processing         | RecursiveTextSplitter, DocLoaders            |
| Clustering              | K-Means (Scikit-learn)                       |
| Data Validation         | Pydantic                                     |
| Monitoring & Debugging  | LangSmith, LangGraph Studio                  |
| Backend Utilities       | JSON-based datastore                         |
| Dataset Generation      | Scipy Stats (Normal, Beta, Gamma distributions) |

---

## ⚙️ System Architecture

### ➤ 1. ReAct Agent (Agentic V1)
- Built using **LangGraph** nodes and edges.
- LLM acts as the reasoning unit, with modular toolchains handling user tasks.
- **System prompts** define agent behavior and tool access.
- Once user goals are achieved, control returns to the end node.

---

### ➤ 2. Core Tools

#### 📍 Booking Tool
- Books rides based on pickup/drop locations.

#### 📍 Cancellation Tool
- Uses an **unsupervised K-Means clustering model** to categorize cancellation fees:
  - **Fee Waived**
  - **Base Fee Applied**
  - **Base + Variable Fee Applied**
- Decision-making considers:
  - Driver arrival status
  - Wait time
  - Rider/driver ratings
  - Historical cancellation rates

#### 📍 Active Bookings Tool
- Fetches and lists active rides from a JSON-based booking datastore.

#### 📍 Query Handler (RAG Pipeline)
- Standard **Retrieval-Augmented Generation** (RAG) process:
  1. Load and split documents using DocLoaders & RecursiveTextSplitter.
  2. Generate embeddings via HuggingFace models.
  3. Store in **FAISS Vector Database**.
  4. Retrieve relevant documents using similarity search.
  5. Forward documents and query to LLM using a structured prompt.
  6. LLM generates context-aware responses.

---

## 📊 Dataset Generation

- Created realistic synthetic datasets using probabilistic sampling:
  - **Skewed normal**, **beta**, and **gamma** distributions.
- Simulated user-driver behaviors for training the cancellation fee K-Means model.

---

## 🔍 Monitoring & Debugging

- Traces and agent actions monitored using **LangSmith**.
- Graph state flows visualized with **LangGraph Studio** for debugging and performance analysis.

---

## 🔐 Data Validation & Security

- All user/driver data inputs validated using **Pydantic model classes**.
- Secure authentication for login, new user, and driver registrations.

---

## 🚀 How to Run

1. Clone repository:
```bash
git clone https://github.com/MukundSharma11/uberChatbot.git
cd uberChatbot

