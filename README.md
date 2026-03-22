Preview
Code
Blame
151 lines (107 loc) · 4.61 KB
ð Vidya â AI Tutor for Rural India
An intelligent tutoring system using Context Pruning to reduce LLM token usage by 85–92%, making AI-powered education viable on 2G networks.


ð¿ What is Vidya?

Vidya is a two-part project:

File What it is
index.html A single-file web app â upload any PDF textbook and ask questions instantly
context_pruning_rag.
ipynb A Google Colab notebook implementing the full Context Pruning RAG pipeline with cost comparison

ð§ The Core Technique: Context Pruning
Standard RAG sends the entire book as context on every query.
Context Pruning identifies relevant chapters first, then sends only those â cutting tokens by 85–92%.

Student Question
â
Context Pruning â scores each chapter by keyword match (no API call)
â
Relevant Chapter(s) Only â 1-2 chapters instead of all 13
â
Groq LLM â receives ~3,000 tokens instead of ~40,000
â
Answer from your actual textbook

ð How to Use
Web App (education_tutor.html)
Get a free Groq API key at console.groq.com
Open index.html in any modern browser (Chrome, Firefox, Edge)
Enter your Groq API key and click Save
Upload your PDF textbook
Wait ~1–2 minutes for OCR to extract text from all chapters (one-time setup)
Ask any question â answers are instant after setup!

Works with any PDF â including PDFs with broken font encoding (like NCERT textbooks), because text is extracted using Tesseract.js OCR, not native PDF text parsing.


Colab Notebook (context_pruning_rag.
ipynb)
Open in Google Colab
Run all cells in order
Upload your PDF when prompted
The notebook runs both the baseline RAG and Context Pruning systems on test questions
A cost summary table shows the token and cost savings

âï¸ Technologies Used
Web App
Technology Purpose
PDF.js (Mozilla) Renders PDF pages to Canvas in the browser
Tesseract.js v5 Browser-based OCR engine (WebAssembly) â reads pages visually, bypasses broken fonts
Groq API + llama-3.1-8b-instant Fast, cheap LLM for generating answers from text
Plain HTML / CSS / JS No frameworks, no build tools, no server needed

Colab Notebook
Technology Purpose
LangChain RAG pipeline framework
pdfplumber PDF text extraction
FAISS Vector store for baseline RAG
HuggingFace Embeddings sentence-transformers/all-MiniLM-L6-v2
LangChain-Groq Groq LLM integration

ð Cost Comparison
Metric Baseline RAG Context Pruning
Tokens per query ~40,000 ~3,000
Data per query ~160 KB ~12 KB
Cost per query ~$0.000200 ~$0.000015
Token reduction — 85–92%

ð Repository Structure
vidya/
âââ education_tutor.html â Complete web app (single file, open in browser)
âââ context_pruning_rag.
ipynb â Google Colab notebook with cost comparison
âââ README.md

ð Why 2G-Friendly?

Setup OCR happens once (ideally on WiFi) â ~1–2 minutes
Every query after setup sends only ~4–6 KB of plain text to Groq
No images are transmitted at query time
A 2G connection (50–100 kbps) handles 4–6 KB in under 1 second

ð Getting a Groq API Key
Go to console.groq.com
Sign up for a free account
Navigate to API Keys â Create API Key
Copy the key (starts with gsk_...)
Paste it into the web app or the notebook
Groq's free tier is sufficient for hundreds of queries.


ð How Context Pruning Scores Chapters
for each chapter:
score = 0
for each keyword in question (words > 3 chars):
if keyword in chapter_title: score += 3 # strong signal
if keyword in chapter_text: score += 1 # weaker signal

select top 2 chapters by score
prune all others
This runs entirely in JavaScript (web app) or Python (notebook) â no extra API call needed for pruning.


â ï¸ Limitations
OCR samples 3 pages per chapter (first, middle, last).
Content on other pages may be missed.
Chapter detection uses regex for "Chapter N" headings.
Non-standard formats fall back to 20-page equal splits.
The Groq API key is stored in browser memory only â not persisted between sessions.

Refreshing the page requires re-running OCR.


ð License
MIT â free to use, modify, and distribute.
