# LLM HuggingFace API

## Introduction

This school project was conducted to learn about Huggingface's API and use Streamlit to deploy the python app [Available here](https://multimodal00llm.streamlit.app/)

It was also an opportunity to try a RAG approach. [This](https://arxiv.org/pdf/2502.15214) scientific paper was used as a source of precise knowledge, the LLM was then queried with added context obtained from the most simmilar embedding found in the collection of chuncks from the article.

Using Hugging Face's InferenceAPI was straightforward. First a user token was generated, then a model was chosen by [browsing the available ones.](https://huggingface.co/models?inference_provider=hf-inference&pipeline_tag=text-generation&sort=trending)
Then all that was needed was to build the *InferenceClient()* with the user token, and start querying!

## What does this code do?

1. Text analysis with *Mistral-7B-Instruct-v0.3*
2. PDF data retrival, embedding and indexing for RAG queries
3. Image description both locally (multimodal/src/local_blip.py) and through api calls, using *blip-image-captioning-base*, further summarized using *Mistral-7B-Instruct-v0.3*

## Get Started

1. clone the code
> git clone git@github.com:ewkt/llm_hf_api.git \
> cd llm_hf_api

1. create a venv to install requirments into
> python -m venv venv \
> venv\Scripts\activate *(or source venv/bin/activate) in unix* \
> pip install -e .

2. set huggigng face token in .env
> HF_TOKEN=xxxxxxxxxxxxxxxx

3. you can run the scripts to look at th generated results:

> python -m multimodal.src.api_call \
> python -m multimodal.src.local_blip

4. you can also run the streamlit app and see the results in your browser on localhost:

> streamlit run multimodal\app.py
--------

## How to deploy streamlit app?

### Option 1: on your personal hardware

First, get a remote machine to run your code. This could be a VPS with lunix installed for example. Then, connect to it through ssh and setup your github ssh keys. Make sure you have python and pip installed:
> sudo apt update \
> sudo apt install python3 python3-pip python3-venv \
Now you can follow the **Get Started** tutorial. Once you have executed the streamlit command, copy the 'Network URL' and try out your streamlit app from your local network!

And voilà! you have yourself an easy multimodal llm api interface!

Advanced steps would include getting a domain name and having streamlit deploy to that url

### Option 2: using streamlit community cloud

When your app is running, click the **Deploy** button and follow the instructions to connect your streamlit account to your github account. 
1. Choose the repo where this code is (after having forked this repo).
2. change the file path to "multimodal/app.py"
3. Click on advanced settings, select python version 3.10, and paste the following secret (because your .env isn't on your repo):
> HF_TOKEN = "your_actual_huggingface_token_here"

Click deploy, and magic! your app gets set-up and opens on your browser.
