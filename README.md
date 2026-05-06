# Nurse Mate Smart Assistant

A prototype FastAPI backend for a nurse-facing clinical assistant integrating EMR/FHIR concepts, NLP intent routing, and task management.

## Project Overview

This repository contains a sample implementation of the `Nurse Mate` API, designed to simulate a nurse co-pilot that:

- routes natural language patient notes and requests through an NLP classifier
- exposes FHIR-style EMR endpoints for patient lookup
- simulates clinical note creation via `DocumentReference`
- supports quick task creation for nursing workflows

## Key Features

- `FastAPI` application with OpenAPI docs
- Mock FHIR `Patient` and `DocumentReference` models
- NLP intent classifier for: 
  - recording assessments
  - querying lab results
  - task creation
  - general communication
- In-memory task queue for demo purposes
- Automated test coverage with `pytest`

## Files of Note

- `main.py` — primary FastAPI application entrypoint
- `nurse_mate_api.py` — companion API implementation with same core endpoints
- `test_main.py` — test suite validating clinical and assistant workflows
- `git_setup.sh` — repository initialization script

## Requirements

- Python 3.11+ (or compatible)
- `fastapi`
- `uvicorn`
- `pydantic`
- `pytest`
- `httpx` / `fastapi.testclient` for tests

## Install

```bash
python -m pip install -r requirements.txt
```

> If `requirements.txt` is not present, install packages directly:

```bash
python -m pip install fastapi uvicorn pydantic pytest httpx
```

## Run the API

```bash
python main.py
```

The API will be available at:

- `http://localhost:8000`
- Swagger docs: `http://localhost:8000/docs`

## Example Endpoints

### Get patient record

```http
GET /api/v1/emr/Patient/123
```

### Process nurse assistant input

```http
POST /api/v1/assistant/process
Content-Type: application/json

{
  "sessionID": "sess-001",
  "userID": "nurse-01",
  "rawText": "Patient Jane Smith, vitals stable. Blood pressure 122 over 78."
}
```

### Create a task

```http
POST /api/v1/tasks
Content-Type: application/json

{
  "title": "Administer IV Fluids",
  "assignedTo": "nurse-02",
  "priority": 1
}
```

## Run Tests

```bash
pytest
```

## Notes

- This project is currently a prototype with in-memory mocks and no persistent storage.
- The FHIR contract is illustrative and not production-grade.
- Use `main.py` as the primary application entrypoint.
