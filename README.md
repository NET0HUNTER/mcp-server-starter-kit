# Model Context Protocol (MCP) Server Starter Kit

<p align="center">
  <img src="https://img.shields.io/badge/Protocol-Model%20Context%20Protocol-8A2BE2?style=for-the-badge&logo=anthropic" alt="MCP Protocol" />
  <img src="https://img.shields.io/badge/Agentic-AI%20Tooling-00C7B7?style=for-the-badge&logo=openai" alt="AI Tooling" />
  <img src="https://img.shields.io/badge/Runtime-Node.js%20%7C%20TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Status-Production%20Ready-success?style=for-the-badge" alt="Production Ready" />
</p>

---

## 🤖 Overview

A production-ready starter kit for building custom **Model Context Protocol (MCP)** servers. This repository provides a structured, extensible architecture for exposing internal APIs, databases, filesystems, and specialized microservices directly to AI models and autonomous coding agents (Claude Desktop, Google Antigravity, Cursor, and OpenAI tools).

---

## ⚡ Key Capabilities

- **Dual Transport Layer**: Pre-configured support for both `stdio` (local agent integration) and Server-Sent Events (`SSE`) for distributed remote tools.
- **Type-Safe Tool Registration**: Automatic input schema validation and error handling using Zod.
- **Resource & Prompt Primitives**: Implements the full MCP specification, including dynamic resources, context prompts, and real-time client notifications.
- **Agent Sandbox Safety**: Built-in timeout controls, parameter sanitization, and execution boundary safeguards.

---

## 🚀 Getting Started

### Installation
```bash
git clone https://github.com/NET0HUNTER/mcp-server-starter-kit.git
cd mcp-server-starter-kit
npm install
```

### Build & Run
```bash
# Build TypeScript
npm run build

# Start local MCP server via stdio
npm start
```

### Integrating with Claude Desktop / Antigravity
Add the server configuration to your MCP settings file (`claude_desktop_config.json` or `antigravity_mcp_config.json`):

```json
{
  "mcpServers": {
    "custom-agent-tools": {
      "command": "node",
      "args": ["/path/to/mcp-server-starter-kit/build/index.js"]
    }
  }
}
```

---

<p align="center">
  <b>Model Context Protocol Starter Kit</b> • Engineered by <a href="https://github.com/NET0HUNTER">@NET0HUNTER</a>
</p>
