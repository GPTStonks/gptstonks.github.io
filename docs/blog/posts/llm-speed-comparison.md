---
title: How Large Language Model (LLM) selection impacts inference time on consumer hardware
date: 2024-01-31
authors: [bytebard]
slug: llm-speed-comparison
description: >
  There are multiple inference frameworks for Large Language Models (LLM) on consumer hardware, from closed services such as OpenAI or AWS Bedrock to open source models quantized with techniques such as GGUF or GPTQ. In this post, we explore the pros and cons of each type of framework, and how it can impact our final service response time using GPTStonks Chat CE as an example.
categories:
  - Tutorial
comments: true
---

# How Large Language Model (LLM) selection impacts inference time on consumer hardware

[![Join waitlist](https://img.shields.io/badge/join_waitlist-0d0d0d?style=for-the-badge&logo=data:image/png;base64,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)](https://gptstonks.net/login)
[![Youtube Channel](https://img.shields.io/badge/channel-ff0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@GPTStonks)
[![X follow us](https://img.shields.io/badge/follow_us-000000?style=for-the-badge&logo=x&logoColor=white)](https://twitter.com/GPTStonks)
[![Discord](https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/MyDDGuEd)
[![GitHub Repo](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/GPTStonks)
[![Docker](https://img.shields.io/badge/Docker_Hub-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://hub.docker.com/u/gptstonks)

Hey finance and AI enthusiasts! :dollar: :brain: Embarking on the journey of Large Language Models (LLMs) can be complex, especially given the plethora of inference frameworks available. These frameworks are indispensable in various applications today! Therefore, we've crafted this comprehensive guide to assist you in navigating these intricate waters. We hope you find it insightful and encourage you to follow us for more!

<!-- more -->

/// tip | TL;DR

This blog post explores how the selection of Large Language Model (LLM) inference frameworks can impact inference time on consumer hardware, focusing on four prominent frameworks: **Llama.cpp's GGUF**, **GPTQ** (with Hugging Face's LLMs), **OpenAI API**, and **AWS Bedrock**. It delves into the **quantization strategies** employed by each framework, discussing their **pros and cons** and providing **benchmark results**. Llama.cpp's GGUF is highlighted for its lightweight quantization techniques, making it ideal for resource-constrained environments over CPU, although it has limited availability of pre-trained models. On the other hand, GPTQ with Hugging Face's LLMs benefits from a vast repository of pre-trained models and a robust community but may require GPUs and higher resource requirements for some models. Additionally, the post briefly touches on OpenAI API's access to advanced language models and its wide range of applications. Overall, the post aims to **empower finance and AI enthusiasts** in **making informed decisions** when selecting LLM inference frameworks for their applications.

/// example | Best configuration in most use cases (OpenAI API)
Add the following to your env variables (by default in `.env.template`):
```bash title=".env.template"
...
LLM_MODEL_ID=openai:gpt-3.5-turbo-1106 # See https://platform.openai.com/docs/models
OPENAI_API_KEY=sk-...XXXX # Your OpenAI API key
...
```
///

///

## Introduction

Large Language Models (LLMs) have emerged as powerful tools in natural language processing, significantly impacting applications in finance and AI. Selecting the right inference framework is pivotal to strike a balance between accuracy and speed. In this guide, we'll delve into four prominent LLM inference frameworks: **Llama.cpp's GGUF**, **GPTQ**, **OpenAI API**, and **AWS Bedrock**. We'll explore fundamental concepts, delve into explicit pros and cons, and provide benchmark results to empower you in making informed decisions.

## Local LLMs with Quantization

LLM quantization involves reducing the precision of model weights, enabling faster inference with minimal accuracy trade-offs. Let's delve into the quantization strategies employed by each framework.

### Llama.cpp's GGUF

/// details-info | Official specification of GGUF
The official specification of GGUF can be found in https://github.com/ggerganov/ggml/blob/master/docs/gguf.md.
///

**GGUF (Generative Graph Model Universal Format)** is a file format specifically designed for storing models meant for inference with the **Generative Graph Model Language (GGML)** and executors based on GGML. Unlike its predecessors (**GGML**, **GGMF**, and **GGJT**), GGUF is a binary format that prioritizes fast loading and saving of models and ease of reading. It serves as a successor to GGML, introducing changes to make the format more extensible, allowing new features to be added without breaking compatibility with existing models.

The key motivations behind GGUF include the ability for **single-file deployment**, **extensibility**, **compatibility with the `mmap` technique** for efficient loading and saving, **user-friendly usage** requiring minimal code, and comprehensive inclusion of all information needed for **model loading within the file itself**. It adopts a key-value structure for hyperparameters (metadata), enabling the **addition of new metadata** without compromising compatibility.

The **file structure** of GGUF is **meticulously defined**, specifying the global alignment, little-endian default (with a provision for big-endian support), and an enum for different data types. The metadata structure includes key-value pairs with types such as integers, floats, booleans, strings, arrays, and complex structures like arrays of arrays. The header provides essential information, such as magic number, version, tensor count, and metadata key-value pairs.

The standardized key-value pairs in GGUF include essential metadata like architecture type, quantization version, and alignment. Additionally, there are architecture-specific metadata for **LLaMA, MPT, GPT-NeoX, GPT-J, GPT-2, Bloom, Falcon, RWKV, Whisper, LoRA,** and **Tokenizer**. The specification also discusses the future extension of GGUF to include a computation graph, enabling executors to run models without their implementations of the architecture, and the use of a standardized naming convention for tensor names.

/// success | Pros
- Utilizes lightweight quantization techniques for efficient inference.
- Ideal for resource-constrained environments.
///

/// danger | Cons
- Limited availability of pre-trained models compared to other frameworks.
///

/// example | How to use it in GPTStonks Chat CE
Download the model using `huggingface-cli` and include the following to your env variables (by default in `.env.template`):
```bash title=".env.template"
...
LLM_MODEL_ID=llamacpp:<PATH TO DOWNLOADED MODEL>
...
```
If you are using a Docker container, the model must be mounted as a volume in the container to make it accessible to the API.
///

### GPTQ (with Hugging Face's LLMs)

/// details-info | Original paper
The original paper can be found in https://arxiv.org/abs/2210.17323.
///

The paper introduces GPTQ, a novel one-shot weight quantization method for Generative Pre-trained Transformer (GPT) models, addressing the challenge of high computational and storage costs associated with these large models. GPT models, renowned for their breakthrough performance in language modeling tasks, have massive sizes, and even inference for large models requires multiple high-performance GPUs.

Existing work on model compression has limitations in the context of GPT models due to their scale and complexity. GPTQ aims to overcome these limitations by proposing an efficient quantization method based on approximate second-order information. The method can quantize GPT models with 175 billion parameters in approximately four GPU hours, reducing the bitwidth down to 3 or 4 bits per weight. Remarkably, GPTQ achieves this with negligible accuracy degradation compared to the uncompressed baseline.

The main contributions and findings of the paper include:

1. **Efficient Quantization:** GPTQ is introduced as a post-training quantization method that can efficiently quantize GPT models with hundreds of billions of parameters in a few hours.

2. **High Precision at Low Bitwidths:** GPTQ achieves high precision even at low bitwidths, quantizing models to 3 or 4 bits per parameter without significant loss of accuracy.

3. **Improved Compression Gains:** GPTQ more than doubles the compression gains compared to previously proposed one-shot quantization methods. This allows the execution of a 175 billion-parameter model inside a single GPU for generative inference.

4. **Extreme Quantization Regime:** The paper demonstrates that GPTQ provides reasonable accuracy even in the extreme quantization regime, where models are quantized to 2-bit or ternary values.

5. **End-to-End Inference Speedups:** GPTQ's improvements can be leveraged for end-to-end inference speedups over FP16, achieving around 3.25x speedup with high-end GPUs (NVIDIA A100) and 4.5x speedup with more cost-effective ones (NVIDIA A6000).

6. **Implementation and Availability:** The authors provide an implementation of GPTQ, making it available to the community through the GitHub repository https://github.com/IST-DASLab/gptq.

7. **Novelty in High Compression Rates:** The paper claims to be the first to show that extremely accurate language models with hundreds of billions of parameters can be quantized to 3-4 bits per component. Previous methods were accurate only at 8 bits, and prior training-based techniques were applied to smaller models.

The authors acknowledge some limitations, such as the lack of speedups for actual multiplications due to the absence of hardware support for mixed-precision operands and the exclusion of activation quantization in the current results. Despite these limitations, the paper encourages further research in this area and aims to contribute to making large language models more accessible.

/// success | Pros
- Hugging Face offers a vast repository of pre-trained models, catering to diverse requirements.
- Benefits from a robust community with frequent updates.
///

/// danger | Cons
- Some models may have higher resource requirements.
///

/// example | How to use it in GPTStonks Chat CE
Add the following to your env variables (by default in `.env.template`):
```bash title=".env.template"
...
LLM_MODEL_ID=hf:<YOUR MODEL ID IN HUGGINGFACE>
LLM_HF_DEVICE=-1 # all GPU devices
LLM_HF_DISABLE_EXLLAMA=true
LLM_HF_TRUST_REMOTE_CODE=true
LLM_HF_GPTQ_BITS=<NUMBER OF BITS IN QUANTIZATION>
LLM_HF_DEVICE_MAP=auto
...
```
///

## External LLMs via APIs

### OpenAI
OpenAI API is a service provided by OpenAI that allows developers to integrate OpenAI's powerful language models into their own applications, products, or services. The API gives developers access to state-of-the-art language models, such as GPT-3, enabling them to leverage advanced natural language processing capabilities without having to train or maintain these models themselves.

Here are key points about the OpenAI API:

1. **Access to Advanced Language Models:** The API provides access to OpenAI's sophisticated language models, allowing developers to perform various natural language understanding and generation tasks.

2. **Wide Range of Applications:** Developers can use the OpenAI API for tasks such as text generation, translation, summarization, question-answering, and more. The versatility of the language models makes the API suitable for a broad spectrum of applications.

3. **Integration with Custom Applications:** Developers can integrate the OpenAI API into their own applications, websites, or services. This enables them to enhance the natural language capabilities of their products without the need to develop and train large-scale language models from scratch.

4. **API Key Authentication:** Access to the OpenAI API typically requires developers to obtain API keys. These keys serve as authentication credentials, allowing OpenAI to track usage and manage access to the API.

5. **Input and Output Customization:** Developers can provide input prompts to the language models through the API, influencing the generated outputs. This allows customization of the model's behavior to suit specific use cases or preferences.

6. **Ongoing Improvements:** OpenAI may release updates to their language models, and developers using the API can benefit from these improvements without having to retrain their own models.

/// success | Pros
- Employs state-of-the-art pre-trained models, ensuring high accuracy.
- Seamlessly integrates with OpenAI's ecosystem.
- Fast, accurate and generally reliable LLMs.
///

/// danger | Cons
- Consideration of usage costs, especially for large-scale applications.
- Need for an account in OpenAI and an API key.
- Closed source, so there is little information about the models' architectures.
///

/// example | How to use it in GPTStonks Chat CE
Add the following to your env variables (by default in `.env.template`):
```bash title=".env.template"
...
LLM_MODEL_ID=openai:gpt-3.5-turbo-1106 # See https://platform.openai.com/docs/models
OPENAI_API_KEY=sk-...XXXX
...
```
///

### AWS Bedrock

Amazon Bedrock is a fully managed service offered by AWS that provides a range of capabilities for building generative AI applications. It includes high-performing foundation models (FMs) from leading AI companies, such as AI21 Labs, Anthropic, Cohere, Stability AI, and Amazon. Amazon Bedrock allows developers to experiment with various FMs, customize them with techniques like fine-tuning and retrieval-augmented generation (RAG), and create managed agents for complex business tasks, all without writing code.

Key features and capabilities of Amazon Bedrock include:

1. **Model Availability and Integration:** Amazon Bedrock offers a choice of foundation models that users can access through the AWS Management Console, AWS SDKs, and open-source frameworks. Models from providers like Meta's Llama 2 with 13B and 70B parameters are also becoming available.

2. **No-Code Development:** Developers can build generative AI applications without writing code. The service supports experimentation with different FMs, customization with private data, and the creation of managed agents for specific tasks.

3. **Serverless and Integrated with AWS:** Amazon Bedrock is serverless, eliminating the need for users to manage infrastructure. It seamlessly integrates with AWS services like CloudWatch and CloudTrail for monitoring, governance, and auditing purposes.

4. **Privacy and Security:** Data privacy is maintained, and users have control over their data. Amazon Bedrock encrypts data in transit and at rest, and users can configure their AWS accounts and Virtual Private Clouds (VPCs) for secure connectivity.

5. **Governance and Monitoring:** The service integrates with AWS Identity and Access Management (IAM) for managing permissions. It logs all activity to CloudTrail, and CloudWatch provides metrics for tracking usage, cost, and performance.

6. **Flexible Interaction:** Users can interact with Amazon Bedrock through the AWS Management Console, SDKs, and open-source frameworks. The service offers chat, text, and image model playgrounds for experimentation with different models.

7. **API Access:** Developers can use the Amazon Bedrock API to interact with foundation models. The API allows users to list available models, run inference requests, and work with streaming responses for interactive applications.

8. **Billing and Pricing Models:** Amazon Bedrock offers billing based on processed input and output tokens, with different pricing models such as on-demand and provisioned throughput.

/// success | Pros
- Provides scalable infrastructure for handling large workloads.
- Integration with other AWS services for enhanced functionality.
- Fast, accurate and generally reliable LLMs.
///

/// danger | Cons
- Consideration of usage costs, especially for large-scale applications.
- Involves a steeper learning curve for users unfamiliar with AWS services.
- Need for an account in AWS and extra configuration.
- Some of the best models (like [Anthropic](https://www.anthropic.com/)'s models) are closed source.
///

/// example | How to use it in GPTStonks Chat CE
Add the following to your env variables (by default in `.env.template`):
```bash title=".env.template"
...
LLM_MODEL_ID=bedrock:anthropic.claude-instant-v1 # See https://docs.aws.amazon.com/bedrock/latest/userguide/model-ids-arns.html
AWS_ACCESS_KEY_ID=<YOUR AWS ACCESS KEY ID>
AWS_SECRET_ACCESS_KEY=<YOUR AWS SECRET ACCESS KEY>
AWS_DEFAULT_REGION=<AWS BEDROCK REGION TO USE>
...
```
///

## Benchmark

### Model selection

In this benchmark, we aim to assess the strengths and weaknesses of various inference frameworks on GPTStonks Chat CE. The models were selected with careful consideration of the following factors:

- **GPTQ:** Considering that consumer hardware often has less than 6GB of GPU VRAM, we opted for a NVIDIA GeForce GTX 1650 Ti with 4GB of VRAM. Consequently, the largest GPTQ model in use has around 3 billion parameters. After experimenting with different models, we found that [daedalus314/Marx-3B-V2-GPTQ](https://huggingface.co/daedalus314/Marx-3B-V2-GPTQ), which was quantized at the beginning of GPTStonks, performed well. However, it's worth noting that 3 billion-parameter models may not be powerful enough for an agent mode.

- **Llama.cpp:** Considering that CPU RAM in most consumer laptops ranges from 8 to 16GB, we selected a model with approximately 7 billion parameters. Among the options, `Zephyr 7B Beta` has proven to be one of the most effective. You can find its GGUF version [here](https://huggingface.co/TheBloke/zephyr-7B-beta-GGUF).

- **OpenAI API:** At the time of writing this article, `GPT-3.5-Turbo-1106` is the latest GPT-3.5 version. It offers a good balance between quality and price, making it suitable for a wide range of use cases.

- **AWS Bedrock:** Anthropic, available through AWS Bedrock, is considered one of the most advanced providers of foundation models and a significant competitor to OpenAI. The `Claude Instant v1` model from Anthropic is a commendable choice, striking a balance between speed, price, and accuracy.


### Results

To provide a practical understanding of the frameworks' performance, we conducted a benchmark test measuring both inference time and response quality. The following detailed results shed light on their comparative strengths, where the response quality is evaluated with GPT-4:

| Framework and model ID             | Inference Time (sec/token) | Response quality (%)
|------------------------|---------------------|--------------|
| **Llama.cpp:** zephyr-7b-beta.Q4_K_M.gguf         |          1.74   |      95 |
| **GPTQ:** daedalus314/Marx-3B-V2-GPTQ    |          1.03    |      10 |
| **OpenAI API:** gpt-3.5-turbo-1106             |          0.14    |      95 |
| **AWS Bedrock:** anthropic.claude-instante-v1            |          0.05    |      90 |


Below is a visual representation of the inference time and response quality for each model and framework:

![inference frameworks benchmark seconds per token]

The graph shows that **closed models** are significantly faster than **local models** when dealing with **limited resources**, even when employing **quantization techniques and consumer GPUs**. It's worth mentioning that these observations might not apply universally to open-source models running on high-end servers. In terms of response quality, similar results can be obtained with both open and closed models, but at the cost of speed or expensive hardware (Zephyr 7B Beta would consume around 7GB of GPU VRAM). From a user's point of view, utilizing external models can result in quicker and more accurate responses, though it does come with considerations such as **API service usage** and a balance between **privacy and autonomy**.

## Conclusion

In summary, exploring the world of LLM inference frameworks requires careful consideration of **quantization techniques**, **inference procedures**, and **sampling methods**. The benchmark results indicate that **closed models** tend to excel over **local models**, especially in scenarios with **limited resources**, even when employing **quantization techniques** and **consumer GPUs**. It's important to note, however, that these findings may not be universally applicable to open-source models on high-end servers.

From a user perspective, tapping into external models can offer quicker and more accurate responses. Yet, it comes with considerations such as **API service usage** and a trade-off in **privacy and autonomy**. By grasping these key concepts and weighing the pros and cons of different frameworks, users can confidently choose the LLM solution that aligns best with their needs.

Stay curious and happy coding! :smile:


[inference frameworks benchmark seconds per token]: llm-speed-comparison/benchmark-sec-token.png
