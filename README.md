# NutriChat
NutriChat is a RAG workflow that lets users query a 1200-page nutrition textbook PDF, with an LLM generating responses based on relevant passages from the textbook.

PDF source: https://pressbooks.oer.hawaii.edu/humannutrition2/

Workflow of the local pipeline:

![alt text](https://github.com/Mehulgoyal353/NutriChat/blob/main/RAG_workflow.png)

## What is RAG?
RAG stands for Retrieval Augmented Generation.

It was introduced in the paper https://arxiv.org/abs/2005.11401.

Each step can be roughly broken down to:
  + **Retrieval** - Finding relevant information from a source based on a query, such as retrieving pertinent Wikipedia passages from a database in response to a question.
  + **Augmented** - Using the relevant retrieved information to modify an input to a generative model (e.g. an LLM).
  + **Generation** - Generating an output given an input. For example, in the case of an LLM, generating a passage of text given an input prompt.

## Why RAG?
The main goal of RAG is to improve the generation outputs of LLMs.

Two primary improvements can be seen as:
  + **Preventing hallucinations** - LLMs are amazing but can suffer from hallucinations, where they produce content that appears correct but isn’t. RAG pipelines improve LLM outputs by providing factual, retrieved inputs, and even if the response seems off, it can be traced back to the original sources.
  + **Work with custom data** - Many base LLMs are trained with internet-scale text data. This means they have a great ability to model language, however, they often lack specific knowledge. RAG systems can provide LLMs with domain-specific data such as medical information or company documentation and thus customized their outputs to suit specific use cases.

These points were outlined in the original RAG paper along with its advantages over fine-tuning.

## Key Terms
  + **Token** - A sub-word piece of text. For example, "hello, world!" could be split into ["hello", ",", "world", "!"]. A token can be a whole word,
part of a word or group of punctuation characters. 1 token ~= 4 characters in English, 100 tokens ~= 75 words.
Text gets broken into tokens before being passed to an LLM.
  + **Embedding** - A learned numerical representation of a piece of data. For example, a sentence of text could be represented by a vector with
768 values. Similar pieces of text (in meaning) will ideally have similar values.
  + **Embedding model** - A model designed to accept input data and output a numerical representation. For example, a text embedding model may take in 384
tokens of text and turn it into a vector of size 768. An embedding model can and often is different to an LLM model.
  + **Similarity search/vector search** - Similarity search/vector search aims to find two vectors which are close together in high-demensional space. For example, two pieces of similar text passed through an embedding model should have a high similarity score, whereas two pieces of text about different topics will have a lower similarity score. Common similarity score measures are dot product and cosine similarity.
  + **Large Language Model** - A model which has been trained to numerically represent the patterns in text. A generative LLM will continue a sequence when given a sequence.
For example, given a sequence of the text "hello, world!", a genertive LLM may produce "we're going to build a RAG pipeline today!".
This generation will be highly dependant on the training data and prompt.
  + **LLM Context Window** - The number of tokens a LLM can accept as input. For example, as of March 2024, GPT-4 has a default context window of 32k tokens (about 96 pages of text) but can go up to 128k if needed. A recent open-source LLM from Google, Gemma (March 2024) has a context
window of 8,192 tokens (about 24 pages of text). A higher context window means an LLM can accept more relevant information
to assist with a query. For example, in a RAG pipeline, if a model has a larger context window, it can accept more reference items
from the retrieval system to aid with its generation.
