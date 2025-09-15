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

*Tiny example (Python):*