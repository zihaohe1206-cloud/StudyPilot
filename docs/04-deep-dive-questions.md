# Deep-Dive Questions

Use this file to prepare interview answers as the project grows.

## Backend

Q: Why FastAPI instead of Node?

A: The project targets AI agent development. Python has stronger ecosystem support for LangGraph, RAG tooling, evaluation, document parsing, and model-related workflows. FastAPI also gives clear API structure and fast iteration.

Q: Why use background jobs for ingestion?

A: Parsing and embedding can take seconds or minutes for larger files. Running this in the request path would cause timeouts and poor user experience. A job queue lets the API return quickly and update material status asynchronously.

## RAG

Q: Why use citations?

A: Learning workflows need trust. Citations let the user verify answers against source material and reduce the impact of unsupported model generation.

Q: How do you handle questions not covered by the material?

A: The answer generator should refuse or ask for clarification when retrieval does not provide enough evidence. This behavior should be tested in the evaluation set.

Q: How do you choose chunk size and top_k?

A: Start with reasonable defaults, then evaluate retrieval results on a fixed question set. Adjust chunk size, overlap, and top_k based on missed evidence, irrelevant retrieval, and context length.

## Multi-Agent

Q: Why not use a single agent?

A: Study planning, retrieval, tutoring, quiz generation, grading, and review scheduling have different responsibilities and output formats. Splitting them into workflow nodes improves testability, debugging, and routing control.

Q: How do you optimize multi-agent orchestration?

A: Use a Router node to classify intent. Simple questions take a short path, while planning, quiz, and review tasks use specialized workflows. Cache repeated retrieval and summaries, validate structured outputs, and store traces for debugging.

Q: What prevents the agent system from becoming unstable?

A: The graph has explicit state, bounded paths, structured node outputs, fallback behavior, and error handling. The frontend does not let arbitrary model decisions directly mutate important data without backend validation.

## Evaluation

Q: How do you know the RAG system is improving?

A: Maintain an evaluation set with known questions, expected source material, expected answer points, and actual outputs. Track retrieval hit, citation quality, and hallucination behavior before and after changes.

## Resume Defense

Q: What is the hardest part of the project?

A: Making the system trustworthy and controllable: cited RAG, refusal behavior, structured outputs, agent traceability, and practical routing are more important than simply calling an LLM API.

