# Code a simple RAG from scratch

Recently, Retrieval-Augmented Generation (RAG) has emerged as a powerful paradigm in the field of AI and Large Language Models (LLMs). RAG combines information retrieval with text generation to enhance language models' performance by incorporating external knowledge sources. This approach has shown promising results in various applications, such as question answering, dialogue systems, and content generation.

In this blog post, we'll explore RAG and build a simple RAG system from scratch using Python and ollama. This project will help you understand the key components of RAG systems and how they can be implemented using fundamental programming concepts.

A RAG system consists of two key components:

A retrieval model that fetches relevant information from an external knowledge source, which could be a database, search engine, or any other information repository.
A language model that generates responses based on the retrieved knowledge.
There are several ways to implement RAG, including Graph RAG, Hybrid RAG, and Hierarchical RAG, which we'll discuss at the end of this post.

Simple RAG
Let's create a simple RAG system that retrieves information from a predefined dataset and generates responses based on the retrieved knowledge. The system will comprise the following components:
1- Embedding model: A pre-trained language model that converts input text into embeddings - vector representations that capture semantic meaning. These vectors will be used to search for relevant information in the dataset.
2- Vector database: A storage system for knowledge and its corresponding embedding vectors. While there are many vector database technologies like Qdrant, Pinecone, and pgvector, we'll implement a simple in-memory database from scratch.
3- Chatbot: A language model that generates responses based on retrieved knowledge. This can be any language model, such as Llama, Gemma, or GPT.

## Indexing phase
The indexing phase is the first step in creating a RAG system. 
It involves breaking the dataset (or documents) into small chunks and calculating a vector representation for each chunk that can be efficiently searched during generation.

The size of each chunk can vary depending on the dataset and the application. For example, in a document retrieval system, each chunk can be a paragraph or a sentence. In a dialogue system, each chunk can be a conversation turn.

After the indexing phrase, each chunk with its corresponding embedding vector will be stored in the vector database. Here is an example of how the vector database might look like after indexing:

   Chunk	                                                             Embedding Vector
Italy and France produce over 40% of all wine in the world.	\[0.1, 0.04, -0.34, 0.21, ...\]
The Taj Mahal in India is made entirely out of marble.	\[-0.12, 0.03, 0.9, -0.1, ...\]
90% of the world's fresh water is in Antarctica.	\[-0.02, 0.6, -0.54, 0.03, ...\]

The embedding vectors can be later used to retrieve relevant information based on a given query. Think of it as SQL WHERE clause, but instead of querying by exact text matching, we can now query a set of chunks based on their vector representations.

To compare the similarity between two vectors, we can use cosine similarity, Euclidean distance, or other distance metrics. In this example, we will use cosine similarity. Here is the formula for cosine similarity between two vectors A and B:

![image](https://github.com/user-attachments/assets/da864ce7-5d5d-4263-8d61-9ff7d3289c99)

## Retrieval phrase
In the diagram below, we will take an example of a given Input Query from User. We then calculate the Query Vector to represent the query, and compare it against the vectors in the database to find the most relevant chunks.

The result returned by The Vector Database will contains top N most relevant chunks to the query. These chunks will be used by the Chatbot to generate a response.


