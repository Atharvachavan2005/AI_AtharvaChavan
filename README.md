# AI-Powered RAG ➜ Slides ➜ Manim Video Pipeline

## 1 · Solution in Plain English
We combine *Retrieval-Augmented Generation (RAG)—an AI pattern where we first *fetch the right text and then let an LLM write the answer[13]—with *context engineering*.  
Instead of squeezing everything into one clever prompt, we hand the LLM all the relevant paragraphs plus the user’s question. With that full context it can write clear slides and the Python code that Manim needs to animate them. The result: accurate, personalised videos with almost no manual work[1].

---

## 2 · Building the Knowledge-Base

| Step | What we do | Why this choice |
|------|------------|-----------------|
| Gather data | Scrape public textbooks / open course notes (PDF → text) | Educational sources match student queries[1] |
| Chunk & clean | Split into ~500-token chunks to keep semantic meaning | Smaller chunks index & retrieve better[21] |
| Embed | *Model:* text-embedding-ada-002 (OpenAI) | High quality, cheap, widely used in RAG tutorials[21] |
| Store | *Vector DB:* Pinecone | Scales to millions of vectors with milliseconds latency |

![WhatsApp Image 2025-09-15 at 13 27 40_a96ade56](https://github.com/user-attachments/assets/00b51b1e-55ee-4845-bd60-74cab7b78b6c)

*Tiny example (Python):*
def retrieve(query, model, index, docs_meta, top_k=5):
    q_emb = model.encode([query], convert_to_numpy=True)
    faiss.normalize_L2(q_emb)
    scores, ids = index.search(q_emb, top_k)
    results = []
    for score, idx in zip(scores[0], ids[0]):
        meta = docs_meta[idx]   # title/source/offset stored earlier
        results.append({"score": float(score), "meta": meta})
    return results

# usage
top_chunks = retrieve("Explain arrays", model, index, docs_meta, top_k=5)
