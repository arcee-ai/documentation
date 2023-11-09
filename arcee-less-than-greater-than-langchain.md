---
description: >-
  Introducing the Arcee+Langchain Integration: Leverage Domain Adapted Language
  Models for Enhanced Text Generation
---

# ⛓ Arcee<>Langchain

## Introducing the Arcee+Langchain Integration: Leverage Domain Adapted Language Models for Enhanced Text Generation



###

### Setting Up

Getting started with Arcee is straightforward. By setting the `ARCEE_API_KEY` environment variable or passing the API key as a named parameter, users can create an instance of the Arcee class and begin generating text in a matter of minutes.

```bash
pip install -q langchain arcee-py
```

If you don't have an API key, you can sign up for a free account at [https://arcee.ai](https://arcee.ai).

```python
from langchain.llms import Arcee

arcee = Arcee(
    model="DALM-PubMed",
    # arcee_api_key="ARCEE-API-KEY" # Alternative setup method
)
```

### Configuration Flexibility

Arcee offers flexibility in configuration, allowing users to adjust parameters such as API URLs and model arguments to best meet their needs.

```python
arcee = Arcee(
    model="DALM-Patent",
    arcee_api_url="https://custom-api.arcee.ai",
    arcee_app_url="https://custom-app.arcee.ai",
    model_kwargs={
        "size": 5,
        "filters": [{"field_name": "document", "filter_type": "fuzzy_search", "value": "Einstein"}],
    },
)
```

This level of customization means Arcee can perfectly align with bespoke user requirements for precise and targeted text generation.

### Generating Text with Contextual Awareness

Arcee stands out by enabling the generation of text that’s not only original but potentially more relevant and informed, enriching the resulting content with contextual depth:

```python
prompt = "Can AI-driven music therapy contribute to the rehabilitation of patients with disorders of consciousness?"
response = arcee(prompt, size=5, filters=[
    {"field_name": "document", "filter_type": "fuzzy_search", "value": "Einstein"},
    {"field_name": "year", "filter_type": "strict_search", "value": "1905"},
])
```

Filters and size parameters allow for nuanced control over the material used to inform the model’s generation process, offering a powerful toolset for custom content creation.

### Arcee Retriever: A Partner in Content Discovery

Complementing the text generation engine is the [ArceeRetriever](https://github.com/langchain-ai/langchain/blob/master/libs/langchain/langchain/retrievers/arcee.py) class, which facilitates the retrieval of contextually relevant documents that inform and enrich the text generation process. The same ease of use and configurability apply, offering robust document retrieval to make the most of Arcee’s DALMs.

```python
from langchain.retrievers import ArceeRetriever

retriever = ArceeRetriever(
    model="DALM-PubMed",
    # Additional configuration options available
)
```

By submitting queries, users can harvest pertinent documents from a corpus of uploaded content, leveraging filters and size configurations to fine-tune the retrieval process.

### Additional Details on Using Arcee with Langchain

To explore the full potential of the Arcee+Langchain integration, it's essential to delve into the practical details of using the Arcee class in conjunction with Langchain. This guide will provide an overview of the process, complete with code examples to help you get started.

#### Step-by-Step Guide to Using Arcee with Langchain

**Step 1: Set Your Environment**

To initialize your setup, ensure that the `ARCEE_API_KEY` is set up in your environment. This is crucial for authentication and accessing the Arcee API.

```bash
export ARCEE_API_KEY='your_api_key_here'
```

Alternatively, you can directly pass the API key as a parameter when creating instances of the Arcee and ArceeRetriever classes.

**Step 2: Import Arcee Class**

Start by importing the Arcee class from the `langchain.llms` module. This class is the gateway to interacting with Arcee's DALMs.

```python
from langchain.llms import Arcee
```

**Step 3: Initialize Arcee**

Create an instance of the Arcee class. You can specify the model along with the API key if it is not already set in the environment.

```python
arcee = Arcee(
    model="DALM-PubMed",  # Choose the appropriate DALM model for your domain
    arcee_api_key="ARCEE-API-KEY"  # Only if not set in the environment
)
```

**Step 4: Customize the Configuration**

Customize the configuration based on your needs. Set the API URLs and default model arguments, which can include filters and size parameters.

```python
arcee = Arcee(
    model="DALM-PubMed",
    arcee_api_url="https://custom-api.arcee.ai",
    arcee_app_url="https://custom-app.arcee.ai",
    model_kwargs={
        "size": 10,  # The number of documents to inform the generation
        "filters": [
            {
                "field_name": "document",
                "filter_type": "fuzzy_search",
                "value": "neuroscience"
            }
        ]
    }
)
```

**Step 5: Generate Text**

Generate text based on a prompt. This allows you to receive content that's informed by the documents retrieved and filtered according to your settings.

```python
prompt = "Discuss the implications of AI in modern neuroscience research."

# Generate text using the provided prompt and the configured model
response = arcee.generate(prompt)
print(response)
```

**Step 6: Using ArceeRetriever for Document Retrieval**

Just as you set up the Arcee class, you can also use the ArceeRetriever class to fetch relevant documents. Import it from the `langchain.retrievers` module.

```python
from langchain.retrievers import ArceeRetriever

# Initialize the retriever
retriever = ArceeRetriever(
    model="DALM-PubMed",
    arcee_api_key="ARCEE-API-KEY"  # Only if not set in the environment
)
```

**Step 7: Retrieve Relevant Documents**

Retrieve documents relevant to your query that can help inform the text generation process.

```python
query = "The impact of AI on neurological disorder treatments."

# Retrieve documents related to your query with optional filters.
documents = retriever.get_relevant_documents(
    query=query,
    size=10,
    filters=[{"field_name": "year", "filter_type": "strict_search", "value": "2020"}]
)

# Printing the titles of the retrieved documents
for doc in documents:
    print(doc.get('title'))
```

**Step 8: Integrate Retrieval with Generation**

You can combine the document retrieval with text generation for a comprehensive content creation workflow.

```python
# First, retrieve documents as shown in Step 7

# Then, pass the retrieved documents to inform the text generation
response = arcee.generate(prompt, context_documents=documents)
print(response)
```

#### Using Arcee with Agents

Initialization Import Langchain's tools and initialize Arcee as the heart of your agent:

```python
from langchain.agents import AgentType, initialize_agent, load_tools
from langchain.llms import Arcee

# Make sure to set the environment variable ARCEE_API_KEY
# export ARCEE_API_KEY='your_api_key_here'

# Initialize the language model with Arcee
arcee = Arcee(
    model="DALM-your_domain",  # Replace 'your_domain' with the specific domain model you want to use, e.g., 'DALM-PubMed'
    arcee_api_key="ARCEE-API-KEY"  # Include your Arcee API key here
)

```

**Load the tools for the agent with Arcee as the LLM**

```python
tools = load_tools(["serpapi", "llm-math"], llm=arcee)
```

**Initialize the agent with Arcee as the LLM and the required tools**

Note: You may need to modify the AgentType and initialization process.

```python
agent = initialize_agent(tools, arcee, agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION, verbose=True)
```

**Run the agent with your question or task**

```python
result = agent.run("Your question here")
print(result)
```

The Arcee+Langchain integration provides a versatile and robust toolkit for generating domain-specific content powered by DALMs. By configuring models, applying filters, and retrieving relevant documents, you can enhance the quality and relevance of your AI-generated text to a considerable extent. Start experimenting with the provided code examples, and tailor them to fit your specific use-cases and domains.
