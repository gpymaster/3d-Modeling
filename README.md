# 3D Model Generator

Generate 3D models from text prompts or images using OpenAI's [Shap-E](https://github.com/openai/shap-e) diffusion model. Outputs are saved as `.obj` files ready for use in any 3D application.

## Features

- **Text to 3D** — describe any object in plain English and get a 3D mesh
- **Image to 3D** — provide a photo and reconstruct it as a 3D model
- **CPU & GPU support** — automatically uses CUDA if available, falls back to CPU
- **OBJ output** — standard format compatible with Blender, Maya, and most 3D tools

## Requirements

- Python 3.8+
- [PyTorch](https://pytorch.org/)
- [Shap-E](https://github.com/openai/shap-e)

Install dependencies:

```bash
pip install torch
pip install git+https://github.com/openai/shap-e.git
```

## Usage

```bash
python 3d_modle.py
```

You will be prompted to choose an input mode:

```
=== 3D Model Generator ===
Choose input type (text/image):
```

**Text mode:**
```
Choose input type (text/image): text
Enter your text prompt (e.g., 'a red apple'): a blue dragon
```

**Image mode:**
```
Choose input type (text/image): image
Enter path to input image (e.g., corgi.png): my_photo.png
```

Generated `.obj` files are saved to the `outputs/` directory.

## Project Structure

```
3d_model/
├── 3d_modle.py        # Entry point — handles user input and routing
├── text_model.py      # Text-to-3D pipeline using shap-e text300M
├── image_to_3d.py     # Image-to-3D pipeline using shap-e image300M
└── outputs/           # Generated .obj files saved here
```

## How It Works

Both pipelines use Shap-E's latent diffusion process:

1. A text or image prompt is encoded into a latent representation
2. A diffusion model samples from that latent space
3. The latent is decoded into a triangular mesh
4. The mesh is written to a `.obj` file

Text generation uses a guidance scale of `15.0` for strong prompt adherence. Image generation uses `3.0` to stay close to the source image while allowing 3D reconstruction.
