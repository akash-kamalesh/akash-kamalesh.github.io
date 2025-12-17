+++
title = "NanoVLM-Lab: Democratizing Vision-Language Model Training for Everyone"
date = 2025-12-17
description = "Exploring methods to build scalable and efficient vision-language models with a focus on representation learning and multimodal alignment."
+++
<img src="/nanovlm_lab_cropped.png" alt="Logo" width="500" height="500" style="display: block; margin: 0 auto;">

## Introduction

A few months ago, I was an undergraduate student working on a research project to improve dual encoder models like CLIP, with a specific focus on visual reasoning capabilities. It was exciting work-the kind that makes you believe you're onto something extremely impressive. But there was a problem I ran into very quickly - the infamous `OutOfMemoryError`. I could reduce it by dropping the batch size to 4, but then I'd have to explain to reviewers why my results came from training with such an unusually small batch size.

Being an undergrad with limited funding, I quickly realized that experimenting with vision-language models on free-tier GPUs was a non-starter. The computational demands were simply too high. So I turned to cloud GPUs, hoping to unlock the ability to train and iterate on my ideas. But here's what I discovered: **the real bottleneck wasn't just the GPU itself-it was everything around it.**

Data preprocessing, validation, experiment tracking, checkpoint management-these tasks consumed enormous amounts of time. And during all that time, the GPU sat idle while I was debugging data pipelines or validating results. But the meter kept running. I was burning money on compute that wasn't actually being used for training. Hours would pass where a $0.50/hour GPU was costing me real money for work that could have been done on my laptop.

In addition to compute, having spoken to researchers at NeurIPS last year, I noticed an increase in studies focused on efficient and more performative foundation models I wanted to create a project that would take care of the heavy lifting-all those tedious, time-consuming processes that eat up GPU hours and money without adding value. My goal was simple: abstract away the complexity with simple, helpful wrappers so that researchers and practitioners could focus on what actually matters: their ideas and their data.

The result is a comprehensive training framework, **NanoVLM-Lab** designed to make vision-language model training accessible to anyone with limited resources. All you need is a dataset and a use-case. Whether you're working with a single free-tier GPU, a modest cloud instance, or even just a laptop for prototyping, NanoVLM-Lab handles the infrastructure so you can focus on the research.

NanoVLM-Lab is built for researchers, students, and practitioners who want to experiment with vision-language models without breaking the bank. Whether you're validating ideas, exploring new approaches, or building proof-of-concepts, this framework gives you the tools to do it efficiently. Whether you're a student exploring machine learning, a researcher with a single GPU, or a practitioner building production systems, this framework is built for you.

---

## The Problem: Resources Shouldn't Stop Independent Research

The current landscape of ML research has a significant barrier to entry: **computational resources**. Training large vision-language models like Qwen-VL or Gemini requires multiple high-end GPUs, making it inaccessible to most researchers and practitioners from academia unless they are supplemented with a dedicated cluster or financial grant.

But here's the thing: **you don't need a massive model to validate your ideas.**

Small, efficient models like nanoVLM can:
- Run on a single T4 GPU (or even CPU for inference)
- Train on consumer hardware in hours instead of days
- Achieve competitive performance on many tasks
- Be deployed on edge devices and mobile platforms

**A note on scale**: While NanoVLM-Lab is designed to work on a single T4 GPU, it's important to understand the trade-offs. You can train with a single batch size and gradient accumulation steps on a single T4, which is great for experimentation and validation. However, if you're planning to use these models in production at scale, you'll need to scale up your compute accordingly. The framework supports this scaling, but single-GPU training is optimized for research and prototyping, not production-level deployments. Think of it as a way to validate your ideas and prove the concept before investing in larger infrastructure.

---

## NanoVLM-Lab

![Training Flow](/flow_diagram.png)

NanoVLM-Lab follows a progressive training pipeline designed to unlock the full potential of vision-language models. You start with either a pre-trained nanoVLM model or initialize a new one from scratch. From there, the framework guides you through **Supervised Fine-Tuning (SFT)**, where you train your model on labeled image-text pairs to adapt it to your specific domain. This is the foundation—fast, straightforward, and effective for most use cases. During SFT, the model learns to structure its reasoning process and answers within special tokens like `<think>` and `</think>`, enabling more coherent and reasoned outputs.

But SFT is just the beginning. Once you have a solid foundation, you can go beyond supervised learning and enter the world of **preference tuning** with either **Direct Preference Optimization (DPO)** or **Group Relative Policy Optimization (GRPO)**. DPO aligns your model with human preferences without needing a separate reward model—this is where things get truly interesting. GRPO takes it further, offering advanced policy optimization with custom reward functions for researchers who want fine-grained control over training dynamics. All three approaches are built on HuggingFace's Transformers and TRL, ensuring compatibility and reliability across the entire pipeline.

---

## Real-World Example: The Power of DPO

Let me show you what's possible with NanoVLM-Lab. Here's a concrete example of how DPO preference tuning transforms model outputs:

| Image | Prompt | Pre-trained nanoVLM Output* | DPO Preference-Tuned Output** |
|-------|--------|---------------------------|------------------------------|
| ![Cake](/cake.jpg) | "Why are cakes usually eaten at party's?" | "birthday" | "Cakes are usually eaten at parties to celebrate and to commemorate special occasions, such as birthdays, anniversaries, or holidays. The festive atmosphere and shared enjoyment create the ideal setting for cakes to be a highlight of the event." |

*After short training on a subset of the dataset using DPO preference optimization.<br>
** Using the checkpoint: lusxvr/nanoVLM-230M-8k

**What's happening here?**

The pre-trained model gives a one-word answer: "birthday." It's not wrong, but it's not very useful. After just a few hours of DPO training on a subset of the dataset, the same model produces a thoughtful, comprehensive answer that actually explains the reasoning.

This is the magic of preference optimization: **you're not just teaching the model facts, you're teaching it how to think and communicate.**

---

## Why This Matters for the Community

### 1. **Democratizing Research**
Not everyone has access to a cluster of A100 GPUs. NanoVLM-Lab means that brilliant ideas from researchers with limited resources can now be validated and explored.

### 2. **Rapid Experimentation**
With a single T4 GPU, you can now:
- Train a prototypical SFT model in 2-4 hours
- Run DPO experiments in 1-2 hours
- Iterate on ideas in a single day

This speed enables a different kind of research - one where you can test hypotheses quickly and build on results iteratively.

### 3. **Testing Hypotheses Quickly**
NanoVLM-Lab isn't just research code. It's built with production in mind:
- YAML-based configuration (no code changes needed)
- Comprehensive documentation
- Example notebooks for every training approach
- Integration with Weights & Biases for experiment tracking

---

## Getting Started

Getting started is simple:

```bash
# Clone the repository
git clone https://github.com/akash-kamalesh/nanovlm-lab
cd nanovlm-lab

# Clone nanoVLM
git clone https://github.com/huggingface/nanoVLM.git

# Install dependencies
pip install -e .

# Run training
python rlvlm/main.py --config configs/sft_config.yaml
```

That's it. No complex setup, no mysterious hyperparameters. Just clear configuration files and working code.

---

## What's Included

- **Three Training Approaches**: SFT, DPO, and GRPO with multiple variants
- **Beginner-Friendly Docs**: Start with the basics, dive into advanced topics as needed
- **Example Notebooks**: Interactive Jupyter notebooks for each training approach
- **Production Features**: Experiment tracking, checkpointing, mixed precision training
- **LoRA Support**: Parameter-efficient fine-tuning for all trainers
- **Custom Reward Functions**: Define your own reward signals for GRPO training

---

## The Bigger Picture

NanoVLM-Lab is more than a training framework—it's a belief that **efficiency matters, and small models deserve the same attention and tooling as large ones.**

The next wave of ML innovation won't come from scaling up, but from getting smarter about how we train and deploy models. This is where researchers with limited hardware can iterate quickly, where practitioners can build for edge devices, and where the community can focus on practical, accessible AI.

Of course, frameworks like Unsloth and LLaMA Factory are excellent alternatives with their own strengths. But NanoVLM-Lab is specifically designed to explore how far we can push small-scale models—to understand their true potential and build a community around efficient, accessible training.

If that resonates with you, NanoVLM-Lab is built for you.

---

## Join the Community

NanoVLM-Lab is open-source and actively developed. Whether you want to:
- Train your own models
- Contribute improvements
- Explore new training techniques
- Build on top of the framework

...we'd love to have you involved.

**Check it out on GitHub**: [akash-kamalesh/nanovlm-lab](https://github.com/akash-kamalesh/nanovlm-lab)

**Read the docs**: Start with the [main README](README.md), then explore the [Configuration Guide](configs/README.md) and [Training Approaches](examples/README.md).

---

<!-- ## Citation

If NanoVLM-Lab helps your research, please consider citing it:

```bibtex
@software{nanovlm_lab,
  title={NanoVLM-Lab: Advanced Training Framework for Small Vision-Language Models},
  author={Kamalesh, Akash},
  year={2025},
  url={https://github.com/akash-kamalesh/nanovlm-lab}
}
``` -->

---

## What's Next?

This is just the beginning, and I'm actively listening to user feedback to shape the future of NanoVLM-Lab. Whether you've found a feature that would be incredibly useful, discovered a limitation you'd like addressed, or have ideas for improvements, I want to hear from you. If you believe a feature would be great to have, please raise an issue on GitHub-and if you're interested in contributing, you're more than welcome to submit a pull request. This project is meant to evolve with the community, and your input directly influences what gets built next.

---

## Final Thoughts

A few years ago, I was frustrated by the limitations of my hardware. Today, I'm excited about what's possible when you focus on efficiency and smart design. NanoVLM-Lab is my contribution to changing how we think about model training.

I hope this project helps you validate your ideas, accelerate your research, and would love to see this project contribute to bigger more amazing developments.

**- Akash Kamalesh**

---

*Have questions? Found a bug? Want to contribute? Open an issue or pull request on [GitHub](https://github.com/akash-kamalesh/nanovlm-lab). Let's build this together.*
