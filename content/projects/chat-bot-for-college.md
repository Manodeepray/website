+++
title = 'Chat Bot for College'
date = 2024-09-04T22:41:27+05:30
draft = false
+++

## Chat Bot for College

### update till 4 - 9 - 24

- I am creating a llm chatbot for my college , the school of Electronics , KIIT university.

- I have used RAG model for the chatbot.

- I have taken the .csv , .pdfs and .txt from the official website of SOEE , KIIT .

- I converted them into FIASS vector database , used HuggingFace embeddings for indexing the data.

- I created 3 different vector stores and 3 different retrievers and ensembled them using langchain ensemble retriever module.

- I am planning on using OpenAI gpt 4 or Claude 3.5 api....currently using meta llama 3b instruct from huggingface api inference.

- I am using create_history_aware_retriever for conversational chatbot.

### Problems:

the response is non-coherent if I use larger llm like gpt-4 , claude or cohere to make it more coherent
