# Build and customize the chatbot

[Back to README](../README.md)

Complete [Getting started](getting-started.md), then open the [starter notebook](../L2_starter_exercise_01_chatbot_application.ipynb). Keep the [solution](../L2_solution_exercise_01_chatbot_application.ipynb) available for comparison.

## 1. Configure the model

The starter passes `api_key="YOUR_API_KEY_HERE"` directly to `ChatOpenAI`. That explicit value prevents the model from using the key you placed in `.env`.

Add this cell before constructing a chatbot:

```python
from dotenv import load_dotenv

load_dotenv()
```

Inside `ChatBot.__init__`, remove the `api_key` argument so the constructor becomes:

```python
self.llm = ChatOpenAI(
    model=model,
    temperature=temperature,
)
```

Rerun the class definition after editing it. Existing instances retain their previous configuration, so recreate `beep42` as well.

## 2. Complete the conversation method

The starter's `invoke` method is intentionally empty and returns `None`. Implement these steps:

1. Append a `HumanMessage` containing the user's text to `self.messages`.
2. Invoke `self.llm` with the full message list.
3. Append the returned assistant message to the list.
4. Return that assistant message.

Compare your implementation with the solution after trying it yourself.

## 3. Add few-shot examples

Each example is a dictionary with `input` and `output` keys:

```python
{
    "input": "Can you help me plan my day?",
    "output": "BEEP. PLANNING MODE ACTIVE. LIST YOUR THREE MAIN TASKS.",
}
```

Add examples to the `examples` list and recreate the chatbot. Aim for a consistent voice across greetings, questions, and requests for clarification. Examples guide the model; they do not guarantee an exact answer.

## 4. Check conversation history

After defining the class, instructions, and examples, create a fresh instance and run:

```python
beep42 = ChatBot(
    name="Beep 42",
    instructions=instructions,
    examples=examples,
)

initial_count = len(beep42.messages)
reply = beep42.invoke("My favorite planet is Saturn.")
assert isinstance(reply, AIMessage)
assert len(beep42.messages) == initial_count + 2
print(reply.content)
print(beep42.invoke("Which planet did I mention?").content)
```

This makes two API requests. Check that the second response refers to Saturn. Inspect `beep42.messages` to see the prompt examples and conversation turns. Avoid saving private conversation data in shared notebook outputs.

## 5. Change the personality

Create a separate chatbot using the same class:

```python
assistant = ChatBot(
    name="Study Assistant",
    instructions="You are a patient study assistant. Explain ideas with short examples.",
    examples=[
        {
            "input": "What is a Python list?",
            "output": "A list stores items in order. For example, colors = ['red', 'blue'].",
        }
    ],
    model="gpt-4o-mini",
    temperature=0.0,
)

print(assistant.invoke("What is a dictionary?").content)
```

The `name` field is stored as metadata; it is not automatically included in the prompt. Put the desired identity and behavior in `instructions` and the examples.

## 6. Reset and compare

Recreate the chatbot to reset its conversation while preserving the configured instructions and examples. Clearing `beep42.messages` directly would also remove the initial prompt messages.

For controlled experiments, create a fresh instance for each variation and change one thing at a time: the instructions, the examples, or the temperature supported by your selected model. Editing the standalone `llm` variable in the solution does not change `beep42.llm`.

## Completion checklist

- The starter reads the API key from the environment.
- `invoke` returns an `AIMessage` and stores both conversation turns.
- A follow-up question can use information from an earlier message.
- A new instance starts with examples and no previous user conversation.
- Your custom personality is reflected in the responses.

See the [technical reference](reference.md) for the exact message structure and implementation limitations.
