# 🎨 Intelligent Visual Synthesis — Text-to-Image Generator

> Full-stack Django web app integrating **Stable Diffusion** for real-time image synthesis from text prompts. Fine-tuned with **LoRA**, reducing GPU memory usage by **~40%**. Built from scratch using Diffusion Models and Conditional GAN (CGAN).

---

## Overview

This project explores the cutting edge of generative AI — building a complete text-to-image pipeline from first principles. It implements Diffusion Models and Conditional GANs from scratch to understand the underlying mathematics, then integrates Stable Diffusion via a Django REST API for production-ready image generation.

**What makes this project unique:** Rather than just calling an API, this project implements the core architectures from scratch, compares results, and deploys as a real web application.

---

## Architecture

```
User Prompt (text)
        ↓
Django REST API (POST /generate)
        ↓
Stable Diffusion Pipeline (HuggingFace Diffusers)
  + LoRA Fine-tuning weights
        ↓
Async image generation (background task)
        ↓
Generated Image returned to frontend
```

### Models Implemented

| Model | Type | Key Concept |
|-------|------|-------------|
| **Conditional GAN (CGAN)** | From scratch | Generator + Discriminator conditioned on text embeddings |
| **Diffusion Model** | From scratch | Forward noising process + learned reverse denoising |
| **Stable Diffusion** | Pre-trained + LoRA | Latent diffusion with fine-tuning for domain adaptation |

---

## Key Technical Achievements

| Achievement | Detail |
|-------------|--------|
| **~40% GPU memory reduction** | LoRA fine-tuning uses low-rank weight matrices instead of full fine-tuning |
| **Production-ready API** | REST endpoints with async processing pipeline |
| **From-scratch implementations** | CGAN and Diffusion Model built to understand core concepts |
| **Full-stack deployment** | Django backend + frontend UI for real-time generation |

---

## LoRA Fine-Tuning

LoRA (Low-Rank Adaptation) significantly reduces memory requirements during fine-tuning:

```python
# Standard fine-tuning: updates all W parameters (huge memory)
# LoRA: W_new = W_original + (A × B) where rank(A,B) << rank(W)
# Result: ~40% GPU memory reduction, same quality output
```

This is the same technique used by state-of-the-art image generation pipelines like DreamBooth.

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-092E20?style=flat&logo=django&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat&logo=pytorch&logoColor=white)
![HuggingFace](https://img.shields.io/badge/HuggingFace-FFD21E?style=flat&logo=huggingface&logoColor=black)

- **Backend:** Django, Django REST Framework
- **ML Framework:** PyTorch, HuggingFace Diffusers
- **Models:** Stable Diffusion, LoRA, CGAN (custom), Diffusion Model (custom)
- **Async Processing:** Django background tasks
- **Environment:** Google Colab (A100 GPU) / Local CUDA

---

## How to Run

```bash
# Clone the repository
git clone https://github.com/Tanujakomperla/Text-to-image.git
cd Text-to-image

# Install dependencies
pip install torch torchvision diffusers transformers django djangorestframework peft accelerate

# Run Django server
python manage.py runserver

# API endpoint
POST /api/generate/
Body: {"prompt": "a beautiful sunset over mountains"}
Response: {"image_url": "/media/generated/output.png"}
```

---

## Sample Results

| Prompt | Model Used |
|--------|------------|
| "a futuristic city at night" | Stable Diffusion + LoRA |
| "a red apple on a wooden table" | CGAN (from scratch) |
| "mountains with snow peaks" | Diffusion Model (from scratch) |

---

## Key Learnings

- **Diffusion models** work by learning to reverse a Gaussian noising process — the math behind DDPM (Denoising Diffusion Probabilistic Models)
- **LoRA's efficiency** comes from decomposing weight updates into two low-rank matrices, making fine-tuning accessible without high-end GPUs
- **Async processing** is essential for image generation — synchronous API calls would timeout given generation latency (5-30 seconds per image)
- Understanding the difference between **unconditional** (DDPM) and **conditional** (classifier-free guidance) generation

---

## Future Improvements

- [ ] Add Stable Diffusion XL support
- [ ] Implement image-to-image and inpainting pipelines
- [ ] Deploy on Hugging Face Spaces for live demo
- [ ] Add prompt enhancement using LLM preprocessing

---

## Author

**Komperla Tanuja**
B.Tech Computer Science | GVP College of Engineering for Women, Visakhapatnam
[LinkedIn](https://www.linkedin.com/in/tanuja-komperla-066755251) | [GitHub](https://github.com/Tanujakomperla)
