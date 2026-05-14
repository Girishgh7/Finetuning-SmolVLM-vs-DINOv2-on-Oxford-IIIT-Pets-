# Reproducibility Notes

These notes describe how I would rerun or verify the project from a clean environment.

## Environment

I developed the experiment in a Kaggle-style notebook workflow. A GPU runtime is recommended for rerunning training and inference. The summary script can run on CPU because it only reads exported CSV/JSON files.

Install dependencies:

```bash
pip install -r requirements.txt
```

## Verify Exported Results

Run:

```bash
python scripts/summarize_results.py
```

The script reads the final CSV and JSON exports and prints the headline metrics, row-level counts, and a few error-pattern checks.

## Rerun the Notebook

1. Open `final_smolvlm_dino_comparison_kaggle (1).ipynb`.
2. Use a GPU runtime.
3. Run the dependency/setup cells first.
4. Execute the dataset loading and split cells.
5. Train/evaluate SmolVLM and DINOv2.
6. Export the CSV/JSON/PNG files used in the report.

## What Is Not Committed

Raw datasets, downloaded model weights, checkpoints, cache directories, and experiment tracking folders are intentionally ignored. They can be regenerated from the notebook and dependency files.
