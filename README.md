# Agentic AI Engineer with LangChain and LangGraph

Hands-on Python notebooks for learning conversational AI with LangChain and OpenAI, featuring few-shot prompting, chatbot personalities, and conversation history.

## Overview

This repository currently contains one chatbot exercise in two versions: a starter notebook with tasks to complete and a solution notebook with a working implementation. The example, **BEEP-42**, responds in the style of a playful sci-fi robot.

Although LangGraph is part of the repository name, the current exercise uses LangChain directly. No LangGraph workflow, tool-calling agent, or graph orchestration is implemented yet.

## What you will learn

- Connect a LangChain chat model to OpenAI.
- Define a chatbot personality through system instructions.
- Guide responses with few-shot input/output examples.
- Retain conversation history across calls on the same chatbot instance.
- Experiment with prompts, examples, and model temperature.

## Notebooks

| Notebook | Purpose |
| --- | --- |
| [Starter](L2_starter_exercise_01_chatbot_application.ipynb) | Configure the model, implement the conversation method, and add examples. |
| [Solution](L2_solution_exercise_01_chatbot_application.ipynb) | Explore the completed `ChatBot` class and ten BEEP-42 examples. |

## Quick start

Use Python 3.13 to match the notebooks' recorded Python 3.13.7 environment. You also need Git and an OpenAI API key with access to the configured model. Model calls use your API account and may incur charges.

From a macOS or Linux terminal with Python 3.13 installed:

```bash
git clone https://github.com/robertishimurasousa/Agentic-AI-Engineer-with-LangChain-and-LangGraph.git
cd Agentic-AI-Engineer-with-LangChain-and-LangGraph
python3.13 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m pip install jupyterlab ipykernel
cp .env.example .env
```

Edit `.env` and replace the placeholder:

```dotenv
OPENAI_API_KEY=your-openai-api-key
```

Start JupyterLab from the repository root:

```bash
python -m jupyterlab
```

Open the **solution notebook**, select the `.venv` Python environment, and run its cells in order. The supplied calls use `gpt-4o-mini` with `temperature=0.0`. The model name is configurable; access depends on your API account.

After creating `beep42`, try this in a new cell:

```python
response = beep42.invoke("My name is Alex.")
print(response.content)
print(beep42.invoke("What is my name?").content)
```

The second call includes the first exchange in its context. The exact wording of the reply can vary.

For Windows instructions, kernel setup, and environment checks, see [Getting started](docs/getting-started.md). Before running the starter notebook, follow the [exercise guide](docs/chatbot-exercise.md): its explicit API-key placeholder must be removed or replaced, and `invoke` is intentionally incomplete.

## Documentation

| Guide | Use it to |
| --- | --- |
| [Getting started](docs/getting-started.md) | Install dependencies, configure credentials, and launch a notebook. |
| [Chatbot exercise](docs/chatbot-exercise.md) | Complete the starter and customize BEEP-42. |
| [Technical reference](docs/reference.md) | Understand configuration, the `ChatBot` interface, and message flow. |
| [Troubleshooting](docs/troubleshooting.md) | Resolve setup, authentication, and notebook execution problems. |
| [Contributing](CONTRIBUTING.md) | Prepare focused changes and validate notebooks. |

## Repository structure

```text
.
├── README.md
├── CONTRIBUTING.md
├── .env.example
├── .gitignore
├── requirements.txt
├── L2_starter_exercise_01_chatbot_application.ipynb
├── L2_solution_exercise_01_chatbot_application.ipynb
└── docs/
    ├── getting-started.md
    ├── chatbot-exercise.md
    ├── reference.md
    └── troubleshooting.md
```

## Current limitations

The chatbot is a learning exercise executed inside a notebook. History lives in a Python list and is lost when the kernel restarts or the instance is recreated. Every call sends the full accumulated message list; there is no trimming, persistence, or retrieval layer. The project has no web interface, deployment configuration, or automated test suite.

Dependencies are currently unpinned, and the repository does not define a tested Python compatibility matrix. The recorded notebook environment is a starting point, not a reproducible environment lock.

## License

No `LICENSE` file is currently included in this repository.
