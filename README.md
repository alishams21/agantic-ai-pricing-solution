# agantic-ai-pricing-solution
This repository contains the components of dynamic pricing engine, leveraging LLM, ML and data analytics to optimize product pricing strategies with push notifications for bargain opportunities and price drops.

# Architecture

![Architecture](images/architecture.jpg)

# Test and PoC Environment

Tests are run in a separate environment to avoid conflicts and PoC for building the components done in Jupyter Notebook.

- **Create a virtual environment**

```bash
conda env create -f environment.yml 
```


- **Activate the virtual environment**

```bash
conda activate llms
```

- lunch jupyter lab

```bash
jupyter lab
```
### tests folder includes:

1. curation of data (using huggingface datasets)

2. training of random forest model (using sklearn)

3. finetuning of openai model (using openai api)

4. finetuning Llama 3 model:
    - QLoRA
    - QUANTIZATION = 4bit
    - R (for rank) = 16
    - ALPHA (for lora a, lora b) = 32
    - TARGET (for attention head "q_proj", "v_proj", "k_proj", "o_proj")
    - DROPOUT = 0.1
    - EPOCHS = 3
    - BATCH_SIZE = 8
    - LEARNING_RATE = 0.0001
    - LEARNING_SCHEDULER_TYPE = cosine
    - WARMUP_RATIO = 0.03
    - GRADIENT_ACCUMULATION = 1
    - OPTIMIZER = paged_adamw_3bit

4. observabiliy:
    - LOG_TO_WANDB = True # log to wandb
    - WANDB_PROJECT = "agantic-ai-pricing-solution" # wandb project
    - WANDB_LOG_MODEL = "checkpoint" # log model to wandb
    - WANDB_ENTITY = "agantic-ai" # wandb entity
    - WANDB_NAME = "agantic-ai-pricing-solution" # name of the run
    - STEPS = 100 # log every 100 steps
    - SAVE_STEPS = 5000 # save model every 5000 steps

## LLM Agent

## Data Agent

## Pricing Agent