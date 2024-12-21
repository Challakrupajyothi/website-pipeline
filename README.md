# website-pipeline
Overview
This document outlines the implementation of a Retrieval-Augmented Generation (RAG) pipeline, which allows users to interact with semi-structured data from PDF files. The system performs text extraction, chunking, embedding generation, and stores embeddings in a vector database for efficient similarity-based retrieval. User queries are processed, and responses are generated using a Large Language Model (LLM) with retrieval-augmented prompts.

Functional Requirements
Data Ingestion

Input: PDF files containing semi-structured data.
Process:
Extract text and relevant structured information from PDFs.
Segment the extracted text into logical chunks for better granularity.
Convert chunks into vector embeddings using a pre-trained SentenceTransformer model.
Store the embeddings in a vector database (FAISS) for efficient similarity-based retrieval.
Query Handling

Input: User's natural language question.
Process:
Convert the user query into a vector embedding using the same SentenceTransformer model.
Perform similarity search in the FAISS database to find relevant chunks.
Pass retrieved chunks to the LLM for response generation.
Comparison Queries

Input: User query asking for a comparison.
Process:
Extract relevant fields or terms to compare across multiple PDFs.
Retrieve corresponding chunks from the database.
Process and aggregate the data for comparison.
Generate a structured response in a tabular or bullet-point format.
Response Generation

Input: Relevant text chunks and the user query.
Process:
Use the LLM with the retrieved context to produce accurate responses.
Ensure factuality by integrating retrieved data directly into the response.
Workflow
Data Ingestion

Extracts text from PDFs using the chunk_text function.
Embeds chunks using SentenceTransformer.
Stores embeddings and metadata in FAISS for retrieval.
Query Processing

Embeds the user query and searches for similar text chunks in the FAISS database.
Response Generation

Uses the retrieved text chunks as context and generates a detailed response with OpenAI's API.
Code Components
Text Chunking

chunk_text(text, chunk_size=200): Splits text into smaller chunks for granular processing.
Embedding Generation

SentenceTransformer('all-MiniLM-L6-v2'): Creates embeddings for text chunks and user queries.
Vector Similarity Search

FAISS Index: Efficiently retrieves the most relevant embeddings for a query.
Web Scraping

UniversitySpider: Extracts text data from university websites for demonstration purposes.
Response Generation

generate_response_with_openai(query, context): Passes retrieved context to OpenAI's GPT model to generate responses.
