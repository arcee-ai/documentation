
# Arcee DALMs Client Documentation

Welcome to the Arcee client documentation! This guide will help you execute domain-adapted language model (DALM) routines using the Arcee client libraries.

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

### Train DALM

Train a DALM with the context you have uploaded.

```python
import arcee
dalm = arcee.train_dalm("medical_dalm", context="pubmed")
# Wait for training to complete
arcee.get_dalm_status("medical_dalm")
```

The DALM training procedure refines your model in context and establishes an index for your model to utilize.

### DALM Generation

Generate responses from your DALM:

```python
import arcee
med_dalm = arcee.get_dalm("medical_dalm")
med_dalm.generate("What are the components of Scoplamine?")
```

### DALM Retrieval

Retrieve documents relevant to a specific query, which can then be viewed directly or used with another LLM.

```python
import arcee
med_dalm = arcee.get_dalm("medical_dalm")
med_dalm.retrieve("my query")
```

## Using the Arcee CLI

The Arcee CLI simplifies training and using your Domain-Adapted Language Model (DALM).

### Upload Context

Upload a context file for your DALM:

```bash
arcee upload context pubmed --file doc1
```

Upload all files within a directory:

```bash
arcee upload context pubmed --directory docs
```

Upload a combination of files and directories:

```bash
arcee upload context pubmed --directory some_docs --file doc1 --directory more_docs --file doc2
```

*Note: The upload command ensures only valid and unique files are uploaded.*

### Train your DALM

Train your DALM with any uploaded context:

```bash
arcee train medical_dalm --context pubmed
# Wait for training to complete...
```

### DALM Generation

Generate text completions using your model:

```bash
arcee generate medical_dalm --query "Can AI-driven music therapy contribute to the rehabilitation of patients with disorders of consciousness?"
```

### DALM Retrieval

Retrieve and view documents relevant to your query using your DALM:

```bash
arcee retrieve medical_dalm --query "Can AI-driven music therapy contribute to the rehabilitation of patients with disorders of consciousness?"
```

## Contributing

We use [invoke](http://www.pyinvoke.org/) to manage this repository. While it's not necessary, it does simplify workflow significantly.

### Set up the Repo

Clone and set up the repository:

```bash
git clone https://github.com/arcee-ai/arcee-python && cd arcee-python
# Optionally set up your virtual environment (recommended)
python -m venv .venv && source .venv/bin/activate
# Install repository
pip install invoke
inv install
```

### Format, Lint, Test

Run code formatting and linting, then execute tests:

```bash
inv format  # runs black and isort
inv lint    # black check, isort check, mypy
inv test    # pytest
```

### Publishing

We publish new versions by creating a release/tag on GitHub, triggering a GitHub action to publish the `__version__` specified in `arcee/__init__.py`.

Increase version in `__init__.py` before releasing to avoid failures.

#### To Create a New Release

- Open a pull request to increase the `__version__` of arcee-py.
- Create a new release with the same name as the `__version__` of arcee-py.

#### Manual Release [Not Recommended]

Manual releases should use alpha or beta versioning.

If necessary, perform a manual release with:

```bash
inv build && inv publish
```
