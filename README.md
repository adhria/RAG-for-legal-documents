
# AI-Powered Document Q&A

A Retrieval-Augmented Generation (RAG) application that lets you upload a PDF and ask questions about its content using OpenAI's language models and LangChain.

## How It Works

1. Upload a PDF through the Streamlit interface
2. The document is split into chunks and embedded using OpenAI's `text-embedding-ada-002` model
3. Embeddings are stored in a FAISS vector database for fast similarity search
4. When you ask a question, relevant chunks are retrieved and passed to `gpt-4o-mini` to generate an answer

## Prerequisites

- Python 3.8+
- An OpenAI API key

## Installation

```bash
git clone <your-repo-url>
cd <repo-folder>
pip install -r requirements.txt
```

### Required packages

```
langchain
langchain-community
langchain-openai
langchain-core
faiss-cpu
streamlit
pypdf
```

## Configuration

Add your OpenAI API key to `scripts/secret.py`:

```python
OPENAI_KEY = "your-openai-api-key"
```

> **Note:** Do not commit `scripts/secret.py` to version control. Add it to your `.gitignore`.

## Project Structure

```
├── app.py                  # Main Streamlit application
├── scripts/
│   ├── secret.py           # OpenAI API key (not committed)
│   └── document_loader.py  # PDF loading and chunking logic
├── requirements.txt
└── README.md
```

## Running the App

```bash
streamlit run app.py
```

Then open [http://localhost:8501](http://localhost:8501) in your browser.

## Usage

1. Launch the app and upload a PDF file
2. Wait for the document to finish processing
3. Type a question in the input box and press Enter
4. The app will return an answer based on the document's content

## Notes

- If the answer is not found in the document, the model will say so rather than hallucinate
- As an alternative to OpenAI embeddings, `HuggingFaceEmbeddings` with `sentence-transformers/all-MiniLM-L6-v2` can be used for a fully local, free embedding option (see commented code in `app.py`)
