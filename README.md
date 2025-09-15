# AI-Powered RAG ➜ Slides ➜ Manim Video Pipeline

## Solution in Plain English

I combine Retrieval-Augmented Generation (RAG) with context engineering. Instead of crafting perfect prompts, I fetch the right text chunks and hand them to the LLM with the user's question. With full context, it writes clear slides and Python code for Manim animations. Result: accurate, personalized videos with minimal manual work.

## Building the Knowledge Base

| Step | What I do | Why this choice |
|------|-----------|-----------------|
| Gather data | Scrape public textbooks / open course notes (PDF → text) | Educational sources match student queries |
| Chunk & clean | Split into ~500-token chunks to keep semantic meaning | Smaller chunks index & retrieve better |
| Embed | *Model:* text-embedding-ada-002 (OpenAI) | High quality, cheap, widely used in RAG tutorials |
| Store | *Vector DB:* Pinecone | Scales to millions of vectors with milliseconds latency |

![architecture](https://github.com/user-attachments/assets/00b51b1e-55ee-4845-bd60-74cab7b78b6c)

```python
def retrieve(query, model, index, docs_meta, top_k=5):
    q_emb = model.encode([query], convert_to_numpy=True)
    faiss.normalize_L2(q_emb)
    scores, ids = index.search(q_emb, top_k)
    results = []
    for score, idx in zip(scores[0], ids[0]):
        meta = docs_meta[idx]
        results.append({"score": float(score), "meta": meta})
    return results

top_chunks = retrieve("Explain arrays", model, index, docs_meta, top_k=5)
```
