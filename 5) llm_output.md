What the LLM will output (medium-sized):

Structured explanation (clear, short bullets).

Slide outline: titles, bullet points, examples, speaker notes.

Manim animation script skeleton: short pseudo or python code snippets that the dev can expand.

Short code snippet — calling OpenAI-style LLM (pseudo):
# pseudo: adapt for your API client (OpenAI, Anthropic, etc.)
prompt = build_prompt(top_chunks, user_query, wrapper_instructions)
response = llm_client.complete(model="gpt-4o", prompt=prompt, max_tokens=800)
print(response.text)