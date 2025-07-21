# 🚀 First things first - How to Run This Project Using Docker
### 1️⃣ Prerequisites:

Ensure Docker is installed on your system.

You must have your own API keys for (All are free and available at respective websites): 

GROQ_API_KEY (Required)

TAVILY_API_KEY (Optional)

LANGSMITH_API_KEY (Optional)

### 2️⃣ Prepare Your Environment Variables
#### Option A: Pass API Keys Directly at Runtime (Recommended)

If you prefer not to use a .env file, you can pass keys directly when running the container. Command mentioned in the 4th step.

#### Option B: Using a .env File

Create a .env file (in the same directory as your Dockerfile). Command mentioned in the 4th step.

Add your API keys like this:

GROQ_API_KEY=your_groq_key_here (Required)

TAVILY_API_KEY=your_tavily_key_here (Optional)

LANGSMITH_API_KEY=your_langsmith_key_here (Optional)

### 3️⃣ Pull the Docker Image

In your terminal or Docker CLI

docker pull mukki11/chatbot

### 4️⃣ Run the Docker Container

In your terminal or Docker CLI

#### ✅ Passing Keys Directly (Recommended): 

docker run --rm -it \

  -e GROQ_API_KEY=your_groq_key_here \
  
  -e TAVILY_API_KEY=your_tavily_key_here \
  
  -e LANGSMITH_API_KEY=your_langsmith_key_here \
  
  mukki11/chatbot:latest

#### ✅ Or, Using .env file:

docker run --rm -it --env-file .env mukki11/chatbot:latest
