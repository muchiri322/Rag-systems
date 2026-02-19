# Rag-systems

```markdown
#  Embedding-Based RAG System  
## Policy Document Question Answering using ChromaDB  
**Reference Book:** *:contentReference[oaicite:0]{index=0}*

---

## 1. Project Overview

This project implements a **Retrieval-Augmented Generation (RAG)** system that answers questions from Kenyan policy documents using semantic embeddings and ChromaDB.

The system converts PDF documents into vector embeddings and enables semantic search over the content. Instead of traditional keyword matching, it retrieves meaning-based results using dense vector representations.

The conceptual foundation of this project is inspired by ideas from *Rooters and Grabbers*, emphasizing structured extraction, retrieval, and intelligent information access.

---

## 2. Objective

To build a working embedding-based retrieval system that:

- Extracts text from large policy PDFs
- Chunks text efficiently
- Generates normalized embeddings
- Stores vectors in ChromaDB
- Retrieves top relevant passages using semantic similarity

---

## 3. Dataset Requirements

### Category (Choose One)

- Kenya Constitution  
- Finance Bills  
- Economic Surveys  
- County Development Plans  
- Parliamentary Acts
- Looters and Grabbers 

### Minimum Requirements

- At least **1 PDF document**
- Minimum **50 pages total**

---

## 4. System Architecture

```

PDF → Text Extraction → Chunking → Embeddings → ChromaDB → Query Embedding → Retrieval

```

---

## 5. Implementation Steps

---

### Step 1 — Text Extraction

**Library Used:** `pypdf`

#### Why Convert PDF to Text?

- Embedding models require raw text input.
- PDFs contain formatted content, not structured text.
- Text must be extracted before chunking or embedding.

#### Challenges in Extraction

- Broken formatting
- Tables and columns misalignment
- Headers and footers mixed with content
- OCR issues (if scanned PDFs)

---

### Step 2 — Chunking

**Tool Used:** `RecursiveCharacterTextSplitter`

#### Parameters

- `chunk_size`: 800–1000
- `chunk_overlap`: 150–200

#### Why Chunking is Necessary

Embedding models have token limits. Large documents must be split into manageable segments to:

- Preserve context
- Improve retrieval precision
- Avoid memory overload

#### Why Overlap Improves Retrieval

Overlap ensures:

- Context continuity across chunks
- Reduced information loss at chunk boundaries
- Better semantic matching during search

---

### Step 3 — Embeddings

**Model Used:** `BAAI/bge-small-en-v1.5`

#### What Are Embeddings?

Embeddings are dense numerical vectors representing the semantic meaning of text.

Example:

```

"tax reform policy" → [0.021, -0.883, 0.441, ...]

```

Texts with similar meaning have vectors that are close in vector space.

#### Why Semantic Search > Keyword Search

| Keyword Search | Semantic Search |
|---------------|----------------|
| Matches exact words | Matches meaning |
| Fails on synonyms | Understands context |
| Limited recall | High contextual relevance |

Example:

- Query: "government revenue allocation"
- Document: "national budget distribution"
- Keyword search may fail
- Embedding search retrieves it correctly

---

### Step 4 — Store in ChromaDB

A persistent ChromaDB collection is created.

#### Stored Fields

- `ids` — Unique identifiers
- `documents` — Text chunks
- `embeddings` — Vector representations
- `metadata` — Source filename

#### Why Metadata Is Important

Metadata allows:

- Source tracing
- Filtering by document
- Multi-document indexing
- Auditability

#### What Happens if Embeddings Are Not Stored?

- Retrieval cannot occur
- No similarity comparison
- System becomes a static document store

---

### Step 5 — Query & Retrieval

Process:

1. Embed user query
2. Compute similarity with stored vectors
3. Retrieve top 3 results
4. Display text + similarity score

#### What Similarity Score Means

Similarity score measures how close two vectors are.

Using cosine similarity:

- Value closer to **1** → Highly similar
- Value closer to **0** → Less similar

#### Why Lower Cosine Distance = Better Match

Cosine distance = 1 − cosine similarity

- Smaller distance → Vectors closer
- Closer vectors → More semantically relevant content

---

## 6. Evaluation Rubric (100 Marks)

| Component           | Marks |
|---------------------|-------|
| Extraction          | 15    |
| Chunking            | 20    |
| Embeddings          | 20    |
| ChromaDB Storage    | 20    |
| Query & Retrieval   | 15    |
| Explanations        | 10    |
| **Total**           | **100** |

---

## 7. Project Deliverables

- Working Python code
- ChromaDB persistent storage
- Example query outputs
- Written explanations for each step
- Minimum 50-page policy document indexed

---

## 8. Key Learning Outcomes

By completing this project, you will understand:

- How embeddings represent semantic meaning
- How vector databases enable semantic retrieval
- Why chunking strategy affects model performance
- How RAG systems combine retrieval and intelligence
- Practical application of NLP pipelines in governance documents

---

## 9. Future Improvements

- Add reranking models
- Use larger embedding models
- Integrate LLM for answer synthesis
- Deploy as a web app (Streamlit/FastAPI)
- Implement metadata filtering by year or policy type

---

## 10. Conclusion

This project demonstrates a full pipeline for building a semantic search system over policy documents using embeddings and ChromaDB. Inspired by structured information handling principles in *Rooters and Grabbers*, it highlights the transition from keyword-based retrieval to intelligent meaning-based search systems.

---


**Course:** In-Class Activity – Policy Document RAG System  
**Tools:** Python, pypdf, LangChain, ChromaDB, Sentence Transformers  
```
