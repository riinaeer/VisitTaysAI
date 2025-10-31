# 🏥 VisitTaysAI — RAG + TTS + Telegram Workflow for n8n

An intelligent hospital assistant demo built with **n8n**, integrating **Retrieval-Augmented Generation (RAG)**, **text-to-speech (TTS)**, and **speech-to-text (STT)** to guide users through **Tampere University Hospital (TAYS)** via **Telegram**.  
It provides conversational responses about TAYS services, navigation, and contact information.

---

## Overview

**VisitTaysAI** connects multiple tools into a single automated workflow:
- 🧠 **RAG engine** using **LangChain + Pinecone Vector Store** to retrieve accurate information from Google Drive documents  
- 💬 **AI Agent (GPT-4o)** with context-aware memory and hospital-specific system prompts  
- 🗣️ **Speech-to-Text (STT)** and **Text-to-Speech (TTS)** for natural voice interaction  
- 🤖 **Telegram Bot** interface for accessibility and real-time conversations  
- 🚍 **Google Routes API** integration for public transport and hospital navigation  

---

## Workflow Components

| Module | Description |
|--------|--------------|
| **Google Drive Trigger** | Watches a shared folder for updates and new files to keep the vector store synchronized |
| **Text Splitter & Data Loader** | Chunks and prepares Google Docs for embedding |
| **Embeddings (OpenAI)** | Creates 1536-dimensional embeddings using `text-embedding-3-small` |
| **Pinecone Vector Store** | Stores and retrieves vectorized knowledge |
| **RAG Tool** | Answers queries by grounding responses in hospital-verified data |
| **AI Agent (Taysa)** | The hospital wayfinding assistant with empathetic, accessibility-aware behavior |
| **Memory Buffer** | Maintains context across up to 5 previous user messages |
| **Speech-to-Text (STT)** | Converts Telegram voice messages into text |
| **Text-to-Speech (TTS)** | Replies in audio form using OpenAI’s `shimmer` voice (OPUS format) |
| **Google Routes API** | Generates route guidance when origin, destination, and travel mode are provided |
| **Telegram Bot** | Serves as the main communication channel between users and the AI |

---

## ⚙️ Requirements

To run this workflow, you’ll need API credentials for:

- 🔑 **Telegram Bot API**
- 🔑 **OpenAI API** (GPT-4o, TTS, and embeddings — ~€5 credit sufficient)
- 🔑 **Google Cloud API** (Routes API — includes free $300 credit)
- 🔑 **Pinecone Vector Database API** (free tier)

You can add these under **n8n → Credentials** before importing the JSON file.

---

## Behavior & Design

- Answers only from the **vector store knowledge base** when possible  
- Respects **accessibility** by avoiding visual language ("look", "see")  
- Limits responses to **600 characters per message**  
- Uses **short, clear sentences** and confirms understanding often  
- Supports both **text and voice replies** depending on user input  
- Remembers **last five messages** for contextual follow-up  

---

## Getting Started

1. **Import the workflow**
   - Go to your n8n dashboard → *Workflows → Import from file* → select `VisitTaysAI_rag.json`

2. **Set credentials**
   - Connect your OpenAI, Google, Pinecone, and Telegram accounts

3. **Start the workflow**
   - Toggle the workflow **Active**
   - Start a chat with your Telegram bot

4. **Try example prompts**
   - “Where is the Eye Centre in TAYS?”
   - “I want to cancel my appointment by phone.”
   - “How can I get from City Campus to TAYS by bus?”

---

## Knowledge Base

All content used by the RAG module is stored in a **Google Drive** folder and synchronized automatically to the **Pinecone Vector Store**.

📂 Example structure:
- Contact Information  
- Cancelling Appointments  
- Hospital Buildings  
- About TAYS Hospital  

> ⚠️ **Note:** The official Google Drive knowledge base is **not included** in this public repository due to **privacy and security reasons**.  
> You can easily **add your own dataset** — upload `.docx` or `.txt` files to your own Google Drive folder, update the folder ID in the workflow, and the system will automatically index and embed your content into Pinecone.

---

## 📄 License

This project is distributed under the **MIT License** — feel free to fork, adapt, and extend responsibly.

---

## Credits

Developed by **Riina** and **Mikaela**
Tampere University · Conversational AI Interaction HTI course

---
