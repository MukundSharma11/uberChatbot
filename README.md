# 🚀 First things first - How to Run This Project Using Docker
## 1️⃣ Prerequisites:

Ensure Docker is installed on your system.

You must have your own API keys for:

GROQ_API_KEY (Required)

TAVILY_API_KEY (Optional)

LANGSMITH_API_KEY (Optional)

## 2️⃣ Prepare Your Environment Variables
### Option A: Using a .env File (Recommended)

Create a .env file (in the same directory as your Dockerfile).

Add your API keys like this:

GROQ_API_KEY=your_groq_key_here (Required)

TAVILY_API_KEY=your_tavily_key_here (Optional)

LANGSMITH_API_KEY=your_langsmith_key_here (Optional)

### Option B: Pass API Keys Directly at Runtime

If you prefer not to use a .env file, you can pass keys directly when running the container.

## 3️⃣ Build the Docker Image

From your project root (where your Dockerfile is located), run:

docker build -t uber-chatbot:latest .

## 4️⃣ Run the Docker Container
### ✅ Using .env file:

docker run --rm --env-file .env uber-chatbot:latest

### ✅ Or, Passing Keys Directly:

docker run --rm \

  -e GROQ_API_KEY=your_groq_key_here \
  
  -e TAVILY_API_KEY=your_tavily_key_here \
  
  -e LANGSMITH_API_KEY=your_langsmith_key_here \
  
  uber-chatbot:latest

## 5️⃣ Project Output

Once running, your project will execute using:

CMD ["python", "main.py"]

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

