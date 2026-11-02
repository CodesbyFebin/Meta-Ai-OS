# Contributing to MeTaBos

MeTaBos is a self-hostable business workspace in single-operator preview.
Contributions should improve real behavior, explain limits and preserve the
approval boundary. Start with [the docs hub](docs/search/README.md),
[architecture](docs/METABOS-ARCHITECTURE.md) and [project board](docs/PROJECTS.md).
Coding agents must also read AGENTS.md and CLAUDE.md.

## Local development

Use Node 22, `npm ci`, then `npm run dev` on http://localhost:4100. Keep real data in
ignored directories and use separate disposable DBs for qualification. Never
commit secrets, credentials, customer data, provider payloads or filled env files.
Preserve MIT/upstream notices and verify the licence of any imported code.

## Pull requests

Describe the user-visible trigger and resulting behavior, affected scopes,
validation performed and remaining gates. Small related changes are easier to
review. Record model/provider tests as fixture-only or live explicitly. A configured
key is not a connection; a connection probe is not a successful business action.
Do not add invented ratings, customers, certifications or production-readiness scores.

```sh
npm run typecheck
npm test -- --maxWorkers=4
npm run build
npm run docs:build
```

Use browser checks for changed user flows, including mobile and error/stale
states. API routes must retain authorization, validation and applicable origin,
idempotency and audit checks. Invoice changes must preserve exact-payload
approval, in-transaction stock validation and atomic durable writes. Generated
API documentation must be regenerated when routes change:
`node --import tsx scripts/gen-api-reference.ts`.

## Documentation and search

Edit authoritative guides in `docs/search/`, then run `npm run docs:build`.
The static site must not read business storage, keys or private runtime state.
Keep answer text and structured metadata consistent. Add distinct pages for
distinct user tasks, not keyword variants. See [search policy](docs/SEARCH-OPTIMIZATION.md).

## Reporting problems

Open an issue with a minimal sanitized reproduction, source revision, Node/browser
version, expected result, actual result and relevant redacted logs. Report security
vulnerabilities privately using [SECURITY.md](SECURITY.md), not public exploit details.

## Good first issues

Look for issues labelled
[`good first issue`](https://github.com/CodesbyFebin/Meta-Ai-OS/labels/good%20first%20issue) or
[`help wanted`](https://github.com/CodesbyFebin/Meta-Ai-OS/labels/help%20wanted).
Comment on the issue before starting so work isn't duplicated. Use
[Discussions](https://github.com/CodesbyFebin/Meta-Ai-OS/discussions) for questions.

## Honest labels

Mark anything that uses sample data as **DEMO** and anything not built as
**PLANNED** or **PENDING**. Do not add fabricated stats, stars, users, benchmarks
or badges. Use real model names (for example `llama3.2:3b` via Ollama); paid model
routes must stay opt-in. All participants follow the [Code of Conduct](CODE_OF_CONDUCT.md).
