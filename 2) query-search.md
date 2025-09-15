3) RAG retrieval phase — how query is handled + code

Process (high level):

User query arrives.

Context engineering: normalize query, optionally expand with intent classifiers or short semantic rewrites.

Embed the query with the same embedding model used for the KB.

Run a k-NN search in the vector DB (top K, e.g., K=5).

(Optional) Re-rank the top results using a cross-encoder or short LLM re-score to improve precision.

Return top chunks + their source metadata to LLM for final composition.

Short code snippet — embed query & retrieve top K from FAISS:


code:
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
top_chunks = retrieve("Explain arrays", model, index, docs_meta, top_k=5)