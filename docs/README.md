# MuZe (MeTaBos) documentation

MuZe is an open-source, self-hosted AI business OS: a Discord-style Next.js + SQLite
workspace where AI agents draft and a human approves the exact payload before
anything is sent. This page maps the docs for people and for AI answer engines.
Machine-readable summary: [`/llms.txt`](../llms.txt).

## Quick facts
| Question | Answer |
|---|---|
| License | MIT |
| Stack | Next.js 15, React 18, TypeScript, SQLite (better-sqlite3), three.js |
| Run locally | `npm ci && npm run dev` → http://localhost:4100 |
| Default AI | Free/local Llama: Ollama `llama3.2:3b`, WebLLM, Llama Guard 3 1B |
| Paid AI | Off unless `MUZEBOS_INFERENCE_PAID=1` plus a key; spend capped |
| Live Meta sending | Needs your own Meta app credentials; otherwise "Not connected" |
| Maturity | Single-operator preview, not production-ready |

## Guides
- [Self-hosting](search/self-hosting.md)
- [Invoice approvals](search/invoice-approvals.md)
- [WebLLM inference](search/webllm-inference.md)
- [UPI and tax limits](search/upi-and-tax.md)
- [Security and data](search/security-and-data.md)
- [Verification](search/verification.md)

## Reference
- [Architecture](METABOS-ARCHITECTURE.md) · [API](METABOS-API.md) · [Inference](METABOS-INFERENCE.md) · [Provider env vars](PROVIDER-ENV.md)
- [Feature status matrix](FEATURE-STATUS-MATRIX.md) · [Release readiness](RELEASE-READINESS.md) · [Verification report](VERIFICATION-REPORT.md)
- [Navigation](METABOS-NAVIGATION.md) · [Operations](METABOS-OPERATIONS.md) · [Themes](THEMES.md) · [Voice](VOICE.md) · [Token saver](TOKEN-SAVER.md)

## Growth and maintenance
- [Launch playbook](LAUNCH_PLAYBOOK.md): drafts for the maintainer to post
- [gh CLI cookbook](GH_CLI_COOKBOOK.md)
