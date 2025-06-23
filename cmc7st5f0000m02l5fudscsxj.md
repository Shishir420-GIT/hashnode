---
title: "Local RAG with Ollama and DeepSeek"
seoTitle: "Local RAG with Ollama and DeepSeek"
seoDescription: "Retrieval-Augmented Generation (RAG) is transforming our understanding of large language models. Instead of expecting an LLM to know every fact, RAG combine"
datePublished: Sun Jun 22 2025 15:04:10 GMT+0000 (Coordinated Universal Time)
cuid: cmc7st5f0000m02l5fudscsxj
slug: local-rag-with-ollama-and-deepseek
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1750604418867/ff5432c3-8a25-4003-b807-7785ad26e89d.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1750604618431/7b20870c-6243-4df2-bc3a-0196b7ae92be.png
tags: rag, ollama, local-llm, gemma, deepseek

---

Retrieval-Augmented Generation (RAG) is transforming our understanding of large language models. Instead of expecting an LLM to know every fact, RAG combines a lightweight, custom knowledge base with powerful generative capabilities. You first ingest your documents, index them for fast similarity search, then ask your model to reason over just the relevant excerpts. The result? Faster, more accurate, and fully private Q&A on any text you choose.

In this post, I’ll show you two implementations of a RAG pipeline I built:

* **A Streamlit-based web UI**, so you can upload and explore documents interactively
    
* **A standalone Python script** for CLI or automated workflows
    

Both share the same core steps, and all use LangChain, Ollama on-device models, and ChromaDB for vector indexing.

## TECH STACK OVERVIEW

• **Python 3.7+** with `python-docx`, `PyPDF2`, `pandas` and `openpyxl`  
• **LangChain** (core + community loaders) for document ingestion and splitting  
• **Ollama Embeddings & ChatOllama** for on-device embeddings and chat inference  
• **ChromaDB** as our local vector database  
• **Streamlit** for building the web interface

## PROJECT STRUCTURE

```bash
.
├── streamlit_app.py    # Interactive RAG demo
├── standalone_script.py       # CLI-only RAG workflow
├── requirements.txt    # All dependencies
└── README.md           # Usage & deployment notes
```

## CORE RAG WORKFLOW

All features—from the UI to the script—follow this four-step pipeline:

1. **Load & split** your source documents into text chunks
    
2. **Build (or load)** a Chroma vector store over those chunks
    
3. **Retrieve** the most relevant chunks for a given query
    
4. **Generate** a final answer with your chosen Ollama chat model
    

## LOADING AND SPLITTING

We support **PDF**, **Word** (`.docx`**plain text** and even **Excel** sheets. Under the hood, each file is written to a temporary path, then passed into the matching LangChain loader. We split documents into 500-character segments with 50-character overlap to maximise context retrieval.

```python
loader = PyPDFLoader(pdf_path)
docs = loader.load()
splitter = RecursiveCharacterTextSplitter(chunk_size=chunk_size, chunk_overlap=chunk_overlap)
splitter.split_documents(docs)
```

## VECTOR STORE CREATION

ChromaDB gives us a lightning-fast, local vector index:

```python
embeddings = OllamaEmbeddings(model="nomic-embed-text")
vectordb   = Chroma(
                collection_name="pdf_collection",
                embedding_function=embeddings,
                persist_directory="./DB/chroma_langchain_db"
             )
vectordb.add_documents(documents=chunks, ids=[uuid1() for _ in chunks])
```

By caching or persisting this directory, repeated runs reuse the same index instead of re-ingesting every time.

## STREAMLIT UI (`streamlit_app.py`)

The Streamlit demo walks you through:

1. **Model selection** via dropdown (e.g. `gemma:2b`, `deepseek-r1:1.5b`)
    
2. **Multi-file upload** (PDF, DOCX, TXT, XLSX)
    
3. **Load & Split** button to chunk all content
    
4. **Build the Vector Store** button to index those chunks
    
5. **Query box** and **Get Answer** button to retrieve and display results
    

Uploads land in your browser session as `UploadedFile` objects; we write them to temporary files so LangChain loaders can treat them like real files.

## STANDALONE SCRIPT (`standalone_script.py`)

For CI pipelines or headless runs, simply call:

```bash
python standalone_script.py
```

It will:

1. Load `./files/Shishir-Resume-PD.pdf` (I used my resume; you can use anything else.).
    
2. Split into chunks
    
3. Build (or load) the Chroma index
    
4. Run a sample query (“What did shishir do using Python?”)
    
5. Print the cleaned response
    

All functionality lives in three reusable functions—`load_and_split`, `create_vector_store`, and `query_and_respond`—So you can drop them into any Python project.

## SETTING UP OLLAMA LOCALLY

To run entirely on-device, you need Ollama installed on your machine.

1. **Install Ollama CLI**
    
    * **macOS**:
        
        ```bash
        brew install ollama
        ```
        
    * **Windows/Linux**:  
        Download the latest package from [https://ollama.com/](https://ollama.com/) and follow the platform and follow the platform-specific installer.
        
2. **Download Required Models**
    
    ```bash
    ollama pull gemma:2b
    ollama pull gemma:7b
    ollama pull deepseek-r1:1.5b
    ollama pull nomic-embed-text
    ```
    
    This step caches the models locally so inference runs offline.
    
3. **(Optional) Run Ollama Daemon for API Access**
    
    ```bash
    ollama serve --port 11434
    ```
    
    If you prefer Python code to call a local REST endpoint, point your client at [`http://localhost:11434`](http://localhost:11434).
    

Your Python scripts and Streamlit app will automatically use the local Ollama socket or REST API—no external network calls required.

## BENEFITS OF KEEPING IT ALL LOCALLY

* **Privacy & Compliance**: Your documents never leave your infrastructure, ideal for sensitive SOPs, internal reports, or proprietary research.
    
* **Latency & Cost**: Local inference eliminates API-call overhead and per-token charges. Queries return in milliseconds rather than seconds.
    
* **Offline Capability**: Work without internet connectivity—perfect for air-gapped environments or field deployments.
    
* **Full Control**: You decide which models and versions to run, when to upgrade, and how to scale on your hardware.
    

## **START RUNNING IT LOCALLY**

1. **Clone the repo:**
    
    ```bash
    git clone https://github.com/shishir/GenAI-Usecases.git
    cd RAG-Examples
    ```
    
2. **Install dependencies:**
    
    ```bash
    pip install -r requirements.txt
    ```
    
3. **Run the Streamlit UI:**
    
    ```bash
    streamlit run streamlit_app.py
    ```
    
    **Or launch the CLI script:**
    
    ```bash
    python standalone_script.py
    ```
    

## And Done!

This Retrieval-Augmented Generation (RAG) lets you combine your documents with on-device LLMs for fast, private, and accurate Q&A. I built both a Streamlit UI and a standalone Python script using LangChain, Ollama, and ChromaDB. Everything runs 100% locally—no API keys, no billing surprises, and sub-second responses. Follow the steps above to clone, install, and get querying in minutes.

---

## TL;DR

* RAG marries retrieval and generative AI for accurate, private Q&A.
    
* Two flavours provided: an interactive Streamlit UI and a CLI-friendly script.
    
* Core steps: load & split documents, build/load Chroma index, retrieve chunks, chat with Ollama.
    
* Supports PDF, Word, text, and Excel—just upload, build, and ask.
    
* Output is sanitised (no `<think>` tags) and model-selectable via a dropdown.
    
* Ready in 20 lines of code; fully open-source and self-hostable.
    

---

---

Thanks for coming this far in the article. I hope I was able to explain the concept well enough. If you face any issues, please feel free to reach out to me; I'd be happy to help.

## 🔗 Let’s stay connected!

[🌐 Linktree](https://linktr.ee/shishirsrivastav)| [🐦 X](https://x.com/shishir_who)| [📸 Instagram](https://www.instagram.com/programmatic.ly)| [▶️ YouTube](https://www.youtube.com/channel/UCCZiCzPtg9pmDwChJ4ROIpA) [✍️ Hashnode](https://hashnode.com/@ShishirSrivastav)| [💻 GitHub](https://github.com/Shishir420-GIT)| [🔗 LinkedIn](https://www.linkedin.com/in/shishir-srivastav)| [🤝 Topmate](https://topmate.io/shishir_srivastav) [🏅 Credly](https://www.credly.com/users/shishir-srivastav-who)

© 2025 Shishir Srivastav. All rights reserved.