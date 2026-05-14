# SmolVLM vs DINOv2 on Oxford-IIIT Pets

This repository contains my final experiment comparing a fine-tuned visual-language model against a dedicated vision classifier for pet breed recognition on the Oxford-IIIT Pet dataset.

I used the project to answer a practical question: if the task is fixed-label image classification, how much do I gain from a purpose-built DINOv2 classifier compared with a smaller VLM that answers in natural language?

## Short Answer

DINOv2-small was the stronger model for closed-set breed classification.

| Model | Task | Train Samples | Test Samples | Accuracy | Macro F1 |
|---|---|---:|---:|---:|---:|
| DINOv2-small | closed-set image classification | 1,200 | 500 | 80.4% | 79.2% |
| SmolVLM-256M-Instruct | image + question to breed text | 600 | 200 | 33.0% | 29.7% |

The VLM is more flexible because it can answer as text, but that flexibility hurt strict label evaluation. Some outputs were close but not directly mappable, and 24 predictions were mapped to `unknown`.

## What Is Inside

| File | Purpose |
|---|---|
| `final_smolvlm_dino_comparison_kaggle (1).ipynb` | Main Kaggle notebook for the final comparison workflow. |
| `final_smolvlm_dino_comparison_kaggle (1).csv` | Model-level summary metrics. |
| `final_smolvlm_dino_comparison_kaggle (2).csv` | SmolVLM row-level predictions. |
| `final_smolvlm_dino_comparison_kaggle (3).csv` | DINOv2 row-level predictions. |
| `final_smolvlm_dino_comparison_kaggle (2).json` | Dataset, model, split, and metric metadata. |
| `final_smolvlm_dino_comparison_kaggle (2).png` | DINOv2 confusion matrix. |
| `final_smolvlm_dino_report.docx` | Final written report generated from the available results. |
| `scripts/summarize_results.py` | Lightweight script to verify the exported metrics. |

The extra notebooks are intermediate Kaggle runs that I kept for traceability while iterating on the final workflow.

## Dataset

I used `timm/oxford-iiit-pet`, which contains 37 cat and dog breed classes. The raw dataset is not checked into this repository; it is loaded through the Hugging Face `datasets` library in the notebooks.

## Models

- `facebook/dinov2-small`
- `HuggingFaceTB/SmolVLM-256M-Instruct`

DINOv2 was evaluated as a direct image classifier. SmolVLM was evaluated by asking the model for the breed name from an image-question pair, then mapping the generated text back to the known breed labels.

## Reproduce the Summary

Create an environment with the dependencies:

```bash
pip install -r requirements.txt
```

Then run:

```bash
python scripts/summarize_results.py
```

Expected headline output:

```text
DINOv2-small accuracy: 80.4%
SmolVLM mapped accuracy: 33.0%
Accuracy gap: 47.4 percentage points
```

To rerun training/evaluation, open the final notebook in Kaggle or Jupyter and execute the cells in order. A GPU runtime is recommended for model training and inference.

## Notes From My Experiment

- DINOv2 is the better choice when the output space is fixed and the goal is accurate breed classification.
- SmolVLM needs stricter answer formatting, more training examples, or stronger post-processing before it is competitive on this exact benchmark.
- The comparison is not perfectly apples-to-apples because the available final exports use different train/test subset sizes for the two models. I treated the results as an experimental comparison, not a formal benchmark paper.

