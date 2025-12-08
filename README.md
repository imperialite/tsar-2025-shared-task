# TSAR 2025 - Shared Task on Readability-Controlled Text Simplification

This repository provides the **official evaluation code and key resources** for the TSAR 2025 Shared Task on developing systems for **Readability-Controlled Text Simplification (RCTS)**. The task requires generating simplified text targeted at specific **CEFR** (Common European Framework of Reference) levels.


## Key Resources

| Resource | Description |
| :--- | :--- |
| **Shared Task Website** | [https://tsar-workshop.github.io/shared-task/](https://tsar-workshop.github.io/shared-task/) |
| **Hugging Face Collection** | **Train/Test Data and CEFR Models** are available here: [https://huggingface.co/collections/cardiffnlp/tsar-2025-shared-task-on-rcts](https://huggingface.co/collections/cardiffnlp/tsar-2025-shared-task-on-rcts) |
| **Findings Paper** | Official summary and results published in the ACL Anthology: [https://aclanthology.org/2025.tsar-1.8/](https://aclanthology.org/2025.tsar-1.8/) |

## Evaluation Scripts

| Script | Purpose | Notes |
| :--- | :--- | :--- |
| `tsar2025_evaluation_script.py` | **Official Evaluation:** Computes all final scores (CEFR, MeaningBERT, BERTScore). | Produces an Excel file (`results.xlsx`). Handles incomplete runs. |
| `tsar2025_autorank.ipynb` | **Ranking Analysis:** Computes system comparisons using the AutoRank methodology. | Provides detailed statistical comparisons between submitted systems. |


## Submission Format

### Submission Structure

The `tsar2025_evaluation_script.py` script expects the following file organization in your local directory:
```
tsar2025_evaluation_script.py
tsar2025_test.jsonl # The gold test set with references
submissions/ 
└── Team/ 
 ├── run1.jsonl 
 └── run2.jsonl
```
The script will:
1. Read gold data (`tsar2025_test.jsonl`) and submissions from `submissions/<team>/`.
2. Align system outputs to gold entries (partial submissions supported).
3 Compute:
  - **CEFR metrics**: Weighted F1, Adjacent Accuracy (±1 level), RMSE  
    (via three ModernBERT CEFR classifiers)
  - **MeaningBERT similarity** to original and reference texts
  - **BERTScore F1** to original and reference texts
4. Produce a summary table and saves it to `results.xlsx`.

### Submission File Format (`.jsonl`)

Submissions must be provided as **JSON Lines (`.jsonl`)** files. Each line must contain two required fields:

| Field | Description |
| :--- | :--- |
| `text_id` | The identifier of the corresponding entry in the test dataset. |
| `simplified` | The system-generated simplification, targeting the required CEFR level. |

**Example Submission:**

```jsonl
{"text_id": "TSAR-0001", "simplified": "The dog ran quickly to fetch the ball."}
{"text_id": "TSAR-0002", "simplified": "She felt very sad when the movie ended."}
```

## Citation
If you use the TSAR 2025 Shared Task data or evaluation pipeline in your research, please cite the following work:

> Fernando Alva-Manchego, Regina Stodden, Joseph Marvin Imperial, Abdullah Barayan, Kai North, and Harish Tayyar Madabushi. 2025. [Findings of the TSAR 2025 Shared Task on Readability-Controlled Text Simplification](https://aclanthology.org/2025.tsar-1.8/). In *Proceedings of the Fourth Workshop on Text Simplification, Accessibility and Readability (TSAR 2025)*, pages 116–130, Suzhou, China. Association for Computational Linguistics.


```BibTeX
@inproceedings{alva-manchego-etal-2025-findings,
    title = "Findings of the {TSAR} 2025 Shared Task on Readability-Controlled Text Simplification",
    author = "Alva-Manchego, Fernando  and
      Stodden, Regina  and
      Imperial, Joseph Marvin  and
      Barayan, Abdullah  and
      North, Kai  and
      Tayyar Madabushi, Harish",
    editor = "Shardlow, Matthew  and
      Alva-Manchego, Fernando  and
      North, Kai  and
      Stodden, Regina  and
      Saggion, Horacio  and
      Khallaf, Nouran  and
      Hayakawa, Akio",
    booktitle = "Proceedings of the Fourth Workshop on Text Simplification, Accessibility and Readability (TSAR 2025)",
    month = nov,
    year = "2025",
    address = "Suzhou, China",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2025.tsar-1.8/",
    doi = "10.18653/v1/2025.tsar-1.8",
    pages = "116--130",
    ISBN = "979-8-89176-176-6",
    abstract = "This paper presents the findings of the first Shared Task on Readability-Controlled Text Simplification at TSAR 2025. The task required systems to simplify English texts to specific target readability levels of the Common European Framework of Reference for Languages (CEFR). We received 48 submissions from 20 participating teams, with approaches predominantly based on large language models (LLMs), which included iterative refinement, multi-agent setups, and LLM-as-a-judge pipelines. For this shared task, we developed a new dataset of pedagogical texts and evaluated submissions using a weighted combination of semantic similarity and CEFR-level accuracy. The results of the participating teams demonstrate that while LLMs can perform substantially well on this task, dependable and controlled simplification often requires complex, multi-iterative processes. Our findings also suggest that the capabilities of current systems are beginning to saturate existing automatic evaluation metrics, underscoring the need for reevaluation and practicality."
}
```

## Organizers
* [Fernando Alva-Manchego](https://feralvam.github.io/) (Cardiff University, UK)
* [Regina Stodden](https://scholar.google.com/citations?hl=de&user=nYP4mXYAAAAJ) (University of Bielefeld, Germany — LLM4KMU Project)
* [Joseph Marvin Imperial](https://www.josephimperial.com/) (National University Philippines and University of Bath, UK)
* [Abdullah Barayan](https://scholar.google.com/citations?user=jIuEUPAAAAAJ) (Cardiff University, UK)
* [Kai North](https://www.linkedin.com/in/kai-n/) (Cambium Assessment, USA)
* [Harish Tayyar Madabushi](https://www.harishtayyarmadabushi.com/) (University of Bath, UK)
