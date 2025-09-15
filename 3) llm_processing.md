# Building a Smart Q&A System

Instead of crafting perfect prompts, I grab relevant info from my knowledge base and feed it to the AI with the user's question. The AI gets actual facts instead of guessing.

## Data Sources

I pull from company docs, textbooks, FAQs, API docs, support tickets, web pages, PDFs, and public datasets. Convert to plain text, split into 200-800 word chunks with overlap, store with source metadata.

## Embedding Model

Using `sentence-transformers/all-MiniLM-L6-v2` because it's small, fast, good quality, and runs locally without eating resources.

Each text chunk becomes a vector (list of numbers representing meaning). Questions get converted to vectors too, then I find similar chunks.

```python
from sentence_transformers import SentenceTransformer
import faiss

model = SentenceTransformer("all-MiniLM-L6-v2")
docs = ["Array is a contiguous memory structure...", "Functions in Python..."]

embs = model.encode(docs, convert_to_numpy=True)

index = faiss.IndexFlatIP(embs.shape[1])
faiss.normalize_L2(embs)
index.add(embs)
```
