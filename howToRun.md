# 🚀 First things first - How to Run This Project Using Docker
## 1️⃣ Prerequisites:

Ensure Docker is installed on your system.

You must have your own API key for Groq (It's free and available at their website): 

GROQ_API_KEY

## 2️⃣ Pull the Docker Image

In your terminal or Docker CLI

docker pull mukki11/chatbot

## 3️⃣ Run the Docker Container

In your terminal or Docker CLI

### ✅ Passing Keys Directly (Recommended): 

docker run --rm -it \

  -e GROQ_API_KEY=your_groq_key_here \
  
  mukki11/chatbot:latest

### ✅ Or, Using .env file:

Create a .env file (in the same directory as your Dockerfile). Command mentioned in the 4th step.

Add your API key like this:

GROQ_API_KEY=your_groq_key_here

and then run this command

docker run --rm -it --env-file .env mukki11/chatbot:latest
