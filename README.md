# Bengali NLP Safety Challenge 2026 — ALIEN_X

Fine-grained Bengali toxicity detection using machine learning, pretrained language models, and label-specific ensembles.

This repository documents **Team ALIEN_X’s** experiments for the **Bengali NLP Safety Challenge 2026**, including training notebooks, saved predictions, submission files, and a reproducibility audit of the historical V38 system.

## Overview

Bengali online comments can contain Bengali script, Romanized Bengali, and mixed-language text. This project explores complementary modeling approaches to predict overall toxicity and six related attributes.

Each comment receives seven binary predictions:

| Label | Prediction target |
|---|---|
| `is_toxic` | Overall toxicity |
| `implicit_toxicity` | Implicit toxicity |
| `sarcasm` | Sarcasm |
| `contains_profanity` | Profanity |
| `threatening` | Threatening content |
| `identity_attack` | Identity-directed attacks |
| `sexual_content` | Sexual content |

The labels follow the competition’s annotations. They are separate prediction targets; the presence of an attribute should not automatically be treated as proof of overall toxicity.

## Modeling Approach

The experiment history includes:

- **TF–IDF and logistic regression** for lexical baselines.
- **BanglaBERT** for contextual Bengali text representations.
- **Transliteration-oriented transformer models** for cross-script inputs.
- **Frozen Bengali sentence embeddings with linear classifiers**.
- **Label-specific probability and logit blending**.
- **Threshold selection and ranking-based decisions**.
- **Specialist experiments** targeting individual attributes.

The historical V38 system combines selected outputs from earlier experiments. It is a label-specific ensemble assembled from trained models and cached predictions.

## Repository Structure

```text
.
├── Data Sets/
│   ├── train.csv
│   ├── validation.csv
│   ├── test.csv
│   ├── sample_submission.csv
│   └── bengali-nlp-safety-challenge-2026/
│       └── Improve_*.csv
├── Final/
│   ├── NLP_02_Alien_x_Sayem_Islam_Leon.ipynb
│   ├── My final best submission is V38.docx
│   └── ... packaged final artifacts
├── NoteBooks K/
│   └── bengali_nlp_safety_v17_kaggle_dual_gpu.ipynb
├── Resources/
│   ├── Class_1_Bengali_NLP_Toxicity_TFIDF.ipynb
│   └── ... reference materials
├── csv/
│   └── ... versioned submission files
├── bengali_nlp_safety_*.ipynb
├── starter_kit.ipynb
├── optimized_v2_config.json
├── validation_ensemble_probabilities_v2.csv
├── test_ensemble_probabilities_v2.csv
└── ... experiment data and result archives
```

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/SamZx14/Bangali-Safety-NLP-Challange-Alien_X-2026.git
cd Bangali-Safety-NLP-Challange-Alien_X-2026
```

### 2. Choose a notebook

| Purpose | Starting point |
|---|---|
| Explore the task | `starter_kit.ipynb` |
| Study the TF–IDF baseline | `Resources/Class_1_Bengali_NLP_Toxicity_TFIDF.ipynb` |
| Explore the early ensemble workflow | `bengali_nlp_safety_colab_ready_v2.ipynb` |
| Inspect cross-script experiments | `bengali_nlp_safety_colab_ready_v35_LIVE_crossscript.ipynb` |
| Run the Kaggle dual-GPU variant | `NoteBooks K/bengali_nlp_safety_v17_kaggle_dual_gpu.ipynb` |
| Audit dataset compatibility and historical artifacts | `Final/NLP_02_Alien_x_Sayem_Islam_Leon.ipynb` |

**The notebook in `Final/` performs a reproducibility audit. It does not train the V38 model or generate a new competition submission.**

### 3. Prepare the environment

Open the selected notebook in **Google Colab**, **Kaggle Notebooks**, or a compatible local Jupyter environment.

- Follow the notebook’s dependency and setup cells.
- Enable a GPU for transformer training.
- Update dataset, cache, and output paths for your environment.
- Supply any historical prediction files or archives required by that version.
- Use your own credentials if the notebook downloads competition data.

These notebooks represent different experiments and may require different dependencies and input artifacts.

### 4. Prepare the data

Training and validation files use the following columns:

```text
ID,text,is_toxic,implicit_toxicity,sarcasm,contains_profanity,threatening,identity_attack,sexual_content
```

Test files contain:

```text
ID,text
```

Set the notebook’s data directory to the intended dataset release. For example, when running from the repository root:

```python
from pathlib import Path

DATA_DIR = Path("Data Sets")
```

Check the selected notebook’s path configuration before running subsequent cells.

### 5. Run the workflow

Execute the notebook cells in order to load data, prepare features, train or load the required models, evaluate predictions, and export outputs where supported.

Some later notebooks depend on cached results from earlier experiments. Review their input requirements before starting a run.

## Evaluation Metric

The competition score combines overall toxicity performance with performance across the six attributes:

```text
Score = 0.5 × MacroF1(is_toxic)
      + 0.5 × Mean(positive-class F1 across the six attributes)
```

- Overall toxicity contributes **50%** of the score.
- Each remaining attribute contributes **1/12** of the total.
- Attribute F1 is computed across all evaluation rows.

This differs from ordinary seven-label macro-F1, micro-F1, and accuracy.

## Historical V38 Result

The project records **V38** as its selected historical submission, with a **reported public leaderboard score of approximately 0.608**.

This is a historical reported result, not an independently reproduced score or a verified private leaderboard result. Later version numbers identify additional experiments and do not necessarily indicate better performance.

Exact reproduction depends on the original dataset release, cached predictions, fitted components, and decision rules.

## Dataset Versions and Reproducibility

The repository contains artifacts associated with different dataset releases. The final audit notebook distinguishes:

| Dataset context | Training rows | Validation rows | Test rows |
|---|---:|---:|---:|
| Historical V38 release | 3,297 | 500 | 1,000 |
| Later package checked by the audit | 3,292 | 500 | 1,000 |

**Equal test-set sizes do not imply identical examples or IDs.**

Before evaluating or combining artifacts:

1. Confirm that the dataset and predictions belong to the same release.
2. Verify IDs and their ordering.
3. Check label names and column order.
4. Run the relevant audit checks.

Historical predictions must not be copied onto another release by row position. A new release requires predictions generated for that release’s exact test examples.

The audit also expects specific historical filenames. Do not assume differently named submission files are equivalent without checking their contents and IDs.

## Submission Format

Submission files must contain an `ID` column followed by seven binary prediction columns:

```csv
ID,is_toxic,implicit_toxicity,sarcasm,contains_profanity,threatening,identity_attack,sexual_content
example_001,1,0,0,1,0,0,0
example_002,0,0,0,0,0,0,0
```

The rows above are illustrative. Use the exact IDs and ordering required by the corresponding sample submission.

## Limitations

- Historical experiment artifacts may be required to reproduce particular versions.
- Repeated validation use can make development scores optimistic.
- Rare labels and subjective annotations complicate evaluation.
- Competition results do not establish performance in other domains.

This repository is intended for competition research and experimentation. Real-world moderation use requires additional evaluation and human oversight.

## Acknowledgments

Thanks to the Bengali NLP Safety Challenge 2026 organizers and the researchers and maintainers behind the datasets, pretrained models, and open-source libraries used in these experiments.

## Usage and Licensing

Follow the competition’s rules for dataset access, use, and redistribution, and check the licenses of individual pretrained models and external resources.

No repository-level license is currently included.

© Samira Ibrahim. All rights reserved.
