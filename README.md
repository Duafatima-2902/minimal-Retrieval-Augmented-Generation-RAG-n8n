# minimal-Retrieval-Augmented-Generation-RAG-n8n
This project is a *minimal Retrieval-Augmented Generation (RAG)* workflow built in [n8n](https://n8n.io).  
It lets you upload documents, store their embeddings in *Pinecone*, and then query them through an AI agent.

![WhatsApp Image 2025-08-24 at 21 42 34_fb2f3110](https://github.com/user-attachments/assets/441fd989-1ddc-4d99-ad48-e9620b85778b)

---

## ⚙ What It Does

1. *Indexing Workflow*
   - Triggered when a file is uploaded to Google Drive.  
   - Downloads the file.  
   - Splits the text into chunks.  
   - Generates embeddings using OpenAI.  
   - Stores embeddings in Pinecone vector DB.

2. *Query Workflow*
   - Triggered when a chat message is received.  
   - Embeds the user’s question.  
   - Queries Pinecone for the most relevant chunks.  
   - Passes context + question to an AI model (OpenRouter / OpenAI).  
   - Returns an answer based on your documents.

---

## 🛠 Setup Instructions

### 1. Clone This Repository

git clone https://github.com/YOUR-USERNAME/n8n-rag-demo.git
cd n8n-rag-demo
2. Import Workflow
Open your local n8n instance.

Import the provided workflow.json file.

3. Add Credentials
You’ll need to configure the following credentials inside n8n:

OpenAI API Key → for embeddings.

Pinecone API Key + Environment → for vector storage.

OpenRouter / OpenAI API Key → for the chat model.

Google Drive credentials → for file ingestion.

⚠ These are not included in the repo. You must add them manually in your n8n settings.

📂 Pinecone Setup
Go to Pinecone Console.

Create a new index (example name: rag).

Dimensions: 1536 (for text-embedding-ada-002).

Metric: cosine.

Pod Type: starter (free tier works).

Copy your API key + environment into n8n credentials.

▶ How to Run
Index Documents:

Upload a .txt or .pdf file into the Google Drive folder linked in the trigger.

Workflow runs automatically → stores embeddings in Pinecone.

Ask Questions:

Send a chat message (via webhook/Telegram/etc depending on your setup).

Workflow fetches context from Pinecone and returns an AI-generated answer.

📝 Notes
The workflow is split into two parts: Indexing and Querying.

Make sure your Pinecone index exists before running queries.

Embedding model and index dimension must match.
