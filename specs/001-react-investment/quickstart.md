# Quickstart: AI Investment Portfolio Agent

This project implements a command-line AI Agent that generates investment portfolios based on the user's age, risk tolerance, term, and goals, using the ReAct (Reasoning and Acting) pattern.

## Prerequisites

1. Python 3.11 or higher.
2. `uv` or `pip` installed for dependency management.
3. Access to an LLM provider (Ollama for local execution or a valid OpenAI/Anthropic API key).

## Installation

```bash
# Clone the repository and navigate to the project directory
git clone <repository-url>
cd argentarius

# Create and activate a virtual environment via uv
uv venv
source .venv/bin/activate

# Install dependencies (LangChain, Pydantic, etc.)
uv pip install -r src/requirements.txt
```

## Running the Agent

1. Make sure your local LLM (e.g., Ollama `llama3.1`) is running. Alternatively, copy `.env.example` to `.env` and fill in your API key.
2. Start the CLI application:

```bash
python src/run.py
```

3. Follow the prompts! The bot will ask for your investment term, max drawdown %, age, and goal. It will then display its "Thoughts" before generating the final portfolio allocation.

## Development

- To run the validation unit tests for input constraints `pytest tests/unit/`
- To run integration tests mocking the ReAct loop `pytest tests/integration/`
