# What the AI Gives Back

The system outputs three things:

**Structured explanation** - clear, short bullets that actually make sense

**Slide outline** - titles, bullet points, examples, and speaker notes ready to use

**Animation script** - basic Python/pseudo-code that developers can build on for Manim animations

```python
# Works with OpenAI, Anthropic, etc.
prompt = build_prompt(top_chunks, user_query, wrapper_instructions)
response = llm_client.complete(model="gpt-4o", prompt=prompt, max_tokens=800)
print(response.text)
```

