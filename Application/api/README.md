# API Endpoints

This directory contains the FastAPI application and endpoint implementations for the Test Environment Manager Agent.

## Endpoints

- Environment lifecycle management (create, update, delete, clone)
- Environment status and health monitoring
- Cost analysis and reporting
- Scheduling configuration

## Structure

```
api/
├── main.py              # FastAPI application entry point
├── routers/             # API route handlers
│   ├── environments.py  # Environment management endpoints
│   ├── health.py        # Health check endpoints
│   ├── costs.py         # Cost analysis endpoints
│   └── schedules.py     # Scheduling endpoints
├── models/              # Pydantic models for request/response
├── dependencies.py      # Shared dependencies and middleware
└── requirements.txt     # Python dependencies
```

## Usage

```bash
pip install -r requirements.txt
uvicorn main:app --reload
```
