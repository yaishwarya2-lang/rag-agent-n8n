# BrewlightAgent: a RAG chatbot built with n8n, Pinecone and Gemini

A chat agent that answers questions from company documents instead of guessing. It says "I couldn't find that" when the answer isn't in the source.

**Live portfolio:** [YOUR PORTFOLIO URL]
**Interactive architecture:** [YOUR PORTFOLIO URL]/rag-pipeline.html
**Demo video:** [YOUR VIDEO URL]

![Chat demo](images/demo.png)

## The problem

[One or two sentences. Example: Knowledge lives in scattered documents, and generic chatbots answer confidently even when they don't know.]

## How it works

**1. Ingestion workflow** (`workflows/1-ingestion.json`)
Google Drive file download, then a default data loader, then a recursive text splitter, then Gemini embeddings, then storage in a Pinecone index.

**2. Chat agent workflow** (`workflows/2-chat-agent.json`)
Chat trigger, then an AI agent (Gemini chat model) with simple memory. The agent uses a Pinecone vector store as a retrieval tool and answers only from what it retrieves.

![Ingestion workflow](images/ingestion.png)
![Agent workflow](images/agent.png)

## Tech stack

n8n, Pinecone, Google Gemini (chat and embeddings), Google Drive

## Try it yourself

1. Import both JSON files from `workflows/` into n8n (menu, then Import from file).
2. Create your own credentials for Google Gemini, Google Drive and Pinecone. No keys are stored in this repo.
3. Create a Pinecone index that matches your embedding model's dimensions.
4. Upload `sample-data/Brewlight_Labs_Employee_Handbook.pdf` to Google Drive and point the Download node at it.
5. Use the same index and **the same namespace** in the ingestion node and the agent's Pinecone tool.
6. Run the ingestion workflow once, then chat. Try: "How many days of paid annual leave do employees get?" (Expected: 24)

## What I learned

- Namespace and embedding model must match between ingestion and retrieval, or search returns nothing.
- A specific tool description and system prompt decide whether the agent searches and stays grounded.
- Free API tiers have rate limits, so add retries and use a stable model.
- [Add one lesson of your own.]

## Next steps

- Source citations in answers
- A test set of real questions to measure accuracy
- Tuning chunk size and overlap

## Author

[Your Name] · [LinkedIn URL] · [Email]
