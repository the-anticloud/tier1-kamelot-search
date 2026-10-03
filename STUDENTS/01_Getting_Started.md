# KAMELOT_SEARCH — Student Getting Started

## What You'll Build
A hybrid search engine over your local documents using BM25 + dense embeddings + re-ranking — no cloud search API needed.

## Prerequisites
- Python 3.10+
- Ollama installed with `nomic-embed-text`

## Install
```bash
ollama pull nomic-embed-text
pip install kamelot-search
```

## First Working Example
```python
from kamelot import SearchIndex, Document

index = SearchIndex(backend="local", embedding="nomic-embed-text")

docs = [
    Document(id="1", text="The Anticloud system uses PAX for local inference coordination."),
    Document(id="2", text="KAMELOT_SEARCH provides hybrid retrieval without cloud APIs."),
    Document(id="3", text="SOVEREIGN_OS manages resource partitioning for AI workloads."),
]
index.add(docs)

results = index.search("local AI inference", top_k=3, mode="hybrid")
for r in results:
    print(f"[score: {r.score:.3f}] {r.text[:80]}")
```

## Index a Folder of Documents
```python
from kamelot import SearchIndex

index = SearchIndex(backend="local", embedding="nomic-embed-text")
index.build_from_directory("./my_documents/")

results = index.search("authentication security", top_k=5)
for r in results:
    print(f"  [{r.source}] {r.text[:100]}")
```

## On Kaggle (loiskleinner account, T4 GPU)
```python
!pip install kamelot-search
!curl -fsSL https://ollama.ai/install.sh | sh
!ollama serve &
import time; time.sleep(5)
!ollama pull nomic-embed-text
# Then upload your documents as a Kaggle dataset and index them
```

## What's Next
- Try `mode="hybrid"` vs `mode="dense"` and compare result quality
- Add a re-ranker with `Reranker(model="cross-encoder/ms-marco-MiniLM-L-6-v2")`
- Connect to MIIRAI_CHAT as a retrieval backend
