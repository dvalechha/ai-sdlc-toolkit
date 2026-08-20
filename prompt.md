# Codex Prompt — Initialize `ai-sdlc-toolkit` Backend

You are helping build a new backend project called **`ai-sdlc-toolkit`**.

Repository:

`https://github.com/dvalechha/ai-sdlc-toolkit`

## Problem Statement

The goal of this project is to build a reusable **AI-assisted SDLC toolkit**.

The first capability will be **AI-assisted Jira story refinement**.

The initial workflow will eventually look like:

```text
Frontend
   |
   v
FastAPI Backend
   |
   v
Story Refinement Service
   |
   +--> Jira Provider
   |
   +--> LLM Provider
```

A user will eventually provide a Jira issue key such as:

```text
PAYMENTS-123
```

The backend will retrieve the Jira story, analyze it using an LLM, and return a structured refinement/readiness report containing items such as:

* ambiguities
* missing information
* blocking questions
* edge cases
* dependencies
* security/privacy considerations
* suggested acceptance criteria
* overall readiness assessment

Later, Jira Webhooks may also trigger the same refinement workflow automatically.

The project should therefore be designed as a broader **AI SDLC platform/toolkit**, not as a one-off Jira script.

---

## Architecture Direction

Use:

* Python
* FastAPI
* Pydantic
* Uvicorn
* pytest

Keep the architecture modular and easy to extend.

A reasonable initial structure would be:

```text
app/
├── main.py
├── api/
│   └── routes/
├── core/
│   └── config.py
├── models/
├── services/
├── providers/
│   ├── jira/
│   └── llm/
└── __init__.py

tests/
```

Do not overengineer the first iteration.

However, keep these future abstractions in mind:

```text
StoryProvider
    |
    +-- JiraProvider
    +-- Future alternative providers

LLMProvider
    |
    +-- OpenAIProvider
    +-- Future EnterpriseLLMGatewayProvider
```

The personal development version will initially use:

* Personal Jira
* OpenAI API

Later, the enterprise version may replace these with:

* Enterprise Jira / Jira MCP / Jira REST integration
* Internal enterprise LLM gateway

The core refinement logic should therefore not be tightly coupled to OpenAI or Jira-specific implementation details.

---

## Important Security / Repository Rules

This repository is intended to remain generic and potentially public.

Do not commit:

* API keys
* Jira tokens
* credentials
* secrets
* `.env` files
* enterprise-specific URLs
* proprietary company information

Provide a `.env.example` where appropriate.

Ensure `.env` and other local secret files are excluded via `.gitignore`.

---

# First Iteration Scope

For this first pass, do **not implement Jira integration or LLM logic yet**.

Only establish a clean backend foundation.

## Requirements

### 1. Initialize the FastAPI application

Create the minimum project structure necessary for a maintainable FastAPI backend.

### 2. Add a health-check endpoint

Implement:

```http
GET /health
```

It should return a simple structured response similar to:

```json
{
  "status": "ok",
  "service": "ai-sdlc-toolkit"
}
```

Use a Pydantic response model rather than returning an untyped dictionary if reasonable.

### 3. Add configuration structure

Create a lightweight configuration approach that can later support environment variables such as:

```text
OPENAI_API_KEY
JIRA_BASE_URL
JIRA_EMAIL
JIRA_API_TOKEN
```

Do not require these values for the application to start yet.

### 4. Add dependency management

Use a simple modern dependency setup.

Prefer `pyproject.toml` unless there is a strong reason not to.

Include the dependencies necessary for this initial version.

### 5. Add tests

Create at least one automated test for:

```http
GET /health
```

The test should verify:

* HTTP 200
* expected JSON response

### 6. Add developer documentation

Update/create `README.md` with concise instructions covering:

* project purpose
* prerequisites
* local setup
* installing dependencies
* starting FastAPI locally
* accessing Swagger/OpenAPI docs
* running tests

### 7. Validate locally

After implementation:

* install dependencies if needed
* run the tests
* start or otherwise validate the FastAPI application
* confirm `/health` works

---

# Engineering Expectations

Keep this first implementation intentionally small.

Prefer:

* clear naming
* separation of routes/configuration/models
* type hints
* simple code
* minimal dependencies

Avoid introducing things we do not need yet, including:

* database
* Docker
* authentication
* Jira SDK
* OpenAI SDK
* agent frameworks
* LangChain
* LangGraph
* queues
* caching
* persistence
* frontend code

Those will be introduced deliberately in later iterations.

---

# Expected Result

At the end of this task, the repository should contain a working FastAPI backend that can be run locally and exposes:

```text
GET /health
```

with automated tests passing.

Before finishing, provide me with:

1. A short summary of what you changed
2. The resulting project structure
3. Commands to run the server
4. Commands to run the tests
5. Confirmation of whether the health-check test passed
6. Any design decisions you made that may affect later Jira/LLM integration
