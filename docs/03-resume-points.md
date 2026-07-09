# Resume Points

Update this file whenever a feature becomes real. Mark items as Draft until implemented.

## Project Name

StudyPilot: RAG and multi-agent learning assistant.

## Draft Resume Summary

Built a personal learning assistant with Vue, FastAPI, PostgreSQL, Redis, vector retrieval, and LangGraph. The system supports study material ingestion, cited RAG question answering, study plan generation, quiz grading, weak-point tracking, and multi-agent learning workflows.

## Draft Bullets

- Built a FastAPI backend for an AI learning assistant, including authentication, material upload, PostgreSQL persistence, and Docker Compose local deployment. Status: Draft.
- Implemented a RAG pipeline for private study materials, including document chunking, embeddings, vector retrieval, answer generation, citation display, and no-evidence refusal behavior. Status: Draft.
- Designed LangGraph-based multi-agent orchestration with Router, Retriever, Tutor, Planner, Quizzer, Grader, and Reviewer nodes, using explicit state and structured outputs to control workflow behavior. Status: Draft.
- Reduced multi-agent cost and latency by routing simple questions through a short Retriever -> Tutor path and reserving full workflows for planning, quiz, and review tasks. Status: Draft.
- Added asynchronous document ingestion with Redis-backed jobs to avoid blocking API requests during parsing and embedding. Status: Draft.
- Created a RAG evaluation set to measure retrieval hit rate, citation quality, and hallucination risk, then used results to tune chunking and retrieval parameters. Status: Draft.

## Evidence To Collect

- Architecture diagram in README.
- API examples.
- Screenshots or demo GIF.
- RAG evaluation results.
- AgentRun trace examples.
- Test output.
- Deployment command.

