# 📄 RAG System with LangChain and OpenAI

This project demonstrates how to build a **Retrieval-Augmented Generation (RAG)** system using LangChain, OpenAI's GPT model, and a local PDF document as a source of knowledge. The workflow includes document loading, chunking, embedding, storing in a vector database (Chroma), and querying with contextual compression or hierarchical retrieval strategies.

---

## 📦 Requirements

Install the dependencies with:

```bash
pip install -r requirements.txt
```

Or manually install key libraries:

```bash
pip install python-dotenv langchain openai chromadb cohere
```

---

## 🔐 Environment Variables

To avoid exposing the `OPENAI_API_KEY`, the project uses a `.env` file. Create a `.env` file in the same directory as the notebook (`parentRAG.ipynb`) with the following content:

```
OPENAI_API_KEY=your_openai_api_key
```

If you use Cohere for reranking, include:

```
COHERE_API_KEY=your_cohere_api_key
```

---

## 🧠 Features

- Load and split PDF documents into small manageable chunks.
- Use **OpenAI embeddings** to convert text into vector representations.
- Store document vectors using **ChromaDB**.
- Query and retrieve relevant chunks using two different retrieval methods:
  - **ParentDocumentRetriever** (hierarchical retrieval).
  - **ContextualCompressionRetriever** with **Cohere reranking** (compressed retrieval).
- Use **ChatGPT (gpt-3.5-turbo)** to generate answers using the retrieved context.
- Designed for legal and technical question-answering tasks.

---

## 📁 Structure

```
📄 parentRAG.ipynb      # Main notebook implementing the RAG pipeline
📄 DOC-SF238339076816-20230503.pdf   # Source document (PDF)
📁 chieldVectorDB       # Vector store for Parent Retriever
📁 naiveDB              # Vector store for basic retriever
.env                    # Environment variables
```

---

## ⚙️ Execution Flow

1. **Load PDF** with `PyPDFLoader`
2. **Split into Chunks** using `RecursiveCharacterTextSplitter`
3. **Embed and Store**:
   - Parent-child structure in Chroma + InMemory store.
   - Flat structure with reranking (Cohere).
4. **Setup Retrieval Chain**:
   - `ParentDocumentRetriever` for hierarchical lookup.
   - `ContextualCompressionRetriever` with Cohere rerank for precise context.
5. **Define Prompt** and run RAG pipeline to answer custom questions.

---

## 🧪 Sample Query

```python
parent_chain_retrieval.invoke("What are the main risks of the AI legal framework?")
compressor_retrieval_chain.invoke("What are the main risks of the AI legal framework?")
```

---

## 📌 Notes

- The `.env` setup is mandatory to run the OpenAI-based LLM and embeddings.
- The PDF file used is assumed to be legal documentation; the model answers questions based on its content.
- Adjust chunk sizes, overlap, and retriever parameters to fit your needs and performance.
