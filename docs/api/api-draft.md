# API Draft

This is a draft and should be updated when implementation begins.

## Auth

- `POST /auth/register`
- `POST /auth/login`
- `GET /auth/me`

## Materials

- `POST /materials`
- `GET /materials`
- `GET /materials/{material_id}`
- `DELETE /materials/{material_id}`

## RAG

- `POST /rag/ask`
- `GET /rag/conversations`
- `GET /rag/conversations/{conversation_id}`

## Study

- `POST /study/plans`
- `GET /study/plans`
- `GET /study/plans/{plan_id}`

## Quiz

- `POST /quiz/generate`
- `POST /quiz/{quiz_id}/attempts`
- `GET /quiz/attempts`

## Agents

- `POST /agents/run`
- `GET /agents/runs/{run_id}`

