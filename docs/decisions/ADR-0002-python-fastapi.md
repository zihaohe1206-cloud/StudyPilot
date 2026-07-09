# ADR-0002: Use Python and FastAPI for Backend

Date: 2026-07-09

## Status

Accepted

## Context

The project targets AI agent development rather than only traditional web backend development. The developer already knows JavaScript and Vue.

## Decision

Use Python and FastAPI as the primary backend stack.

## Rationale

- Python has strong support for LangGraph, RAG, evaluation, document processing, and AI application tooling.
- FastAPI is approachable for frontend developers because API contracts are explicit and development is fast.
- JavaScript skills remain useful for the Vue frontend and product experience.

## Consequences

Positive:

- Shorter path to agent and RAG implementation.
- Better alignment with AI application roles.

Tradeoffs:

- Need to learn Python backend conventions.
- Existing JavaScript backend knowledge will not transfer one-to-one.

