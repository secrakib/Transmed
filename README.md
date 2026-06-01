# TransMed: Cross-Lingual Clinical Outcome Prediction in Low-Resource Healthcare Settings

<p align="center">
  <img src="https://github.com/secrakib/Transmed/blob/main/overview.png" alt="TransMed" width="800"/>
</p>

<p align="center">
  <b>Bridging the linguistic divide in clinical AI through machine translation and multilingual transformers</b>
</p>

<p align="center">
  <a href="https://github.com/secrakib/Transmed"><img src="https://img.shields.io/badge/Repository-TransMed-blue"></a>
  <a href="#"><img src="https://img.shields.io/badge/License-MIT-green"></a>
  <a href="#"><img src="https://img.shields.io/badge/Python-3.10+-orange"></a>
  <a href="#"><img src="https://img.shields.io/badge/Status-Research-red"></a>
</p>

---

## Overview

**TransMed** is a cross-lingual clinical natural language processing framework designed to enable clinical outcome prediction in low-resource healthcare settings without requiring native-language clinical training datasets.

The framework leverages machine translation systems to transform high-resource clinical corpora into low-resource languages and subsequently fine-tunes multilingual transformer models for downstream clinical prediction tasks.

This repository contains the code, experimental pipelines, model training scripts, evaluation procedures, and supplementary materials associated with the manuscript:

> **TransMed: A Cross-Lingual Framework for Clinical Outcome Prediction in Low-Resource Healthcare Settings**
> Rakib Ullah, Mimjamam Ul Haque Monmoy, Syed Nadim Mehdi, Mohammad Junayed Hasan, and M. R. C. Mahdy

---

## Research Objectives

This work investigates three fundamental research questions:

1. Can machine translation enable effective clinical outcome prediction in low-resource languages without native-language clinical training data?
2. How does translation quality relate to downstream clinical prediction performance?
3. Which translation-model combinations yield the best performance for clinical prediction tasks?

---

## Framework Architecture

```text
MIMIC-III Clinical Notes
           │
           ▼
  Machine Translation
           │
 ┌─────────┼─────────┐
 │         │         │
 ▼         ▼         ▼
OpusMT  BanglaT5NMT  Google Translate
           │
           ▼
      ChatGPT
           │
           ▼
Translated Clinical Corpora
           │
           ▼
 Multilingual Transformer Models
           │
 ┌─────────┼─────────┐
 │                     │
 ▼                     ▼
Mortality        Length of Stay
Prediction       Prediction
           │
           ▼
     Evaluation
```

---

## Key Contributions

* First systematic framework for translation-mediated clinical outcome prediction in low-resource languages.
* Comprehensive benchmarking of 16 translation-model combinations.
* Analysis of the relationship between translation quality and downstream clinical utility.
* Demonstration that clinically meaningful performance can be achieved without native-language clinical datasets.
* Reproducible pipeline for extending clinical NLP research to linguistically underserved healthcare environments.

---

## Experimental Configuration

### Translation Systems

The study evaluates four translation approaches:

| Translation System  | Type                       |
| ------------------- | -------------------------- |
| OpusMT              | Neural Machine Translation |
| BanglaT5NMT         | Bengali NMT                |
| Google Translate    | Commercial NMT             |
| ChatGPT Translation | Large Language Model       |
| Code-Mixed Variants | Hybrid Clinical Text       |

### Language Models

| Model       | Description               |
| ----------- | ------------------------- |
| mBERT       | Multilingual BERT         |
| XLM-RoBERTa | Cross-lingual Transformer |
| IndicBERT   | Indic Language Model      |
| BanglaBERT  | Bengali Transformer       |

### Prediction Tasks

#### Mortality Prediction (MP)

Binary classification task predicting whether a patient survives or dies during hospitalization.

#### Length-of-Stay Prediction (LOS)

Multiclass classification task predicting hospitalization duration categories.

---

## Repository Structure

```text
TransMed/
│
├── Codes/
│   │
│   ├── Ablation Study and Avg. of seeds/
│   │   │
│   │   ├── Ablation Study/
│   │   │   ├── Code/
│   │   │   │   ├── Custom Loss and Weighting/
│   │   │   │   └── Oversampling/
│   │   │   └── Ablation study Results.docx
│   │   │
│   │   └── Average+-std of four models on three different seeds/
│   │       ├── Length Of stay prediction/
│   │       │   ├── Code/
│   │       │   └── Results (.xlsx)
│   │       │
│   │       └── Mortality Prediction/
│   │           ├── Code/
│   │           └── Results (.xlsx)
│   │
│   ├── Computatuional Analysis/
│   │   └── BanglaNMT and Opus MT/
│   │       ├── Notebook/
│   │       └── Result/
│   │
│   ├── Length Of Stay/
│   │   └── Notebook/
│   │       ├── Dataset Creation/
│   │       ├── Google Translate Translation Code/
│   │       └── Sliding Window Code For OPUS & BanglaNMT Translation/
│   │
│   └── Mortality Prediction/
│       └── Notebook/
│           ├── 1000 instances BanglaNMT/
│           ├── 1000 instances Google/
│           └── 1000 instances Opus/
│
├── LICENSE
├── README.md
└── .gitignore
```

### Folder Description

| Folder                     | Description                                                                                      |
| -------------------------- | ------------------------------------------------------------------------------------------------ |
| **Length Of Stay**         | Dataset construction, machine translation, and LOS prediction experiments.                       |
| **Mortality Prediction**   | Mortality prediction experiments using translated clinical notes.                                |
| **Computational Analysis** | Runtime and computational efficiency analysis of translation systems.                            |
| **Ablation Study**         | Experiments investigating oversampling, custom loss functions, and weighting strategies.         |
| **Average ± Std of Seeds** | Reproducibility experiments across multiple random seeds with aggregated performance statistics. |

### Included Resources

The repository contains:

* Dataset preparation notebooks
* Translation pipelines (OpusMT, BanglaNMT, Google Translate)
* Mortality prediction experiments
* Length-of-stay prediction experiments
* Computational efficiency analyses
* Ablation studies
* Multi-seed reproducibility experiments
* Statistical summaries and result spreadsheets

All experiments reported in the manuscript can be reproduced using the notebooks and supplementary result files provided in this repository.


## Installation

Clone the repository:

```bash
git clone https://github.com/secrakib/Transmed.git

cd Transmed
```

Create a virtual environment:

```bash
python -m venv transmed_env

source transmed_env/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Running Experiments

### Step 1: Data Preparation

```bash
python preprocessing/prepare_dataset.py
```

### Step 2: Machine Translation

```bash
python translation/run_translation.py
```

### Step 3: Fine-Tuning

```bash
python training/train.py
```

### Step 4: Evaluation

```bash
python evaluation/evaluate.py
```

---

## Main Results

### Best Baseline Performance

| Task                      | AUC-ROC |
| ------------------------- | ------- |
| Length of Stay Prediction | 65.3%   |
| Mortality Prediction      | 64.9%   |

### Mortality Prediction with Cost-Sensitive Learning

| Metric  | Value  |
| ------- | ------ |
| AUC-ROC | 75.05% |

### Key Finding

Translation quality alone does not reliably predict downstream clinical performance. The relationship between BLEU scores and clinical effectiveness varies substantially across tasks, suggesting that conventional machine translation evaluation metrics may not adequately capture clinical utility.

---

## Data Availability

This study utilizes data derived from the **MIMIC-III Clinical Database**.

Because MIMIC-III contains protected health information and is distributed under a data use agreement, the raw dataset cannot be redistributed through this repository.

Researchers can obtain access through:

https://physionet.org/content/mimiciii/

after completing the required credentialing and data use agreement process.

To facilitate reproducibility, this repository provides:

* Data preprocessing scripts
* Translation pipelines
* Training procedures
* Evaluation scripts
* Experimental configurations
* Hyperparameter settings

No identifiable patient information is included in this repository.

---

## Code Availability

All source code required to reproduce the experiments reported in the manuscript is publicly available at:

https://github.com/secrakib/Transmed

The repository includes:

* Data preprocessing code
* Translation workflows
* Model fine-tuning scripts
* Evaluation pipelines
* Statistical analysis procedures
* Result generation utilities

---

## Reproducibility

To support transparent and reproducible research, we provide:

* Fixed random seeds
* Hyperparameter configurations
* Model checkpoints (where permitted)
* Evaluation scripts
* Statistical analysis notebooks

Researchers should be able to reproduce all reported results after obtaining authorized access to MIMIC-III.

---

## Citation

If you use this repository in your research, please cite:

```bibtex
@article{ullah2026transmed,
  title={TransMed: A Cross-Lingual Framework for Clinical Outcome Prediction in Low-Resource Healthcare Settings},
  author={Ullah, Rakib and Monmoy, Mimjamam Ul Haque and Mehdi, Syed Nadim and Hasan, Mohammad Junayed and Mahdy, M. R. C.},
  journal={PLOS Digital Health},
  year={2026}
}
```

---

## Authors

* Rakib Ullah
* Mimjamam Ul Haque Monmoy
* Syed Nadim Mehdi
* Mohammad Junayed Hasan
* M. R. C. Mahdy

---

## License

This project is released under the MIT License. See the `LICENSE` file for details.

---

## Acknowledgements

This work utilizes the MIMIC-III Clinical Database made available through PhysioNet and builds upon advances in multilingual NLP, machine translation, and clinical artificial intelligence research.

The authors acknowledge the broader open-source community whose tools and models made this research possible.
