# StudyPilot

StudyPilot 是一个用于从前端开发转向后端 + AI Agent 开发的学习型项目。

项目目标是做一个个人学习助理：它可以导入学习资料，基于资料进行带引用的问答，生成学习计划，生成测验，批改答案，并通过多 Agent 工作流安排复习。

## 当前状态

规划和文档阶段。还没有编写应用代码。

新开 AI 窗口时，先读这些文件：

1. `docs/project-memory.md`
2. `docs/sessions/` 里的最新会话摘要
3. `docs/superpowers/specs/2026-07-09-studypilot-design.md`
4. `docs/project-memory.md` 里的“下一步”

## GitHub 要求

这个项目最终必须提交到 GitHub，作为作品集和简历证明材料。

要求：

- 保持清晰的 git 提交历史。
- 每个阶段完成后都要提交一次有意义的 commit。
- README 要能让面试官快速理解项目目标、架构、启动方式和亮点。
- 最终 GitHub 仓库应包含可运行代码、核心文档、截图或 demo、RAG 评估结果和简历亮点说明。
- 如果仓库暂时不公开，也要保证本地仓库可以随时推送到 GitHub。

## 计划技术栈

- 前端：Vue 3、TypeScript、Pinia、Vue Router
- 后端：Python、FastAPI
- 数据库：PostgreSQL
- 异步任务/缓存：Redis + RQ 或 Celery
- RAG：pgvector 或 Qdrant
- Agent 编排：LangGraph
- 部署：Docker Compose
- 测试：pytest，少量关键前端测试

## 记录语言规范

默认使用中文记录项目内容：

- 文档、开发日志、会话摘要、ADR 默认中文。
- 代码注释默认中文，只在逻辑不够直观时写简短注释。
- 变量名、函数名、类名、API 路径、库名、框架名保留英文。
- 不写“赋值给变量”这类没有信息量的注释。

## 每次开发结束必须更新

- `docs/project-memory.md`
- `docs/devlog/YYYY-MM-DD.md`
- `docs/sessions/YYYY-MM-DD-HHMM.md`
- `docs/03-resume-points.md`
- `docs/04-deep-dive-questions.md`
