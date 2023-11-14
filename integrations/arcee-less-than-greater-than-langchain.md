# ⛓ Arcee<>Langchain

## Enhancing Models with Domain Expertise: The Arcee+Langchain Solution for Specialized Language Models

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

For this cookbook, we'll be using `DALM-PubMed`, you can train your own DALMs using our [DALM toolkit](https://github.com/arcee-ai/DALM)!

***

### Configuration

With Arcee+Langchain, you can customize settings such as API URLs and model arguments:

```python
arcee = Arcee(
    model="DALM-PubMed",
    model_kwargs={
        "size": 5,
        "filters": [
            {
            "field_name": "document", 
            "filter_type": "fuzzy_search", 
            "value": "innovation"
            }
        ]
    }
)
```

Adjust these parameters according to your domain-specific needs.

Arguments:

* field\_name: The field to filter on. Can be 'document' or 'name' to filter on your document's raw text or title Any other field will be presumed to be a metadata field you included when uploading your context data&#x20;
* Select between 'fuzzy\_search' for a flexible match allowing variance within the target field, and 'strict\_search' for a precise match requiring the exact term to appear in the field. 'fuzzy\_search' can identify related terms even when the exact match is absent, while 'strict\_search' ensures the specific term is present, but does not require an exact phrase match.
* value: The actual value to search for in the context data/metadata

{% hint style="info" %}
You invoke the model even without model\_kwargs.
{% endhint %}

```python
from langchain.llms import Arcee

# Create an instance of the Arcee class
arcee = Arcee(
    model="DALM-PubMed",
    arcee_api_key="ARCEE-API-KEY" # if not already set in the environment
)
```

### Generating Text with Contextual Awareness

Arcee enables text generation enriched with contextual depth:

```python
prompt = "Explore the role of AI in neuroscience."
response = arcee.generate(prompt, size=10, 
        filters=[
            {
            "field_name": "document", 
            "filter_type": "fuzzy_search", 
            "value": "solar energy"
            }
])
print(response)
```

### Document Retrieval with ArceeRetriever

ArceeRetriever complements the text generation by retrieving contextual documents:

```python
from langchain.retrievers import ArceeRetriever

retriever = ArceeRetriever(model="DALM-PubMed", arcee_api_key="ARCEE-API-KEY")
documents = retriever.get_relevant_documents(query="Neurobiology", size=5)
```

### Combining Retrieval and Generation

Use the `ArceeRetriever` class to inform the generation process with retrieved documents, creating enriched content:

{% hint style="info" %}
Note: while using `arcee.generate,` pass your prompts as a list.
{% endhint %}

```python
# Retrieve documents with ArceeRetriever
documents = retriever.get_relevant_documents(query="Impact of AI on healthcare", size=5)

# Generate informed text with Arcee
response = arcee.generate([prompt], context_documents=documents)
print(response)
```
