# Creating Slides and Animations

## Slide Creation

I parse the AI's outline and use `python-pptx` to build PowerPoint files. Could also use Google Slides API for cloud sharing.

```python
from pptx import Presentation

prs = Presentation()
for s in llm_outlines:
    slide = prs.slides.add_slide(prs.slide_layouts[1])
    slide.shapes.title.text = s["title"]
    body = slide.shapes.placeholders[1].text_frame
    for b in s["bullets"]:
        p = body.add_paragraph()
        p.text = b
prs.save("output_slides.pptx")
```

## Manim Animations

Take the AI's animation script skeleton and expand it into working Manim code for visual explanations.
