5) Content generation — slides + Manim animation (what APIs, process, code snippets)

Slide creation pipeline:

Parse LLM slide outline (title, bullet points, examples).

Use python-pptx (or Google Slides API) to programmatically build .pptx or Google Slides. python-pptx is simple and local; Google Slides is great for cloud edits and sharing.

Short code snippet — create slides with

# pip install python-pptx
from pptx import Presentation

prs = Presentation()
# assume llm_outlines is a list of slides: [{"title":"...", "bullets":[...]}]
for s in llm_outlines:
    slide = prs.slides.add_slide(prs.slide_layouts[1])  # Title + Content
    slide.shapes.title.text = s["title"]
    body = slide.shapes.placeholders[1].text_frame
    for b in s["bullets"]:
        p = body.add_paragraph()
        p.text = b
prs.save("output_slides.pptx")