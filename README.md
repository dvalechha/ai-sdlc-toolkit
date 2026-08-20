# AI SDLC Toolkit

A reusable backend for AI-assisted software delivery workflows. The first planned
capability is Jira story refinement; this initial version establishes the FastAPI
foundation and a health-check endpoint only.

## Prerequisites

- Python 3.11 or newer

## Local setup

Create and activate a virtual environment, then install the project with its test
dependencies:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -e '.[test]'
```

Copy the example environment file if you want to prepare local integration
settings. None of these values are required in the initial version:

```bash
cp .env.example .env
```

## Run the API

```bash
uvicorn app.main:app --reload
```

The API is available at <http://127.0.0.1:8000>. Interactive Swagger UI is at
<http://127.0.0.1:8000/docs>, and the OpenAPI schema is at
<http://127.0.0.1:8000/openapi.json>.

Check service health with:

```bash
curl http://127.0.0.1:8000/health
```

## Run tests

```bash
pytest
```

Jira and LLM integrations are intentionally not implemented yet. Configuration
placeholders are optional so the application can run without credentials.
