---
description: >-
  Introducing the Arcee+Langchain Integration: Leverage Domain Adapted Language
  Models for Enhanced Text Generation
---

# ⛓ Arcee<>Langchain

## Integrating Arcee+Langchain: Domain Adapted Language Models for Enhanced Text Generation

### Introduction

Arcee seamlessly integrates with Langchain to provide enhanced text generation using Domain Adapted Language Models (DALMs). This guide will walk you through the setup and usage of this powerful combination.

### Setting Up

1.  Install the necessary packages with pip.

    ```sh
    pip install -q langchain arcee-py
    ```

    If you don't have an API key, sign up for a free account at [Arcee.ai](https://arcee.ai).
2.  Set your `ARCEE_API_KEY` environment variable or pass it directly when creating an instance.

    ```sh
    export ARCEE_API_KEY='your_api_key_here'
    ```

    Alternatively, include the API key directly in your script:

    ```python
    from langchain.llms import Arcee
    arcee = Arcee(model="DALM-your_domain", arcee_api_key="ARCEE-API-KEY")
    ```

### Configuration

With Arcee, you can customize settings such as API URLs and model arguments:

```python
arcee = Arcee(
    model="DALM-Patent",
    model_kwargs={
        "size": 5,
        "filters": [
            {"field_name": "document", "filter_type": "fuzzy_search", "value": "innovation"}
        ]
    }
)
```

Adjust these parameters according to your domain-specific needs.

### Generating Text with Contextual Awareness

Arcee enables text generation enriched with contextual depth:

```python
prompt = "Explore the role of AI in renewable energy advances."
response = arcee.generate(prompt, size=10, filters=[
    {"field_name": "document", "filter_type": "fuzzy_search", "value": "solar energy"}
])
print(response)
```

### Document Retrieval with ArceeRetriever

ArceeRetriever complements the text generation by retrieving contextual documents:

```python
from langchain.retrievers import ArceeRetriever

retriever = ArceeRetriever(model="DALM-PubMed", arcee_api_key="ARCEE-API-KEY")
documents = retriever.get_relevant_documents(query="Neural Networks", size=5)
for doc in documents:
    print(doc.get('title'))
```

### Combining Retrieval and Generation

Use the `ArceeRetriever` class to inform the generation process with retrieved documents, creating enriched content:

```python
# Retrieve documents with ArceeRetriever
documents = retriever.get_relevant_documents(query="Impact of AI on healthcare", size=5)

# Generate informed text with Arcee
response = arcee.generate(prompt, context_documents=documents)
print(response)
```

### Using Arcee with Agents

Create an Agent with Arcee at its core for intelligent task handling:

```python
from langchain.agents import initialize_agent
from langchain.llms import Arcee

# Initialize Arcee
arcee = Arcee(model="DALM-PubMed", arcee_api_key="ARCEE-API-KEY")

# Initialize the agent
agent = initialize_agent(agent_type="Zero-Shot", llm=arcee, verbose=True)
result = agent.run("Explain the developments in bioinformatics.")
print(result)
```
