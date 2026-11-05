# Contributing

Thanks for helping improve these learning exercises. Keep documentation, notebook explanations, and new code comments in English.

## Local setup

Follow [Getting started](docs/getting-started.md). Work on a branch and keep each change focused on one exercise, correction, or documentation improvement.

## Notebook changes

- Keep the starter and solution aligned on the same learning objective.
- Preserve intentional starter TODOs unless the exercise itself is changing.
- Use environment variables for credentials; never insert real keys into notebook cells or outputs.
- Avoid unrelated changes to execution counts, notebook metadata, or generated output.
- Review saved outputs for credentials and private conversation data before committing.
- Update the README and relevant guides when setup, dependencies, or behavior changes.

## Validation

There is currently no automated test suite. For implementation changes, use a fresh kernel and run the solution from top to bottom with your own API credentials. This makes live requests and may incur charges.

Check that a successful call returns an `AIMessage`, adds two messages to history, and allows a subsequent turn to refer to earlier input. Confirm that a newly created instance starts a fresh conversation. Do not compare exact generated wording.

For documentation-only changes, check relative links, referenced filenames, command accuracy, and Markdown formatting. Live model calls are not required to validate prose changes.

Before submitting:

```bash
git diff --check
git diff --stat
git status --short
```

Inspect the full diff as well, including notebook outputs. Ensure `.env` and `.venv` are not staged.

## Pull requests and issue reports

Explain the problem, the resulting behavior, and how you validated the change. State whether validation included live API calls or only local checks.

For a bug report, include the notebook name, failing cell, Python and dependency versions, and a redacted error message. Do not include your API key or private prompt data.
