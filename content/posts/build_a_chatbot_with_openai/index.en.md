---
title: "Engineering a OpenAI-Powered Chatbot - Part 1"
date: 2023-03-30T13:58:07+08:00
draft: true
---

## 1 Problem Statement

AI assistant / Q&A bot for summarizing customer reviews on books, and recommending similar books

## 2 The Dataset
Amazon product reviews - Books

## 3 The Architecture
AI Service: OpenAI
Search Index?: Cognitive Search
SQL Database: Azure SQL
Vector Database: Vector Search database
Backend compute: App Service
Frontend compute: Bot Service
Conversation logs: Cosmos DB
Auth: Azure AD / Auth0
Framework: Langchain

## 4 Generating Embeddings for Products and Users


## 5 Sentiment Analysis, Named Entity Recognition and Opinion Mining


## 6 Prompt Engineering and Best Practices
prompt versioning


## 7 Putting it all together, AI assistant to do both opinion summarization and recommendations


## 7 Guardrails and Content Moderation


## 8 Final Thoughts


## Special Thanks / References
https://huyenchip.com/2023/04/11/llm-engineering.html
https://platform.openai.com/docs/guides/safety-best-practices
https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-openai-api
https://platform.openai.com/docs/guides/production-best-practices/evaluation-and-iteration
https://cseweb.ucsd.edu/~jmcauley/datasets/amazon_v2/
https://python.langchain.com/en/latest/getting_started/getting_started.html
https://www.youtube.com/watch?v=J-dETevTkm4&t=4468s&ab_channel=MicrosoftDeveloper
https://techcommunity.microsoft.com/t5/ai-applied-ai-blog/revolutionize-your-enterprise-data-with-chatgpt-next-gen-apps-w/ba-p/3762087
https://github.com/Azure-Samples/azure-search-openai-demo
https://www.youtube.com/watch?v=YKY0V42MCtk
https://mitchellh.com/writing/prompt-engineering-vs-blind-prompting



Nathan Cheng
what if i want the granular opinion on the entities within the text?
If you want to extract more granular opinions on the entities within a piece of text, you can use OpenAI's Named Entity Recognition (NER) model to identify the entities mentioned in the text, and then use a sentiment analysis model to extract opinions on each of those entities. Here's an example code snippet in Python that demonstrates this:

python
Copy code
import openai
import os

**set up OpenAI API credentials**
openai.api_key = os.environ["OPENAI_API_KEY"]

**define the text to analyze**
text_to_analyze = "I loved the acting in the movie, but the plot was a bit slow."

**use OpenAI to extract named entities from the text**
response = openai.Completion.create(
    engine="davinci",
    prompt=(f"Named entity recognition of text: {text_to_analyze}\n"
            "Entities:"),
    max_tokens=50,
    n=1,
    stop=None,
    temperature=0.5,
)

**extract the named entities from the OpenAI response**
entities = [choice.text.strip() for choice in response.choices]

**use OpenAI to extract sentiment on each entity**
for entity in entities:
    response = openai.Completion.create(
        engine="text-davinci-002",
        prompt=(f"Sentiment analysis of entity: {entity}\n"
                "Sentiment:"),
        max_tokens=1,
        n=1,
        stop=None,
        temperature=0.5,
    )
    sentiment = response.choices[0].text.strip()
    print(f"{entity}: {sentiment}")
This code snippet first sends a request to OpenAI's NER model to extract named entities from the text "I loved the acting in the movie, but the plot was a bit slow." The response from OpenAI will be a list of entities mentioned in the text, which in this case might be something like ["the acting", "the movie", "the plot"].

Then, for each entity identified in the text, the code sends a request to OpenAI's sentiment analysis model to extract the sentiment expressed about that entity. The sentiment analysis model will return a sentiment score or label, such as "positive", "negative", or "neutral", for each entity.

By combining OpenAI's NER and sentiment analysis models, you can extract more granular opinions on the entities mentioned within a piece of text.



