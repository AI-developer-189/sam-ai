# SAM — Smart Agentic Multimodal

> **One intelligent assistant. Multiple AI capabilities.**

SAM is a **multimodal agentic AI assistant** built with **LangGraph, Qwen, Retrieval-Augmented Generation (RAG), FAISS, OCR, Stable Diffusion, and Gradio**.

It brings multiple AI capabilities together in a single conversational interface, allowing users to ask questions, interact with documents and images, perform calculations, and generate images.

---

## ✨ What is SAM?

**SAM** stands for **Smart Agentic Multimodal**.

The name is also inspired by **Sangamithran**, representing the idea of a companion that brings different capabilities together.

SAM uses an **agentic workflow** to understand a user's request and route it to the appropriate specialized tool.

Instead of building separate applications for different tasks, SAM combines them into one AI assistant.

---

## 🚀 Features

### 💬 General AI Assistant

SAM can answer general questions using:

* Qwen2.5-1.5B-Instruct
* Hugging Face Transformers

Example:

```text
What is Retrieval-Augmented Generation?
```

---

### 📚 Document Question Answering with RAG

SAM can process uploaded documents and answer questions using **Retrieval-Augmented Generation**.

The RAG pipeline includes:

```text
Document
   ↓
Text Extraction
   ↓
Text Chunking
   ↓
Embeddings
   ↓
FAISS Vector Store
   ↓
Similarity Retrieval
   ↓
Qwen LLM
   ↓
Context-Aware Answer
```

For scanned documents where normal text extraction is insufficient, the system can use **Tesseract OCR**.

---

### 🖼️ Image-to-Text

SAM can extract text from uploaded images using **Tesseract OCR**.

Supported image formats include:

* PNG
* JPG
* JPEG
* WEBP
* BMP
* TIFF

Example:

```text
Upload an image → Extract the text
```

---

### 🎨 Text-to-Image Generation

SAM can generate images from natural-language prompts.

The workflow uses:

```text
User Prompt
     ↓
Qwen2.5-VL-3B-Instruct
     ↓
Prompt Enhancement
     ↓
Stable Diffusion v1.5
     ↓
Generated Image
```

Example:

```text
Create a futuristic city at night with flying vehicles.
```

---

### 🧮 Calculator

SAM can route arithmetic expressions to a dedicated calculator tool.

Example:

```text
125 * 8 + 250
```

---

## 🧠 Agentic Architecture

SAM uses **LangGraph** to orchestrate its different capabilities.

```text
                         ┌───────────────┐
                         │  User Query   │
                         └───────┬───────┘
                                 ↓
                     ┌─────────────────────┐
                     │   SAM Agent Core    │
                     │      LangGraph      │
                     └──────────┬──────────┘
                                ↓
              ┌─────────────────┼─────────────────┐
              │                 │                 │
              ↓                 ↓                 ↓
        Direct Answer       RAG Tool          Vision Tool
              │                 │                 │
              │                 │          Image → Text
              │                 │
              ↓                 ↓
        Qwen LLM          FAISS + Qwen
              │                 │
              └────────┬────────┘
                       │
             ┌─────────┴─────────┐
             ↓                   ↓
       Calculator Tool     Text → Image
                                 │
                         Qwen2.5-VL
                                 ↓
                       Stable Diffusion
                                 │
                                 ↓
                         Generated Image
```

### Tool-based workflow

SAM can route requests to specialized capabilities including:

```text
direct_tool
calculator_tool
rag_tool
image_to_text_tool
text_to_image_tool
```

This tool-based architecture allows each capability to perform a specific task while LangGraph manages the overall workflow.

---

## 🛠️ Technology Stack

| Technology                 | Purpose                                           |
| -------------------------- | ------------------------------------------------- |
| **Python**                 | Core development                                  |
| **LangGraph**              | Agent workflow orchestration                      |
| **LangChain**              | RAG and AI components                             |
| **Qwen2.5-1.5B-Instruct**  | General LLM                                       |
| **Qwen2.5-VL-3B-Instruct** | Vision-language processing and prompt enhancement |
| **Sentence Transformers**  | Text embeddings                                   |
| **FAISS**                  | Vector similarity search                          |
| **Tesseract OCR**          | Text extraction from images/scanned documents     |
| **PyMuPDF**                | PDF processing and rendering                      |
| **PyPDF**                  | PDF text extraction                               |
| **Transformers**           | Model loading and inference                       |
| **PyTorch**                | Deep learning framework                           |
| **Stable Diffusion v1.5**  | Image generation                                  |
| **Gradio**                 | Web interface                                     |

---

## 🤖 AI Models

### Language Model

```text
Qwen/Qwen2.5-1.5B-Instruct
```

Used for general conversational responses and RAG-based answer generation.

### Vision-Language Model

```text
Qwen/Qwen2.5-VL-3B-Instruct
```

Used for vision-language processing and improving prompts for image generation.

### Embedding Model

```text
sentence-transformers/all-MiniLM-L6-v2
```

Used to convert text chunks into vector embeddings for semantic retrieval.

### Image Generation Model

```text
runwayml/stable-diffusion-v1-5
```

Used for text-to-image generation.

---

## 🔎 RAG Pipeline

SAM's document-question-answering system follows these steps:

### 1. Document Processing

Uploaded PDFs are processed to extract their textual content.

### 2. OCR Fallback

When sufficient text cannot be extracted from a document, the pages can be rendered and processed using Tesseract OCR.

### 3. Text Chunking

The extracted content is divided into smaller chunks for efficient retrieval.

```python
RecursiveCharacterTextSplitter(
    chunk_size=700,
    chunk_overlap=100
)
```

### 4. Embedding Generation

Each chunk is converted into an embedding using:

```text
all-MiniLM-L6-v2
```

### 5. Vector Storage

Embeddings are stored in a **FAISS** vector index.

### 6. Similarity Retrieval

Relevant chunks are retrieved based on the user's question.

### 7. Response Generation

The retrieved context is provided to the Qwen language model to generate the final response.

---

## 🖥️ Interface

SAM uses **Gradio** to provide an interactive conversational interface.

The interface supports:

* 💬 Chat-based interaction
* 📄 PDF upload
* 🖼️ Image upload
* 📚 Document-based questions
* 🔤 OCR
* 🧮 Calculations
* 🎨 Image generation
* 🧹 Chat clearing

---

## 📂 Project Structure

A recommended repository structure is:

```text
SAM/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebook/
│   └── SAM.ipynb
│
├── data/
│   └── sample_documents/
│
└── assets/
    └── screenshots/
```

> Keep model weights, generated images, uploaded documents, cache folders, and other large temporary files out of GitHub.

---

## ⚙️ Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/sam.git
cd sam
```

Install the dependencies:

```bash
pip install -U transformers accelerate sentence-transformers \
langchain langchain-community langchain-huggingface \
langchain-text-splitters langgraph faiss-cpu pypdf pymupdf \
pytesseract huggingface_hub gradio diffusers safetensors ftfy \
qwen-vl-utils
```

Install OpenAI CLIP:

```bash
pip install git+https://github.com/openai/CLIP.git
```

---

## 🔤 Tesseract OCR

Tesseract OCR is required for image text extraction and OCR-based document processing.

### Google Colab

```bash
apt-get update
apt-get install -y tesseract-ocr
```

For local Windows installation, install Tesseract separately and configure its executable path if required.

---

## ▶️ Running SAM

The current implementation can be run using the provided Jupyter/Google Colab notebook.

Open:

```text
notebook/SAM.ipynb
```

Run the cells sequentially.

The Gradio interface will then launch and provide an interactive interface for SAM.

A GPU runtime is recommended because the project uses transformer models and Stable Diffusion.

---

## 💡 Example Interactions

### General AI

```text
What is Agentic AI?
```

### Document RAG

Upload a PDF and ask:

```text
Summarize this document.
```

or:

```text
What are the important points in this document?
```

### Image OCR

Upload an image:

```text
Extract the text from this image.
```

### Calculator

```text
250 * 16 + 500
```

### Image Generation

```text
Generate an image of an AI robot working in a futuristic laboratory.
```

---

## 🎯 Objective

The primary objective of SAM is to demonstrate how multiple modern AI technologies can be integrated into a **single agentic multimodal system**.

The project combines:

* Agentic AI
* Large Language Models
* Retrieval-Augmented Generation
* Vector databases
* Multimodal AI
* Computer vision
* OCR
* Image generation
* Tool-based orchestration

into one unified application.

---

## 🔮 Future Enhancements

Possible future improvements include:

* 🌐 Web search integration
* 🧠 Persistent conversational memory
* 📚 Multiple-document RAG
* 🔗 Source citations for retrieved information
* 🎤 Speech-to-text
* 🔊 Text-to-speech
* ⚡ Streaming responses
* 👁️ Advanced image understanding
* 🚀 FastAPI backend
* ☁️ Cloud deployment
* 🔐 User authentication
* 📊 RAG evaluation and monitoring

---

## 📌 Project Highlights

```text
✓ Agentic AI
✓ LangGraph Workflow
✓ 5 Specialized Tools
✓ Multimodal Interaction
✓ Retrieval-Augmented Generation
✓ FAISS Vector Search
✓ OCR
✓ Vision-Language Model
✓ Text-to-Image Generation
✓ Gradio Interface
```

---

## 👨‍💻 Author

**Vishwa A**

**B.Tech — Artificial Intelligence & Data Science**

---

## ⭐ If You Like the Project

If SAM helped you understand how agentic and multimodal AI systems can be built, consider giving this repository a ⭐.

Feedback and contributions are welcome.

---

### SAM

**Smart Agentic Multimodal**

> *One assistant. Multiple capabilities.*
