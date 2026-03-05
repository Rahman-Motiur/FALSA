
# FALSA: Fairness-Aware Latent Space Alignment for Vision-Language Models

Official implementation of the paper:

**FALSA: Fairness-Aware Latent Space Alignment in Vision-Language Models for Medical Image Segmentation**

Md Motiur Rahman, Smriti Bhatt, Miad Faezipour  
Purdue University

📄 Paper: (link will be added after publication)

---

# Overview

Vision-language models (VLMs) such as CLIP, BLIP, and SAM have demonstrated strong performance in multimodal medical tasks. However, these models often inherit demographic biases from large-scale training datasets, leading to unequal performance across patient groups.

This repository provides the implementation of **FALSA**, a fairness-aware framework designed to reduce demographic and intersectional bias in medical image segmentation while maintaining high predictive performance.

FALSA introduces fairness mechanisms directly into the latent representation space of vision-language models.

---

# Key Contributions

FALSA introduces three main components:

### 1. Demographic-Invariant Contrastive Learning (DICL)

Encourages image-text representations to align based on semantic similarity rather than demographic attributes, preventing bias amplification in multimodal embeddings.

### 2. Adaptive Fairness Calibration (AFC)

Uses adversarial learning with gradient reversal to suppress demographic information from both visual and textual embeddings.

### 3. Unified Cross-Attribute Fairness Loss (UniFairLoss)

Jointly minimizes:

- intra-group performance disparities  
- cross-group correlation of errors  
- intersectional bias across demographic attributes  

This allows FALSA to improve fairness without sacrificing segmentation performance.

---

# Framework Architecture

The FALSA pipeline integrates fairness modules into a vision-language segmentation architecture.

```
Image Encoder (SAM / SAMed)
        │
        ▼
Demographic-Invariant Contrastive Learning (DICL)
        │
        ▼
Adaptive Fairness Calibration (AFC)
        │
        ▼
Mask Decoder
        │
        ▼
Segmentation Prediction
        │
        ▼
UniFairLoss Optimization
```

---

# Datasets

## Harvard-FairSeg

- 10,000 retinal fundus images  
- optic cup and rim segmentation masks  
- multimodal data (image + clinical text)

Demographic attributes include:

- gender  
- race  
- ethnicity  
- language  

## MIMIC-CXR

- 370,000 chest radiographs  
- heart and lung segmentation tasks  
- demographic metadata including gender and age  

---

# Evaluation Metrics

Segmentation performance is evaluated using:

- Dice coefficient  
- Intersection over Union (IoU)

Fairness is evaluated using:

- Equity-Scaled Dice (ES-Dice)  
- Equity-Scaled IoU (ES-IoU)  
- Group Standard Deviation (GSD)  
- Disparity Index (DI)  
- Relative Performance Gap (RPG)

These metrics evaluate both **accuracy** and **demographic fairness**.

---

# Results

FALSA improves both segmentation performance and fairness across demographic groups.

Example results (Harvard-FairSeg dataset):

| Model | Dice | ES-Dice | GSD |
|------|------|------|------|
| SAMed | 86.71 | 84.50 | 1.63 |
| SAMed + FALSA | **87.01** | **86.82** | **0.88** |

Key outcomes:

- Up to **70–80% reduction in fairness disparity**
- Improved **equity-scaled segmentation metrics**
- Reduced demographic performance gaps

---

# Installation

Clone the repository:

```bash
git clone https://github.com/Rahman-Motiur/FALSA.git
cd FALSA
```

Create environment:

```bash
conda create -n falsa python=3.10
conda activate falsa
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# Training

Example training command:

```bash
python train.py \
  --model SAMed \
  --dataset Harvard-FairSeg \
  --epochs 300 \
  --batch_size 16
```

---

# Project Structure

```
FALSA/
│
├── datasets/
│   ├── harvard_fairseg
│   └── mimic_cxr
│
├── models/
│   ├── falsa_modules
│   ├── sam
│   └── samed
│
├── losses/
│   ├── dicl_loss.py
│   ├── afc_loss.py
│   └── unfair_loss.py
│
├── training/
│   ├── train.py
│   └── trainer.py
│
├── evaluation/
│   ├── metrics.py
│   └── fairness_metrics.py
│
└── README.md
```

---

# Citation

If you use this work, please cite:

```bibtex
@article{rahman2026falsa,
  title={FALSA: Fairness-Aware Latent Space Alignment in Vision-Language Models for Medical Image Segmentation},
  author={Rahman, Md Motiur and Bhatt, Smriti and Faezipour, Miad},
  journal={International Journal of Computer Vision},
  year={2026}
}
```

---

# Contact

Md Motiur Rahman  
PhD Candidate, Electrical & Computer Engineering Technology  
Purdue University  

Email: rahma112@purdue.edu

---

# License

This project is released under the **MIT License**.
