# API 草案

这是草案，开始实现后需要持续更新。

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

