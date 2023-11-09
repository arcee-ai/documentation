---
description: >-
  This is a tutorial from Arcee and AI Makerspace on how to train an end to end
  RAG model jointly with retriever and generator to create a Domain Adapted
  Language Model (a DALM). E2E RAG training allows
---

# E2ERAG Cookbook

The model we train will learn how to retrieve documents from our context documents and generate responses in a unified system.

We will:

* Clone and Install DALM dependencies
* Prepare a toy dataset
* Run E2E RAG training for our DALM
* Run inference on our trained DALM
* Export our trained retriever model
* Query example DALMs at https://app.arcee.ai

![e2erag](https://i.imgur.com/0uMWN8H.png)

```python
!nvidia-smi
```

## Install the DALM repo `indomain`

We will install DALM package https://github.com/arcee-ai/DALM from pypi!

**DALM**

```python
!pip install -qqq indomain
```

## Prepare Dataset of Examples

E2E RAG requires a dataset of \[passage, question, answer] triples

At inference time, our model will take a users query, draw from the available passages, and pass relevant context to the generator to create an answer.

### Toy Dataset

For this tutorial we will train a simple toy dataset to show how the E2E RAG training can be accomplished. To build your own DALM, you should train on your own documents

### Generating Q+A Pairs

If you do not have labeled triples, you can generate QA pairs with:

```
dalm qa-gen path/to/dataset.csv
```

for example to generate QA pairs with the "taesiri/arxiv\_qa" hugging face dataset:

```
!dalm qa-gen "taesiri/arxiv_qa" --output-dir qa-outputs --passage-column-name text --title-column-name title
```

For more information, you can run `dalm qa-gen --help`

```python
import pandas as pd
df = pd.read_csv("https://raw.githubusercontent.com/arcee-ai/DALM/main/dalm/datasets/toy_data_train.csv")
df.to_csv("dataset.csv")
df.head()
```

## Train DALM model with gpt-neo-125m generator and bge-large-en retriever

For this demo notebook, we will train a small 125 million GPT Neo model and we will train the small bge retriever model.

For better results, you will want to substitute `meta-llama/Llama-2-7b` and `bge-large-en`. You will need a bigger GPU (like A10080GB) to train this - and make sure to adjust batch size to saturate your GPU memory

```python
!dalm train-rag-e2e \
"./dataset.csv" \
"BAAI/bge-large-en" \
"EleutherAI/gpt-neo-125m" \
--output-dir "./rag_e2e_checkpoints" \
--with-tracking \
--report-to all \
--per-device-train-batch-size 1
```

## Evaluate Retriever Training

Here we will evalauate our contextualized retriever against our passage data that we will have in our database at retrieval time

```python
!dalm eval-rag "./dataset.csv" \
  --retriever-name-or-path "BAAI/bge-large-en" \
  --generator-name-or-path "EleutherAI/gpt-neo-125m" \
  --passage-column-name Abstract \
  --query-column-name Question \
  --answer-column-name Answer \
  --evaluate-generator \
  --query-batch-size 5 \
  --retriever-peft-model-path ./rag_e2e_checkpoints/retriever \
  --generator-peft-model-path ./rag_e2e_checkpoints/generator
```

## Query Example DALM

In this tutorial, we showed how to train a retriever model with a small generator. To see a DALM in production, we can query DALM models on https://app.arcee.ai to get an idea for their behavior at scale.

For example, we can query `DALM-Patent` on https://app.arcee.ai that has been trained on the USPTO Patent database

![infergif](https://arcee-public.s3.us-east-2.amazonaws.com/infer.gif)
