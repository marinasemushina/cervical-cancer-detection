# Detection of abnormal cervical cells using SimSiam and Faster R-CNN

This repository contains the code for the master's thesis:

**"Development and evaluation of machine learning methods for cervical cancer cytological screening"**

Moscow Institute of Physics and Technology (MIPT), 2026

---

## Overview

The project implements a three-stage approach for detecting abnormal cervical cells in cytological images:

1. **Self-supervised pre-training** of ResNet-50 encoder using **SimSiam** on unlabeled cytological images
2. **Fine-tuning** of **Faster R-CNN** detector with SimSiam-initialized backbone
3. **Adaptive Test-Time Augmentation (TTA)** with dynamic confidence threshold adjustment

---

## Repository structure
```
├── SSL(SimSiam).ipynb # SimSiam pre-training on unlabeled data
├── Basline(ImageNet).ipynb # Baseline Faster R-CNN with ImageNet weights
├── SimSiam+FasterRCNN.ipynb # Faster R-CNN with SimSiam-initialized backbone
└── Test_basline + TTA.ipynb # Evaluation with baseline TTA and adaptive TTA

```
---

## Results

| Model configuration | mAP@0.5 (%) | 95% CI |
|:---|:---|:---|
| Baseline (ImageNet initialization) | 63.70 | [62.08 – 65.34] |
| SimSiam initialization | 64.87 | [63.38 – 66.37] |
| SimSiam + Adaptive TTA | 65.41 | [64.19 – 66.99] |

**Key findings:**
- SimSiam initialization improves mAP by **+1.17%** over ImageNet baseline
- Adaptive TTA provides an additional **+0.54%** gain
- Total improvement over baseline: **+1.71%**

---

## Requirements

- Python 3.8+
- PyTorch 1.12.1
- torchvision 0.13.1
- CUDA 11.3 (recommended)
- Additional libraries: numpy, pandas, matplotlib, opencv-python, tqdm

---

## Dataset

The experiments use the publicly available **HMCHH-TCT-CellDet** dataset:

| Parameter | Value |
|:---|:---|
| Images | 8,037 |
| Annotated abnormal cells | 15,761 |
| Image size | 2048 × 2048 pixels |
| Patches (after splitting) | 333 per slide |

**Source:** Zhang X. et al. "A large annotated cervical cytology images dataset for AI models to aid cervical cancer screening". *Scientific Data*, 2025. DOI: [10.1038/s41597-025-04374-5](https://doi.org/10.1038/s41597-025-04374-5)

---

## Usage

### 1. Mount Google Drive with the dataset

```python
from google.colab import drive
drive.mount('/content/drive')
```

### 2. Clone this repository

```bash
git clone https://github.com/marinasemushina/cervical-cancer-detection.git
cd cervical-cancer-detection
```

### 3. Run notebooks in the following order
Step	Notebook	Description

1.	SSL(SimSiam).ipynb	Self-supervised pre-training on unlabeled data

2.	Basline(ImageNet).ipynb	Baseline training with ImageNet initialization

3.	SimSiam+FasterRCNN.ipynb	Fine-tuning with SimSiam-initialized backbone

4.	Test_basline + TTA.ipynb	Evaluation with baseline TTA and adaptive TTA

Citation
If you use this code, please cite:
```bibtex
@mastersthesis{Semushina2026,
  author = {Semushina, M.A.},
  title = {Development and evaluation...},
  school = {MIPT},
  year = {2026}
}
```
## License

MIT License — see [LICENSE](LICENSE)
