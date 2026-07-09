# 架构说明

## 高层结构

```text
用户
  -> Vue Web App
  -> FastAPI Backend
  -> PostgreSQL
  -> Redis
  -> Vector Store
  -> LLM Provider
```

## 后端模块

计划在 `apps/api` 中拆分这些模块：

- `auth`：注册、登录、JWT、当前用户依赖。
- `materials`：资料上传、元数据、解析状态。
- `ingestion`：解析、切分、embedding 任务。
- `rag`：检索、上下文构建、回答生成。
- `study`：学习计划、任务、进度。
- `quiz`：测验生成、作答记录、批改。
- `agents`：LangGraph 工作流和节点实现。
- `evals`：RAG 评估脚本和样例。

## 前端页面

计划在 `apps/web` 中实现这些区域：

- 登录/注册页面。
- 学习资料库。
- 带引用展示的 RAG 对话页。
- 学习计划页。
- 测验页。
- 复习看板。
- 如果时间允许，增加 Agent run 调试视图。

## 数据流：资料上传

```text
上传文件
  -> 创建 StudyMaterial 记录
  -> 投递 ingestion 任务
  -> 解析文档
  -> 切分文本
  -> 创建 embedding
  -> 保存 chunks
  -> 标记资料可用
```

## 数据流：资料问答

```text
用户提问
  -> Router 判断请求类型
  -> Retriever 检索相关 chunks
  -> Tutor 生成带引用回答
  -> API 保存消息和 AgentRun 轨迹
  -> 前端展示回答和来源
```

