<p align="center">
  <img src="https://raw.githubusercontent.com/NodeCommand/.github/main/profile/logo.svg" alt="Node Command Logo" width="96" height="96" />
</p>

<h1 align="center">Node Command</h1>

<p align="center">
  <strong>Hardened, Zero-Trust Control Plane & Native Agent Ecosystem for Autonomous AI and Model Context Protocol (MCP)</strong>
</p>

<p align="center">
  <a href="https://nodecommand.app"><img src="https://img.shields.io/badge/Website-nodecommand.app-0052FF?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Website" /></a>
  <a href="https://dash.nodecommand.app"><img src="https://img.shields.io/badge/Console-dash.nodecommand.app-059669?style=for-the-badge&logo=speedtest&logoColor=white" alt="Console" /></a>
  <a href="https://nodejs.org"><img src="https://img.shields.io/badge/Runtime-Node.js%20Native%20ESM-339933?style=for-the-badge&logo=node.js&logoColor=white" alt="Node.js" /></a>
  <a href="https://modelcontextprotocol.io"><img src="https://img.shields.io/badge/MCP-SDK%20v2%20Compliant-7C3AED?style=for-the-badge&logo=anthropic&logoColor=white" alt="MCP v2" /></a>
  <a href="#architectural-pillars"><img src="https://img.shields.io/badge/Supply--Chain-Zero%20External%20Deps-EA580C?style=for-the-badge" alt="Zero Deps" /></a>
</p>

---

## 🌐 Overview

**Node Command (NC)** is an enterprise-grade, zero-trust remote execution and agent orchestration platform. It safely bridges Large Language Models (LLMs), AI coding environments, and autonomous agents directly to remote physical servers, cloud instances, and edge clusters.

Instead of exposing vulnerable SSH keys, configuring fragile VPN tunnels, or opening risky inbound network ports, Node Command connects machines via **cryptographically attested, outbound-only RFC 6455 / RFC 8446 WebSocket tunnels**. AI models interact with your infrastructure exclusively through strictly bounded, auditable, and human-in-the-loop gated Model Context Protocol (MCP) tools.

---

## 🏛️ Ecosystem Architecture

```
                    ┌────────────────────────────────────────┐
                    │        Autonomous AI & LLM Host        │
                    │   (Claude, OpenAI, Cursor, OpenCode)   │
                    └───────────────────┬────────────────────┘
                                        │ High-Assurance MCP v2 Tools
                                        ▼
   ┌────────────────────────────────────────────────────────────────────────┐
   │                    Node Command Cloud Control Plane                    │
   │  - Multi-tenant tenant quota locking & node:sqlite WAL snapshot store   │
   │  - RFC 9700 hardened OAuth 2.0 / 2.1 authorization server             │
   │  - Caddy HTTP/3 reverse proxy with dynamic Blue/Green edge switching   │
   │  - Deterministic health certification via deploy-doctor               │
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

## 📦 Core Repositories

| Repository | Scope & Purpose | Visibility |
|---|---|---|
| **[NodeCommand](https://github.com/NodeCommand/NodeCommand)** | Primary public portal, quickstart guides (`npx node-command`), client manifests, and examples. | `Public` |
| **[nc-platform](https://github.com/NodeCommand/nc-platform)** | The central multi-tenant control plane, zero-dependency SQLite WAL backend, Caddy edge, and Web Console. | `Private` |
| **[nc-agent](https://github.com/NodeCommand/nc-agent)** | Native cross-platform background workers and privileged service helpers across Linux, Windows, and macOS. | `Public` |
| **[nc-protocol](https://github.com/NodeCommand/nc-protocol)** | Canonical MCP tool surfaces, JSON Schema 2020-12 specifications, and Standard Schema validation types. | `Public` |
| **[skills](https://github.com/NodeCommand/skills)** | Comprehensive suite of 25 verified, production-ready specialist AI agent skills with deterministic routers. | `Public` |

---

## 🛡️ Architectural Pillars

### 1. Zero External Dependencies
The control plane, CLI, and agent runtimes are engineered entirely on native Node.js ESM APIs (`node:sqlite`, `node:util` `parseArgs`, native HTTP/WebSocket transports). By eliminating hundreds of transient third-party npm packages, Node Command eradicates supply-chain takeover and dependency confusion vulnerabilities at the foundation.

### 2. Outbound-Only Zero-Trust Perimeter
Agents never open listening sockets or expose local attack surfaces. Connections are initiated outbound over TLS to the control plane. Machine identity is enforced with hardware/OS device attestation and cryptographic token proof headers.

### 3. Model Context Protocol (MCP) Native
Engineered directly against the official Model Context Protocol TypeScript SDK v2 (`@modelcontextprotocol/*`). Every tool includes strict Standard Schema validation, canonical annotations (`readOnlyHint`, `destructiveHint`), and interactive `inputRequired` elicitation for sensitive commands.

### 4. Deterministic Blue/Green Deployment
Production deployment uses zero-downtime Blue/Green switching orchestrated by Caddy dynamic upstreams. Containers enforce `restart: unless-stopped` to prevent inactive slot resurrection, single-writer `flock` lock isolation with descriptor cloaking (`9>&-`), and deterministic post-deploy health gating through `deploy-doctor`.

### 5. TUF-Hardened Over-The-Air (OTA) Updates
Remote daemon updates are governed by The Update Framework (TUF) threat model. Binaries and targets are cryptographically signed with offline root keys, strictly enforcing monotonic version progression to prevent rollback, freeze, or mix-and-match tampering.

---

## 🚀 Live Services & Endpoints

- 🌍 **Official Portal:** [nodecommand.app](https://nodecommand.app)
- 🎛️ **Web Console:** [dash.nodecommand.app](https://dash.nodecommand.app)
- 🔌 **Production MCP Gateway:** [mcp.nodecommand.app](https://mcp.nodecommand.app)
- 🔐 **OAuth 2.1 Authorization:** [auth.nodecommand.app](https://auth.nodecommand.app)

---

## 🔒 Security & Coordinated Disclosure

Security is fundamental to everything we build at Node Command. If you discover a vulnerability or potential security concern, please submit a report directly via our [Security Policy](https://github.com/NodeCommand/.github/security/policy) or contact `security@nodecommand.app`.

---

<p align="center">
  <sub>© Node Command Organization. Developed and maintained by <a href="https://hhc.zone">Hüseyin Hadi Çığ</a>. Distributed under Apache 2.0 / MIT.</sub>
</p>
