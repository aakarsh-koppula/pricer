---
base_model: meta-llama/Llama-3.2-3B
library_name: transformers
model_name: price-2025-11-28_18.47.07
tags:
- generated_from_trainer
- trl
- sft
licence: license
---

# Model Card for price-2025-11-28_18.47.07

This model is a fine-tuned version of [meta-llama/Llama-3.2-3B](https://huggingface.co/meta-llama/Llama-3.2-3B).
It has been trained using [TRL](https://github.com/huggingface/trl).

## Quick start

```python
from transformers import pipeline

question = "If you had a time machine, but could only go to the past or the future once and never return, which would you choose and why?"
generator = pipeline("text-generation", model="ed-donner/price-2025-11-28_18.47.07", device="cuda")
output = generator([{"role": "user", "content": question}], max_new_tokens=128, return_full_text=False)[0]
print(output["generated_text"])
```

## Training procedure

[<img src="https://raw.githubusercontent.com/wandb/assets/main/wandb-github-badge-28.svg" alt="Visualize in Weights & Biases" width="150" height="24"/>](https://wandb.ai/ed-donner/price/runs/5qbw6oh4) 


This model was trained with SFT.

### Framework versions

- TRL: 0.25.1
- Transformers: 4.57.2
- Pytorch: 2.9.0+cu126
- Datasets: 4.0.0
- Tokenizers: 0.22.1

## Citations



Cite TRL as:
    
```bibtex
@misc{vonwerra2022trl,
	title        = {{TRL: Transformer Reinforcement Learning}},
	author       = {Leandro von Werra and Younes Belkada and Lewis Tunstall and Edward Beeching and Tristan Thrush and Nathan Lambert and Shengyi Huang and Kashif Rasul and Quentin Gallou{\'e}dec},
	year         = 2020,
	journal      = {GitHub repository},
	publisher    = {GitHub},
	howpublished = {\url{https://github.com/huggingface/trl}}
}
```