# L5 Narrow / L2 General Classification — KAMELOT_SEARCH
**Platform:** Anticloud | **PAX:** 27B | **IP:** USPTO pending 2026, Anticloud FZ LLE

## L5 Narrow
KAMELOT_SEARCH specializes in semantic retrieval over the Anticloud document corpus and codebase.
No web crawling, no external index sync, no cloud vector DB. All embeddings local, all indices on disk,
all retrieval offline. Maximum retrieval quality within the sovereign boundary.

## L2 General
KAMELOT_SEARCH serves every tier project that needs RAG context: ANTICODE_AGENT, INTE11ECT_APP,
PAX_RETRIEVAL (T2), MIIRAI_CHAT. One index, universal consumption.

## PAX Integration
PAX 27B queries KAMELOT_SEARCH for top-k chunks before generating responses. Retrieval step and
generation step are both AIOSS-chained, creating a full audit trail from query to grounded response.

## AIOSS Audit Relevance
Each search session appends: query hash + retrieved chunk hashes + retrieval metadata. Reproducible
retrieval: any auditor can re-run the same query and verify the same chunks were used.

## Regulatory
GDPR Art. 17 (right to erasure — chunks can be deleted by document), ISO 27001 A.8.2 (information classification)
