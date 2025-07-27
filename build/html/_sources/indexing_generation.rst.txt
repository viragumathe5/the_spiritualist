Indexing
========

Overview
--------

Indexing refers to the process of **embedding and storing the source documents** to enable fast and accurate semantic retrieval.
This is a **preprocessing step** that transforms raw textual data into vector representations, which are then indexed in Elasticsearch
for approximate nearest neighbor (ANN) search.

Indexing Pipeline
-----------------

1. **Document Collection**
   - Source documents are curated from *The Spiritualist* domain.
   - Each document is split into smaller, manageable chunks (e.g., paragraphs or 512-token spans).

2. **Embedding Generation**
   - Each text chunk is encoded using the MPNet from sentence-transformers.
   - The output is a 768-dimensional dense vector.

3. **Data Structuring**
   - Each document chunk is structured with:
     - ``content``: the raw text chunk
     - ``embedding``: the corresponding vector
     - ``metadata``: title, source, tags, etc.

4. **Insertion into Elasticsearch**
   - Chunks are batched and inserted into an Elasticsearch index.
   - The index uses a ``dense_vector`` field for ANN-enabled similarity search.

Why Chunking?
-------------

Chunking improves:
- Contextual precision during retrieval
- Reduction of irrelevant matches
- Better alignment with LLM input limits

Tools Used
----------

- ``sentence-transformers`` (MPNet model)
- ``Elasticsearch`` with ANN plugin (e.g., FAISS, HNSW, or native k-NN)
- Custom Python scripts for batching and bulk indexing

Generation
==========

Overview
--------

The **generation phase** takes retrieved document chunks and uses them to guide a large language model (LLM) in answering the user's query.
This is the “generation” step in the Retrieval-Augmented Generation (RAG) pipeline.

Generation Process
------------------

1. **User Query Input**
   - The user inputs a natural language query.

2. **Embedding & Retrieval**
   - The query is embedded using the same MPNet model.
   - Top-*k* most similar chunks are retrieved from Elasticsearch.

3. **Prompt Construction**
   - A prompt is constructed by concatenating:
     - Retrieved context (chunks)
     - The original user query

   Example prompt structure::

     Context:
     [Chunk 1]
     [Chunk 2]
     ...

     Question:
     What is the purpose of spiritual awakening?

4. **LLM Completion**
   - The prompt is passed to an gpt-4o.
   - The LLM generates a fluent and context-aware answer.

5. **Response Formatting**
   - Post-processing is performed to clean up and format the answer for the end user.

Generation Stack
----------------

+----------------+-------------------------------+
| Component      | Tool                          |
+================+===============================+
| Embedding      | MPNet                         |
+----------------+-------------------------------+
| Retrieval      | Elasticsearch                 |
+----------------+-------------------------------+
| Generation     | gpt-4o                        |
+----------------+-------------------------------+
| Prompting      |                               |
+----------------+-------------------------------+

Summary
-------

Indexing and generation complete the RAG pipeline by enabling efficient semantic search and grounded text generation.
This combination allows for intelligent and reliable answers to be provided to users using domain-specific content.


.. toctree::
   :maxdepth: 10
   :caption: Contents: