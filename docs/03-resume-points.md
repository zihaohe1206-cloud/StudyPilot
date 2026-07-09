# 简历亮点

这个文件要随着功能实现持续更新。未实现的内容标记为“草稿”。

## 项目名称

StudyPilot：基于 RAG 和多 Agent 编排的个人学习助理。

## 简历摘要草稿

使用 Vue、FastAPI、PostgreSQL、Redis、向量检索和 LangGraph 构建个人学习助理系统，支持学习资料导入、带引用的 RAG 问答、学习计划生成、测验批改、薄弱点跟踪和多 Agent 学习工作流。

## 简历 bullet 草稿

- 构建 AI 学习助理后端，基于 FastAPI 实现用户鉴权、资料上传、PostgreSQL 持久化和 Docker Compose 本地部署。状态：草稿。
- 实现面向私有学习资料的 RAG 流程，包括文档切分、embedding、向量检索、回答生成、引用展示和无证据拒答。状态：草稿。
- 基于 LangGraph 设计 Router、Retriever、Tutor、Planner、Quizzer、Grader、Reviewer 等多 Agent 节点，通过显式状态和结构化输出控制工作流行为。状态：草稿。
- 通过 Router 将简单问题路由到 Retriever -> Tutor 短路径，将学习计划、测验和复习任务路由到完整工作流，降低多 Agent 调用成本和延迟。状态：草稿。
- 使用 Redis 后台任务异步处理文档解析和 embedding，避免大文件上传阻塞主请求。状态：草稿。
- 建立 RAG 评估集，跟踪检索命中率、引用质量和幻觉风险，并据此调整 chunk 策略和检索参数。状态：草稿。

## 后续要收集的证据

- README 架构图。
- API 示例。
- 截图或 demo GIF。
- RAG 评估结果。
- AgentRun 轨迹样例。
- 测试输出。
- 部署命令。

