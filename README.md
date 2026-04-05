

```markdown
# RAG_Binod - Web-Based Retrieval-Augmented Generation System

A simple yet powerful RAG system that pulls information from web pages, stores it in a vector database, and answers your questions using Groq's Llama 3.1 model. It finds relevant context through semantic search and generates accurate answers with proper source references.

## Features

- Automatically scrapes and cleans content from any web page
- Smart chunking with overlapping sections to preserve context
- Semantic search using Hugging Face embeddings (all-MiniLM-L6-v2)
- Efficient vector storage with Chroma DB
- Fast response generation with Groq's Llama 3.1 8B model
- Shows source URLs so you can verify the information

## Prerequisites

- Python 3.11 or higher
- A Groq API key (you can get it from https://console.groq.com)

## Installation

1. Clone the repository:
```bash
git clone git@github.com:Just-Binod/RAG_Binod.git
cd RAG_Binod
```

2. Create and activate a virtual environment:
```bash
python -m venv .venv

# On macOS/Linux
source .venv/bin/activate

# On Windows
.venv\Scripts\activate
```

3. Install the required packages:
```bash
pip install -r requirements.txt
```

4. Create a `.env` file in the root folder and add your API key:
```env
GROQ_API_KEY=your_groq_api_key_here
```

## Dependencies

- langchain
- langchain-groq
- langchain-huggingface
- langchain-community
- chromadb
- beautifulsoup4
- requests
- python-dotenv
- sentence-transformers

## How It Works

The system follows a straightforward flow:

1. **Document Processing**  
   Fetches web pages, removes unnecessary HTML (scripts, styles, navigation), and converts the content into clean documents.

2. **Chunking**  
   Splits the text into smaller overlapping chunks (500 characters with 50 character overlap) using RecursiveCharacterTextSplitter.

3. **Embedding**  
   Converts each chunk into a 384-dimensional vector using the `all-MiniLM-L6-v2` model.

4. **Vector Store**  
   Saves everything in Chroma DB for fast similarity search.

5. **Retrieval & Generation**  
   When you ask a question, it finds the most relevant chunks and passes them to Llama 3.1 to generate a natural answer.

## Usage

The system comes pre-loaded with a few Wikipedia pages (Artificial Intelligence, Machine Learning, Car, and Life).

Simply run the notebook and ask questions like this:

```python
ask_question("What is artificial intelligence?")
```

### Customizing the System

- **Add your own URLs**:  
  Edit the `urls` list in the notebook and add any web pages you want.

- **Change the number of retrieved chunks**:  
```python
ask_question("Your question here", k=5)   # default is 3
```

## Configuration Options

You can easily tweak the settings:

```python
# Chunking settings
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,
    chunk_overlap=50
)

# Embedding model
embeddings = HuggingFaceEmbeddings(model_name="all-MiniLM-L6-v2")

# LLM settings
llm = ChatGroq(
    temperature=0,                    # 0 = more factual, 1 = more creative
    model_name="llama-3.1-8b-instant"
)
```

## Future Improvements

- Persistent Chroma DB storage
- Caching for web pages
- Support for PDFs and local files
- Web interface using Streamlit or Gradio
- Evaluation metrics for RAG performance
- Hybrid search (semantic + keyword)
- Support for multiple LLM providers

## License

This project is open source and licensed under the MIT License.

## Author

**Just-Binod**  
GitHub: [@Just-Binod](https://github.com/Just-Binod)

## Contributing

Feel free to open issues or submit pull requests. Any contribution or feedback is welcome!

If this project helped you, don't forget to drop a star ⭐
```

This version feels much more natural, readable, and friendly while keeping all the important information. You can directly save it as `README.md`. Let me know if you want any section adjusted!
