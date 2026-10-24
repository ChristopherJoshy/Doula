<div align="center">
  <img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:3b0764,35:7e22ce,70:c026d3,100:f0abfc&height=190&section=header&text=Doula&fontSize=68&fontColor=ffffff&animation=twinkling&fontAlignY=36&desc=Maternal%20health%20tools%20over%20FHIR%20and%20MCP.&descAlignY=58&descSize=17" alt="Doula animated header" />

  <p>
    <img src="https://img.shields.io/badge/TypeScript-ESM-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript" />
    <img src="https://img.shields.io/badge/MCP-Streamable%20HTTP-7E22CE?style=for-the-badge" alt="MCP server" />
    <img src="https://img.shields.io/badge/Clinical%20data-FHIR-C026D3?style=for-the-badge" alt="FHIR" />
    <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-F0ABFC?style=for-the-badge" alt="MIT License" /></a>
  </p>
</div>

## 🤰 What it is

Doula is a TypeScript Model Context Protocol server that connects MCP clients to FHIR-backed maternal-health context and a set of domain tools. It exposes structured tools through an HTTP server rather than asking a language model to invent its own data access.

## 🔌 Request path

```mermaid
flowchart LR
  A[MCP client] --> B[Express transport]
  B --> C[MCP server and tool registry]
  C --> D[Domain tools]
  D --> E[FHIR client]
  E --> F[FHIR endpoint]
  D --> G[Validation and response]
```

## 🧰 Stack

| Area | Tools |
|---|---|
| Runtime | Node.js 20+, TypeScript, ESM |
| Protocol and transport | `@modelcontextprotocol/sdk`, Express, Streamable HTTP |
| Clinical interface | FHIR client via `@smile-cdr/fhirts` |
| Validation and logging | Zod, Pino |
| Tests | Vitest |

## 🚀 Run locally

```bash
git clone https://github.com/ChristopherJoshy/Doula.git
cd doula
npm ci
cp .env.example .env
npm run dev
```

In PowerShell, use `Copy-Item .env.example .env`. Configure `PORT`, `LOG_LEVEL`, and the FHIR connection/auth context expected by the server. The development server uses `tsx`; production output is built with TypeScript.

```bash
npm test
npm run typecheck
npm run build
```

## 🗂️ Layout

```text
src/server/   MCP transport and lifecycle
src/fhir/     FHIR client and context
src/tools/    tool implementations and registry
src/core/     errors, logging and request context
data/         local fixtures and reference data
tests/        Vitest suite
```

## 📄 License

MIT. See [`LICENSE`](LICENSE).

## ⚠️ Clinical-data boundary

This is a prototype integration, not clinical advice or a production EHR. Use synthetic fixtures for development. Any real deployment needs authorization, privacy review, clinical validation, and access-control testing appropriate to its FHIR environment.