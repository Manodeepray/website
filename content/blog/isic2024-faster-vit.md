+++
title = 'Faster-Vit Archietecture'
date = 2024-09-05T20:33:07+05:30
draft = false
+++

# Exploring Vision Transformers for Skin Cancer Classification: A Deep Learning Journey

## Introduction

Skin cancer remains one of the most common cancers globally, making early diagnosis and accurate classification essential. In recent years, deep learning has played a pivotal role in automating the detection and classification of skin lesions. Vision Transformers (ViTs) are emerging as a powerful tool for image classification tasks, including medical image analysis.

In this blog, I will share insights from my project, where I applied ViTs to classify skin lesions from the ISIC 2024 dataset into benign and malignant categories. I also explored a novel ViT model incorporating a token learning layer to optimize training time. Let's dive into the details!

## Dataset Overview: ISIC 2024

The ISIC 2024 dataset is a comprehensive collection of skin lesion images, serving as a benchmark for melanoma detection. The dataset includes various types of skin lesions, making it ideal for training and evaluating deep learning models for binary classification tasks. The key challenge here is to develop AI algorithms that can distinguish histologically confirmed malignant skin lesions from benign ones.

To mimic non-dermoscopic images, this dataset uses standardized cropped lesion-images of lesions from 3D Total Body Photography (TBP). Vectra WB360, a 3D TBP product from Canfield Scientific, captures the complete visible cutaneous surface area in one macro-quality resolution tomographic image. An AI-based software then identifies individual lesions on a given 3D capture. This allows for the image capture and identification of all lesions on a patient, which are exported as individual 15x15 mm field-of-view cropped photos. The dataset contains every lesion from a subset of thousands of patients seen between the years 2015 and 2024 across nine institutions and three continents.

## Vision Transformers (ViTs)

ViTs represent a paradigm shift in image classification. Unlike traditional methods, which rely on convolutional layers, ViTs use a transformer architecture that originated in natural language processing (NLP). The transformer model processes images as sequences of patches (tokens) and learns the relationships between them.

The main ViT models I tested were:

- Standard ViT
- ViT with a token learning layer

The token learning layer aimed to reduce training time by refining the input tokens before they were fed into the transformer model. This optimization was particularly useful for large datasets like ISIC 2024.

## Results and Comparison

ViTs demonstrated strong performance in classifying skin lesions. The ability of ViTs to capture long-range dependencies between image patches proved beneficial in medical image analysis, especially with the token learning layer model, which improved both accuracy and efficiency.

### Key Findings

- **ViTs:** Outperformed traditional methods in terms of accuracy and training efficiency.
- **Token Learning:** The token learning layer in ViTs significantly reduced training time while maintaining high accuracy.

## Conclusion

This project highlighted the potential of Vision Transformers in the field of medical image analysis, specifically skin cancer classification. ViTs, with their ability to model global context and dependencies, offer a promising alternative to traditional deep learning methods. As ViTs continue to evolve, they could become the go-to model for various computer vision tasks in healthcare.

In future work, I plan to explore hybrid models that combine the strengths of ViTs with other architectures, as well as investigate the interpretability of these models in clinical settings.

Thanks for reading! Stay tuned for more deep learning adventures!

---

_Code [Github](https://github.com/Manodeepray/Visual_transformer_paper_code)_
