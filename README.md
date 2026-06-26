# FreeDeepseekAPI

<p align="center">
  <strong>本地 OpenAI 兼容 API 代理，用于 DeepSeek Web Chat</strong>
</p>

<p align="center">
  <a href="https://github.com/ForgetMeAI/FreeDeepseekAPI/blob/main/LICENSE"><img alt="License MIT" src="https://img.shields.io/badge/license-MIT-green.svg" /></a>
  <img alt="Node.js 18 plus" src="https://img.shields.io/badge/node-18%2B-339933.svg" />
  <img alt="No npm dependencies" src="https://img.shields.io/badge/dependencies-0-blue.svg" />
  <img alt="OpenAI compatible" src="https://img.shields.io/badge/OpenAI-compatible-111111.svg" />
</p>

<p align="center">
  <a href="#-快速开始">快速开始</a> •
  <a href="#-功能特点">功能特点</a> •
  <a href="#-请求示例">请求示例</a> •
  <a href="#-模型">模型</a> •
  <a href="#-接口端点">接口端点</a> •
  <a href="#-open-webui">Open WebUI</a>
</p>

FreeDeepseekAPI 在本地启动一个 API 服务器，用于 **DeepSeek Web Chat**（`chat.deepseek.com`），并允许将 DeepSeek Web 连接到 Open WebUI、LiteLLM、Hermes、Claude Code、OpenAI SDK 风格客户端以及其他 OpenAI 兼容工具。

该项目通过您在自己独立 Chrome 配置文件中已登录的普通 DeepSeek 账户工作。本地服务器接收 API 请求，然后通过保存的浏览器会话自动向 DeepSeek Web 发送请求。

> ⚠️ 这是一个实验性质的 Web Chat 代理。DeepSeek 可能随时更改其内部 Web API 而不预先通知。对于生产环境，建议使用 DeepSeek 官方付费 API。

ForgetMeAI: https://t.me/forgetmeai

---

## 导航

- [它能做什么](#-它能做什么)
- [功能特点](#-功能特点)
- [快速开始](#-快速开始)
- [Windows 启动](#-windows-启动)
- [Linux / Chromium 启动](#-linux--chromium-启动)
- [VPS / 无头模式启动](#-vps--无头模式启动)
- [诊断 / 医生](#-诊断--医生)
- [会话复用与聊天重置](#-会话复用与聊天重置)
- [多账户池](#-多账户池)
- [控制台登录思路](#-控制台登录思路)
- [验证运行](#-验证运行)
- [请求示例](#-请求示例)
  - [Chat Completions](#chat-completions)
  - [推理（Reasoning）](#推理reasoning)
  - [网页搜索](#网页搜索)
  - [流式输出](#流式输出)
  - [Anthropic Messages API](#anthropic-messages-api)
  - [OpenAI Responses API](#openai-responses-api)
  - [工具调用](#工具调用)
- [模型](#-模型)
- [接口端点](#-接口端点)
- [Open WebUI](#-open-webui)
- [更新登录状态](#-更新登录状态)
- [项目状态](#-项目状态)

---

## ✨ 它能做什么

- 将 DeepSeek Web 作为本地 API 端点使用。
- 将 DeepSeek 连接到 Open WebUI 及其他 OpenAI 兼容客户端。
- 获取标准 JSON 响应或流式 SSE 响应。
- 使用推理模型并获取独立的 `reasoning_content`。
- 提供 Anthropic Messages API 适配层，用于 Claude Code / Anthropic SDK。
- 提供 OpenAI Responses API 适配层，用于新的 OpenAI/Codex 风格客户端。
- 为不同的代理/用户维护独立的 Web 会话。

## 🚀 功能特点

- **OpenAI 兼容 API**：`POST /v1/chat/completions`
- **Anthropic 兼容适配层**：`POST /v1/messages`
- **OpenAI Responses 适配层**：`POST /v1/responses`
- **流式输出**：支持 SSE 分块和普通非流式 JSON 响应
- **推理内容输出**：对思考模型返回独立的 `reasoning_content`
- **工具调用**：解析 OpenAI tools、Anthropic tools 和 Responses 函数工具
- **模型能力查询**：`GET /v1/model-capabilities` 返回别名到真实 Web 模式的映射
- **代理会话**：为每个 `user` 或代理 ID 维护独立的 DeepSeek 会话
- **会话恢复**：自动重置过期或损坏的链/会话
- **零依赖**：仅需 Node.js 18+，无需安装任何 npm 依赖

---

## ⚡ 快速开始

```bash
git clone https://github.com/ForgetMeAI/FreeDeepseekAPI.git
cd FreeDeepseekAPI
npm run auth
npm start
