# TSAR 2025 - Shared Task on Readability-Controlled Text Simplification

This repository contains the data and code used for the TSAR 2025 Shared Task. More information on the Shared Task setup can be found on the website: https://tsar-workshop.github.io/shared-task/

The Shared Task Findings paper is now published at ACL: https://aclanthology.org/2025.tsar-1.8/

## Shared Task Evaluation Script

This script evaluates system submissions against the official TSAR-2025 gold data. It loads each team’s `.jsonl` run, aligns predictions using `text_id`, and computes CEFR and semantic similarity metrics.  

### Process
- Reads gold data (`tsar2025_test.jsonl`) and submissions from `submissions/<team>/`.
- Aligns system outputs to gold entries (partial submissions supported).
- Computes:
  - **CEFR metrics**: Weighted F1, Adjacent Accuracy (±1 level), RMSE  
    (via three ModernBERT CEFR classifiers)
  - **MeaningBERT similarity** to original and reference texts
  - **BERTScore F1** to original and reference texts
- Produces a summary table and saves it to `results.xlsx`.

### Submission Format
Each JSONL line must contain:
```json
{
  "text_id": "...",
  "simplified": "..."
}
```

### Output
- Console summary of all runs.
- A file `results.xlsx` containing coverage, CEFR metrics, MeaningBERT, and BERTScore for each submission.

### Requirements
`transformers>=4.55`, `torch`, `numpy`, `pandas`, `scikit-learn`, `evaluate`

## Organizers
* Fernando Alva-Manchego (Cardiff University, UK)
* Regina Stodden (University of Bielefeld, Germany — LLM4KMU Project)
* Kai North (Cambium Assessment, USA)
* Joseph Marvin Imperial (National University Philippines and University of Bath, UK)
* Abdullah Barayan (Cardiff University, UK)
* Harish Tayyar Madabushi (University of Bath, UK)
