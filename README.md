# Retrieval-Augmented-Conversational-AI

# Healthcare Assistant Chatbot (RAG-based)
A conversational AI system for answering health-related questions using a hybrid of retrieval-based and generative NLP methods.

# Project Overview
This chatbot uses a combination of:

Retrieval (Semantic Search): Finds the most relevant answers from a pre-defined FAQ knowledge base using sentence embeddings.

Generation (Text Generation): Uses a Transformer model (T5) to generate a more fluent, coherent answer based on the retrieved content.

This is a lightweight implementation of Retrieval-Augmented Generation (RAG) for domain-specific QA.

# Components
Knowledge Base:

A CSV file (faq.csv) containing healthcare questions and their corresponding answers.

Sentence Embeddings (Retriever):

Uses all-MiniLM-L6-v2 from Sentence-Transformers to embed user queries and knowledge base questions into dense vectors.

Performs semantic similarity search using cosine similarity.

Answer Generator:

Uses t5-small from Hugging Face Transformers to generate answers using the format:

question: <user_input> context: <combined_retrieved_answers>
Chat Loop:

Accepts multi-turn user input and produces context-aware answers.

# Workflow 
Data Loading:

The chatbot loads the healthcare FAQs into a pandas DataFrame.

Preprocessing:

All questions in the FAQ are encoded into embeddings using a SentenceTransformer model and stored in memory.

User Query Handling:

When a user types a question, it is also encoded into an embedding.

Retrieval:

The system computes cosine similarity between the user query and all questions in the knowledge base.

It retrieves the top-k most similar FAQ entries.

Answer Generation:

The answers from the retrieved FAQs are concatenated into a single context string.

The context and user question are passed to a T5 model to generate a more natural and comprehensive response.

Conversation:

The user can continue asking questions in a loop.

Typing "exit" ends the session.

# Benefits
Domain-Specific Accuracy: Uses curated FAQs for reliable responses.

Conversational Ability: Generates fluid, human-like answers rather than copy-pasting FAQ text.

Lightweight: Can run on CPU for small to moderate workloads.


