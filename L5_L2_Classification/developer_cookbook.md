# Developer Cookbook — KAMELOT_SEARCH
**Stack:** Python 3.11, FAISS, sentence-transformers, SQLite

## Index the codebase
```python
from kamelot_search import KamelotIndex
idx = KamelotIndex("./kamelot_index/")
idx.index_directory("E:/fenta/Downloads/The Anticloud", extensions=[".py", ".md"])
idx.save()
```

## Semantic search
```python
results = idx.search("How to append to AIOSS chain", top_k=5)
for r in results:
    print(f"[{r.score:.3f}] {r.source}:{r.line} — {r.snippet[:80]}")
```

## RAG context for PAX
```python
chunks = idx.retrieve_for_prompt("Deploy TIER_7 biosignal project", max_tokens=2048)
prompt = f"Context:
{chunks}

Question: How do I deploy K_BRAINFLOW?"
```

## Incremental update
```python
idx.update_file("E:/fenta/Downloads/The Anticloud/TIER_1_ANTICLOUD_CORE/AIOSS_FORMAT/aioss_format.py")
```

## Audited search session
```python
session = idx.search_with_audit("AIOSS verify command", top_k=3, aioss_chain="./search.aioss")
print(session.chain_hash)
```

## Performance
FAISS IVF index (nlist=1024): 10x speedup vs flat for >100k chunks.
Models: all-MiniLM-L6-v2 for speed, all-mpnet-base-v2 for quality.
Pre-warm on startup: `idx.warm()`.

## Integration
RAG backend for ANTICODE_AGENT, INTE11ECT_APP, MIIRAI_CHAT, PAX_RETRIEVAL (T2).
Indexed by KANTOR_K5 for curated knowledge documents.
