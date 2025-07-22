# 🚀 First things first - How to Run This Project Using Docker
## [Read howToRun.md](./howToRun.md)

-------------------------------------------------------------------------------------------------------------------------------------------------

# 🚖 Agentic Uber Chatbot

### A modular, LLM-driven conversational agent for simulating Uber-like ride operations—booking rides, cancellations with fee adjudication, active ride management, and query resolution. Built using LangGraph, LangChain, Groq LLMs, and a RAG pipeline. Debugged and monitored using Langsmith. Pydantic Data Validation. Multiple versions were designed:
### - Agentic V1: ReAct agent with LangGraph orchestrating LLM-bound tools.
### - Agentic V2: Manual tool triggering via LLM instructions.
### - Workflow: LangGraph nodes and edges define conversation flow and decision points.

---

## 📌 Project Overview

This project implements an **agentic framework** to automate ride management tasks using a **ReAct-based agent**, enabling:
- Ride booking
- Ride cancellations with automated fee decisions
- Listing active bookings
- Contextual question-answering using a Retrieval-Augmented Generation (RAG) pipeline

---

## 🛠️ Tech Stack

| Category                | Libraries/Tools                              |
|-------------------------|----------------------------------------------|
| Language Models         | Groq LLM's                                   |
| Agent Orchestration     | LangGraph, LangChain                         |
| Vector Database         | FAISS                                        |
| Embeddings              | HuggingFace Transformers                     |
| Data Processing (RAG)   | RecursiveTextSplitter, DocLoaders            |
| Clustering              | K-Means (Scikit-learn)                       |
| Data Validation         | Pydantic                                     |
| Monitoring & Debugging  | LangSmith, LangGraph Studio                  |
| Backend Utilities       | JSON-based datastore                         |
| Dataset Generation      | Numpy (Normal, Gamma distributions)          |

---

## ⚙️ System Architecture

### ➤ 1. ReAct Agent (Agentic V1)
- Designed a **ReAct-based** conversational agent using **LangGraph** nodes and edges to orchestrate dynamic tool usage..
- LLM acts as the reasoning unit, with modular toolchains handling user tasks.
- System prompts define agent behavior and tool access.
- System prompts guide the LLM’s decision-making across steps.
- Once user goals are achieved, control returns to the end node

<p align="center">
  <img src="Images/Agentic Architecture.png" alt="ReAct Agent" width="500"/>
</p>

### ➤ 2. Workflow Orchastrator
- Implemented a Workflow Orchestrator using LangGraph, where nodes represent sequential or conditional actions forming a deterministic flow.
- LLM was only involved in the RAG pipeline.
- Each node invokes a specific function/tool such as booking, cancellation processing, listing active bookings, or database interaction.
- The control flow is explicitly hardcoded using LangGraph edges.
- Designed for structured, rule-based task execution where operations must follow a predefined sequence.
- Suitable for automated processes where conversational or reasoning abilities are unnecessary.

<p align="center">
  <img src="Images/Workflow Architecture.png" alt="Workflow Orchastrator" width="500"/>
</p>

---

## Core Tools

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
  - Other transactional factors
 
<p align="center">
  <img src="Images/Driver Cluster.png" alt="Driver Cluster" width="500"/>
  <img src="Images/Rider Cluster 1.png" alt="Rider Cluster" width="500"/>
</p>


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
- **Skewed normal** and **gamma** distributions.
- Simulated user-driver behaviors for training the cancellation fee K-Means model.

<p align="center">
  <img src="Images/Ratings Sampling.png" alt="Ratings Distribution" width="500"/>
</p>

---

## 🔍 Monitoring & Debugging

- Traces and agent actions monitored using **LangSmith**.
- Graph state flows visualized with **LangGraph Studio** for debugging and performance analysis.

---

## 🔐 Data Validation & Security

- All user/driver data inputs validated using **Pydantic model classes**.
- Secure authentication for login, new user, and driver registrations.

