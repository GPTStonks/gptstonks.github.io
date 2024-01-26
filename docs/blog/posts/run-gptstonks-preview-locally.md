---
title: How to run GPTStonks Chat Community Edition (CE) on a personal computer
date: 2024-01-10
authors: [bytebard]
slug: run-gptstonks-locally
description: >
  Learn how to run GPTStonks Chat CE (Community Edition) on your own personal computer
  using minimal hardware! GPTStonks Chat is designed to run with open source LLM providers
  such as Hugging Face. Furthermore, with libraries such as Llama.cpp GPTStonks can
  be run on consumer hardware even without GPUs. An example is provided with Zephyr-7B.
categories:
  - Tutorial
comments: true
---

# 🚀 Running GPTStonks Chat Community Edition (CE) on Your Personal Computer

[![Join waitlist](https://img.shields.io/badge/join_waitlist-0d0d0d?style=for-the-badge&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAC0AAAAtCAYAAAA6GuKaAAAAIGNIUk0AAHomAACAhAAA+gAAAIDoAAB1MAAA6mAAADqYAAAXcJy6UTwAAAAGYktHRAD/AP8A/6C9p5MAAAAHdElNRQfoAR0OGiOxBDMeAAASyklEQVRYw6VYaZRV1ZX+9j7n3jfXXMVQIBRDEQbRGOcgghBtFDVOK06dKOIQokmMpG1MHKJGg2icWolCpI2JZqlpjcZWE40hEuMQNTgwqSAyFkWNb7z3nnN2/7iPol0GJN13rbPuu++d/db39vvO3t+3Cf/E5d57CPK3R0HNo4FtqyEGcI1toEI3cMAJ0Ad9Y4+x5R8vxIar/g1tRx0HWvF7uNpWyNHTgFIZ6pwzkDz/rH3Gwfu6MVp7P+gn/wqpr4eoRIvUDJkjNYO/QTrR6JQH9/LPEf5lyT+MzV93LczEdowcMxGoyU3CETOvpwkTzqdcJuVIo/LQf6Gy9OF9Bk37lOH1D4D+fQ7cnHPhvKZx3L3tThTyx0roBCr5pK0d+m0q9G1Bz1bwF8+Anj5vILZ0602wI0aBf7IQGDbqCNq67We2UJrsHEeUrrtDJh94nWzeWpLAwH3zdDSec+b/H7T5ZCn4pbmQtnMhXvM46t6ylArFKVIxsIEFDIFU5imXa51HxZ4ttHMT3OFnITF9Hgr33gwZNhp0+62QISOOwJatS02xOMGEAgkAstrodP1dNHHiNdi6o4ggQmrBeUicPPv/DjrYvAx45xpwy7FgVTMWfduXUqEwFYGDCyxsYCGBABGDVOZpZAfPQ7F/MzrWIxo+G6htAT1wH2R4+xHYunWJyRcmRoGFDSSOCwA22nrp+ru9SZOuth07CwgNMtdcBG/WMXvEpfb0QX7Lr9DzwS3Qg4+F9mtHo7z9fjalaSTxb3UOA0scgCgchyAYR9mWl+Gl+pkSoGceBUaNPxpd25fYqDzBQuBcvEQIcICzjl05PATdhRo9ftwKlMPQvL4GN3/05j8HenvHI9i67mZkWo6F8upGS3nH/WTKxzAAAQAncBYQJ3AiEAeIFcBE7RwEEyhZt1YoHUJ5s9Cz424bltvtrn0iEBFgIA5wxrErB4egqz+dnDz5z+KsuXn1q/tOjw0dv8FHa36EEYNnI6XSY7i8/X4vzE9PWAPfGKgoAlUMXMXBVmKaSMXBBQ4cCNgAZLxOqXAX8uFwUwoyNty1VyCV6v6Kg1QErixAGTHHkSgmR7Wd6ArFlwa9+8weQX+q5K3d+RRWrLsRjcNOh/XrxxajvqUVZ6eH7CNgDyEzrGI4zXCaIBogRYAGiAVQEv93GgUo9MLngHyCeAR4BHgAvOqzjuPYI5AmEAOkXOgoDB2bvR5EPQC4+89Y2fEIRg87G1CJ9lKlc4lyZqqwBiAQZwFmEDM8xYB2II8BA7ARQAsYDJXJPYz0kB9VVOMWf+NHh7HsXCSudFBkAbIC5xFgYtCkUQUOEHTAuZpbE1MPec19sglYuWfQCgDWV9ZgffEt1PlN8FR2dBD1/Ny6cCoTQJD4pIkDOQGJg4KDEgAiYEdgB2hS4GTuP6Vp1HdRym8Wl4p408YNXNPwKltzMKxtjb9GIE4AJyAHsCMo5VVUfe2PadZRi+yqdREMcMuav++dHtvKHyOpstCJwfUFV7itAjvVskbECiEpRBTfQ9KISMGwglMMUgylCNrXQtmaZWhpu4LCnm6gCFZJFG9+GujtfkfVNV/kp9JveZ6G0gxWBKUovie9ih7UeKN3ysyFWPdh6GDQ+MSyvdJDfRCugzNlHN4wG+8V/vr90FYuIQgBUs1sfNIhAkK8FARaBFoABRL42WWoGzWfKj09FBbB+58I/yuX4vpRGub790E9cd92rm9+nU10MCIzFNaBRMBKl7mu7gZ1/HGL7DvvR4Cg5dFH8HmX3hH1osd0oKP7NweUJLqYiQlKAeLArEHiQM6ByEKRgyGFCAoeWfhaRLz0Mpdqm0+Frh5CAHPAGUiMOwUAkPjG1QjAwO3PwV0+6++qYfCchMG9bPJTLOmCS+VuKM6YcXvyjZUReYSmB371uYABQKfIx4Ubz8Z1I355Zghq9VgBToHYgcWBnAKTArGCEofIMRQpJJQnzs8u48yI+ZTv6gEFkHGzoTauhHl5ISSqgFQScAL5xUL4tz+L6LsnvcstQ872dOqrJLTJfenQ36XeW2Wscsg0j4QAKH/9AsBayLBmUDlE+q47P8vpHaYfd4xbXl8gmVEBx5yFgiEFQxwvZljSMIizbJUWm6x9gGpHzTdRXw84BA+dAfWXH4NcJ8SvSYGo1Y04XElxB1DzMcKHbgY2fAyE4SZ0bLnb9XQ9aTd+YlRCw69rRf7oqYgOPgxQqpFBg/ILF8EZi76LLvkMaHqk9zkw8QGdpusFspWmtAvg2xAJF8G3ITwTwjchEtbAMyGSNpSsTjxQm2mdr8qdvYkwj0TDFPCzZ8G1z4HoppHUve1GlMuHCid+7RrbF1FxZ55MBBozE+7tDeCaeoDi7lhZtQFB637I3ncf3KARh6Kra5GLbJ1kszf2v/j8Y6k582Aso/kX9+zOdB8FKJIZVCZkQ1IIqtXBECOqZtxSNfOsIH7NY35u9PxSVOwtwUENORp4dS7c5AuBbMsYKm1dQlHvOTCFsSj3/oB2rL1JMs05IR92zR+hD9wP6rS5UKfORXHTNoTDhsH/1f0Ixoz8si3uXBZGxalBVJ4c9vQtTk2bNafwwL3EuQz6f3jjbk6XiQBWiZCYHTEUKyhRYCgQWTAUFOu42TEXxatb3GV6e9POoK3pKNiVl8KNPR/s1Y5G78b7yeWnQzmIJog1jErfPNq2ltA0fgFsZz5a9SfYtx5F+c0PEKUbkPnlYoRjxk/l7R33GwTjjF8VYWHYyL29izIzTt5pVq19qmHbGtjjj4E68kiwZQ1LSiJWiJir9XhXtuO7JQXLGk5pNprTFaWw04vw0uUnImw9BZJpakNly33kitPhCcQDRANOARYRS6X3m+hYtZBSDTXMCnj3BVBdPXJP3AM7fuI0Lu5cajkY5/xdEiGONyZoMN3dN3oHHzK659gzUHjs2ZgeTD4c6aIhNlG1kexqJpYVLHHcTFjBEVKRLX0n49cNSakcxlz9Pdhkc3tQ2b4kcpUZTlGcYU0QhXgx4CRiV+m7GDvWLORcc21UKEJ+vxhm4hdnoNy9xFE41nkE8bBbn6i4X5ugvH/U1XlR/e8fI25qjJvLSddcDGad6kfla85JjgEwZGCpXa8lfp9cNFpceXyCkx0+eRNR2XmHiwpHiTgAUi2TcasWK4DEBw7WEqLwIFfoGyGc6FHpppno61pkovJoM9C/4vYuVYkAh3hZGRb+8eVn7aZNXTctugW6TqWgWW/eJn0fhNYMicDQUIhEQ4mDFhvXZxGQjUUh2crxygTT2ATkTJBKgCHEA4JKaRerOI8B6wAWOHIQFzIXe86GKZwsJZtyCNjpqqa2gHgEMQxYgRgCeQI4gjPhfra3e5pZ9+FaNfuX4JGqGYuKf8h75P/BqpjHESlErGBYIyINQwohMQIiBGA4Tq4klVlAOn291f6G3RolrulOMURXJadmkCKQIihNUJnUy5StvYyyNQs5meokj2NK6KpcrcpY8mKaQQuEHbly+aiWFctV/s7FUKdf8000qTok2dtRknC2c7aOIWCq0mSX/nACwMFX/iuZROP5YbD9dyr/4YpMTdub5IJD4WwLZDetSKraxcZqThGDkzVPoX74RdK9/U+b5z/5Yv1JX94oUXCMczYdO5kqPRwGKCIOgCOAdWi2bH3U9fVXeATlME4NwhVvfXlNkhNLrNJiSMEg7oABaQQUVxb2Mi+nk80X5G3h/SntP0Fr2/mw5e0r/FTjXPJTq4Q1DGlYYggToAisGMrX4JqaxzFkxCWwvRu19GPkw9fCn//go5TOPKg8BjSqVYcGsi5VowAFgGxGSsWEBBXwRB6CPlfGbV96BS267me+Svw2YkZE1fLHHAP208vTqca5fa685lvLr8CqvhdAQScGtZ0LW9j4mp9quZD91PvC1TLJClAMTjCopuYxDGm/lML+bVTaAhw9F27zm6hcOxOc0Bt4F1AVA98FepdJgJLYHXkC0hLr6QN1K/pdGV0m393AuSuUTi6PmBAQ7QL8p2yqaW6fi9Y9uf1pPH7yckys+wqah34dUX49Bo25GFHho1cSqcY5OpF6F6wgzCBPATW1j8rgkZch7OpA0AU67BLI648BLS3g9slDCZXTnI5B7eY1dj8rgDRAPixnPcsZHYM+gJpwmB6Jl8OP0G8L6xs5N8fjxG/AKq914vlMov7CLlf58IW+NzBvwgJ8sfbogZbaMPgcRPmNGNY+H7b8yevJdPNcL5l9jROpHsrWL0HL6EsR9XYg2gY64EzYNx4EGppBudxg9H98l5PSNNGyG7CO6/su0OxxfDDT/lYe3VagxoZPu/HHzWo8VHkFh/BINNlETUTl8WlS68umt3N58W18u/FESKkTzBqFoANkA2RVDaw4HGEB3TwDve9fgWTNpFayhRadbFmDvo/LKHeCB58Aee0XkORgiKodgs5N/+Hy+VOjikFUsbBlC1t16LFjF1BZQBUBIoAbW27pe+SZK/d77olPu/HT9XicmzoMfmQRwvYbca9ZsZ0laJzfcjJ6Sj0og5FTaV9BT1Wkj0yrWk3O4TUITNcfcduBD0FctAXOvo2wvww/A249DdGqB+EaWyE1DUOptPUeuOKpTmPA1Ttd7YQ6rtekCeQB5AGc9opcl32x7usnwHR27dsA8i3ZjNX9a5GEYDDXJjqDD64yUf/lygYmSeqWEf6k27qjTyKIw5TW8z4VazufBFbfA0mOhlN1rapz4z2UL5xsAwsTCKKyQVQxsEF1FlJ2QCXOMFccEAookfsDTzj4dAkq/XVfPevzR71vSifeKG2AUR4yqiG5Ltp0dY8LFgSQnGHUhwiu3Ry8e2WdavZJgFc27TalpvMpmI9+BqkdB8o1DtPlzfeSlE6GBkQzZGBOspvPpAmsCazjA8gpr0/V5+6UVa/2mxVvQR94+N5BvyI7sTzcCKMSqNF1qXV2+3V9CP8tIPIsazjScKSSkVR+uD1Yd2WNGuwTHF7btASlrqfR8fGDCGsnAemW4VLauhiudBJ0PKwRhXgWoAikGKSqgD0CK4A1oBLKqbrM3W7mrOd48iSkzzs1Fkx7Az3qh+dCEaGZc5kPbMcNJSlfTmI9BcRuGgIWAcNpSHhkaHukUbf+VbhkB7Uch3JhA3SibrgpbF6MsDCbY/00IKbEysBsTwRgIZATKAcoVpZz2cU0fOT1/Mm6iosc6i9bGEvTPQF+3m1HghRSlMm+i66buij8TsCkQ1aocOxwQjAMYodjQYlIKld1mQ+uzniZmsTYBji/ob1Y6rivbCsnVEghVAyn4tpbHZ9V6QBozVCaoDXBSyqn63OL/f33X8BhPk+2guzBR+32iHsG3YHb5e/YH43f6pPCnb4JVcpFSNoQCRMiZSOkbYC0DZF0IXwXxb7SmSgNXpG0blPSlL7khf0TEzaAvys2CqFCA6lY2Gppk1DiEhdYcARHKr3Y1Lct4EJvnqyBbZ+G3KyLBrBp7OV6jjdglGtoC4gUMUMLg0mBq+ME5TQUWSgwSBgU58DTLjqaJarAhWkBgUgB5MDEYOa4vXsCNgLxBLAC0g4k2iGZXhzVD1vAvd15sRG8ydORnn7Rp3Dt+SBKAhfYg6BFPwyoNSHFesTskq3V+y4zHBLHslUl17Bfd572G6YrL3eNVbo7pN02LmQFywxRsfxUiqA1oH12nM0ulsFjF6ggn4eKgPbD4E//7Ahhj6ANBVhaOAQbOf9WVhIXCum1Af+vGQhzVWfHSjAkBlTqHc9rPK8/6nmIRF6/+PLrbvD87GWivB2WGFF1FhgxwTEAjsub8tghm13sho5dwFFPngnQB52I7Kzv/UNse20ut4arMVSSeNzbiOEuNaWI8hJtgy+kTYSUjZAwMb8TLkBO3DtNnJ5bina+MaVhJsrdf4WWEKv//C2MPeSqM6XSd5eKguaECZCwAVKRgR8Z6EgcKHOvqWm7ivq68qhEwPh/gf+Fr+0R117r9Hx/PLqojLOjkdiBwooaJOYK61Wh4gEDHCkGecmViUTDBTuk8MYxg0/DtmAL2oddCBKH/afejZUv3fRrP5H9Lmu907GCIY2IGfDYIZe7xw76wlUc9ebBBvqg4/cK+HNBA8Bl/gRsUUWcZUejk0p/qUfqAmbv/ZAJkSKwl3wz7dfP6XKVv53QchpWFz/EofXHAQDa9rsMShymzLoDd39/4cOJZN2lyktuASlA+85lm+5F64QfkO3Kgx30hBPAI874PEj7pj0AYHH4HsajAcvoHYxAzcGBK16ZsCZsFP+mvOl+/wc1p+PZ8gocnz7qM7EdG38KVkms/O08TJp53RQK+k5JsNqQrB3zIOU35Dnqgx5xDqjuqH2Fs+/Xg9EqiBFcGr2IZ2V94nnZ7N9ceAZ4Dvjvytt7je3evAT93U9iy7uX4/WfAh3PHYjyh7eguOY6SOH1fwrH/wAUXpj5bemUfwAAACV0RVh0ZGF0ZTpjcmVhdGUAMjAyNC0wMS0yOVQxNDoyNjoyMCswMDowMMR5rqgAAAAldEVYdGRhdGU6bW9kaWZ5ADIwMjQtMDEtMjlUMTQ6MjY6MjArMDA6MDC1JBYUAAAAKHRFWHRkYXRlOnRpbWVzdGFtcAAyMDI0LTAxLTI5VDE0OjI2OjM1KzAwOjAwfKMY8gAAAABJRU5ErkJggg==)](https://gptstonks.net/joinwaitlist)
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
- 📊 **Get historical data:** Visualize financial data via [OpenBB](https://openbb.co/) (OpenBB account needed).
- 📈 **Create awesome plots:** Auto-plot historical price data using cool candle charts.
- 🧐 **Perform complex analysis:** Ask complex queries like stock overviews, sentiment analysis, or latest news.
- 🤖 **Customize the agent:** Integrate any LLM in [LangChain](https://www.langchain.com/) and [LlamaIndex](https://www.llamaindex.ai/) for supercharged performance.
- 🧰 **Expand your tools:** Seamlessly integrate custom or pre-existing tools.

The future of finance with AI is closer than ever!

## Meet the GPTStonks Chat CE Trio

GPTStonks Chat CE flaunts a microservice trio:

- 💻 **Frontend:** Crafted in React, featuring the chatbot and charts powered by [TradingView's Lightweight Charts](https://www.tradingview.com/lightweight-charts/). Get it on [GitHub Packages](https://ghcr.io/gptstonks/front-end:main) and [DockerHub](https://hub.docker.com/r/gptstonks/front-end).

- 🚀 **Backend (API):** Python-powered with FastAPI, running a [LangChain agent](https://www.langchain.com/use-case/agents) that decides which tools to use. Grab it on [GitHub Packages](https://ghcr.io/gptstonks/front-end:main) and [DockerHub](https://hub.docker.com/r/gptstonks/api).

- 🗃️ **Database:**
  Open-source MongoDB is readily available on [DockerHub](https://hub.docker.com/_/mongo), standing ready to manage essential provider tokens (PATs), presently focusing on OpenBB's.

## Running GPTStonks Chat CE with Docker Compose :whale:

### Configuration :gear:

/// details-info | How to install Docker Compose
To install Docker Compose, follow the official [installation guide](https://docs.docker.com/compose/install/#installation-scenarios).
///

/// details-tip | Downloading configuration files with git
If you already have `git` installed, you can obtain the configuration files by cloning GPTStonks' API repository:
```bash
git clone https://github.com/GPTStonks/api.git && cd api
```
After that, proceed to [Large language model selection :brain:](#large-language-model-selection).
///

Getting this trio up and running is a breeze with **Docker Compose**. Just head over to your local directory, create a new file called `docker-compose.yaml`, and include the following content:

```yaml title="docker-compose.yaml"
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

Furthermore, a brief script is necessary to initialize the database with the appropriate structure. To complete this task, create a file named `mongo-init.js` and include the provided code.

```js title="mongo-init.js"
db = db.getSiblingDB('mongodb');

db.tokens.insertOne({
    description: "Initial document"
});
```

### Large language model selection :brain:

In this tutorial, the selected model is [`Zephyr 7B Beta - GGUF`](https://huggingface.co/TheBloke/zephyr-7B-beta-GGUF). Download it with `huggingface-cli`:

```bash
huggingface-cli download TheBloke/zephyr-7B-beta-GGUF zephyr-7b-beta.Q4_K_M.gguf --local-dir . --local-dir-use-symlinks False
```

/// details-info | How to install `huggingface-cli`
`huggingface-cli` can be installed in your Python environment using `pip` (from HuggingFace's [docs](https://huggingface.co/docs/huggingface_hub/main/en/guides/cli)):
```bash
pip install -U "huggingface_hub[cli]"
```
///

Once you've successfully downloaded the model, you'll want to mount it into `/api/gptstonks_api/zephyr-7b-beta.Q4_K_M.gguf`. This is crucial, as the environment variable `LLM_MODEL_ID` specified in `.env.template` references this path within the container. To achieve this, set the `LOCAL_LLM_PATH` to the local directory where the model is stored before running `docker compose up`, like so:

```bash
LOCAL_LLM_PATH=path/to/downloaded/model/zephyr-7b-beta.Q4_K_M.gguf docker compose up
```

/// details-settings | Using a different model
Considering a different model? No worries – it's as easy as adjusting the `LLM_MODEL_ID` in the `.env.template` file to the name of your preferred model. After that, a simple command:

```bash
LOCAL_LLM_PATH=path/to/downloaded/model/new-model-name docker compose up
```

And you're good to go! 🚀

If you're leaning towards using closed LLMs, like **OpenAI**, the process is **straightforward with GPTStonks Chat CE**. Just insert a valid `OPENAI_API_KEY`, and set `LLM_MODEL_ID` to `openai:<model-name>` (e.g., `openai:gpt-3.5-turbo-1106`).

A quick heads-up: different models may perform best with specific prompt structures. Keep that in mind for optimal results! 👍💻
///

### Starting GPTStonks Chat CE

When Docker Compose is initiated using the command `docker compose up`, it takes a few minutes to download all the necessary images. After this process is complete, the environment automatically starts. Upon observing the message:

```vbnet
INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
```

as provided by the API in the Docker Compose output, you can access GPTStonks Chat CE by navigating to `localhost:3000` in your web browser. The webpage will display content similar to the following:

![GPTStonks Chat view]

/// success
🌟 Congratulations! You've got GPTStonks Chat CE running on your PC. 🌟
///

## Chatting with GPTStonks Chat CE: Let the Fun Begin! 🎉

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

/// details-note | Benefits of using tables, candle charts and downloaded data
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

## Seeking simplicity? Give GPTStonks Chat web a try!

We're thrilled to share that our web service is on the horizon. Forget about hardware or configurations—immerse yourself in refining your investments with top-notch information. If you're eager to get started, be sure to join the [beta waitlist](https://gptstonks.net/joinwaitlist). Stay tuned for more updates on this exciting development!

## 🚨 Important Remarks

As we delve into the realm of open-source and local CPU RAM, here are a few considerations:

- ⚡ **Speed is contingent on model size and hardware**. The inclusion of GPUs, utilization of smaller models, or external providers such as OpenAI can enhance both accuracy and speed.
- 💡 Zephyr 7B Beta - GGUF requires approximately 7GB of CPU RAM.
- 🤖 **Effective prompting** is essential for **optimal performance**. Check out our `.env.template` for prompts inspired by [OpenAI's guide](https://platform.openai.com/docs/guides/prompt-engineering?ref=upstract.com).

Time to explore, analyze, and thrive! 🚀✨

[gptstonks chat view]: run-gptstonks-preview-locally/example-gptstonks-chat.png
[microsoft historical price chart]: run-gptstonks-preview-locally/example-chart.png
[microsoft historical price table]: run-gptstonks-preview-locally/example-command.png
[news nvidia]: run-gptstonks-preview-locally/news-nvidia.png
[set openbb pat]: run-gptstonks-preview-locally/set-openbb-pat.png
