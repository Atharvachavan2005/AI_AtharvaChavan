# Animation Pipeline

## Manim Process

The AI gives me a basic Manim script with scene names and animation steps. I validate it for safety, then run Manim to create video files.

```python
from manim import *

class ArrayIntro(Scene):
    def construct(self):
        arr = Square().scale(0.5)
        self.play(Write(Text("Array: contiguous memory")))
```

```bash
manim -pql manim_scene.py ArrayIntro
```

## Why This Stack

**all-MiniLM-L6-v2** - cheap, fast, good quality, easy to host myself

**FAISS** - fast search, simple to set up  

**GPT-4** - best reasoning with long context, less prompt engineering needed

**python-pptx + Manim** - programmatic generation, widely used, works with CI
