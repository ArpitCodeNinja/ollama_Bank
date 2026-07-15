# 🏦 OllamaBank - Ollama-powered banking assistant

<div align="center">

**A Retrieval-Augmented Generation (RAG) Demo using Ollama + ChromaDB**

[![Python](https://img.shields.io/badge/Python-3.8+-blue)](https://www.python.org/)
[![Ollama](https://img.shields.io/badge/Ollama-LLM-orange)](https://ollama.ai/)
[![Streamlit](https://img.shields.io/badge/Streamlit-UI-purple)](https://streamlit.io/)
[![License](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)

</div>

---

## 📋 Overview

**BankRAG** is a Retrieval-Augmented Generation (RAG) demo application that combines the power of Ollama (local LLM) with a vector database to create an intelligent banking knowledge assistant. The system can answer user queries about banking by retrieving relevant information from a banking knowledge base and generating context-aware responses.

### 🎯 Key Features

- 🔒 **100% Local** - Runs entirely on your machine, no external API calls
- 🧠 **Intelligent Retrieval** - Semantic search using vector embeddings
- 💡 **Context-Aware Responses** - Grounded in factual banking knowledge
- 💻 **Interactive UI** - User-friendly Streamlit web interface
- 🚀 **Two Interfaces** - CLI and Web UI options
- 📚 **Comprehensive Knowledge** - 100+ banking facts included

---

## 🛠️ Technologies Used

| Technology | Purpose | Version |
|------------|---------|---------|
| **Python** | Core language | 3.8+ |
| **Ollama** | Local LLM & Embeddings | Latest |
| **Streamlit** | Web interface | 1.28.0+ |
| **NumPy** | Numerical operations | 1.24.0+ |

### Models Used

- **Embedding Model**: `hf.co/CompendiumLabs/bge-base-en-v1.5-gguf`
- **Language Model**: `hf.co/bartowski/Llama-3.2-1B-Instruct-GGUF`

---

## 📦 Installation

### Prerequisites

- Python 3.8+
- Ollama installed locally
- 4GB+ RAM (8GB recommended)

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/bankrag.git
cd bankrag
```

### Step 2: Install Python Dependencies

```bash
pip install -r requirements.txt
```

### Step 3: Install Ollama

**macOS/Linux:**
```bash
curl -fsSL https://ollama.ai/install.sh | sh
```

**Windows:** Download from [ollama.ai/download](https://ollama.ai/download)

### Step 4: Pull Required Models

```bash
# Pull the embedding model
ollama pull hf.co/CompendiumLabs/bge-base-en-v1.5-gguf

# Pull the language model
ollama pull hf.co/bartowski/Llama-3.2-1B-Instruct-GGUF
```

### Step 5: Verify Installation

```bash
ollama list
python -c "import ollama; print('Ollama Python package installed')"
```

---

## 🚀 Usage

### Option 1: Web Interface (Recommended)

```bash
streamlit run streamlit-app.py
```

Open `http://localhost:8501` in your browser.

### Option 2: Command Line Interface

```bash
python main.py
```

Then enter your banking question when prompted.

---

## 💬 Example Interactions

### Query 1: General Banking
**User**: "What is UPI and how does it work?"

**Response**:
```
UPI (Unified Payments Interface) is a real-time payment system 
developed by the National Payments Corporation of India (NPCI). 
It enables instant bank-to-bank transfers through mobile phones 
using a Virtual Payment Address (VPA). UPI supports multiple 
bank accounts in a single mobile app, making it convenient for 
peer-to-peer and merchant transactions.
```

### Query 2: Security
**User**: "How can I protect myself from phishing?"

**Response**:
```
To protect yourself from phishing attacks, always:
1. Never share OTP, PIN, CVV, or passwords
2. Never click unknown banking links in SMS or email
3. Always verify beneficiaries before transfers
4. Regularly monitor account statements
5. Use strong passwords and enable two-factor authentication
```

### Query 3: Account Types
**User**: "What's the difference between savings and current accounts?"

**Response**:
```
Savings Account:
- Designed for personal savings
- Earns interest on deposits
- Limited monthly transactions

Current Account:
- Designed for businesses
- No interest on deposits
- Unlimited daily transactions
- Higher minimum balance required
```

---

## 📁 Project Structure

```
bankrag/
│
├── streamlit-app.py        # Streamlit web application
├── main.py                 # CLI application
├── banking.txt             # Banking knowledge base
├── requirements.txt        # Python dependencies
├── README.md              # This file
│
└── chroma_db/             # Vector database (auto-generated)
```

---

## 🏗️ How It Works

### 1. Data Ingestion
- The `banking.txt` file contains comprehensive banking facts
- Each line is treated as a separate knowledge chunk

### 2. Vector Embedding
- Each text chunk is converted into a vector embedding using Ollama's embedding API
- Embeddings capture the semantic meaning of the text

### 3. Storage
- Vectors are stored in memory as a list of `(chunk, embedding)` tuples
- Ready for fast similarity search

### 4. Query Processing
- User submits a question
- The query is converted into a vector embedding

### 5. Retrieval
- System finds the most semantically similar chunks using cosine similarity
- Top-K most relevant chunks are retrieved (default: 3)

### 6. Response Generation
- Retrieved chunks are combined into a context prompt
- Ollama generates a response using the language model
- Response is grounded in the retrieved context

---

## 🔧 Configuration

### Changing Models

Edit the model variables in `main.py` or `streamlit-app.py`:

```python
EMBEDDING_MODEL = 'your-embedding-model'
LANGUAGE_MODEL = 'your-language-model'
```

### Changing Top-K Retrieval

Modify the `top_n` parameter in the `retrieve()` function call:

```python
retrieved_knowledge = retrieve(input_query, top_n=5)  # Retrieve 5 chunks
```

### Adding More Knowledge

Add new banking facts to `banking.txt`:

```bash
echo "New banking fact here" >> banking.txt
```

---

## 🧪 Testing

### Test the CLI Version

```bash
python main.py
```

### Test the Web Version

```bash
streamlit run streamlit-app.py
```

---

## 🐛 Troubleshooting

### Ollama Connection Error

```bash
# Check if Ollama is running
ollama list

# Start Ollama
ollama serve
```

### Model Not Found

```bash
# Pull the required models
ollama pull hf.co/CompendiumLabs/bge-base-en-v1.5-gguf
ollama pull hf.co/bartowski/Llama-3.2-1B-Instruct-GGUF
```

### Memory Issues

- Use smaller models
- Reduce the number of chunks in `banking.txt`
- Close other applications

### File Encoding Errors

Ensure `banking.txt` is saved with UTF-8 encoding.

---

## 📊 Performance

| Metric | Value |
|--------|-------|
| **Average Response Time** | 2-5 seconds |
| **Knowledge Chunks** | ~100+ |
| **Top-K Retrieval** | 3 chunks |
| **Memory Usage** | ~500MB |
| **Disk Usage** | ~200MB |

---

## 🔮 Future Enhancements

- [ ] Persistent vector database (ChromaDB)
- [ ] Chat history and conversation memory
- [ ] Source citations in responses
- [ ] Support for PDF and DOCX documents
- [ ] Multi-language support
- [ ] Docker containerization

---

## 🤝 Contributing

Contributions are welcome! Here's how:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

---

<div align="center">

**Built with ❤️ using Python, Ollama, and Streamlit**

⭐ Star this repo if you found it useful!

</div>
