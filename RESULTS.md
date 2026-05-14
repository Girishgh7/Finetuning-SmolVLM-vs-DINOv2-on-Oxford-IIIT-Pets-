# Results

This page summarizes the available exported metrics for my SmolVLM vs DINOv2 comparison on Oxford-IIIT Pets.

## Model-Level Metrics

| Model | Evaluation Style | Train Samples | Test Samples | Accuracy | Macro F1 |
|---|---|---:|---:|---:|---:|
| DINOv2-small | Direct closed-set classifier | 1,200 | 500 | 80.4% | 79.2% |
| SmolVLM-256M-Instruct | Image-question to text, mapped back to labels | 600 | 200 | 33.0% | 29.7% |

## Key Takeaways

- DINOv2-small performed much better for the strict classification task.
- SmolVLM produced natural-language answers, which made evaluation harder because generated text needed to be normalized back to a breed label.
- The SmolVLM result included 24 `unknown` mapped predictions out of 200 examples.
- DINOv2 had 402 correct predictions out of 500 examples.
- SmolVLM had 66 mapped-class correct predictions out of 200 examples.

## Caveat

The two models were evaluated on different subset sizes in the available final exports. I kept the comparison transparent and reported the exact sample counts instead of presenting it as a fully controlled benchmark.

## Source Files

- `final_smolvlm_dino_comparison_kaggle (1).csv`
- `final_smolvlm_dino_comparison_kaggle (2).csv`
- `final_smolvlm_dino_comparison_kaggle (3).csv`
- `final_smolvlm_dino_comparison_kaggle (2).json`
- `final_smolvlm_dino_comparison_kaggle (2).png`
