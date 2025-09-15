1) Short intro (how we’ll solve it — RAG + context engineering)

We will solve this by using Retrieval-Augmented Generation (RAG) but replace heavy prompt-engineering with context engineering: for every user query we gather only the most relevant curated text (knowledge base chunks, docs, examples), assemble that as context with a small customizable prompt, and send both to the LLM. That keeps the model focused, reduces hallucination, and produces higher-quality answers because the LLM reasons over explicit supporting text instead of relying only on handcrafted prompt tricks.

2) Knowledge base — where data comes from, embedding choice, and why

Data sources: corporate docs, textbooks, FAQs, API docs, past Q&A logs, scraped webpages (cleaned), PDFs, and trusted public datasets. Convert each source to plain text → split into chunks (200–800 tokens, overlap ~50 tokens) → store chunk metadata (source, page, offset).

Embedding model (one choice): sentence-transformers/all-MiniLM-L6-v2 (SBERT).
Why this one?

Small and very fast for bulk indexing (lightweight for production and dev). 
Hugging Face
+1

Good semantic quality for typical RAG tasks with low storage and compute cost; easy to run locally or in a small server. 
Milvus

How it creates mapping: each text chunk → embedding(vector) (e.g., 384-dim) and you store those vectors in a vector DB (FAISS/Chroma/Milvus). Retrieval = nearest-neighbor similarity (cosine or inner product) between query vector and chunk vectors.

Short code snippet — create embeddings & index with sentence-transformers + FAISS: