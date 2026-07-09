# Architecture

## High-Level View

```text
User
  -> Vue Web App
  -> FastAPI Backend
  -> PostgreSQL
  -> Redis
  -> Vector Store
  -> LLM Provider
```

## Backend Modules

Planned modules inside `apps/api`:

- `auth`: registration, login, JWT, current user dependency.
- `materials`: upload, metadata, parsing status.
- `ingestion`: parsing, chunking, embedding jobs.
- `rag`: retrieval, context building, answer generation.
- `study`: study plans, tasks, progress.
- `quiz`: quiz generation, attempts, grading.
- `agents`: LangGraph workflows and node implementations.
- `evals`: scripts and fixtures for RAG evaluation.

## Frontend Areas

Planned areas inside `apps/web`:

- Auth pages.
- Material library.
- Chat/RAG page with citations.
- Study plan page.
- Quiz page.
- Review dashboard.
- Agent run/debug view if time allows.

## Data Flow: Upload

```text
Upload file
  -> create StudyMaterial row
  -> enqueue ingestion job
  -> parse document
  -> chunk text
  -> create embeddings
  -> store chunks
  -> mark material ready
```

## Data Flow: Question Answering

```text
User question
  -> Router classifies request
  -> Retriever fetches chunks
  -> Tutor generates answer with citations
  -> API stores messages and AgentRun trace
  -> Frontend renders answer and sources
```

