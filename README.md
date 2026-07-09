# StudyPilot

StudyPilot is a learning project for moving from frontend development to backend plus AI agent development.

The product goal is a personal learning assistant that can ingest study materials, answer questions with citations, generate study plans, create quizzes, grade answers, and schedule review through a multi-agent workflow.

## Current Status

Planning and documentation stage. No application code has been written yet.

Start here when opening this project in a new AI window:

1. Read `docs/project-memory.md`.
2. Read the latest file in `docs/sessions/`.
3. Read `docs/superpowers/specs/2026-07-09-studypilot-design.md`.
4. Continue from the "Next Actions" section in `docs/project-memory.md`.

## Planned Stack

- Frontend: Vue 3, TypeScript, Pinia, Vue Router
- Backend: Python, FastAPI
- Database: PostgreSQL
- Async/cache: Redis plus RQ or Celery
- RAG: pgvector or Qdrant
- Agent orchestration: LangGraph
- Deployment: Docker Compose
- Testing: pytest, focused frontend tests

## Documentation Rules

Every meaningful development session should update:

- `docs/project-memory.md`
- `docs/devlog/YYYY-MM-DD.md`
- `docs/sessions/YYYY-MM-DD-HHMM.md`
- `docs/03-resume-points.md`
- `docs/04-deep-dive-questions.md`

