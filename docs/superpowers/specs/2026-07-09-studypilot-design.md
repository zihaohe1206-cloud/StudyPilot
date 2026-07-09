# StudyPilot 设计说明

日期：2026-07-09

## 1. 目标

StudyPilot 是一个作品集级别的个人学习助理项目，服务于“前端开发者转向后端 + AI Agent 开发”的学习目标。

这个项目要通过真实功能训练后端工程能力，同时产出可写进简历的证据：可运行系统、清晰架构、技术决策、RAG 评估、多 Agent 编排，以及能经得起追问的实现细节。

## 2. 成功标准

项目成功时，应该能够展示：

- 用户登录鉴权和学习资料管理。
- 文档导入、解析、切分、embedding 和检索。
- 带引用的 RAG 回答，以及证据不足时的拒答。
- 基于用户目标和资料生成学习计划。
- 生成测验、批改答案、记录错题并安排复习。
- 用显式路由、状态、兜底和结构化输出实现多 Agent 工作流。
- 使用 Docker 本地启动。
- 有足够文档让新的 AI 窗口或开发者快速理解项目。
- 最终提交到 GitHub，形成可展示的作品集仓库。
- 简历亮点都有真实实现支撑。

## 3. 非目标

第一版不重点做：

- 训练或微调基础模型。
- 企业级权限、计费或团队协作。
- 复杂社交功能。
- 过大的 LMS 平台功能。
- 不受控制的全自动 Agent 工具调用。

## 4. 产品范围

StudyPilot 帮助用户基于自己的资料学习。

核心流程：

1. 用户登录。
2. 用户上传 PDF、Markdown 笔记或复制的文章文本。
3. 后端解析并切分资料。
4. 系统创建 embedding 并保存可检索 chunks。
5. 用户基于资料提问。
6. 系统检索相关 chunks，并生成带引用回答。
7. 用户要求生成学习计划。
8. Planner 根据资料和学习目标生成计划。
9. 用户完成生成的测验。
10. 系统批改答案，记录薄弱点，并建议复习任务。

## 5. 架构

计划仓库结构：

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

运行时组件：

```text
Vue Web App
  -> FastAPI API
    -> PostgreSQL
    -> Redis job queue/cache
    -> Vector store
    -> LLM provider
```

FastAPI 负责产品 API、鉴权、文档元数据、学习计划、测验记录和 Agent 入口。

后台任务负责耗时操作，例如文档解析、切分、embedding 和重新索引。

Agent 层由后端服务调用，前端不直接调用 Agent。

## 6. 数据模型草案

初始实体：

- User：账号、用户资料、鉴权相关信息。
- StudyMaterial：上传文件或文本来源。
- DocumentChunk：chunk 文本、来源位置、embedding 引用、元数据。
- Conversation：用户对话会话。
- Message：用户和助手消息。
- StudyPlan：学习计划、里程碑和任务。
- Quiz：与资料和知识点关联的测验。
- QuizAttempt：用户答案和批改结果。
- WeakPoint：根据测验和复习历史跟踪的薄弱点。
- AgentRun：一次工作流运行的输入、输出、节点路径、错误和成本信息。

## 7. RAG 设计

RAG 流程：

1. 解析源资料。
2. 标准化文本。
3. 切分 chunks。
4. 保存 chunks 和来源元数据。
5. 创建 embeddings。
6. 根据问题检索相关 chunks。
7. 必要时 rerank 或过滤。
8. 构建回答上下文。
9. 生成带引用回答。
10. 证据不足时拒答或要求澄清。

关键设计点：

- 每个 chunk 尽量保留 material id、标题、页码/章节和字符偏移。
- 回答必须引用 chunk id 或来源位置。
- chunk size、overlap、top_k 等参数要记录，并根据评估结果调整。
- RAG 应该优先说“资料中没有找到依据”，而不是编造答案。

## 8. Agent 设计

Agent 是专用工作流节点，不是随意发挥的人设。

计划节点：

- Router：判断用户意图，选择短路径或长路径。
- Retriever：从资料中检索证据。
- Tutor：基于证据解释概念。
- Planner：根据目标、时间限制和资料生成学习计划。
- Quizzer：生成题目和参考答案。
- Grader：根据证据和参考要点评分。
- Reviewer：把薄弱点转换成复习任务。
- Supervisor：校验输出、处理兜底并记录运行轨迹。

为什么不用单 Agent：

- 学习计划、检索、讲解、出题、批改和复习有不同输入输出协议。
- 拆成节点更容易测试和调试。
- 简单问题走短路径，可以降低延迟。
- 结构化节点输出更容易发现失败。

优化策略：

- 简单资料问答走 Router -> Retriever -> Tutor。
- 学习计划请求走 Router -> Retriever -> Planner。
- 测验流程走 Router -> Retriever -> Quizzer，用户回答后再进入 Grader。
- 复习流程走 Router -> Reviewer，必要时再调用 Retriever。
- 缓存重复检索和摘要。
- 保存或展示前先校验结构化 JSON 输出。
- 记录 AgentRun 轨迹，方便调试和面试解释。

## 9. 嵌入项目的后端学习路线

Phase 1 训练：

- FastAPI route、dependency、Pydantic schema。
- 登录鉴权和 JWT。
- PostgreSQL schema 设计。
- 文件上传和元数据管理。
- Docker Compose。

Phase 2 训练：

- 文档解析。
- 后台任务。
- embedding 和向量检索。
- RAG 回答生成。
- 引用处理。

Phase 3 训练：

- 产品工作流。
- 测验和复习数据模型。
- AI 输出校验。
- 评估思维。

Phase 4 训练：

- LangGraph。
- 状态机。
- Router 设计。
- 多 Agent 调试。
- 成本和延迟控制。

## 10. 文档系统

文档是项目的一部分，默认使用中文记录。

必须维护的文件：

- `docs/project-memory.md`：给新 AI 窗口看的当前状态。
- `docs/devlog/YYYY-MM-DD.md`：每日工程日志。
- `docs/sessions/YYYY-MM-DD-HHMM.md`：AI 对话/开发会话摘要。
- `docs/decisions/ADR-XXXX-title.md`：重要架构决策。
- `docs/03-resume-points.md`：随着功能实现持续更新的简历亮点。
- `docs/04-deep-dive-questions.md`：面试追问题和准备答案。
- `docs/evals/rag_eval_set.md`：RAG 评估样例。

每次有实质开发，都要在结束前更新 project memory、devlog 和 session summary。

## 11. 简历策略

项目应该产出这些方向的简历亮点：

- 后端 API 和鉴权。
- 异步文档处理。
- 带引用和拒答能力的 RAG。
- 基于 LangGraph 的多 Agent 编排。
- 评估和优化。
- Docker 本地部署。

每条简历亮点都应该能指向实现证据：GitHub 仓库、文件路径、文档、截图、API 示例、提交记录或评估结果。

最终 GitHub 仓库需要能支撑面试官快速判断：

- 项目是否真实可运行。
- 架构和技术选型是否清楚。
- RAG 和 Agent 是否有实现深度。
- 开发过程是否有持续提交和文档记录。

## 12. 风险

风险：功能太多，但深度不够。

应对：把 RAG、Agent 编排和工程文档作为深挖重点。

风险：多 Agent 变成装饰。

应对：只有当任务拆分能带来可测试性、可追踪性或更强控制时才使用多 Agent。

风险：后端学习碎片化。

应对：每个后端知识点都绑定到一个功能，并记录为什么需要它。

风险：新 AI 窗口丢失上下文。

应对：持续维护 `docs/project-memory.md` 和 `docs/sessions/`。

## 13. 阶段计划

Phase 0：文档和脚手架。

- 创建仓库结构。
- 写设计说明、项目记忆、ADR、简历/深挖文档。
- 决定第一版向量库和任务队列。

Phase 1：后端 MVP。

- FastAPI 应用。
- PostgreSQL 连接。
- User model 和 JWT auth。
- 资料上传和列表。
- Docker Compose。

Phase 2：RAG。

- 文档解析和切分。
- embeddings。
- 向量检索。
- RAG 回答接口。
- 引用和拒答。
- 初始评估集。

Phase 3：学习工作流。

- 学习计划。
- 测验。
- 答案批改。
- 薄弱点跟踪。
- 复习建议。

Phase 4：多 Agent 编排。

- LangGraph Router、Retriever、Tutor、Planner、Quizzer、Grader、Reviewer。
- AgentRun 轨迹。
- 结构化输出校验。
- 短路径和长路径优化。

Phase 5：作品集打磨。

- README 架构说明。
- 截图或 demo GIF。
- 测试。
- 错误处理和日志。
- 部署说明。
- GitHub 仓库整理、推送和可展示性检查。
- 最终简历亮点。
