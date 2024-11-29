# 🔍 What is Fusion?

Fusion is a technique for combining the results from multiple search methods—like traditional keyword-based search (e.g., BM25) and semantic search (vector-based).

Each method has its strengths:

- Keyword-based search excels at precise term matching.
- Vector-based search captures meaning and context.
  Instead of choosing one, Fusion merges their outputs, creating a balanced, unified ranking that combines precision and semantic understanding.

# 💡 How Does It Work?

Fusion operates in three steps:

```plaintext
BM25:
{'doc1': 2.5, 'doc2': 1.8, 'doc3': 1.2}

Vector Similarity:
{'doc2': 0.8, 'doc4': 0.7, 'doc1': 0.6}
```

- Score Normalization: Scores from different methods (often in varying scales) are normalized to bring them into a common range.

```plaintext
normalized_score = (score - min_score) / (max_score - min_score)
```

After normalization:

```plaintext
BM25:
{'doc1': 1.0, 'doc2': 0.6667, 'doc3': 0.0}

Vector Similarity:
{'doc2': 1.0, 'doc4': 0.875, 'doc1': 0.75}
```

- Score Combination: Using techniques like Reciprocal Rank Fusion (RRF), scores are aggregated to produce a final ranking. RRF ensures diverse results while prioritizing relevance.

```plaintext
final_score(doc) = (score1(doc) + score2(doc)) / number_of_methods
```

```plaintext
doc1: (1.0 + 0.75) / 2 = 0.875
doc2: (0.6667 + 1.0) / 2 = 0.83335
doc3: (0.0 + 0.0) / 2 = 0.0
doc4: (0.0 + 0.875) / 2 = 0.4375

```

- Reordering: Documents are ranked based on combined scores, ensuring the best of both worlds.

```plaintext
['doc1', 'doc2', 'doc4', 'doc3']
```
