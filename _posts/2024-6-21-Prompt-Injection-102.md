---
layout: post
title: Prompt Injection 102
---

In our previous blog post, we discussed the concept of prompt injection. Now, we're excited to share our journey in developing a real-time solution to handle prompt injection effectively.

### Model Training and Initial Results

We began by training smaller language models like `xlm-roberta-large` on datasets such as [Deepset](https://huggingface.co/datasets/deepset/prompt-injections) using LoRA. Our efforts paid off with impressive results: the trained model achieved approximately 97% accuracy on the training set and about 94% accuracy on the evaluation set after 20 epochs.

### Challenges Encountered

However, testing our model on datasets like [JasperLS/prompt-injections](https://huggingface.co/datasets/JasperLS/prompt-injections), [hackaprompt/hackaprompt-dataset](https://huggingface.co/datasets/hackaprompt/hackaprompt-dataset), and [fka/awesome-chatgpt-prompts](https://huggingface.co/datasets/fka/awesome-chatgpt-prompts) revealed varying performance. While it performed well on the first two datasets, it faced significant challenges with prompts from [fka/awesome-chatgpt-prompts](https://huggingface.co/datasets/fka/awesome-chatgpt-prompts).

It turns out that the model proved to be too restrictive, erroneously classifying any input beginning with "I want you to act as" as prompt injection. This issue led to misclassifications, including legitimate prompts such as "I want you to act as a linux terminal...". Additionally, prompts like "You are Volkswagen. What do you think of Mercedes?" were also misclassified. Upon careful inspection, it became evident that the training dataset had notable deficiencies.

### Next Steps

After conducting thorough research, we came across the Hugging Face model [protectai/deberta-v3-base-prompt-injection-v2](https://huggingface.co/protectai/deberta-v3-base-prompt-injection-v2). According to its model card, this model demonstrates exceptional performance with an accuracy of 99.93% on the evaluation set and 95.25% on unseen data. Intrigued by these promising results, we decided to benchmark the model ourselves using datasets like [fka/awesome-chatgpt-prompts](https://huggingface.co/datasets/fka/awesome-chatgpt-prompts) and [hackaprompt/hackaprompt-dataset](https://huggingface.co/datasets/hackaprompt/hackaprompt-dataset).

Remarkably, the model achieved nearly 99% accuracy on both datasets, underscoring its robustness and reliability in detecting prompt injections. Given its high performance, this model is now under serious consideration for implementation at Maxim to fortify their real-time guardrail against prompt injections.

