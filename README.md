<![CDATA[# 🏛️ Bihar Tourism RAG Chatbot

An AI-powered conversational chatbot that serves as an intelligent **Bihar Tourism Guide**, built using **Retrieval-Augmented Generation (RAG)**. Ask questions about tourist attractions, culture, history, food, festivals, and travel in Bihar — via text or voice!

---

## ✨ Features

- **RAG-Powered Responses** — Answers grounded in curated tourism documents for accuracy and relevance
- **Conversational Memory** — Maintains chat history with context-aware follow-up question handling
- **Voice Input** — Built-in speech-to-text microphone support for hands-free interaction
- **Multi-Language Support** — Ask questions in your own language
- **Extensive Knowledge Base** — Ingests 200+ location-specific PDFs and official Bihar tourism brochures


---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────────┐
│                   Streamlit Frontend                     │
│              (Text Input + Voice Input)                  │
└──────────────────┬───────────────────────────────────────┘
                   │
                   ▼
┌──────────────────────────────────────────────────────────┐
│            History-Aware Retriever                       │
│  (Reformulates follow-up questions into standalone       │
│   queries using chat history)                            │
└──────────────────┬───────────────────────────────────────┘
                   │
          ┌────────┴────────┐
          ▼                 ▼
┌──────────────────┐ ┌─────────────────────────────────────┐
│   ChromaDB       │ │   Chat History (Trimmed)            │
│  Vector Store    │ │   (Session-based, max 1000 tokens)  │
│  (OpenAI Embeds) │ └─────────────────────────────────────┘
└──────────────────┘
          │
          ▼
┌──────────────────────────────────────────────────────────┐
│           LLM — Llama 3.3 70B (via Groq)                │
│   (System prompt: Bihar Tourism Guide persona)           │
└──────────────────────────────────────────────────────────┘
```

---

## 📁 Project Structure

```
bihar_tourism_chatbot/
├── app.py                     # Main Streamlit application
├── conversastionqa.ipynb      # Notebook for data ingestion & experimentation
├── requirements.txt           # Full pinned dependencies (pip freeze)
├── chroma_db/                 # Persisted ChromaDB vector store
│   └── chroma.sqlite3
└── pdf_directory/             # Source documents for RAG
    ├── *.pdf                  # Official Bihar tourism brochures
    └── knowledge_base/        # 200+ location-specific PDFs
        ├── mahabodhi_temple.pdf
        ├── nalanda_university_ruins.pdf
        ├── rajgir_ropeway.pdf
        └── ...
```

---

## 🛠️ Tech Stack

| Component         | Technology                                      |
| ------------------ | ----------------------------------------------- |
| **Frontend**       | Streamlit                                       |
| **LLM**            | Llama 3.3 70B Versatile (via Groq API)          |
| **Embeddings**     | OpenAI Embeddings                               |
| **Vector Store**   | ChromaDB (persistent, local)                    |
| **Framework**      | LangChain (chains, retrievers, history)         |
| **Voice Input**    | `streamlit-mic-recorder` (speech-to-text)        |
| **Language**       | Python                                          |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- [Groq API Key](https://console.groq.com/) (for LLM inference)
- [OpenAI API Key](https://platform.openai.com/) (for embeddings)

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/aditya21111/tourism_rag
   cd bihar_tourism_rag
   ```

2. **Create and activate a virtual environment**

   ```bash
   python -m venv venv
   source venv/bin/activate  # macOS/Linux
   # venv\Scripts\activate   # Windows
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**

   Create a `.env` file in the project root:

   ```env
   GROQ_API_KEY=your_groq_api_key_here
   OPENAI_API_KEY=your_openai_api_key_here
   ```

5. **Run the application**

   ```bash
   streamlit run app.py
   ```

   The app will open in your browser.

---

## 💬 Usage

| Action                  | How                                                                 |
| ----------------------- | ------------------------------------------------------------------- |
| **Ask a question**      | Type in the chat input box                                          |
| **Use voice**           | Click the 🎤 button, speak, then click ⏹️ to submit                |
| **Follow-up questions** | Just ask naturally — the chatbot remembers your conversation context |

### Example Questions

- *"What are the top tourist places in Bihar?"*
- *"Tell me about Mahabodhi Temple"*
- *"बिहार में कौन कौन से वन्यजीव अभयारण्य हैं?"*
- *"What is the best time to visit Rajgir?"*
- *"How to reach Bodh Gaya from Patna?"*

---

## 📚 Knowledge Base

The chatbot is powered by a rich collection of source documents:

| Source                                   | Description                                    |
| ---------------------------------------- | ---------------------------------------------- |
| **Blissful Bihar Brochure**              | Official state tourism brochure (English)       |
| **Buddha Circuit Guide**                 | Dedicated Buddhist pilgrimage circuit guide      |
| **Eco Circuit Brochure**                 | Eco-tourism destinations and circuits            |
| **Magnificent Bihar 2020**               | Comprehensive tourism overview                   |
| **Tourist Attractions of Bihar 2020**    | District-wise attraction catalog                 |
| **Ready Reckoner**                       | Quick reference tourism guide                    |
| **200+ Location PDFs**                   | Individual attraction profiles with details      |

---

## ⚙️ Configuration

### Switching to Local Embeddings (Ollama)

For offline/local development without the OpenAI API, uncomment the Ollama embedding lines in [app.py]:

```python
from langchain_ollama import OllamaEmbeddings
embedding = OllamaEmbeddings(model='mxbai-embed-large')
```

> **Note:** You will need to re-index the documents with the new embedding model if you switch.



## 📄 License

This project is open source. Feel free to use and modify it for your own purposes.

---

<p align="center">
  Made with ❤️ for Bihar Tourism
</p>
]]>
