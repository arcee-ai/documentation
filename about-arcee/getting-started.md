# Getting started

### What is Arcee?

Arcee is a sophisticated text generation platform that harnesses the power of DALMs, offering users the capability to create text that's finely tuned to specific domains such as PubMed and Patent literature. The DALMs understand the nuances and terminologies of these specialized fields, enabling the generation of content that is not just coherent but also domain-appropriate.

## Arcee DALMs

### Installation

To install the Arcee package, simply run the following pip command:

```bash
pip install arcee-py
```

### Authenticating

Obtain your Arcee API key from [app.arcee.ai](https://app.arcee.ai).

In bash:

```bash
export ARCEE_API_KEY=your_api_key
```

In a notebook:

```python
import os
os.environ["ARCEE_API_KEY"] = "your_api_key"
```

### Upload Context

Upload context for your domain-adapted language model to draw from.

```python
import arcee
arcee.upload_doc("pubmed", doc_name="doc1", doc_text="whoa")
# Alternatively, you can upload multiple documents at once:
# arcee.upload_docs("pubmed", docs=[{"doc_name": "doc1", "doc_text": "foo"}, {"doc_name": "doc2", "doc_text": "bar"}])
```
