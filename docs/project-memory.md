# Project Memory

This file is the short, durable memory for new AI windows and future development sessions. Keep it concise and update it after every meaningful session.

## Project

StudyPilot: a personal learning assistant built as a portfolio project for backend plus AI agent development.

## Goal

Build an end-to-end AI learning system that shows practical backend engineering, RAG, multi-agent orchestration, evaluation, and product thinking.

The project should be strong enough to support resume bullets and technical interview deep dives.

## Chosen Route

Route B: build the project directly and learn missing backend/AI knowledge as each feature requires it.

## Planned Stack

- Vue 3 + TypeScript for frontend
- FastAPI for backend
- PostgreSQL for core data
- Redis for async jobs and caching
- pgvector or Qdrant for vector search
- LangGraph for multi-agent orchestration
- Docker Compose for local startup

## Key Decisions

- Use Python/FastAPI instead of Node as the primary backend path because Python has stronger AI agent, RAG, and evaluation ecosystem support.
- Build a real project from week one instead of completing a full backend course first.
- Keep documentation as a first-class part of the project so a new AI window can understand context quickly.
- Treat multi-agent design as a controlled workflow problem, not as a reason to call many agents for every request.

## Current Progress

- Project folder created at `C:\Users\18316\Desktop\StudyPilot`.
- Documentation structure created.
- Initial design spec, project memory, resume points, deep-dive questions, and ADRs are being written.
- No application code has been created yet.

## Next Actions

1. Review `docs/superpowers/specs/2026-07-09-studypilot-design.md`.
2. Confirm whether to start implementation planning.
3. If approved, create an implementation plan for Phase 0 and Phase 1.
4. Scaffold the monorepo with `apps/web` and `apps/api`.

## Open Questions

- Use pgvector inside PostgreSQL first, or start with Qdrant?
- Use RQ or Celery for background jobs?
- Which LLM provider should be used for the first working version?
- Should deployment target be local-only first, or a small cloud server later?

## Latest Session Summary

2026-07-09: Confirmed Route B and created the initial project documentation plan.

