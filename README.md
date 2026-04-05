Here's a comprehensive README file for your RAG (Retrieval-Augmented Generation) system:

```markdown
# RAG_Binod - Web-Based Retrieval-Augmented Generation System

A powerful RAG system that extracts information from web pages, stores it in a vector database, and answers questions using Groq's LLM (Llama 3.1). The system uses semantic search to retrieve relevant context before generating accurate, source-backed responses.

##  Features

- **Web Scraping**: Automatically fetches and cleans content from web pages
- **Intelligent Chunking**: Splits documents into manageable, overlapping chunks for better context
- **Semantic Search**: Uses HuggingFace embeddings (all-MiniLM-L6-v2) for meaningful text representation
- **Vector Storage**: Implements Chroma DB for efficient similarity search
- **LLM Integration**: Leverages Groq's Llama 3.1 8B model for high-quality responses
- **Source Attribution**: Retrieved chunks include source URLs for transparency

##  Prerequisites

- Python 3.11+
- Groq API key (sign up at [console.groq.com](https://console.groq.com))

## Installation

1. **Clone the repository**
```bash
git clone git@github.com:Just-Binod/RAG_Binod.git
cd RAG_Binod
```

2. **Create and activate a virtual environment**
```bash
python -m venv .venv
source .venv/bin/activate  # On macOS/Linux
# or
.venv\Scripts\activate  # On Windows
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Set up environment variables**
Create a `.env` file in the root directory:
```env
GROQ_API_KEY=your_groq_api_key_here
```

##  Dependencies

```
langchain
langchain-groq
langchain-huggingface
langchain-community
chromadb
beautifulsoup4
requests
python-dotenv
sentence-transformers
```

##  Architecture

1. **Document Processing**
   - Fetch HTML content from configured URLs
   - Clean HTML (remove scripts, styles, navigation elements)
   - Convert to Document objects with metadata

2. **Chunking Strategy**
   - RecursiveCharacterTextSplitter
   - Chunk size: 500 characters
   - Overlap: 50 characters (maintains context between chunks)

3. **Embedding Model**
   - Model: `all-MiniLM-L6-v2` (Sentence Transformers)
   - Creates 384-dimensional vector representations

4. **Vector Store**
   - Backend: Chroma DB
   - Stores document chunks with their embeddings

5. **Retrieval & Generation**
   - Semantic similarity search (k=3 by default)
   - Context-aware prompting
   - Groq Llama 3.1 8B for answer generation

## 💻 Usage

### Basic Usage

```python
# Import the notebook or run the cells in order
# The system is pre-configured with 4 Wikipedia pages:
# - Artificial Intelligence
# - Machine Learning  
# - Car
# - Life

# Query the system
ask_question("What is artificial intelligence?")
```

### Custom URLs

Modify the `urls` list in the notebook:
```python
urls = [
    "https://your-website.com/page1",
    "https://your-website.com/page2",
    # Add more URLs as needed
]
```

### Adjust Search Parameters

```python
# Change number of retrieved chunks
ask_question("Your question", k=5)  # Default is 3
```

## 📊 How It Works

1. **Indexing Phase**
   - Fetches and cleans web content
   - Splits text into overlapping chunks
   - Generates embeddings for each chunk
   - Stores in Chroma DB

2. **Query Phase**
   - Converts user question to embedding
   - Finds most similar chunks in vector store
   - Retrieves top-k relevant documents
   - Constructs context-aware prompt
   - Generates answer using Groq LLM

## 🔧 Configuration Options

### Chunk Size Adjustment
```python
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,  # Adjust based on your needs
    chunk_overlap=50  # 10-20% of chunk size recommended
)
```

### Embedding Model
```python
embeddings = HuggingFaceEmbeddings(
    model_name="all-MiniLM-L6-v2"  # Alternative: "all-mpnet-base-v2" (larger)
)
```

### LLM Model
```python
llm = ChatGroq(
    temperature=0,  # 0 = deterministic, 1 = creative
    model_name="llama-3.1-8b-instant"  # Or "mixtral-8x7b-32768"
)
```

## 📝 Example Output

```
Retrieved Evidence:

--- Chunk 1 ---
Source: https://en.wikipedia.org/wiki/Artificial_intelligence
Artificial intelligence (AI) is the intelligence of machines...

Answer:
According to the provided context, artificial intelligence refers to the 
"intelligence of machines".
```

## 🐛 Troubleshooting

### Git Push Issues (Port 22 Blocked)
If you encounter `Connection refused` on port 22:
```bash
# Option 1: Update remote URL
git remote set-url origin ssh://git@ssh.github.com:443/Just-Binod/RAG_Binod.git

# Option 2: Configure SSH (recommended)
echo -e "Host github.com\n    Hostname ssh.github.com\n    Port 443\n    User git" >> ~/.ssh/config
```

### Missing GROQ_API_KEY
Ensure your `.env` file exists and contains:
```
GROQ_API_KEY=your_actual_key
```

### Chroma DB Issues
```bash
pip install chromadb --upgrade
```

##  Future Improvements

- [ ] Add persistent Chroma DB storage
- [ ] Implement caching for fetched web pages
- [ ] Add support for PDF and local documents
- [ ] Create web interface (Streamlit/Gradio)
- [ ] Add evaluation metrics for RAG quality
- [ ] Implement hybrid search (semantic + keyword)
- [ ] Add support for multiple LLM providers

## 📄 License

This project is open source and available under the MIT License.

## 👤 Author

**Just-Binod**
- GitHub: [@Just-Binod](https://github.com/Just-Binod)

## Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/Just-Binod/RAG_Binod/issues).

## ⭐ Show Your Support

Give a ⭐️ if this project helped you!
```

This README provides comprehensive documentation for your RAG system, including setup instructions, architecture explanation, usage examples, and troubleshooting tips. You can save this as `README.md` in your repository root.
