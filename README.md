# ALIEN_X · Bengali NLP Safety Challenge 2026

**Fine-grained Bengali toxicity detection with lexical models, pretrained transformers, and label-specific ensembles.**

[Explore the Notebooks](https://github.com/SamZx14/Bangali-Safety-NLP-Challange-Alien_X-2026/tree/main/NoteBooks) · [Final Audit](https://github.com/SamZx14/Bangali-Safety-NLP-Challange-Alien_X-2026/blob/main/Final/NLP_02_Alien_x.ipynb) · [Submission Archive](https://github.com/SamZx14/Bangali-Safety-NLP-Challange-Alien_X-2026/tree/main/csv)

---

## Overview

This repository documents **Team ALIEN_X’s** work for the **Bengali NLP Safety Challenge 2026: Fine-Grained Bengali Toxicity Understanding**.

The project explores how lexical features, contextual language models, and ensemble methods can identify toxicity across Bengali, Romanized Bengali, and mixed-language comments. It preserves the experiment history—from TF–IDF baselines to transformer ensembles and label-specific specialists—alongside prediction files, result archives, and reproducibility checks.

**Project highlights**

- Seven binary prediction targets covering overall toxicity and related attributes.
- TF–IDF and BanglaBERT ensemble baselines.
- Cross-script modeling and embedding-based classifiers.
- Label-specific blending, thresholds, and ranking rules.
- Historical V38 submission with a **reported public leaderboard score of approximately 0.608**.
- A dedicated audit notebook for checking dataset-version compatibility.

> **Repository status:** This is an experimental research archive. Individual notebooks can depend on version-specific datasets, cached predictions, or earlier experiment outputs.

## The Task

For each input comment, the system predicts seven binary labels:

| Label | Target |
|---|---|
| `is_toxic` | Overall toxicity |
| `implicit_toxicity` | Implicit toxicity |
| `sarcasm` | Sarcasm |
| `contains_profanity` | Profanity |
| `threatening` | Threatening content |
| `identity_attack` | Identity-directed attacks |
| `sexual_content` | Sexual content |

Each target is evaluated according to the competition’s annotations. Attribute predictions are separate outputs; sarcasm, identity mentions, or sexual content should not automatically be interpreted as overall toxicity.

## Modeling Approach

The project investigates complementary sources of predictive information:

| Component | Role |
|---|---|
| **TF–IDF + logistic regression** | Capture lexical patterns and provide a classical baseline |
| **BanglaBERT** | Learn contextual representations of Bengali comments |
| **Transliteration-oriented transformer experiments** | Explore Bengali, Romanized, and mixed-script inputs |
| **Frozen Bengali embeddings + linear classifiers** | Add semantic features without fully fine-tuning the embedding model |
| **Label-specific ensembles** | Combine selected predictions differently for each target |
| **Thresholds and ranking rules** | Convert scores into binary decisions |

### Historical V38 System

V38 combines selected outputs from earlier experiments. Its components include a BanglaBERT/TF–IDF baseline, historical model predictions, cross-script transformer scores, and embedding-based classifiers.

Different labels use different combinations and decision rules. Reproducing V38 therefore requires the corresponding historical inputs and intermediate artifacts, rather than running a single newly trained model.

Later notebooks explore sarcasm, identity-attack and sexual-content specialists, full-data refitting, frozen embedding ensembles, R-Drop, Mixout, and transfer learning. Their version numbers identify experiments; they do not imply steadily improving performance.

## Repository Guide

```text
Bangali-Safety-NLP-Challange-Alien_X-2026/
│
├── Data Sets/                 # Dataset files and alternate packaged data
├── Data zip/                  # Archived data bundles
│
├── NoteBooks/                 # Baselines and versioned experiments
│   ├── starter_kit.ipynb
│   ├── bengali_nlp_safety_colab_ready_v2.ipynb
│   ├── bengali_nlp_safety_colab_ready_v35_LIVE_crossscript.ipynb
│   └── ...
│
├── Final/                     # Final documentation and audit artifacts
│   ├── NLP_02_Alien_x.ipynb
│   ├── My final best submission is V38.docx
│   └── ...
│
├── Resources/                 # TF–IDF tutorial and reference materials
├── csv/                       # Submission files and saved probabilities
├── json/                      # Saved configuration files
│   └── optimized_v2_config.json
│
├── Results 1/                 # Archived experiment outputs
├── Results 2/
├── Results 3/
├── Results 4/
├── Results 4.1/
├── Results 4.2/
├── Results 4.3/
├── Results 5/
│
└── README.md
```

### Where to Start

| Goal | File |
|---|---|
| Understand the competition workflow | `NoteBooks/starter_kit.ipynb` |
| Explore the classical baseline | `Resources/Class_1_Bengali_NLP_Toxicity_TFIDF.ipynb` |
| Study the early ensemble | `NoteBooks/bengali_nlp_safety_colab_ready_v2.ipynb` |
| Inspect cross-script modeling | `NoteBooks/bengali_nlp_safety_colab_ready_v35_LIVE_crossscript.ipynb` |
| Explore the Kaggle dual-GPU variant | `NoteBooks/bengali_nlp_safety_v17_kaggle_dual_gpu.ipynb` |
| Check dataset and historical-artifact compatibility | `Final/NLP_02_Alien_x.ipynb` |
| Inspect saved baseline settings | `json/optimized_v2_config.json` |

> The notebook in `Final/` is a **reproducibility audit**. It checks dataset contracts and historical artifacts; it does not train V38 or generate a new competition submission.

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/SamZx14/Bangali-Safety-NLP-Challange-Alien_X-2026.git
cd Bangali-Safety-NLP-Challange-Alien_X-2026
```

### 2. Choose an Environment

Use **Google Colab**, **Kaggle Notebooks**, or a compatible local **Jupyter** environment.

For transformer experiments:

- Enable a GPU.
- Follow the selected notebook’s installation and setup cells.
- Check its required datasets, model downloads, and cached artifacts.
- Update paths for your runtime.
- Supply your own credentials when downloading competition data.

Dependencies and hardware requirements vary across experiments. The repository does not currently provide a single pinned environment for every notebook.

### 3. Configure the Data Paths

The standard dataset filenames are:

```text
train.csv
validation.csv
test.csv
sample_submission.csv
```

Set the selected notebook’s data path to the appropriate release. For example, when the working directory is the repository root:

```python
from pathlib import Path

DATA_DIR = Path("Data Sets")
```

When the working directory is `NoteBooks/`, the corresponding relative path is:

```python
DATA_DIR = Path("../Data Sets")
```

Some notebooks use Colab, Kaggle, or archive-specific paths. Review their configuration cells before execution.

### 4. Run the Selected Workflow

Execute notebook cells in order:

1. Install and import the required packages.
2. Load the correct dataset release.
3. Validate the schema and IDs.
4. Prepare features and train or load models.
5. Evaluate validation predictions where supported.
6. Apply the experiment’s ensemble and decision rules.
7. Export predictions in the required submission format.

For experiments that consume earlier outputs, prepare those artifacts before running dependent cells.

## Data Format

Labeled training and validation files contain:

```text
ID
text
is_toxic
implicit_toxicity
sarcasm
contains_profanity
threatening
identity_attack
sexual_content
```

Unlabeled test files contain:

```text
ID
text
```

### Dataset Versions Matter

The project includes artifacts associated with different releases:

| Release context | Training rows | Validation rows | Test rows |
|---|---:|---:|---:|
| Historical V38-aligned release | 3,297 | 500 | 1,000 |
| Later package checked by the final audit | 3,292 | 500 | 1,000 |

The final audit documents different test-ID sequences for these releases. Matching row counts do not establish compatibility.

Before combining datasets, probabilities, or submissions:

- Verify the dataset release.
- Match predictions using the correct IDs.
- Confirm ID ordering and label-column order.
- Run the relevant audit assertions.
- Check any required hashes or artifact-specific expectations.

**Never copy historical predictions onto a different test set by row position.** Predictions for another release must be generated for that release’s actual examples.

## Evaluation

The competition score gives equal total weight to overall toxicity and the six remaining attributes:

```text
Score = 0.5 × MacroF1(is_toxic)
      + 0.5 × Mean(positive-class F1 across the six attributes)
```

| Component | Contribution |
|---|---:|
| Macro-F1 for `is_toxic` | 50% |
| Positive-class F1 for each remaining attribute | 8⅓% |

Toxicity macro-F1 averages F1 across the negative and positive classes. Each attribute uses positive-class F1 across all evaluation rows.

This metric differs from ordinary seven-label macro-F1, micro-F1, and accuracy. Comparisons should use the same scoring function and dataset release.

## Results and Configuration

### Historical V38 Result

| Item | Status |
|---|---|
| Selected historical submission | V38 |
| Reported public leaderboard score | Approximately **0.608** |
| Independent reproduction of that score | Not established |
| Private leaderboard result | Not verified here |

The reported score describes the historical competition submission. It should not be interpreted as performance on another dataset release or as a general deployment benchmark.

### Saved V2 Baseline Configuration

The saved configuration in `json/optimized_v2_config.json` records:

| Setting | Value |
|---|---|
| Transformer | `csebuetnlp/banglabert` |
| Random seed | `42` |
| Maximum sequence length | `128` |
| Learning rate | `2e-5` |
| Training epochs | `5` |
| Transformer ensemble weight | `0.70` |
| TF–IDF ensemble weight | `0.30` |

These settings describe the saved **V2 baseline**. They are not the complete V38 configuration. The configuration’s `validation_macro_f1` field should also not be treated as the official competition score without confirming how it was calculated.

## Submission Format

A submission contains the test IDs followed by seven binary prediction columns:

```csv
ID,is_toxic,implicit_toxicity,sarcasm,contains_profanity,threatening,identity_attack,sexual_content
example_001,1,0,0,1,0,0,0
example_002,0,0,0,0,0,0,0
```

These rows are illustrative. Use the exact IDs and ordering from the relevant sample submission.

Before submission, confirm:

- The column names and order match the sample submission.
- Every required test ID appears exactly once.
- Predictions contain only `0` and `1`.
- No values are missing.
- The predictions belong to the intended dataset release.

The archive includes `csv/submission_v38_NO_PN.csv`, while the audit expects a historical artifact named `submission_v38_NO_PROFANITY_ABLATION.csv`. Verify their contents and provenance before treating them as equivalent.

## Reproducibility and Limitations

This repository preserves development history, but exact reproduction of every experiment is not guaranteed.

- Some notebooks depend on cached predictions, archives, or fitted components from earlier runs.
- Historical pretrained-model revisions and environments may not be fully pinned.
- Repeated validation use can make development results optimistic.
- Rare attributes and annotation disagreement complicate evaluation.
- Public leaderboard performance does not establish generalization to other platforms, topics, or communities.

For a new experiment, record the dataset version, notebook version, dependencies, random seeds, model revisions, decision thresholds, and output hashes.

## Responsible Use

This project supports research into Bengali online safety. Model predictions can be affected by context, dialect, spelling variation, code-mixing, and annotation choices.

Use additional evaluation and human review before applying the models to consequential moderation decisions. Dataset access and redistribution must follow the competition’s terms, and external models and resources retain their respective licenses.

## Acknowledgments

Developed by **Team ALIEN_X** for the **Bengali NLP Safety Challenge 2026**.

Thanks to the competition organizers, dataset contributors, and the researchers and maintainers behind the pretrained models and open-source tools used throughout the project.

## License

No repository-level license is currently included. Consult the repository owner for reuse permissions and review the applicable terms for datasets, pretrained models, and third-party resources separately.

© Samira Ibrahim. All rights reserved.
