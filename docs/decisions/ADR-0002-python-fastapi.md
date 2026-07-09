# ADR-0002：后端选择 Python 和 FastAPI

日期：2026-07-09

## 状态

已接受

## 背景

项目目标是 AI Agent 开发，而不是单纯传统 Web 后端。开发者已经具备 JavaScript 和 Vue 基础。

## 决策

主后端技术栈选择 Python 和 FastAPI。

## 理由

- Python 对 LangGraph、RAG、评估、文档处理和 AI 应用工具支持更强。
- FastAPI 对前端开发者比较友好，API 契约清晰，迭代速度快。
- 原有 JavaScript 能力仍然可以用于 Vue 前端和产品体验。

## 影响

正向影响：

- 更快进入 Agent 和 RAG 实现。
- 更贴近 AI 应用开发岗位。

取舍：

- 需要学习 Python 后端约定。
- 现有 JavaScript 后端经验不能完全直接迁移。

