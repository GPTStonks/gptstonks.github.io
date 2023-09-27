<p align="center">
  <img src="./resources/logo-chatbot.png" alt="Logo">
</p>

A sleek and modern chatbot that helps retail investors access financial data to make better-informed decisions.

![](./resources/demo.gif)

## Description

GPTStonks Chatbot democratizes the access to financial data by providing a chat interface on top of [OpenBB](https://openbb.co/)'s
functionalities. Its main contributions are:

- **Made for everyone**: Using cutting-edge AI to understand and response your financial queries in natural language.
- **Modern design**: Leveraging web technologies for a modern and responsive design.
- **Customizable data**: Easy to tailor to fit the specific needs of any user to obtain the wanted
  data.
- **Real-time**: Swift real-time responses to ensure the retrieved data is up-to-date.

## Functionalities

The chatbot can currently perform two types of actions:

1. **General financial knowledge**: when asked about general financial questions, such as *What is a margin call?*,
   the chatbot generates a response based on the documents seen during its training.
2. **OpenBB functions**: when asked to retrieve specific financial information, OpenBB's SDK is used to provide accurate
   and updated answers.

The chatbot accuracy depends on the LLM used to generate the responses. All [Hugging Face](https://huggingface.co/) models are currently supported, and OpenAI's models support will be added soon. Also, the chatbot is intended for topics related to finance and investing, and GPTStonks and its members discourage its usage outside this scope.

## Installation

We are currently working on creating a [docker compose](https://docs.docker.com/compose/) and executables to distribute GPTStonks Chatbot. Stay tuned!

## Contributing

As we are open source, we welcome contributions from the community. Feel free to open issues and
submit some pull requests to our repositories.

## Disclaimer

GPTStonks Chatbot is meant to be an interface to get financial data and general knowledge. Therefore, it cannot provide financial or investment advise.
