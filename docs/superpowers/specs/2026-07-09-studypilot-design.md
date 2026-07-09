# StudyPilot Design Spec

Date: 2026-07-09

## 1. Purpose

StudyPilot is a portfolio-grade learning assistant project designed for a frontend developer who wants to grow into backend plus AI agent development.

The project should teach backend engineering through practice while producing resume-ready evidence: a working system, clear architecture, documented decisions, RAG evaluation, multi-agent orchestration, and interview-ready deep dives.

## 2. Success Criteria

The project is successful when it can demonstrate:

- User authentication and study material management.
- Document ingestion, parsing, chunking, embedding, and retrieval.
- RAG answers with citation traces and refusal behavior when evidence is missing.
- Study plan generation based on user goals and uploaded materials.
- Quiz generation, grading, wrong-answer tracking, and review suggestions.
- Multi-agent workflow implemented with explicit routing, state, fallback, and structured outputs.
- Docker-based local startup.
- Documentation that lets a new AI window or developer understand the project quickly.
- Resume bullets backed by real implementation details.

## 3. Non-Goals

The first version will not focus on:

- Training or fine-tuning base models.
- Full enterprise permissions or billing.
- Complex social features.
- Overly broad LMS functionality.
- Fully autonomous agents that make uncontrolled tool calls.

## 4. Product Scope

StudyPilot helps a user learn from their own materials.

Core user flow:

1. User signs in.
2. User uploads PDFs, Markdown notes, or copied article text.
3. Backend parses and chunks the material.
4. System creates embeddings and stores searchable chunks.
5. User asks questions about the material.
6. System retrieves relevant chunks and answers with citations.
7. User asks for a study plan.
8. Planner creates a plan from the material and target.
9. User takes generated quizzes.
10. System grades answers, records weak points, and suggests review tasks.

## 5. Architecture

Planned repository structure:

```text
StudyPilot/
  apps/
    web/
    api/
  docs/
    superpowers/specs/
    devlog/
    sessions/
    decisions/
    api/
    evals/
  docker-compose.yml
  README.md
```

Runtime components:

```text
Vue Web App
  -> FastAPI API
    -> PostgreSQL
    -> Redis job queue/cache
    -> Vector store
    -> LLM provider
```

FastAPI owns product APIs, authentication, document metadata, study plans, quiz records, and agent endpoints.

Background jobs handle expensive tasks such as document parsing, chunking, embedding, and re-indexing.

The agent layer should be called by backend services, not directly by the frontend.

## 6. Data Model Draft

Initial entities:

- User: account, profile, authentication metadata.
- StudyMaterial: uploaded file or text source.
- DocumentChunk: chunk text, source position, embedding reference, metadata.
- Conversation: user dialogue sessions.
- Message: user and assistant messages.
- StudyPlan: generated plan with milestones and tasks.
- Quiz: generated quiz linked to material and knowledge points.
- QuizAttempt: user answers and grading result.
- WeakPoint: tracked topic weakness based on quiz and review history.
- AgentRun: trace of a workflow run, inputs, outputs, node sequence, errors, and cost metadata.

## 7. RAG Design

RAG pipeline:

1. Parse source material.
2. Normalize text.
3. Split into chunks.
4. Store chunks with source metadata.
5. Create embeddings.
6. Retrieve top relevant chunks for a question.
7. Rerank or filter when needed.
8. Build answer context.
9. Generate answer with citations.
10. Refuse or ask for clarification when evidence is insufficient.

Important design points:

- Every chunk should retain material id, title, page/section if available, and character offsets when practical.
- Answers should cite chunk ids or source locations.
- Retrieval parameters such as chunk size, overlap, and top_k should be documented and revisited using evaluation results.
- RAG should prefer saying "not found in the provided material" over making unsupported claims.

## 8. Agent Design

Agents are specialized workflow nodes, not independent personalities.

Planned nodes:

- Router: classifies user intent and selects a short or long workflow path.
- Retriever: fetches relevant evidence from uploaded materials.
- Tutor: explains concepts using retrieved evidence.
- Planner: creates study plans from goals, time constraints, and materials.
- Quizzer: creates questions and expected answers.
- Grader: grades user answers against evidence and expected points.
- Reviewer: turns weak points into review tasks.
- Supervisor: validates outputs, handles fallbacks, and records workflow traces.

Why not a single agent:

- Study planning, retrieval, explanation, quiz creation, and grading have different input/output contracts.
- Separate nodes are easier to test and debug.
- Short paths reduce latency for simple questions.
- Structured node outputs make failures easier to detect.

Optimization strategy:

- Simple material questions use Router -> Retriever -> Tutor.
- Study plan requests use Router -> Retriever -> Planner.
- Quiz flows use Router -> Retriever -> Quizzer -> Grader when the user answers.
- Review flows use Router -> Reviewer, optionally using Retriever for supporting material.
- Cache repeated retrieval and summaries.
- Validate structured JSON outputs before saving or showing them.
- Record AgentRun traces for debugging and interview explanation.

## 9. Backend Learning Path Embedded in the Project

Phase 1 teaches:

- FastAPI routes, dependencies, Pydantic schemas.
- Authentication and JWT.
- PostgreSQL schema design.
- File upload and metadata management.
- Docker Compose.

Phase 2 teaches:

- Document parsing.
- Background jobs.
- Embeddings and vector search.
- RAG answer generation.
- Citation handling.

Phase 3 teaches:

- Product workflows.
- Quiz and review data models.
- AI output validation.
- Evaluation thinking.

Phase 4 teaches:

- LangGraph.
- State machines.
- Router design.
- Multi-agent debugging.
- Cost and latency control.

## 10. Documentation System

Documentation is part of the product.

Required files:

- `docs/project-memory.md`: short state file for new AI windows.
- `docs/devlog/YYYY-MM-DD.md`: daily engineering log.
- `docs/sessions/YYYY-MM-DD-HHMM.md`: AI conversation/session summary.
- `docs/decisions/ADR-XXXX-title.md`: important architecture decisions.
- `docs/03-resume-points.md`: resume bullets updated as features are implemented.
- `docs/04-deep-dive-questions.md`: interview questions and prepared answers.
- `docs/evals/rag_eval_set.md`: RAG evaluation examples.

Every substantial session should end by updating project memory, devlog, and session summary.

## 11. Resume Strategy

The project should produce concrete resume bullets in these categories:

- Backend API and authentication.
- Async document processing.
- RAG with citations and refusal.
- Multi-agent orchestration with LangGraph.
- Evaluation and optimization.
- Docker-based local deployment.

Each resume bullet should point to implementation evidence: file paths, docs, screenshots, API examples, or evaluation results.

## 12. Risks

Risk: too many features, not enough depth.

Mitigation: make RAG, agent orchestration, and engineering docs the depth areas.

Risk: multi-agent design becomes decorative.

Mitigation: only use multi-agent workflows where task separation provides testability, traceability, or better control.

Risk: backend learning feels fragmented.

Mitigation: map each backend topic to a feature and document the reason it was needed.

Risk: new AI windows lose project context.

Mitigation: maintain `docs/project-memory.md` and `docs/sessions/`.

## 13. Phase Plan

Phase 0: Documentation and scaffolding.

- Create repository structure.
- Write design spec, memory, ADRs, resume/deep-dive docs.
- Decide first vector store and job queue.

Phase 1: Backend MVP.

- FastAPI app.
- PostgreSQL connection.
- User model and JWT auth.
- Material upload and listing.
- Docker Compose.

Phase 2: RAG.

- Document parsing and chunking.
- Embeddings.
- Vector search.
- RAG answer endpoint.
- Citations and refusal behavior.
- Initial evaluation set.

Phase 3: Learning workflow.

- Study plans.
- Quizzes.
- Answer grading.
- Weak-point tracking.
- Review suggestions.

Phase 4: Multi-agent orchestration.

- LangGraph Router, Retriever, Tutor, Planner, Quizzer, Grader, Reviewer.
- AgentRun traces.
- Structured output validation.
- Short-path and long-path optimization.

Phase 5: Polish and portfolio.

- README with architecture.
- Screenshots or demo GIF.
- Tests.
- Error handling and logs.
- Deployment notes.
- Final resume bullets.

