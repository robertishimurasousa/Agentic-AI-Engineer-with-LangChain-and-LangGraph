# Troubleshooting

[Back to README](../README.md)

## Python 3.13 is not found

The setup commands assume Python 3.13 is already installed. Install that interpreter, or select an existing compatible interpreter and adjust the environment-creation command. The notebooks record Python 3.13.7; other versions are not validated by this repository.

## `ModuleNotFoundError`

Check the active notebook interpreter:

```python
import sys
print(sys.executable)
```

Select the repository's `.venv` environment. In a terminal using that environment, run:

```bash
python -m pip install -r requirements.txt
python -m pip install jupyterlab ipykernel
python -m pip check
```

Restart the kernel after installing packages. If the environment is missing from the kernel picker, follow [kernel registration](getting-started.md#4-select-the-notebook-kernel).

## Missing or invalid API key

Confirm that `.env` exists in the repository root and that its placeholder has been replaced. Run this diagnostic without printing the credential:

```python
import os
from pathlib import Path
from dotenv import load_dotenv

print("Working directory:", Path.cwd())
print("Local .env exists:", Path(".env").is_file())
load_dotenv()
key = os.getenv("OPENAI_API_KEY")
print("Key configured:", bool(key) and key not in {"YOUR_API_KEY_HERE", "your-openai-api-key"})
```

A configured value does not prove the credential is valid. Check the key's status in your API account if authentication still fails.

In the starter, remove `api_key="YOUR_API_KEY_HERE"` from `ChatOpenAI` and load `.env` before constructing the chatbot. See the [exercise guide](chatbot-exercise.md#1-configure-the-model).

`load_dotenv()` does not overwrite an existing environment variable by default. If you changed `.env` after the key was loaded, restart the kernel. If the kernel inherits an old key from the shell that launched Jupyter, correct that shell variable and relaunch Jupyter.

## Model access, quota, or rate-limit errors

Read the error returned by the API. Confirm that the configured model is accessible to your account and that the project has available usage quota. For a temporary rate limit, wait before retrying rather than repeatedly running all cells.

To change the model, pass `model="your-accessible-model-id"` when constructing `ChatBot`. Updating only the standalone `llm` variable in the solution does not update the chatbot's own model client.

## `invoke` returns `None`

The starter's method is intentionally unfinished. Implement message storage, the model call, and the return value, then rerun the class-definition and chatbot-construction cells.

## `NameError` or changes are not reflected

Run cells in order: imports, environment setup, class definition, instructions, examples, instance creation, then model calls. After editing the class or examples, create a new instance. Restarting the kernel clears stale definitions, but also clears conversation history.

## The chatbot forgets earlier messages

Use the same `ChatBot` instance across turns. Rerunning the `beep42 = ChatBot(...)` cell starts a new conversation. Saved notebook outputs do not restore the previous Python object or its history.

## A failed request leaves duplicate user turns

The solution appends the user message before requesting a reply and does not roll it back on failure. A repeated call adds another copy. For this exercise, recreate the chatbot to start clean; this also discards previous live turns. See [state and failure behavior](reference.md#state-and-failure-behavior).

## Replies do not follow the expected personality

Check that the example list is nonempty, the instructions describe the desired behavior, and the examples use a consistent voice. Recreate the chatbot after editing them. The `name` parameter alone does not set the personality, and generated replies need not match saved notebook output exactly.

## A long conversation exceeds the context limit

The implementation sends all examples and accumulated messages on every request. Create a fresh instance for a shorter conversation. History trimming or summarization would require extending the exercise.
