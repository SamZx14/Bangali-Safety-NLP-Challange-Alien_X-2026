# BUBT Bengali NLP Safety Challenge 2026
## System Description Paper Template

This Overleaf-ready LaTeX project is intended for teams submitting system-description papers to the BUBT Bengali NLP Safety Challenge 2026.

## Quick start

1. Upload the ZIP file directly to Overleaf using **New Project > Upload Project**.
2. Open `main.tex`.
3. For anonymous review, use:

```latex
\usepackage[review]{bubtcompetition}
```

4. For the final camera-ready paper, use:

```latex
\usepackage[final]{bubtcompetition}
```

5. Replace the example title, authors, team ID, text, results, tables, and references.
6. Compile using pdfLaTeX.

## Recommended paper length

- Main paper: 4--6 pages.
- References: excluded from the main limit unless the organizers specify otherwise.
- Appendix: optional; organizers may choose whether it is included in the limit.

## Required content

A complete system description should normally include:

- Abstract
- Introduction
- Task Description
- Dataset
- System Overview
- Methodology
- Experimental Setup
- Results
- Error Analysis
- System Submission Information
- Reproducibility Statement
- Limitations
- Ethical Considerations
- Conclusion
- References

Ablation analysis is strongly encouraged when applicable.

## Competition labels

The template includes the seven competition labels:

- `is_toxic`
- `implicit_toxicity`
- `sarcasm`
- `contains_profanity`
- `threatening`
- `identity_attack`
- `sexual_content`

## Disclosure requirements

Teams should disclose:

- external datasets;
- pretrained models;
- commercial or open LLM/API use;
- retrieval resources;
- data augmentation;
- ensemble methods;
- manual post-processing;
- code availability.

Do not report fabricated leaderboard scores or experiments that were not performed.

## Files

- `main.tex` -- main paper source
- `bubtcompetition.sty` -- formatting and review/final modes
- `references.bib` -- example bibliography
- `figures/` -- place figures here
- `AUTHOR_GUIDELINES.md` -- concise submission rules

## Suggested organizer policy

The organizers may adopt the following wording:

> Each participating team must submit a system-description paper describing the final competition system. The paper must report enough methodological and implementation detail to permit meaningful scientific comparison. All external data, pretrained models, generative-AI tools, APIs, and post-processing procedures must be disclosed. Fabricated results, plagiarism, or undisclosed use of prohibited resources may result in rejection or disqualification.

