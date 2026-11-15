Prompt Engineering for Image Generation with Gemini
A practical Jupyter notebook demonstrating how to improve AI-generated images by moving from a simple text prompt to a structured, reference-guided prompt engineering workflow using Google Gemini on Vertex AI.

The notebook uses the Pythagorean theorem as an example and progressively builds a more detailed prompt for generating a presentation-style educational visual.

What this notebook demonstrates
This notebook explores three useful techniques for image generation:

Simple image prompting
Generate an image directly from a short natural-language prompt.

Prompt enhancement with an LLM
Break an image concept into structured components such as subject, action, environment, camera position, lighting, and visual style, then ask Gemini to turn those components into a richer image-generation prompt.

Reference-guided image generation
Provide an existing image or slide template to Gemini as a visual style reference when generating the final image.

The overall workflow is:

Idea → Structured keywords → Enhanced prompt → Reference image → Generated image

Example
The notebook starts with a very simple prompt:

A diagram illustrating visual proof of the Pythagorean theorem.

This is sent directly to the Gemini image model.

The notebook then builds a more controlled prompt using several explicit characteristics:

Prompt element	Example
Subject	A simple slide
Action	Explaining visual proof of the Pythagorean theorem
Location/background	White background
Camera	Eye-level shot
Lighting	White light
Style	Minimalist
These values are combined into a list of mandatory keywords.

A Gemini text model is then asked to transform the keywords into a single detailed image-generation prompt.

Prompt enhancement
The notebook uses the following pattern:

keywords = [
    subject,
    action,
    location,
    camera_control,
    lighting,
    style
]
