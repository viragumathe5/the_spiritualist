Retrieval
=========

Overview
--------

The **retrieval** phase plays a central role in the Retrieval-Augmented Generation (RAG) architecture.
It is responsible for finding the most relevant content chunks from the vector database (Elasticsearch)
based on the user’s query. The objective is to minimize irrelevant context and maximize semantic alignment
between the query and the source material.

How Retrieval Works
-------------------

1. **Query Embedding**
   - The user input (query) is embedded into a dense vector using the **MPNet** from sentence-transformers.

2. **Vector Search in Elasticsearch**
   - The query embedding is passed to Elasticsearch to perform **approximate nearest neighbor (ANN)** search.
   - Elasticsearch computes similarity (typically cosine similarity) between the query vector and all stored document vectors.
   - The top-*k* most relevant chunks are returned.

3. **Result Filtering (Optional)**
   - Retrieved chunks may be filtered or re-ranked based on:
     - Metadata (e.g., source, tags)
     - Confidence scores
     - Keyword matching as a secondary heuristic

Why MPNet?
----------

- MPNet provides superior semantic understanding compared to traditional models like BERT or SBERT.
- It captures positional information effectively, enhancing context matching in spiritual or philosophical queries.

Vector Search Strategy
----------------------

- Vector dimension: 768  
- Similarity metric: Cosine similarity  
- Index type: Dense vector with support for ANN  
- Top-*k*: Typically 3 to 10 most similar chunks returned

Tools and Stack
---------------

+----------------------+-------------------------------+
| Component            | Technology                    |
+======================+===============================+
| Query Embedding      | MPNet (sentence-transformers) |
+----------------------+-------------------------------+
| Vector Search Engine | Elasticsearch                 |
+----------------------+-------------------------------+
| ANN Strategy         | FAISS / HNSW / native k-NN    |
+----------------------+-------------------------------+

Benefits of Retrieval
---------------------

- **Semantic Precision**: Finds meaningfully similar text, not just keyword matches.
- **Context Control**: Returns exactly the right amount of data for grounding LLM responses.
- **Speed and Scalability**: Efficient enough to serve in production environments.

Retrieval in RAG Flow
---------------------

::

   User Query
       ↓
   MPNet Embedding
       ↓
   Elasticsearch Vector Search
       ↓
   Top-k Document Chunks
       ↓
   Prompt Builder for LLM

Summary
-------

The retrieval phase is the bridge between the user’s intent and the knowledge embedded in the system.
By semantically matching the query to indexed content, it ensures that only the most relevant
information is used for answer generation.


.. toctree::
   :maxdepth: 10
   :caption: Contents: