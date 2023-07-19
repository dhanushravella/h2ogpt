# h2oGPT

Turn ★ into ⭐ (top-right corner) if you like the project!

Query and summarize your documents or just chat with local private GPT LLMs using h2oGPT, an Apache V2 open-source project.

- **Private** offline database of any documents [(PDFs, Excel, Word, Images, Code, Text, MarkDown, etc.)](docs/README_LangChain.md#supported-datatypes)
- **Persistent** database (Chroma, Weaviate, or in-memory FAISS) using accurate embeddings (instructor-large, all-MiniLM-L6-v2, etc.)
- **Efficient** use of context using instruct-tuned LLMs (no need for LangChain's few-shot approach)
- **Upload** and **View** documents via UI (control multiple collaborative or scratch collections)
- **UI** or CLI with streaming of all models
- **Bake-off** UI mode against many models at same time
- **Variety** of models supported (Falcon, Vicuna, WizardLM including AutoGPTQ, 4-bit/8-bit, LORA)
- **GPU** support from HF models, and **CPU** support using LLaMa cpp and GPT4ALL
- **Linux, Docker, MAC, and Windows** support
- **Inference Servers** support (HF TGI server, vLLM, Gradio, OpenAI)
- **OpenAI-compliant Python client API** for client-server control
- **Evaluate** performance using reward models

### Live Demos
- [![img-small.png](docs/img-small.png) Live h2oGPT Document Q/A Demo](https://gpt.h2o.ai/)
- [🤗 Live h2oGPT Chat Demo 1](https://huggingface.co/spaces/h2oai/h2ogpt-chatbot)
- [🤗 Live h2oGPT Chat Demo 2](https://huggingface.co/spaces/h2oai/h2ogpt-chatbot2)
- [![](https://colab.research.google.com/assets/colab-badge.svg) h2oGPT CPU](https://colab.research.google.com/drive/13RiBdAFZ6xqDwDKfW6BG_-tXfXiqPNQe?usp=sharing)
- [![](https://colab.research.google.com/assets/colab-badge.svg) h2oGPT GPU](https://colab.research.google.com/drive/143-KFHs2iCqXTQLI2pFCDiR69z0dR8iE?usp=sharing)

### Resources:
- [Discord](https://discord.gg/WKhYMWcVbq)
- [Apache V2 models (Falcon 40, etc.) at 🤗](https://huggingface.co/h2oai/)
- [YouTube: 100% Offline ChatGPT Alternative?](https://www.youtube.com/watch?v=Coj72EzmX20)
- [YouTube: Ultimate Open-Source LLM Showdown (6 Models Tested) - Surprising Results!](https://www.youtube.com/watch?v=FTm5C_vV_EY)
- [YouTube: Blazing Fast Falcon 40b 🚀 Uncensored, Open-Source, Fully Hosted, Chat With Your Docs](https://www.youtube.com/watch?v=H8Dx-iUY49s)
- [Technical Paper: https://arxiv.org/pdf/2306.08161.pdf](https://arxiv.org/pdf/2306.08161.pdf)

### Video Demo:

https://github.com/h2oai/h2ogpt/assets/2249614/2f805035-2c85-42fb-807f-fd0bca79abc6

YouTube 4K version: https://www.youtube.com/watch?v=_iktbj4obAI

### Guide:
<!--  cat README.md | ./gh-md-toc  -  But Help is heavily processed -->
* [Supported OS and Hardware](#supported-os-and-hardware)
* [Compare to PrivateGPT et al.](docs/README_LangChain.md#what-is-h2ogpts-langchain-integration-like)
* [Roadmap](#roadmap)
* [Getting Started](#getting-started)
   * [TLDR Install & Run](#tldr)
   * [GPU (CUDA)](docs/README_GPU.md)
   * [CPU](docs/README_CPU.md)
   * [MACOS](docs/README_MACOS.md)
   * [Windows 10/11](docs/README_WINDOWS.md)
   * [CLI chat](docs/README_CLI.md)
   * [Gradio UI](docs/README_ui.md)
   * [Client API](docs/README_CLIENT.md)
   * [Inference Servers](docs/README_InferenceServers.md)
   * [Python Wheel](docs/README_WHEEL.md)
   * [Offline Mode](docs/README_offline.md)
* [Development](#development)
* [Help](#help)
   * [LangChain file types supported](docs/README_LangChain.md#supported-datatypes)
   * [CLI Database control](docs/README_LangChain.md#database-creation)
   * [Why h2oGPT for Doc Q&A](docs/README_LangChain.md#what-is-h2ogpts-langchain-integration-like)
   * [FAQ](docs/FAQ.md)
   * [Useful Links](docs/LINKS.md)
   * [Fine-Tuning](docs/FINETUNE.md)
   * [Docker](docs/INSTALL-DOCKER.md)
   * [Triton](docs/TRITON.md)
* [Acknowledgements](#acknowledgements)
* [Why H2O.ai?](#why-h2oai)
* [Disclaimer](#disclaimer)

### Supported OS and Hardware

[![GitHub license](https://img.shields.io/github/license/NVIDIA/nvidia-docker?style=flat-square)](https://raw.githubusercontent.com/h2oai/h2ogpt/main/LICENSE)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![macOS](https://img.shields.io/badge/mac%20os-000000?style=for-the-badge&logo=macos&logoColor=F0F0F0)
![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)

**GPU** mode requires CUDA support via torch and transformers.  A 6.9B (or 12GB) model in 8-bit uses 8GB (or 13GB) of GPU memory. 8-bit precision, 4-bit precision, and AutoGPTQ can further reduce memory requirements down no more than about 6.5GB when asking a question about your documents (see [low-memory mode](docs/FAQ.md#low-memory-mode)).

**CPU** mode uses GPT4ALL and LLaMa.cpp, e.g. gpt4all-j, requiring about 14GB of system RAM in typical use.

GPU and CPU mode tested on variety of NVIDIA GPUs in Ubuntu 18-22, but any modern Linux variant should work.  MACOS support tested on Macbook Pro running Monterey v12.3.1 using CPU mode, as well as MAC M1 using MPS.

### Roadmap

- Integration of code and resulting LLMs with downstream applications and low/no-code platforms
- Complement h2oGPT chatbot with search and other APIs
- High-performance distributed training of larger models on trillion tokens
- Enhance the model's code completion, reasoning, and mathematical capabilities, ensure factual correctness, minimize hallucinations, and avoid repetitive output
- Add other tools like search
- Add agents for SQL and CSV question/answer

## Getting Started

First one needs a Python 3.10 environment.  For help installing a Python 3.10 environment, see [Install Python 3.10 Environment](docs/INSTALL.md#install-python-environment).  On newer Ubuntu systems and environment may be installed by just doing:
```bash
sudo apt-get install -y build-essential gcc python3.10-dev
virtualenv -p python3 h2ogpt
source h2ogpt/bin/activate
```
or use conda:
```bash
conda create -n h2ogpt -y
conda activate h2ogpt
conda install python=3.10 -c conda-forge -y
```
Check your installation by doing:
```bash
python --version # should say 3.10.xx
pip --version  # should say pip 23.x.y ... (python 3.10)
```
On some systems, `pip` still refers back to the system one, then one can use `python -m pip` or `pip3` instead of `pip` or try `python3` instead of `python`.

### TLDR

For [MACOS](docs/README_MACOS.md#macos) and [Windows 10/11](docs/README_WINDOWS.md) please follow their instructions.

On Ubuntu, after Python 3.10 environment installed do:
```bash
git clone https://github.com/h2oai/h2ogpt.git
cd h2ogpt
# fix any bad env
pip uninstall -y pandoc pypandoc pypandoc-binary
# broad support, but no training-time or data creation dependencies

# CPU only:
pip install -r requirements.txt --extra-index https://download.pytorch.org/whl/cpu

# GPU only:
pip install -r requirements.txt --extra-index https://download.pytorch.org/whl/cu118
```
Then run:
```bash
# Required for Doc Q/A: LangChain:
pip install -r reqs_optional/requirements_optional_langchain.txt
# Required for CPU: LLaMa/GPT4All:
pip install -r reqs_optional/requirements_optional_gpt4all.txt
# Optional: PyMuPDF/ArXiv:
pip install -r reqs_optional/requirements_optional_langchain.gpllike.txt
# Optional: Selenium/PlayWright:
pip install -r reqs_optional/requirements_optional_langchain.urls.txt
# Optional: support docx, pptx, ArXiv, etc. required by some python packages
sudo apt-get install -y libmagic-dev poppler-utils tesseract-ocr libreoffice
# Optional: for supporting unstructured package
python -m nltk.downloader all
# Optional: For AutoGPTQ support on x86_64 linux
pip uninstall -y auto-gptq ; CUDA_HOME=/usr/local/cuda-11.8  GITHUB_ACTIONS=true pip install auto-gptq --no-cache-dir
```
See [AutoGPTQ](docs/README_GPU.md#gpu-cuda) for more details for AutoGPTQ and other GPU installation aspects.

Place all documents in `user_path` or upload in UI ([Help with UI](docs/README_ui.md)).

UI using GPU with at least 24GB with streaming:
```bash
python generate.py --base_model=h2oai/h2ogpt-oasst1-512-12b --load_8bit=True  --score_model=None --langchain_mode='UserData' --user_path=user_path
```
UI using LLaMa.cpp model:
```bash
wget https://huggingface.co/TheBloke/WizardLM-7B-uncensored-GGML/resolve/main/WizardLM-7B-uncensored.ggmlv3.q8_0.bin
python generate.py --base_model='llama' --prompt_type=wizard2 --score_model=None --langchain_mode='UserData' --user_path=user_path
```
which works on CPU or GPU (assuming llama cpp python package compiled against CUDA or Metal).

If using OpenAI for the LLM is ok, but you want documents to be parsed and embedded locally, then do:
```bash
python generate.py  --inference_server=openai_chat --base_model=gpt-3.5-turbo --score_model=None
```
and perhaps you want better image caption performance and focus local GPU on that, then do:
```bash
python generate.py  --inference_server=openai_chat --base_model=gpt-3.5-turbo --score_model=None --captions_model=Salesforce/blip2-flan-t5-xl
```

Add `--share=True` to make gradio server visible via sharable URL.  If you see an error about protobuf, try:
```bash
pip install protobuf==3.20.0
```

Once all files are downloaded, the CLI and UI can be run in offline mode, see [offline mode](docs/README_offline.md).

### Run h2oGPT using Docker
1. Make sure Docker & Nvidia Containers are setup correctly by following instructions [here](docs/INSTALL-DOCKER.md).

2. Specify the required model using `HF_MODEL` parameter.
All open-source models are posted on [🤗 H2O.ai's Hugging Face page](https://huggingface.co/h2oai/).
```bash
docker run \
    --runtime=nvidia --shm-size=64g \
    -e HF_MODEL=h2oai/h2ogpt-gm-oasst1-en-2048-open-llama-7b \
    -p 8888:8888 -p 7860:7860 \
    --rm --init \
    -v `pwd`/h2ogpt_env:/h2ogpt_env \
    gcr.io/vorvan/h2oai/h2ogpt-runtime:61d6aea6fff3b1190aa42eee7fa10d6c
```
3. Navigate to http://localhost:7860/  & start using h2oGPT.

To run h2oGPT with custom entrypoint, refer [here](docs/INSTALL-DOCKER.md).

### Development

- To create a development environment for training and generation, follow the [installation instructions](docs/INSTALL.md).
- To fine-tune any LLM models on your data, follow the [fine-tuning instructions](docs/FINETUNE.md).
- To create a container for deployment, follow the [Docker instructions](docs/INSTALL-DOCKER.md).
- To run h2oGPT tests, run `pip install requirements-parser ; pytest -s -v tests client/tests`

### Help

- For advanced fine-tuning, also check out [H2O LLM Studio](https://github.com/h2oai/h2o-llmstudio)

- Flash attention support, see [Flash Attention](docs/INSTALL.md#flash-attention)

- [Docker](docs/INSTALL-DOCKER.md#containerized-installation-for-inference-on-linux-gpu-servers) for inference

- [FAQs](docs/FAQ.md)

- [README for LangChain](docs/README_LangChain.md)

- More [Links](docs/LINKS.md), context, competitors, models, datasets

### Acknowledgements

* Some training code was based upon March 24 version of [Alpaca-LoRA](https://github.com/tloen/alpaca-lora/).
* Used high-quality created data by [OpenAssistant](https://open-assistant.io/).
* Used base models by [EleutherAI](https://www.eleuther.ai/).
* Used OIG data created by [LAION](https://laion.ai/blog/oig-dataset/).

### Why H2O.ai?

Our [Makers](https://h2o.ai/company/team/) at [H2O.ai](https://h2o.ai) have built several world-class Machine Learning, Deep Learning and AI platforms:
- #1 open-source machine learning platform for the enterprise [H2O-3](https://github.com/h2oai/h2o-3)
- The world's best AutoML (Automatic Machine Learning) with [H2O Driverless AI](https://h2o.ai/platform/ai-cloud/make/h2o-driverless-ai/)
- No-Code Deep Learning with [H2O Hydrogen Torch](https://h2o.ai/platform/ai-cloud/make/hydrogen-torch/)
- Document Processing with Deep Learning in [Document AI](https://h2o.ai/platform/ai-cloud/make/document-ai/)

We also built platforms for deployment and monitoring, and for data wrangling and governance:
- [H2O MLOps](https://h2o.ai/platform/ai-cloud/operate/h2o-mlops/) to deploy and monitor models at scale
- [H2O Feature Store](https://h2o.ai/platform/ai-cloud/make/feature-store/) in collaboration with AT&T
- Open-source Low-Code AI App Development Frameworks [Wave](https://wave.h2o.ai/) and [Nitro](https://nitro.h2o.ai/)
- Open-source Python [datatable](https://github.com/h2oai/datatable/) (the engine for H2O Driverless AI feature engineering)

Many of our customers are creating models and deploying them enterprise-wide and at scale in the [H2O AI Cloud](https://h2o.ai/platform/ai-cloud/):
- Multi-Cloud or on Premises
- [Managed Cloud (SaaS)](https://h2o.ai/platform/ai-cloud/managed)
- [Hybrid Cloud](https://h2o.ai/platform/ai-cloud/hybrid)
- [AI Appstore](https://docs.h2o.ai/h2o-ai-cloud/)

We are proud to have over 25 (of the world's 280) [Kaggle Grandmasters](https://h2o.ai/company/team/kaggle-grandmasters/) call H2O home, including three Kaggle Grandmasters who have made it to world #1.

### Disclaimer

Please read this disclaimer carefully before using the large language model provided in this repository. Your use of the model signifies your agreement to the following terms and conditions.

- Biases and Offensiveness: The large language model is trained on a diverse range of internet text data, which may contain biased, racist, offensive, or otherwise inappropriate content. By using this model, you acknowledge and accept that the generated content may sometimes exhibit biases or produce content that is offensive or inappropriate. The developers of this repository do not endorse, support, or promote any such content or viewpoints.
- Limitations: The large language model is an AI-based tool and not a human. It may produce incorrect, nonsensical, or irrelevant responses. It is the user's responsibility to critically evaluate the generated content and use it at their discretion.
- Use at Your Own Risk: Users of this large language model must assume full responsibility for any consequences that may arise from their use of the tool. The developers and contributors of this repository shall not be held liable for any damages, losses, or harm resulting from the use or misuse of the provided model.
- Ethical Considerations: Users are encouraged to use the large language model responsibly and ethically. By using this model, you agree not to use it for purposes that promote hate speech, discrimination, harassment, or any form of illegal or harmful activities.
- Reporting Issues: If you encounter any biased, offensive, or otherwise inappropriate content generated by the large language model, please report it to the repository maintainers through the provided channels. Your feedback will help improve the model and mitigate potential issues.
- Changes to this Disclaimer: The developers of this repository reserve the right to modify or update this disclaimer at any time without prior notice. It is the user's responsibility to periodically review the disclaimer to stay informed about any changes.

By using the large language model provided in this repository, you agree to accept and comply with the terms and conditions outlined in this disclaimer. If you do not agree with any part of this disclaimer, you should refrain from using the model and any content generated by it.

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=h2oai/h2ogpt&type=Timeline)](https://star-history.com/#h2oai/h2ogpt&Timeline)
