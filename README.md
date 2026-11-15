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

The text model receives instructions similar to:
Expand the following keywords into a single, high-fidelity,
descriptive prompt for image generation.

Every keyword must be included.

Output only the final prompt.
The generated description becomes the prompt used by the image-generation model.

This pattern is useful because it separates:

what you want from
how the image-generation prompt should describe it

That makes the workflow easier to reuse across different subjects and visual styles.

Reference image workflow

The notebook also demonstrates using an existing image as a style guide.

The reference file used in the example is:
slide-template.png
It is loaded and supplied alongside the generated prompt:
with open(reference_image, "rb") as f:
    image = f.read()

The request then asks Gemini to use the reference image as a general style and formatting guide, rather than reproducing it exactly.

This is particularly useful for:

presentation slides
branded educational content
maintaining visual consistency
generating multiple images in a similar style
using an existing design as inspiration

The final generated image is saved as:
slide-image.png

Models

The notebook currently uses:

IMAGE_MODEL_ID = "gemini-3.1-flash-image"
TEXT_MODEL_ID = "gemini-3-flash-preview"

Compatibility update

The image-generation endpoint was updated in July 2026:

gemini-3.1-flash-image-preview

was replaced with:
gemini-3.1-flash-image

Check the current Vertex AI documentation before running the notebook, as model identifiers and preview endpoints can change over time.

Requirements

The notebook was developed with:

Python 3.11
Jupyter Notebook
Google Gen AI Python SDK
Google Cloud Vertex AI
IPython

The key imports are:

from IPython.display import Image, Markdown, display
from google import genai
from google.genai import types

Install the project dependencies using:

Shell

pip install -r requirements.txt

Google Cloud setup

You will need access to a Google Cloud project configured for Vertex AI.

The notebook expects a helper function:

from helper import authenticate

credentials, project_id = authenticate()

The Gemini client is then created with:

client = genai.Client(
    project=project_id,
    location="global",
    credentials=credentials,
    http_options=types.HttpOptions(
        base_url=os.getenv("GOOGLE_VERTEX_BASE_URL")
    )
)

Depending on your environment, you may need to configure authentication and the GOOGLE_VERTEX_BASE_URL environment variable before running the notebook.

Repository structure

A typical repository structure is:

.
├── README.md
├── prompt-engineering-image-generation.ipynb
├── helper.py
├── requirements.txt
└── slide-template.png

After running the notebook, the generated image will also appear:

slide-image.png

Running the notebook
1. Clone the repository
Shell
git clone <repository-url>
cd <repository-name>
2. Create a virtual environment
Shell
python -m venv .venv

Activate it.

macOS/Linux:

Shell
source .venv/bin/activate

Windows:

PowerShell
.venv\Scripts\Activate.ps1
3. Install dependencies
Shell
pip install -r requirements.txt
4. Configure Google Cloud authentication

Ensure your environment can authenticate to the Google Cloud project used for Vertex AI.

5. Add the reference image

Place:

Plain Text
slide-template.png

in the same directory as the notebook.

6. Run the notebook
Shell
jupyter notebook

Open the notebook and run the cells sequentially.

Supported aspect ratios

The notebook generates images using a 16:9 aspect ratio, which is useful for presentation slides.

The API also supports formats such as:

Plain Text
1:1
3:2
2:3
3:4
4:3
4:5
5:4
9:16
16:9
21:9

For example:

Python
image_config=types.ImageConfig(
aspect_ratio="16:9"
)
Key idea: structure improves control

A useful takeaway from this notebook is that image prompting does not have to rely on writing one large prompt manually.

Instead, describe the image through reusable dimensions:

Plain Text
Subject
+ Action
+ Environment
+ Camera
+ Lighting
+ Style
+ Reference image

Then allow a language model to transform those constraints into a richer image-generation prompt.

This approach can make prompt construction more systematic and easier to reuse across different image-generation tasks.

Important notes
AI output will vary

Generative AI models are probabilistic. Running exactly the same prompt multiple times may produce different images.

Treat the generated outputs as variations rather than deterministic results.

Reference images are guidance

A reference image should generally be treated as a visual or stylistic guide rather than an expectation that the generated output will reproduce the source exactly.

Review generated content

Always review generated images before using them in educational, professional, or published material, particularly where diagrams need to be mathematically or factually accurate.

Resources
Get started with Google Cloud Vertex AI
Gemini 3.1 Flash Image documentation\n)\n)\n)
Google's image prompting guide
Potential extensions

This notebook can be extended to experiment with:

different image styles
presentation templates
brand reference images
multiple reference images
prompt comparison experiments
different aspect ratios
automated image saving
batches of generated slides
prompt evaluation
visual consistency across a series of images
Responsible use

When using generative AI for image creation:

verify factual and educational content
check generated text carefully
respect copyright and intellectual property
avoid supplying sensitive or confidential information unless the environment is approved for that data
ensure AI-generated visuals are appropriate for their intended audience and context
License

Add the appropriate license for your repository.

For example:

Plain Text
MIT License

if you intend others to reuse and modify the code.

Acknowledgements

This project uses Google's Gemini models through Vertex AI and the Google Gen AI Python SDK.


### A couple of improvements I made

I’ve deliberately made the README explain the **learning journey** rather than dumping the code into documentation. I also corrected the malformed links in the notebook’s Resources section and added setup, repository structure, model configuration, responsible-use guidance, and the important distinction between **prompt enhancement** and **reference-guided generation**.
