---
title: How to run GPTStonks Chat Community Edition (CE) on a personal computer
date: 2024-01-10
authors: [daedalus, bytebard]
slug: run-gptstonks-locally
description: >
  Learn how to run GPTStonks Chat CE (Community Edition) on your own personal computer
  using minimal hardware! GPTStonks Chat is designed to run with open source LLM providers
  such as Hugging Face. Furthermore, with libraries such as Llama.cpp GPTStonks can
  be run on consumer hardware even without GPUs. An example is provided with Zephyr-7B.
categories:
  - Tutorial
---

# 🚀 Running GPTStonks Chat Community Edition (CE) on Your Personal Computer

[![X follow us](https://img.shields.io/badge/follow_us-000000?style=for-the-badge&logo=x&logoColor=white)](https://twitter.com/GPTStonks)
[![Discord](https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/MyDDGuEd)
[![GitHub Repo](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/GPTStonks)
[![Docker](https://img.shields.io/badge/Docker_Hub-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://hub.docker.com/u/gptstonks)

Hey stock enthusiasts! 📈 Ready to unleash the power of GPTStonks Chat Community Edition (CE) on your humble PC? We've got you covered! In this guide, we'll walk you through the steps. Let's dive in! 🚀

<!-- more -->

## What GPTStonks Chat CE Can Do for You?

GPTStonks Chat CE is your financial wizard, offering a magical blend of functionalities:

- 🌐 **Analyze the web:** Fetch and analyze the latest info about companies, states, investors, and more.
- 🕵️‍♂️ **Trace the info:** Understand how the data is retrieved, making debugging a breeze.
- 📊 **Get historical data:** Visualize financial data via OpenBB (OpenBB account needed).
- 📈 **Create awesome plots:** Auto-plot historical price data using cool candle charts.
- 🧐 **Perform complex analysis:** Ask complex queries like stock overviews, sentiment analysis, or latest news.
- 🤖 **Customize the agent:** Integrate any LLM in LangChain and LlamaIndex for supercharged performance.
- 🧰 **Expand your tools:** Seamlessly integrate custom or pre-existing tools.

The future of finance with AI is closer than ever!

## Meet the GPTStonks Chat CE Trio

GPTStonks Chat CE flaunts a microservice trio:

- 💻 **Frontend:** Crafted in React, featuring the chatbot and charts powered by [TradingView's Lightweight Charts](https://www.tradingview.com/lightweight-charts/). Get it on [GitHub Packages](https://ghcr.io/gptstonks/front-end:main) and [DockerHub](https://hub.docker.com/r/gptstonks/front-end).

- 🚀 **Backend (API):** Python-powered with FastAPI, running a [LangChain agent](https://www.langchain.com/use-case/agents) that decides which tools to use. Grab it on [GitHub Packages](https://ghcr.io/gptstonks/front-end:main) and [DockerHub](https://hub.docker.com/r/gptstonks/api).

- 🗃️ **Database:**
  Open-source MongoDB is readily available on [DockerHub](https://hub.docker.com/_/mongo), standing ready to manage essential provider tokens (PATs), presently focusing on OpenBB's.

## Running GPTStonks Chat CE with Docker Compose

Getting this trio up and running is a breeze with Docker Compose:

```yaml
version: "3.8"

services:
  api:
    image: gptstonks/api:latest
    ports:
      - "8000:8000"
    env_file:
      - .env.template
    volumes:
      - ${LOCAL_LLM_PATH}:/api/gptstonks_api/zephyr-7b-beta.Q4_K_M.gguf

  frontend:
    image: gptstonks/front-end:latest
    ports:
      - "3000:80"

  mongo:
    image: mongo
    ports:
      - "27017:27017"
    environment:
      - MONGO_INITDB_DATABASE=mongodb
    volumes:
      - mongo-data:/data/db
      - ./mongo-init.js:/docker-entrypoint-initdb.d/mongo-init.js:ro

volumes:
  mongo-data:
```

/// tip
To install Docker Compose, follow the official [installation guide](https://docs.docker.com/compose/install/#installation-scenarios).
///

In this tutorial, the selected model is [`Zephyr 7B Beta - GGUF`](https://huggingface.co/TheBloke/zephyr-7B-beta-GGUF). Download it with `huggingface-cli`:

```bash
huggingface-cli download TheBloke/zephyr-7B-beta-GGUF zephyr-7b-beta.Q4_K_M.gguf --local-dir . --local-dir-use-symlinks False
```

Once you've successfully downloaded the model, you'll want to mount it into `/api/gptstonks_api/zephyr-7b-beta.Q4_K_M.gguf`. This is crucial, as the environment variable `LLM_MODEL_ID` specified in `.env.template` references this path within the container. To achieve this, set the `LOCAL_LLM_PATH` to the local directory where the model is stored, like so:

```bash
LOCAL_LLM_PATH=path/to/downloaded/model/zephyr-7b-beta.Q4_K_M.gguf docker compose up
```

/// settings
Considering a different model? No worries – it's as easy as adjusting the `LLM_MODEL_ID` in the `.env.template` file to the name of your preferred model. After that, a simple command:

```bash
LOCAL_LLM_PATH=path/to/downloaded/model/new-model-name docker compose up
```

And you're good to go! 🚀

If you're leaning towards using closed LLMs, like **OpenAI**, the process is **straightforward with GPTStonks Chat CE**. Just insert a valid `OPENAI_API_KEY`, and set `LLM_MODEL_ID` to `openai:<model-name>` (e.g., `openai:gpt-3.5-turbo-1106`).

A quick heads-up: different models may perform best with specific prompt structures. Keep that in mind for optimal results! 👍💻
///

When Docker Compose is initiated using the command `docker compose up`, it takes a few minutes to download all the necessary images. After this process is complete, the environment automatically starts. Upon observing the message:

```vbnet
INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
```

as provided by the API in the Docker Compose output, you can access GPTStonks Chat CE by navigating to `localhost:3000` in your web browser. The webpage will display content similar to the following:

![GPTStonks Chat view]

/// success
🌟 Congratulations! You've got GPTStonks Chat CE running on your PC. 🌟
///

## Chatting with GPTStonks CE: Let the Fun Begin! 🎉

Now for the fun part! Head over to `localhost:3000` and witness the magic. Throw any financial query at it, and let the chatbot impress you. Here's a peek when asked about Nvidia's latest news:

![news Nvidia]

Great! The news is summarized, and a header is added for transparency to ensure the data's source is well-known. Additionally, we can inquire about more specific financial data. Currently, OpenBB is the sole provider for this purpose, but there are plans to incorporate additional providers in the future.

To use OpenBB as external provider, first create your account following their [instructions](https://docs.openbb.co/terminal/usage/hub). Then, set up the API keys of your financial data providers (e.g., Financial Modelling Prep, Polygon, etc.) in OpenBB Platform's API keys section. **Most of them have free plans!** Finally, we can set up our OpenBB PAT in GPTStonks Chat CE by going to the API Keys section that appears after selecting the red arrow on the left:

![set OpenBB PAT]

After configuring OpenBB's PAT, let's proceed to request specific data. For example, you can inquire about the historical price of MSFT using the command `get the historical price of MSFT`:

![Microsoft historical price table]

Awesome! The data comes back in the form of a handy table that we can effortlessly navigate, download as JSON or Excel, or unleash the magic of visualization with just a click on the brush 🖌️. And there you have it, the plot automatically generated by GPTStonks Chat CE using TradingView's [Lightweight Charts](https://www.tradingview.com/lightweight-charts/) 📊:

![Microsoft historical price chart]

It's a seamless experience, **making financial data analysis a breeze**!

/// info
Having financial data presented in tables, candle charts, and JSON or Excel format offers several distinct benefits, each catering to specific aspects of analysis:

1. **Tables:**

    - **Structured Information:** Tables provide a structured and organized representation of data, making it easy to read and comprehend.
    - **Comparative Analysis:** Side-by-side comparison of different financial metrics becomes convenient, facilitating quick insights.
    - **Numerical Precision:** Tables retain numerical precision, ensuring accurate representation without losing significant data.

2. **Candle Charts:**

    - **Visual Patterns:** Candle charts offer a visual representation of price movements, making it easier to identify patterns and trends in the market.
    - **Historical Context:** The historical context provided by candle charts aids in understanding market sentiment and potential future movements.
    - **Decision Support:** Traders often use candle charts to make decisions based on chart patterns and technical analysis.

3. **Downloaded data as Excel (or JSON):**

    - **Custom Analysis:** Excel provides a versatile platform for custom analysis, allowing users to apply formulas, create pivot tables, and conduct scenario analysis.
    - **Data Manipulation:** Users can manipulate financial data in Excel, enabling tasks like sorting, filtering, and aggregating data for specific insights.
    - **Graphical Representations:** Excel's charting capabilities allow for the creation of various charts and graphs, enhancing visual representation for better interpretation.

///

## 🚨 Important Remarks

As we delve into the realm of open-source and local CPU RAM, here are a few considerations:

- ⚡ Speed is contingent on model size and hardware. The inclusion of GPUs, utilization of smaller models, or external providers such as OpenAI can enhance both accuracy and speed.
- 💡 Zephyr 7B Beta - GGUF requires approximately 7GB of CPU RAM.
- 🤖 Effective prompting is essential for optimal performance. Check out our `.env.template` for prompts inspired by [OpenAI's guide](https://platform.openai.com/docs/guides/prompt-engineering?ref=upstract.com).

Time to explore, analyze, and thrive! 🚀✨

[gptstonks chat view]: run-gptstonks-preview-locally/example-gptstonks-chat.png
[microsoft historical price chart]: run-gptstonks-preview-locally/example-chart.png
[microsoft historical price table]: run-gptstonks-preview-locally/example-command.png
[news nvidia]: run-gptstonks-preview-locally/news-nvidia.png
[set openbb pat]: run-gptstonks-preview-locally/set-openbb-pat.png
