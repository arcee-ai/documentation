# Train and Deploy DALMs

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
