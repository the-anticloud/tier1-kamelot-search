# KAMELOT_SEARCH — Educator's Teaching Guide

## Course Fit: information retrieval, search systems, RAG pipelines, NLP

## 3-Week Module: Sovereign Search Infrastructure

### Week 1: Search Fundamentals and the Case for Local RAG
**Lecture Topics:**
- BM25 vs. dense retrieval vs. hybrid search
- Why KAMELOT_SEARCH avoids cloud search APIs
- Chunking strategies: fixed-size, semantic, sentence-window
- Recall vs. precision tradeoffs in enterprise search

**Lab Exercise:**
```python
from kamelot import SearchIndex, Document
index = SearchIndex(backend="local", embedding="nomic-embed-text")
docs = [
    Document(id="1", text="Anticloud is a sovereign AI infrastructure system"),
    Document(id="2", text="PAX provides inference coordination for local models"),
]
index.add(docs)
results = index.search("sovereign AI infrastructure", top_k=3, mode="hybrid")
for r in results:
    print(f"[{r.score:.3f}] {r.text[:80]}")
```

### Week 2: Hybrid Retrieval Pipelines
**Lecture Topics:**
- Sparse + dense fusion with Reciprocal Rank Fusion (RRF)
- Re-ranking with a local cross-encoder (e.g., ms-marco models via Ollama)
- Metadata filtering and faceted search
- Streaming results for low-latency UX

**Lab Exercise:**
```python
from kamelot import SearchIndex, Reranker
reranker = Reranker(model="cross-encoder/ms-marco-MiniLM-L-6-v2")
index = SearchIndex(backend="local", reranker=reranker)
index.build_from_directory("./docs/")
results = index.search("authentication best practices", top_k=10)
reranked = reranker.rerank(query="authentication best practices", docs=results)
print(reranked[:3])
```

### Week 3: KAMELOT_SEARCH in the Anticloud Ecosystem
**Lecture Topics:**
- Connecting KAMELOT_SEARCH to INTE11ECT_APP and MIIRAI_CHAT
- Feeding search results into PAX_RETRIEVAL
- Index refresh pipelines with api-oss-data
- Benchmarking: latency, recall@10, MRR

**Lab Exercise:**
```python
from kamelot import SearchIndex
from pax_client import PAXRetrieval
search = SearchIndex(backend="local")
search.build_from_directory("./knowledge_base/")
pax = PAXRetrieval(search_backend=search)
answer = pax.answer("What is the Anticloud deployment model?")
print(answer)
```

## Exam Questions
1. Explain Reciprocal Rank Fusion. Why does combining BM25 and dense scores with RRF outperform either method alone?
2. Describe how chunking strategy affects retrieval quality. What chunk size would you choose for technical documentation and why?
3. How would you benchmark KAMELOT_SEARCH on a Kaggle T4 GPU? What metrics would you report?
