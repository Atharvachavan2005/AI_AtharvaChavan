4) LLM processing — which LLM, what we provide, example customize prompt, and expected outputs

Which LLM is best suited (one recommendation): use a modern GPT-4.x family endpoint (e.g., GPT-4o / latest GPT-4.1 family) for production RAG — they combine strong reasoning, long-context handling, and reliability for grounded answers. These models handle wide reasoning and higher-quality synthesis when given retrieved context. 
Databricks
+1

What we provide to the LLM (context engineering):

Top K retrieved chunks (each labeled with source) — concatenated or passed as few separate context blocks.

The user query.

A short customizable wrapper prompt (2–6 lines) that instructs the model how to use the chunks: prioritize provenance, cite sources inline, produce structured output (explanation → slide outline → manim script), and limit hallucination.

Example customize prompt (short):
You are an assistant that must use ONLY the provided knowledge chunks (marked [SRC]) to answer the user.
1) Give a concise structured explanation (4-8 bullet points).
2) Produce a slide outline: title + 4 slides with bullet points + one example per slide.
3) Produce a small Manim animation script skeleton (high level).
Cite the source tag next to factual claims (e.g., [SRC: doc1.pdf]).
If the answer is not in the chunks, say "not found in provided context" instead of guessing.