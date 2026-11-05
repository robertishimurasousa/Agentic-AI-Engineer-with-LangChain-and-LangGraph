# Getting started

[Back to README](../README.md)

This guide prepares a local environment for the completed chatbot notebook.

## Prerequisites

- Git.
- Python 3.13 with `pip` and `venv`, matching the notebooks' recorded Python 3.13.7 environment. Other versions have not been validated by this repository.
- An OpenAI API key with access to the model configured in the notebook.
- Network access for dependency installation and model requests.

## 1. Clone the repository

```bash
git clone https://github.com/robertishimurasousa/Agentic-AI-Engineer-with-LangChain-and-LangGraph.git
cd Agentic-AI-Engineer-with-LangChain-and-LangGraph
```

## 2. Create an isolated Python environment

On macOS or Linux:

```bash
python3.13 -m venv .venv
source .venv/bin/activate
```

On Windows PowerShell:

```powershell
py -3.13 -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, use `.\.venv\Scripts\python.exe` instead of `python` in the remaining Python commands; activation is not required when using the interpreter directly.

Install the project dependencies and notebook tools:

```bash
python -m pip install -r requirements.txt
python -m pip install jupyterlab ipykernel
```

`requirements.txt` lists the chatbot libraries. JupyterLab and IPython kernel support are installed separately for running the notebooks. The JupyterLab installation command follows the [official Jupyter installation guide](https://jupyter.org/install).

## 3. Configure the API key

On macOS or Linux:

```bash
cp .env.example .env
```

On Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Open `.env` in an editor and replace `YOUR_API_KEY_HERE` with your API key. Keep the variable name `OPENAI_API_KEY` unchanged. The file should contain one assignment:

```dotenv
OPENAI_API_KEY=your-openai-api-key
```

The solution calls `load_dotenv()` before creating the model. `ChatOpenAI` reads `OPENAI_API_KEY` from the environment when an explicit key is not supplied; see the [LangChain OpenAI integration reference](https://reference.langchain.com/python/langchain-openai/langchain_openai). `.env` is already ignored by Git. Keep real keys out of notebook cells and saved outputs.

## 4. Select the notebook kernel

Register a recognizable kernel from the activated environment:

```bash
python -m ipykernel install --user --name agentic-ai-engineer --display-name "Python (Agentic AI Engineer)"
python -m jupyterlab
```

Select **Python (Agentic AI Engineer)** when opening a notebook. In VS Code, open the repository folder and select the `.venv` interpreter using the notebook kernel picker instead.

To verify the interpreter and imports without making an API request, run this in a notebook cell:

```python
import sys
from langchain_openai import ChatOpenAI
from langchain_core.messages import HumanMessage, AIMessage
from dotenv import load_dotenv

print(sys.executable)
```

The interpreter path should point to this repository's `.venv` directory.

## 5. Run the solution

Open [the solution notebook](../L2_solution_exercise_01_chatbot_application.ipynb) and execute cells from top to bottom. The class definition and chatbot construction prepare the conversation; each `beep42.invoke(...)` cell makes a model request.

The solution contains four sample calls. Running all cells executes those calls again, even if the notebook already displays saved output. Responses should follow the BEEP-42 personality, but exact text is not an acceptance criterion.

To start the exercise yourself, continue with the [chatbot exercise guide](chatbot-exercise.md).

## Verify your setup

- Imports complete without errors.
- The selected interpreter belongs to `.venv`.
- The solution creates `beep42` and a call returns an `AIMessage`.
- `response.content` contains the assistant's reply.
- A successful call adds two entries to `beep42.messages`.

If a step fails, use [Troubleshooting](troubleshooting.md).
