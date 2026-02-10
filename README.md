# llama2-medical-chatbot

A local medical Q&A chatbot built with LangChain, Chainlit, FAISS, and a Llama 2 GGML model. It indexes your PDF files, retrieves relevant chunks, and answers questions with sources.

## Project Layout

- data/ - PDF files used as the knowledge base
- vectorstore/db_faiss/ - FAISS index created by ingest.py
- ingest.py - build the vector store from PDFs
- model.py - Chainlit app and retrieval pipeline
- requirements.txt - Python dependencies

## Requirements

- Python 3.9+ recommended
- A Llama 2 GGML model available through CTransformers
- Access to the Llama 2 model on Hugging Face (may require an account and token)

## Setup

1. Create and activate a virtual environment.

```bash
python -m venv .venv
.venv\Scripts\activate
```

2. Install dependencies.

```bash
pip install -r requirements.txt
```

3. Add PDF files to the data/ folder.

## Build the Vector Store

Run the ingestion script to index your PDFs.

```bash
python ingest.py
```

This creates the FAISS index in vectorstore/db_faiss/.

## Run the Chatbot

Start the Chainlit app.

```bash
chainlit run model.py
```

Open the URL shown in the terminal to chat with the bot.

## Configuration

You can adjust these values in the code:

- Vector store path: DB_FAISS_PATH in ingest.py and model.py
- Embedding model: HuggingFaceEmbeddings model_name in ingest.py and model.py
- LLM: CTransformers model settings in model.py

Model download note: model.py uses `TheBloke/Llama-2-7B-Chat-GGML`. If the download fails, make sure your Hugging Face access is approved for Llama 2 and your token is configured.

## Usage Tips

- Add more PDFs and re-run ingest.py to update the knowledge base.
- If you see slow responses, reduce chunk size or max_new_tokens.
- If you get empty answers, verify the PDFs are readable and the vectorstore exists.

## License

MIT
