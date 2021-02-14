---
layout: post
title: BERTology Transfer Learning in Natural Language Processing
---

![initial_googleai](https://user-images.githubusercontent.com/41947720/107882848-9c291f80-6f11-11eb-8dc1-f33ea0e2f428.png)

Representation Learning is of prime importance in supervised learning tasks, it is ultimately the representations of the input data which play a major role in determining the performance of the model. Having said this, there are scenarios where learning representations of the input data requires transferring of knowledge from related but different tasks. This is where transfer learning comes in. Transfer Learning helps us to utilize a more generalizable set of features and fine-tune them for the downstream task. To know more about transfer learning please go through my blog [linked here](https://nish-19.github.io/Transfer-Learning/)

In my recent work in NLP I have been using BERT and related models for certain downstream tasks like text classification on domain specific data. I am writing this blog with the motive of introducing you to the recent boom in transfer learning in natural language processing with the advent of architectures like BERT.

I will focus on the description of BERT and talk about using them in your works using HuggingFace.

## Motivation

![transformers](https://user-images.githubusercontent.com/41947720/107882859-aba86880-6f11-11eb-9bc2-182fcda289f3.png)

The 2017 OpenAI’s paper ["Transformers: Attention is all you need"](https://arxiv.org/abs/1706.03762) brought about a revolution in the field of deep learning in natural language processing by performing better than traditional recurrent neural network architectures like LSTMs and GRUs. Transformers, in general are seen to handle long term dependencies in text better than LSTMs and this led to them performing significantly better than LSTM based architectures on tasks like Machine Translation.

Transformers are the reason for the birth of BERT and the series of other architectures that follow. Motivated by the developments in Computer Vision, NLP researchers were eyeing to create a model capable of generating better representations of input text that could be used directly for downstream tasks.

Using the decoder layer of transformers, we could train it for language modelling i.e. next word prediction task. We can train the stack of decoders of the Transformers on a huge corpus of data and allow it to learn the “context” of the language. This trained transformer decoder stack can then be used for obtaining better representations of input data for downstream tasks like text classification.

## Entry of BERT

![bert_pretraining](https://user-images.githubusercontent.com/41947720/107882867-ba8f1b00-6f11-11eb-977e-d70bf217df0f.png)

Well, everything fine until now. But there is a catch. The above mentioned decoder architecture of Transformers doesn’t learn “bi-directional” contextualized embeddings making it less sophisticated in comparison to ELMo (Bi-Directional LSTM based architecture for generating dynamic contextualized embeddings).

Well, BERT said why not combine the idea of both ELMo and Transformers?

BERT uses the transformer encoder part and trains a “masked language model” randomly masking 15% of its input tokens. The task is to predict these tokens correctly.

Now for incorporating sentence level knowledge, BERT introduces another task in the pre-training – “The next sentence prediction”.
The task here is to determine if the second sentence follows the first one. For doing so, BERT introduces its special way of tokenization. The first token outputted by BERT is the <CLS> token which contains information about the next sentence classification task. Apart from this the two sentences are separated by a special <SEP> token.

In addition to single-sentence classification task and single sentence tagging task, this additional mechanism of pre-training for next sentence prediction allows BERT to solve a array of problems. These include sentence pair classification tasks like Natural Language Inference tasks, and question answering tasks.

<img width="690" alt="bert_types" src="https://user-images.githubusercontent.com/41947720/107882874-c7137380-6f11-11eb-992e-07464561673f.png">

## USING BERT

If you have been wondering when do I get to learn how to use BERT in my project, then thanks for hanging on until this stage. Here we will talk about two popular ways of using BERT: -

1. For Generating Contextualized Embeddings
2. For Fine-Tuning.

Before diving into it, let us set up our environment for running BERT.

We will use Pytorch and HuggingFace for running BERT.
HuggingFace is a NLP startup which release open source NLP state-of-the-art models which can be used by anyone.

![huggingface](https://user-images.githubusercontent.com/41947720/107882891-d692bc80-6f11-11eb-807d-ebc50d6d8bd4.png)

These models run with the support of deep learning libraries like Pytorch or Tensorflow 2.0.

Having known this, let us install the transformers module which contains the actual implementation BERT and related models.
pip install transformers.

For installing pytorch -> "pip install pytorch" (You could do conda install as well, depending on your virtual environment). (Note: Using anaconda is highly recommended).

Here, I will highlight the main steps involved in running BERT the full code is made available on github along with a dataset to experiment on here.

### TOKENIZATION:

![tokenization](https://user-images.githubusercontent.com/41947720/107882900-e3171500-6f11-11eb-8d87-909addd2da98.png)

Tokenization is the first step of any natural language processing task. We break the sentences to words/ sub-word chunks and use this for generating features that can be used to train the model.

The HuggingFace Transformers comes with its own tokenizer which varies as per the BERT model you are using.

The entire process of tokenization can be further divided into three parts: -

1. Converting the sentence/ sentence pair into numerical tokens.
2. Padding the sequences to a maximum length.
3. Defining the attention masks and the token_type_ids

**Attention masks** – These indicate whether the token corresponds to a word or refers to padding.

For normal words 1 is used as masking number. For padding tokens 0 is used as the masking token.

**Token_Type_Ids** – This is a special id which marks the difference between the pair of sentences in case of a sentence pair input. The first sentence from the <CLS> token till the <SEP> is represented by 0 and the second sentence uptil <SEP> is represented by 1.

Having finished the tokenization phase we can now either train a classifier on top of the embeddings obtained from BERT or we could tune the entire BERT architecture for about 2-4 epochs. In general, it is observed that fine-tuning gives better performance over using the embeddings directly.

[The entire code for this can be found on my GitHub repository here.](https://github.com/Nish-19/BERT_Tutorial) Please do check it out.

For in-depth understanding of how BERT works, I strongly recommend going through [this](http://jalammar.github.io/illustrated-bert/) awesome blog written by Jay Ammar.
