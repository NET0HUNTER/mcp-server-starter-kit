# Model Context Protocol (MCP) Server Starter Kit

A clean, production-ready starter template for building custom **Model Context Protocol (MCP)** servers using TypeScript, Zod, and role-based access control.

This kit provides a standalone foundation to connect AI agents (like Claude Desktop, Cursor, or custom LLM orchestration frameworks) to your private databases, REST APIs, and microservices—without exposing any internal company credentials or proprietary endpoints.

---

## 🚀 Features

- **Official SDK:** Built on `@modelcontextprotocol/sdk`.  
- **Strict Schema Validation:** Uses **Zod** for strongly-typed input validation.  
- **Security & RBAC Guardrails:** Built-in permission middleware (`enforceAuth`) preventing unauthorized reads or mutations.  
- **Safe Stdio Communication:** Directs all diagnostic messages to `stderr` so stdio JSON-RPC messaging is never corrupted.  
- **Client Ready:** Includes configuration templates for **Claude Desktop** and **Cursor**.

---

## 📁 Project Structure

mcp-server-starter-kit/

├── src/

│   ├── index.ts        \# Server entrypoint and Stdio transport setup

│   ├── tools.ts        \# Tool definitions (Read & Write tools with Zod schemas)

│   └── auth.ts         \# Role-based access control (RBAC) middleware

├── configs/

│   ├── claude\_desktop\_config.json   \# Ready-to-copy Claude Desktop config

│   └── cursor\_mcp\_config.json       \# Ready-to-copy Cursor MCP config

├── .env.example        \# Environment variable template

├── package.json        \# Dependencies and scripts

└── tsconfig.json       \# TypeScript compiler settings

---

## 🛠️ Quickstart (Run in 3 Minutes)

### 1\. Install Dependencies

npm install

### 2\. Build the Project

npm run build

### 3\. Test Running Locally

Run directly via TypeScript development runner:

npm run dev

*(You will see `[INFO] starter-mcp-server running on stdio transport.` printed to stderr.)*

---

## 🔌 Connecting to AI Clients

### 1\. Claude Desktop

Add this to your Claude Desktop configuration file:

- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`  
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

{

  "mcpServers": {

    "custom-tools": {

      "command": "node",

      "args": \[

        "/ABSOLUTE/PATH/TO/mcp-server-starter-kit/dist/index.js"

      \],

      "env": {

        "USER\_ROLE": "admin"

      }

    }

  }

}

### 2\. Cursor

In Cursor, go to **Settings** → **Features** → **MCP**, or add to `.cursor/mcp.json`:

{

  "mcpServers": {

    "custom-tools": {

      "command": "npx",

      "args": \[

        "-y",

        "tsx",

        "/ABSOLUTE/PATH/TO/mcp-server-starter-kit/src/index.ts"

      \]

    }

  }

}

---

## ✍️ How to Add Your Own Custom Tools

Open `src/tools.ts` and add a new tool using `mcp.tool()`:

mcp.tool(

  'tool\_name',

  'Clear description explaining to the LLM when and why to use this tool.',

  {

    parameter\_name: z.string().describe('Description of the parameter')

  },

  async (args) \=\> {

    // 1\. Enforce permission if needed

    enforceAuth(securityContext, 'your.scope');

    // 2\. Query your database or call your REST API

    const data \= await fetch(\`https://api.yourdomain.com/v1/resource?id=\${args.parameter\_name}\`);

    const result \= await data.json();

    // 3\. Return formatted text content to the model

    return {

      content: \[

        {

          type: 'text',

          text: JSON.stringify(result, null, 2\)

        }

      \]

    };

  }

);

---

## 🛡️ Security Best Practices

- **Never log to stdout:** `console.log()` writes to standard output, which corrupts the JSON-RPC channel used by MCP. Always use `console.error()` for debugging and logs.  
- **Never execute raw mutations without validation:** Use Zod constraints (`.min()`, `.max()`, `.email()`, `.enum()`) to sanitize all model outputs before they touch your backend.  
- **Keep secrets in `.env`:** Never hardcode API keys or database credentials inside tool handlers.

---

## 📄 License

MIT License. Free to use and adapt for personal or commercial projects.