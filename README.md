RAG-Based PDF Question Answering Chatbot
A document-based question-answering chatbot built with Python, LangChain, ChromaDB, Hugging Face embeddings, and the Groq API. Upload a PDF in Google Colab and ask questions about its contents. The chatbot retrieves relevant passages and uses a large language model (LLM) to generate answers with source-page references.
Features
- Upload and process one PDF at a time in Google Colab.
- Extract page text using PyPDFLoader.
- Split text into overlapping chunks for retrieval.
- Generate semantic embeddings with sentence-transformers/all-MiniLM-L6-v2.
- Store and search document chunks in ChromaDB.
- Retrieve the top three relevant chunks for each question.
- Generate context-based responses using Groq and openai/gpt-oss-120b.
- Display the PDF filename and source page numbers.
- Ask questions through a simple ipywidgets interface.
- Instruct the model to say when an answer cannot be found in the supplied context.
Technologies
Purpose	Technology
Language and environment	Python, Google Colab
RAG orchestration	LangChain
PDF text extraction	PyPDF (PyPDFLoader)
Text splitting	RecursiveCharacterTextSplitter
Embeddings	Hugging Face Sentence Transformers (all-MiniLM-L6-v2)
Vector store	ChromaDB (langchain-chroma)
LLM provider	Groq API (langchain-groq)
LLM	openai/gpt-oss-120b
User interface	ipywidgets


How It Works
Upload PDF
    ↓
Extract text and page metadata
    ↓
Split into chunks (1,000 characters; 200 overlap)
    ↓
Generate embeddings
    ↓
Store chunks in ChromaDB
    ↓
User asks a question
    ↓
Retrieve top 3 matching chunks
    ↓
Combine question + retrieved context
    ↓
Groq-hosted LLM generates an answer
    ↓
Show answer and source pages
Getting Started (Google Colab)
1. Open the .ipynb notebook from this repository in Google Colab.
2. Create a Groq API key using your own Groq account.
3. In Colab, open Secrets (key icon in the left sidebar). Add a secret named GROQ_API_KEY and grant the notebook access to it. Never paste the key directly into the notebook or commit it to GitHub.
4. Run the notebook cells in order. The installation cell installs the required libraries:
   !pip -q install langchain langchain-community langchain-groq langchain-huggingface langchain-chroma chromadb pypdf sentence-transformers
5. When prompted, upload a text-based PDF.
6. Allow the notebook to extract text, build the ChromaDB vector store, and initialize the RAG pipeline.
7. Type a question into the notebook's text field and click Ask to see an answer and source pages.
Note: The notebook is designed for Google Colab, not as a deployed website or standalone application. It needs internet access for the Groq API and may require access to the specified model.
Example Questions
- Document-related: “What is this document about?” — the chatbot uses relevant retrieved text to answer.
- Not in the document: “Who is the current Prime Minister of Japan?” — the notebook's test expects: “I could not find this information in the uploaded document.”
Answers depend on the uploaded PDF and the model's behavior; the context-only instruction reduces but does not eliminate unsupported answers.
Project Structure
RAG-Chatbot/
├── README.md
└── Rag_Chatbot.ipynb
The notebook filename above is the recommended GitHub name; rename your downloaded file accordingly if needed.
Limitations
- Supports one uploaded PDF at a time.
- Scanned or image-only PDFs may need OCR.
- Retrieval uses a fixed k=3 and depends on chunking and embedding quality.
- Requires an internet connection and Groq API access.
- The ipywidgets interface is intended for demonstration within Colab.
- Source references show retrieved pages; they do not independently verify every statement in an answer.
Future Improvements
- Support multiple PDF uploads.
- Add OCR for scanned documents.
- Improve retrieval evaluation and citation quality.
- Create a standalone web interface.
About
This project demonstrates a complete introductory Retrieval-Augmented Generation (RAG) workflow: document loading, text chunking, embeddings, vector retrieval, LLM prompting, and an interactive notebook-based question-answering interface.
