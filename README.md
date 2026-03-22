📚 Vidya — AI Tutor for Rural India

Vidya is an AI-based tutoring system designed to make quality education accessible even in low-bandwidth environments. It uses a custom context pruning approach to reduce unnecessary data processing, lowering LLM token usage by up to 85–92% while still providing accurate answers from textbook content.

🌿 Overview

The project has two main components:

index.html – A lightweight browser-based application where users can upload any textbook PDF and ask questions interactively.
context_pruning_rag.ipynb – A Google Colab notebook that demonstrates the full pipeline and compares performance with a standard Retrieval-Augmented Generation (RAG) system.
🧠 Core Concept: Context Pruning

Traditional RAG systems retrieve multiple chunks of text for every query, often including irrelevant information. This increases both token usage and cost.

Vidya improves this by introducing context pruning, where the system first identifies the most relevant chapters before sending content to the language model.

Workflow
The user asks a question
The system analyzes chapter titles and content using keyword matching
Only the top 1–2 relevant chapters are selected
Filtered content is sent to the LLM
The model generates a precise answer based on the selected context

This approach reduces the amount of text sent from around 40,000 tokens to ~3,000 tokens per query.

🚀 How to Use
Web Application
Get a free API key from Groq
Open index.html in a browser
Enter the API key
Upload a textbook PDF
Wait for the one-time OCR process
Start asking questions

The app uses OCR (Tesseract.js), allowing it to work even with scanned or poorly encoded PDFs.

Colab Notebook
Open the notebook in Google Colab
Run all cells in order
Upload a PDF file
Execute test queries
Compare results between baseline RAG and context pruning

A summary table shows token usage and cost savings for each query.

⚙️ Technologies Used
Web App
PDF.js – renders PDF pages in the browser
Tesseract.js – extracts text using OCR
Groq API (LLaMA 3.1) – generates answers
HTML, CSS, JavaScript – frontend implementation
Notebook
LangChain – builds the RAG pipeline
FAISS – vector database for baseline retrieval
HuggingFace Embeddings – semantic encoding
pdfplumber / PyPDF – PDF text extraction
LangChain-Groq – LLM integration
📊 Performance Comparison
Metric	Baseline RAG	Context Pruning
Tokens per query	~40,000	~3,000
Data sent	~160 KB	~12 KB
Cost per query	~$0.000200	~$0.000015
Reduction	—	85–92%
📁 Project Structure
vidya/
├── index.html
├── context_pruning_rag.ipynb
└── README.md
🌐 Designed for Low-Bandwidth Use
OCR runs only once during setup
Each query sends minimal text (around 4–6 KB)
No images are transmitted after processing
Works efficiently even on slow internet connections
🔑 API Key Setup
Sign up on Groq
Generate an API key
Paste it into the web app or notebook

The free tier is sufficient for regular usage.

🧮 Chapter Selection Method

Instead of relying on embeddings for pruning, the system uses a lightweight scoring approach:

Matches between question keywords and chapter titles are given higher weight
Matches within chapter content are given lower weight

The top-ranked chapters are selected, and all others are ignored.

⚠️ Limitations
OCR processes only a subset of pages per chapter
Chapter detection depends on standard formatting
API key is not stored permanently
Refreshing the page requires reprocessing
📄 License

This project is released under the MIT License and can be freely used and modified.
