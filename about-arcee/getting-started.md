---
description: Welcome to your first steps towards building a domain adapted model!
---

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

### Upload Context via Plain Text

Upload context for your domain-adapted language model to draw from.

```python
import arcee
arcee.upload_doc("pubmed", doc_name="doc1", doc_text="whoa")
# Alternatively, you can upload multiple documents at once:
# arcee.upload_docs("pubmed", docs=[{"doc_name": "doc1", "doc_text": "foo"}, {"doc_name": "doc2", "doc_text": "bar"}])
```

### Upload Context via CSV

Upload context for your domain-adapted language model to draw from.

```python
import csv, arcee, os, threading, queue

os.environ["ARCEE_API_KEY"] = "your_api_key"

# Header of CSV needs have these column headers = ['title', 'doc_name', 'doc_text']
# Replace 'title' header with the name of your context target found in Arcee platform
csv_file_path = 'Data.csv'   # 
num_threads = 4   # Increase based on CPU
row_queue = queue.Queue()
seen_entries = set()

def upload_from_csv(row):
    arcee.upload_doc(row[0], doc_name=row[1], doc_text=row[2])
    
def worker():
    for row in iter(row_queue.get, None):
        if f"{row[1]}-{row[2]}" not in seen_entries:
            seen_entries.add(f"{row[1]}-{row[2]}")
            upload_from_csv(row)
        row_queue.task_done()

with open(csv_file_path, newline='', encoding='utf-8') as csvfile:
    next(csvfile)  # Skip headers in CSV
    for row in csv.reader(csvfile):
        row_queue.put(row)

threads = [threading.Thread(target=worker) for _ in range(num_threads)]
for thread in threads:
    thread.start()  # Start number of threads for processing CSV
for _ in range(num_threads):
    row_queue.put(None)  # Send termination signal for end of CSV
for thread in threads:
    thread.join()  # Ensures all threads complete before moving on

print("Document upload complete.")
```
