# How I Handle Search Queries

When someone asks a question, here's what happens:

I clean up their query, convert it to a vector using the same model from before, then search my database for the 5 most similar chunks. Sometimes I'll re-rank these results to get better matches.

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

The function returns the best matching chunks with their similarity scores and source info, which I then feed to the language model.

