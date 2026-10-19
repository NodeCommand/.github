<p align="center">
  <img src="https://raw.githubusercontent.com/NodeCommand/.github/main/profile/logo.svg" alt="Node Command Logo" width="96" height="96" />
</p>

<h1 align="center">Node Command</h1>

<p align="center">
  <strong>Operate your Windows, macOS, and Linux machines from any AI assistant — through one Model Context Protocol (MCP) endpoint.</strong>
</p>

<p align="center">
  <a href="https://nodecommand.app"><img src="https://img.shields.io/badge/Website-nodecommand.app-0052FF?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Website" /></a>
  <a href="https://dash.nodecommand.app"><img src="https://img.shields.io/badge/Console-dash.nodecommand.app-059669?style=for-the-badge&logo=speedtest&logoColor=white" alt="Console" /></a>
  <a href="https://nodejs.org"><img src="https://img.shields.io/badge/Runtime-Node.js%20Native%20ESM-339933?style=for-the-badge&logo=node.js&logoColor=white" alt="Node.js" /></a>
  <a href="https://modelcontextprotocol.io"><img src="https://img.shields.io/badge/MCP-SDK%20v2%20Compliant-7C3AED?style=for-the-badge&logo=anthropic&logoColor=white" alt="MCP v2" /></a>
  <a href="#architectural-pillars"><img src="https://img.shields.io/badge/Supply--Chain-Zero%20External%20Deps-EA580C?style=for-the-badge" alt="Zero Deps" /></a>
  <img src="https://img.shields.io/badge/License-Apache--2.0-blue?style=for-the-badge" alt="License" />
</p>

---

## 🌐 What is Node Command?

**Node Command** gives **ChatGPT, Claude, Grok, Muse, and Gemini** direct, secure, and authenticated access to your computers and servers. Read files, inspect active services, and run terminal commands over outbound-only encrypted connections with strict policy ceilings and an immutable cryptographic audit trail.

- 🔌 **One connector URL** — `https://mcp.nodecommand.app/mcp`. Clients supporting MCP OAuth discovery sign in automatically; no manual key copying or token pasting.
- ⚡ **Single-command install** — `npx node-command` pairs your machine in seconds via an eight-character code, installs it as a background service, and verifies it online.
- 💻 **Multi-host fleets** — Manage a cloud VPS, a home lab server, and a developer laptop in the very same AI conversation. Zero inbound open ports, zero firewall adjustments.
- 👥 **Team access & RBAC** — Share machines with your team as Viewer, Operator, or Admin. Never share SSH keys or root credentials again.
- ⛓️ **Cryptographic proof** — Every executed command is signed and chained in an immutable SHA-256 audit trail. Always know who ran what, when, on which machine, and with what result.
- 🛑 **Hard safety limits** — Per-machine policy ceilings restrict filesystem boundaries, block destructive commands, and enforce fail-closed read-only modes.

---

## ⚡ Quick Start

### 1. Install & Enroll the Agent
Run the single-command installer on any machine (Linux, macOS, Windows) you want to control:

```bash
npx node-command
```

Approve the pairing in your browser with the eight-character code displayed in your terminal. The agent connects outbound-only and installs itself as a system or user service (systemd, Windows SCM, or macOS SMAppService). 

*For automated or headless enrollment, redeem a one-time dashboard token:*
```bash
npx node-command <host_id> <token>
```

### 2. Connect Your AI Assistant
Add the MCP connector endpoint (`https://mcp.nodecommand.app/mcp`) to your AI assistant:
- **Supported Hosts:** ChatGPT, Claude Desktop, Cursor, VS Code, Windsurf, OpenCode, Zed, Cline.
- **Authentication:** Automatic MCP OAuth 2.1 discovery for modern clients, or Personal Access Tokens (PAT) for custom headers.

### 3. Ask & Operate
Your assistant can see every enrolled machine in your workspace. Machine actions always target an **explicit host** — the platform never guesses or executes ambiguously.

---

## 🏛️ System Architecture

```
                    ┌────────────────────────────────────────┐
                    │      Autonomous AI Assistant / IDE     │
                    │   (Claude, ChatGPT, Cursor, OpenCode)  │
                    └───────────────────┬────────────────────┘
                                        │ Model Context Protocol (MCP v2)
                                        ▼
   ┌────────────────────────────────────────────────────────────────────────┐
   │                    Node Command Cloud Control Plane                    │
   │  - Multi-tenant SQLite WAL snapshot store & tenant quota locking       │
   │  - RFC 9700 hardened OAuth 2.0 / 2.1 authorization server             │
   │  - Caddy HTTP/3 reverse proxy with dynamic Blue/Green zero-downtime    │
   │  - Deterministic health certification via deploy-doctor                │
   └───────────────────────────────────┬────────────────────────────────────┘
                                       │
                      Outbound-Only Encrypted TLS Tunnels
                    (No inbound open ports on agent machines)
                                       ▼
   ┌────────────────────────────────────────────────────────────────────────┐
   │                   Node Command Cross-Platform Daemons                  │
   │   - Linux (systemd) · Windows (SCM) · macOS (SMAppService)             │
   │   - Interactive confirmation gating & command whitelist boundaries     │
   │   - Cryptographic Over-The-Air (OTA) updates backed by TUF             │
   └────────────────────────────────────────────────────────────────────────┘
```

---

## 📦 Core Ecosystem & Repositories

| Repository | Scope & Purpose | Visibility |
|---|---|---|
| **[NodeCommand](https://github.com/huseyincig/NodeCommand)** | Primary public product discovery: documentation, manifests, examples, and MCP setup guides. | `Public` |
| **[nc-agent](https://github.com/huseyincig/nc-agent)** | Open-source host agent, background daemon, and CLI installer (`npx node-command`). | `Public` |
| **[nc-protocol](https://github.com/huseyincig/nc-protocol)** | Canonical public wire contracts: WebSocket agent protocol and MCP tool JSON schemas. | `Public` |
| **[skills](https://github.com/huseyincig/mcp-ts-sdk-v2-skills)** | Suite of 25 production-ready, verified specialist AI agent skills with deterministic routers. | `Public` |
| **[nc-platform](https://github.com/huseyincig/nc-platform)** | The central multi-tenant control plane, zero-dependency SQLite storage, and Web Console. | `Private` |

---

## 🛡️ Architectural Pillars

- **Zero External Dependencies:** Built entirely with native Node.js ESM APIs (`node:sqlite`, `node:util` `parseArgs`, native HTTP/WebSocket), eliminating supply-chain vulnerabilities.
- **Outbound-Only Zero-Trust Perimeter:** Daemons never open listening ports. Connections are initiated outbound over TLS with hardware/OS device attestation.
- **MCP TypeScript SDK v2 Native:** Full compliance with `@modelcontextprotocol/*` Standard Schema, tool annotations (`readOnlyHint`, `destructiveHint`), and interactive `inputRequired` elicitation.
- **Deterministic Blue/Green Zero-Downtime:** Dynamic upstream switching via Caddy, `restart: unless-stopped` container isolation, and `deploy-doctor` health gate.
- **TUF-Hardened Over-The-Air Updates:** Cryptographically signed release binaries with monotonic version progression preventing rollback or freeze attacks.

---

## 🚀 Live Services & Endpoints

- 🌍 **Official Portal:** [nodecommand.app](https://nodecommand.app)
- 🎛️ **Web Console:** [dash.nodecommand.app](https://dash.nodecommand.app)
- 🔌 **Production MCP Gateway:** [mcp.nodecommand.app/mcp](https://mcp.nodecommand.app/mcp)
- 🔐 **OAuth 2.1 Authorization:** [auth.nodecommand.app](https://auth.nodecommand.app)

---

## 🔒 Security & Coordinated Disclosure

Security is fundamental to Node Command. If you discover a vulnerability or security concern, please submit a report directly via our [Security Policy](https://github.com/huseyincig/NodeCommand/blob/main/SECURITY.md) or contact `security@nodecommand.app`.

---

<p align="center">
  <sub>© Node Command. Developed and maintained by <a href="https://hhc.zone">Hüseyin Hadi Çığ</a>. Distributed under Apache 2.0 / MIT.</sub>
</p>
