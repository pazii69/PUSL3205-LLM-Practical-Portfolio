# Lab 05 — Retrieval-Augmented Generation (RAG) Pipeline

## 1. Laboratory Session
- **Lab number:** 05
- **Title:** Building a RAG Architecture for Document Q&A
- **Environment:** Google Colab, Python 3
- **Libraries:** LangChain, ChromaDB, Hugging Face (transformers, sentence-transformers), PyPDF

## 2. Objective
The objective of this laboratory activity was to build a Retrieval-Augmented Generation (RAG) pipeline. RAG improves LLM accuracy by retrieving relevant context from external documents before generating an answer. The specific task was to build a baseline Q&A system over a university document and extend it to allow users to upload their own PDF files dynamically.

## 3. Tasks and Implementation
1. **Environment Setup:** Installed LangChain, ChromaDB, and Hugging Face tools. Note: Colab's pre-installed packages produced dependency warnings, but the core RAG libraries functioned correctly.
2. **Document Ingestion:** Created a baseline text document. Used LangChain's `RecursiveCharacterTextSplitter` to chunk the document into manageable segments (chunk_size=100, overlap=10).
3. **Embedding & Vector Store:** Converted the text chunks into vector representations using the `all-MiniLM-L6-v2` sentence-transformer model. Stored these vectors in a ChromaDB vector store for fast similarity search.
4. **LLM Integration:** Used the lightweight `google/flan-t5-base` model via Hugging Face to generate answers based on the retrieved context.
5. **Modification (User Upload):** Extended the pipeline to include a file uploader using `google.colab.files`. When a user uploads a PDF, the system uses `PyPDFLoader` to extract the text, splits it, embeds it, and adds it to the existing ChromaDB vector store. It then prompts the user for a question and answers it using the newly added knowledge.

## 4. Results and Evidence
- **Baseline Test:** When asked "What is the module PUSL3205 about?", the RAG system successfully retrieved the relevant chunk and accurately answered: *"Large Language Models and Generative AI"*.
- **Custom PDF Test:** I uploaded the `Lab sheet 5.pdf` document. The system processed the PDF and successfully added **57 new chunks** to the ChromaDB vector store. When asked "What is this document about?", it generated a response indicating it was about "Science/Tech".

*(See `/screenshots` folder for the successful Q&A outputs and the PDF upload demonstration).*

## 5. Observations
- **Retrieval Quality:** The system successfully avoided hallucinations because it was strictly grounded to the provided text. If the answer wasn't in the document, it would state that it doesn't know.
- **Chunking Trade-offs:** We used small chunks (100 characters). This ensures precise retrieval, but sometimes splits context across chunks. Larger chunks provide more context but might introduce noise.
- **Model Limitations:** `flan-t5-base` is a very small model (approx. 250M parameters). While it successfully extracts answers from the context, it sometimes generates slightly disjointed or overly brief sentences (like "Science/Tech") compared to larger models like Llama-3 or GPT-4.
- **The Power of RAG:** We did not need to fine-tune any model (unlike Lab 4) to make it know about our specific PDF. We simply changed the external database, which is vastly more efficient for factual documents.

## 6. Learning Outcomes
- Can design and implement an end-to-end RAG pipeline.
- Understand the role of document loaders, text splitters, embedding models, and vector databases.
- Can dynamically ingest new user data (PDFs) into a live vector store.
- Can use Hugging Face pipelines to ground LLM generation in retrieved context.
