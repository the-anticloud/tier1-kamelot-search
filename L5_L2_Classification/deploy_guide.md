# Deploy Guide — KAMELOT_SEARCH
## Prerequisites
- Python 3.11+, FAISS-cpu 1.7+ (or faiss-gpu), sentence-transformers 2.6+
- Initial corpus indexing requires internet; after indexing: fully offline

## Environment
- CPU: 8GB RAM for 1M chunks. GPU (faiss-gpu): 4GB VRAM for ANN acceleration.
- Index stored on local SSD.

## Install
```bash
pip install anticloud-kamelot faiss-cpu sentence-transformers
```

## Index the Anticloud corpus
```bash
python -m kamelot_search index --path "E:/fenta/Downloads/The Anticloud"   --extensions .py .md --output ./kamelot_index/
```

## Air-Gap
Pre-download embedding model (all-MiniLM-L6-v2) on networked machine:
```bash
python -c "from sentence_transformers import SentenceTransformer; SentenceTransformer('all-MiniLM-L6-v2')"
# Copy ~/.cache/huggingface/ to air-gap host
```

## AIOSS Integration
```bash
aioss init --module KAMELOT_SEARCH --output ./search.aioss
```
Each search session auto-appends via `idx.search_with_audit()`.

## Verification
```bash
python -m kamelot_search verify --index ./kamelot_index/
```
