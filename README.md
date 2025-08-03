# Healthcare Assistant Chatbot (RAG-based)
A conversational AI system for answering health-related questions using a hybrid of retrieval-based and generative NLP methods.

## 1. Objective
To build a chatbot that can answer healthcare-related questions by:

Retrieving the most relevant questions and answers from a predefined FAQ dataset.

Generating a natural language response tailored to the user's question using generative language models.

## Underlying Concept: Retrieval-Augmented Generation (RAG)
RAG is a hybrid approach that combines retrieval-based and generation-based techniques. It retrieves relevant documents (or FAQ entries in this case) and feeds them into a text generation model to produce a final response.

This allows the model to:

Ground its answers in factual knowledge (retrieved from the FAQ).

Generate fluent, context-aware responses.

## Step-by-Step Theoretical Pipeline
### 1. Knowledge Base Preparation
A CSV file containing healthcare FAQs was used, with each entry having:

A "question" column representing frequently asked health-related queries.

An "answer" column with expert-curated responses.

This serves as the knowledge base for retrieval.

### 2. Embedding Creation using Sentence Transformers
To enable similarity-based retrieval, each FAQ question is converted into a vector representation (embedding) using a pre-trained model (all-MiniLM-L6-v2). These embeddings capture semantic meaning and allow for comparison with user queries.

### 3. User Query Processing
When the user enters a question:

It is also embedded using the same model.

Cosine similarity is calculated between the query and all FAQ embeddings.

The top-k most similar entries (e.g., 3) are selected as relevant context.

### 4. Answer Generation using T5 Model
Instead of directly returning a retrieved answer:

A context-aware prompt is formed: question: <user_input> context: <retrieved_answers>.

This prompt is fed into a pre-trained generative model (t5-small), which produces a fluent answer.

This step ensures the final output is more natural and informative, even if the user query is not an exact match to existing FAQs.

### 5. Interactive Chat Loop
The chatbot runs in a loop:

Accepts multiple user queries.

Retrieves relevant context each time.

Generates an answer and outputs it.

Allows the user to exit gracefully with commands like exit or stop.

## Summary of Results and Benefits
Dynamic Response Generation: Even if the user’s input doesn’t exactly match any FAQ, the chatbot can still generate appropriate, contextually relevant answers.

Accuracy and Fluency: The use of retrieved expert answers grounds the response in factual information, while T5 ensures fluent generation.

Scalability: New FAQs can be added to the CSV without retraining the model.

Domain Relevance: Since the knowledge base is healthcare-focused, the chatbot avoids off-topic responses.

## Advantages of RAG in Healthcare Chatbots
Combines precision (retrieval) with creativity (generation)

Reduces hallucination seen in purely generative chatbots

Easily interpretable pipeline with modular steps

Can be updated frequently by modifying the CSV without retraining
