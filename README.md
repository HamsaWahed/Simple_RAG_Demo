# 🧠 Build a Simple RAG (Retrieval-Augmented Generation) from Scratch
**Retrieval-Augmented Generation (RAG)** is a powerful technique in modern AI that combines the strengths of information retrieval with the generative capabilities of large language models (LLMs). This fusion enables LLMs to generate more accurate and context-aware responses by grounding outputs in external knowledge sources.

RAG has shown significant success across a variety of applications including:

** 🧾 Question answering

** 💬 Dialogue systems

** 📝 Content generation

In this guide, you'll learn how to build a **simple RAG system** from scratch using Python and **Ollama**. This hands-on approach will help you understand the key components of a RAG system and how to implement them step by step.

---

## 📑 Table of Contents

- [What is RAG?](#what-is-rag)
- [System Components](#system-components)
- [Indexing Phase](#indexing-phase)
- [Retrieval Phase](#retrieval-phase)
- [Summary](#summary)

---

## 🤔 What is RAG?

<details>
<summary>Click to expand</summary>

**Retrieval-Augmented Generation (RAG)** combines:

- 🔍 A **retrieval model**: Fetches relevant information from external sources like databases or documents.
- 🤖 A **language model**: Generates answers based on the retrieved data.

This method is widely used in:
- ✅ Question answering
- ✅ Dialogue systems
- ✅ Content generation

RAG variants include:
- **Graph RAG**
- **Hybrid RAG**
- **Hierarchical RAG**

</details>

---

## 🧱 System Components

Our simple RAG system consists of three key components:

- 🔧 **Embedding Model**  
  Converts text into dense vectors (embeddings) that capture semantic meaning.

- 💾 **Vector Database**  
  Stores the embeddings along with the original knowledge chunks. We'll build a simple **in-memory** version (instead of using Qdrant, Pinecone, or pgvector).

- 🤖 **Chatbot**  
  A language model (like LLaMA, Gemma, or GPT) that generates responses using the retrieved chunks.

---

## 🧭 Step 1:🧊 Indexing Phase

<details>
<summary>Click to expand</summary>

The **indexing phase** is the first step in RAG. Here's what it does:

1. Breaks the dataset into small chunks (sentences, paragraphs, etc.)
2. Generates a vector (embedding) for each chunk
3. Stores the chunk and its embedding in the vector database

🔍 **Example:**

```text
| Chunk                                               | Embedding Vector              |
|-----------------------------------------------------|-------------------------------|
| Italy and France produce over 40% of world’s wine.  | [0.1, 0.04, -0.34, 0.21, ...] |
| Taj Mahal in India is made entirely of marble.      | [-0.12, 0.03, 0.9, -0.1, ...] |
| 90% of the world’s fresh water is in Antarctica.    | [-0.02, 0.6, -0.54, 0.03, ...] |


These vectors allow semantic search, where instead of exact keyword matching, we retrieve based on vector similarity.

➕ **Vector Similarity** 
To find relevant chunks, we calculate the cosine similarity between the query vector and stored vectors.

**Cosine similarity formula:**
**cosine_similarity = A • B / (||A|| * ||B||)**

## 🔍 Step 2: Retrieval Phase
In the retrieval phase:

1 - A user **query** is provided.

2- An **embedding** is generated for the query.

3 - We compare this query vector with stored vectors using cosine similarity.

4 - **The top N most relevant chunks** are selected as context.

5 - These chunks are passed to the language model to generate the final **response**.

### Retrival Workflow
[User Query] ➡ [Query Embedding] ➡ [Compare to Vector DB] ➡ [Top N Chunks] ➡ [Chatbot Output]

## 🧠 Next Steps
After building the basic system, you can experiment with:

* Adding real vector databases like Qdrant or Pinecone.

* Using Hybrid RAG by combining keyword search + semantic search.

* Implementing Hierarchical RAG for more structured documents.

* Expanding to multilingual RAG with appropriate models

## 🚀 Summary
This guide demonstrated how to build a simple RAG system using:

Embeddings for semantic understanding

In-memory vector database

A language model to generate rich responses

With just a few components, you can create a system that makes your LLMs more accurate, reliable, and context-aware. 🔍🤖
