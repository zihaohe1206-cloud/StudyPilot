# ADR-0003: Treat Documentation as Project Memory

Date: 2026-07-09

## Status

Accepted

## Context

The project may be developed across multiple AI windows and sessions. New windows often lack context, which can cause repeated explanation, inconsistent decisions, or accidental rework.

## Decision

Maintain a lightweight documentation system:

- `docs/project-memory.md` for current state.
- `docs/sessions/` for AI conversation summaries.
- `docs/devlog/` for daily engineering logs.
- `docs/decisions/` for architecture decisions.
- `docs/03-resume-points.md` and `docs/04-deep-dive-questions.md` for portfolio preparation.

## Consequences

Positive:

- New AI windows can continue quickly.
- Technical decisions become easier to defend.
- Resume writing becomes incremental.

Tradeoffs:

- Requires a few minutes of documentation after each session.
- Docs can become stale if not updated.

