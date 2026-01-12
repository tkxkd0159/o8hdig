# o8hdig

Recommend to use [Query DSL](https://docs.opensearch.org/latest/query-dsl/) for query language.

- [Search methods](https://docs.opensearch.org/latest/search-plugins/)
  - **Keyword search** : OpenSearch implements lexical (keyword) text search using the BM25 algorithm to match and rank documents based on term frequency and document length.
    - pros
      - Precision: Great for exact matches (e.g., searching for a specific error code 0x8004100, a part number, or a proper noun).
      - Explainable: You know exactly why a document was returned (it contained the word).
      - Fast & Cheap: Highly optimized over decades (Lucene).
    - cons
      - Vocabulary Mismatch: If you search "sneakers," it might miss documents that only say "running shoes."
      - No Context: It treats "bank" (river) and "bank" (money) as the exact same word. 
  - **Vector search** : OpenSearch supports similarity (k-nearest neighbor) search using dense and sparse vector embeddings to power use cases such as semantic search, retrieval-augmented generation, and multimodal image search.
    - **Dense vector search** (Semantic Search) : An AI model converts text into a fixed-size list of floating-point numbers. This list represents the meaning of the text in a multi-dimensional space. Every dimension has a non-zero value, and no single dimension represents a specific word. Meaning is distributed across the entire vector.
      - pros
        - Semantic Understanding: It understands synonyms and intent. Searching for "how to fix a flat" will return results about "tire repair" even if the words don't match.
        - Multimodal: Can map text, images, and audio into the same space.
      - cons
        - Black Box: It is difficult to interpret why a specific result was ranked highly.
        - "Fuzzy" Precision: It struggles with exact matches. It might return a document about "Cat 4 cables" when you searched for "Cat 5 cables" because they are semantically similar concepts.    
    - **Sparse vector search** (Learned/Neural Sparse) : While Keyword search technically uses sparse vectors, "Sparse Vector Search" in modern vector databases (like Milvus, Qdrant) refers to Learned Sparse Models. Like keyword search, it maps text to a vocabulary-sized vector. However, it uses an AI model to "expand" the document. It might add the word "shoes" to the vector for a document about "sneakers" and assign it a learned weight of importance, even if the word "shoes" isn't in the text.
      - pros
        - Best of Both Worlds: It fixes the vocabulary mismatch (by adding synonyms via expansion) while keeping the exact-match precision of keywords.
        - Zero-Shot Performance: often performs better on out-of-domain data (e.g., medical or legal docs) than dense vectors which require fine-tuning.
      - cons
        - Storage: The vectors can be physically larger (in terms of RAM/Disk) than dense vectors because they index thousands of expanded terms.
        - Latency: Can be slower than pure dense search depending on the implementation.
  - **AI-powered search** (using AI models) : OpenSearch supports AI-powered search capabilities beyond vector embeddings. OpenSearch’s AI search enables search and ingestion flows to be enriched by any AI service to power the full range of AI-enhanced search use cases.


 
