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

# deployment_and_R&D folder includes:

1. curation of data (using huggingface datasets)

2. training of random forest model to be used as one of the modelsin ensemble model which will built later (using sklearn)

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
    - OPTIMIZER = paged_adamw_32bit

4. observabiliy:
    - LOG_TO_WANDB = True # log to wandb
    - WANDB_PROJECT = "agantic-ai-pricing-solution" # wandb project
    - WANDB_LOG_MODEL = "checkpoint" # log model to wandb
    - WANDB_ENTITY = "agantic-ai" # wandb entity
    - WANDB_NAME = "agantic-ai-pricing-solution" # name of the run
    - STEPS = 100 # log every 100 steps
    - SAVE_STEPS = 5000 # save model every 5000 steps

# LLM Agents

1. Specialist Agent: This agent works based on fine-tuned Llama 3 model.

2. Frontier Agent: This agent works based on RAG (Retrieval-Augmented Generation) with Sentence Transformer and ChromaDB.

3. Random Forest Agent: This agent works based on Random Forest model on top of vectorized ChromaDB using Sentence Transformer.

4. Ensemble Agent: This agent works based on Ensemble of the above agents.

5. Scanner Agent: This agent works based on scanning the web for new products in RSS feeds.

6. Message Agent: This agent works based on sending messages to the user. Platform is pushover.net.

7. Planner Agent: This agent works based on planning the next step based on the current state of the system.

# LLM Framework

1.agent_framework_backend.py: This file contains the backend for the LLM framework.

2.agent_framework_frontend.py: This file contains the frontend for the LLM framework.


# Environment variables are stored in .env file:

```bash
OPENAI_API_KEY
HF_TOKEN
PUSHOVER_TOKEN # should be set in pushover.net
PUSHOVER_USER # should be set in pushover.net
WANDB_API_KEY # should be set in integration of huggingface and wandb.
MODAL_SECRET_KEY # should be set in modal.com and copy pased and named as hf_secrect
```






