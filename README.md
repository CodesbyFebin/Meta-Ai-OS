<p align="center"><img src="docs/assets/hero-banner.svg" alt="MuZe — Meta AI Business Operating Server, with the MUSE silhouette" width="100%"></p>

<h3 align="center">One Discord-style server for every Meta surface. Every agent action is a commit. Nothing ships until you approve it.</h3>

<p align="center"><a href="https://codesbyfebin.github.io/Meta-Ai-OS/"><img src="docs/assets/talk-to-muse.svg" alt="Talk to MUSE: open the interactive pitch page" width="560"></a></p>

> **Note:** GitHub READMEs can't run JavaScript, so MUSE can't talk inside this page. The button opens [`docs/index.html`](docs/index.html), a single-file pitch page where you can click MUSE or talk to it with your browser's Web Speech API. Its replies are **offline demo answers** from [`docs/muse-faq.json`](docs/muse-faq.json). The GitHub Pages link only works once Pages is enabled for this repo; until then, open the file locally.

## The problem
Meta's business tools are fragmented. Business Suite for Pages, Creator Studio for Instagram, WhatsApp Manager, Ads Manager, and separate inboxes for Messenger and Instagram DMs. A founder or agency running several brands ends up with about **12 tabs open**, and no single record of who (or which AI) did what.

## The solution
**MuZe** (the app is called MeTaBos in the code) is one server:

- **Discord-style shell.** Brands are servers, Meta surfaces are channels, and your team and AI agents share the member list.
- **Git for agents.** Every post, inbox reply and ad draft is recorded as a commit with an author, a diff and a status. A commit is only marked *shipped* after a human approved it and it was actually sent.
- **Human approval gate.** **Jev** binds each approval to the hash of the exact payload. If the payload changes, the write is refused. There is no auto-send and no auto-approve path; only approved items reach `/api/dispatch`.
- **MUSE, the voice agentic harness.** Push-to-talk assistant that reads your data and drafts work. It can't approve anything itself.

## Who it's for
- **Businesses:** one unified inbox for WhatsApp, Messenger, Instagram and Facebook leads, ads kept as drafts, GST/ops tools.
- **Creators:** one content studio and calendar for Facebook, Instagram and Threads, with a single approval queue.

## Demo
[![MUSE in the Studio scene](docs/assets/muse-fur-studio.png)](docs/assets/muse-fur-studio.png)

| Fur Lab | 2D fallback | Mobile |
|---|---|---|
| ![Fur Lab panel](docs/assets/muse-fur-lab.png) | ![2D MUSE fallback](docs/assets/muse-fur-2d-fallback.png) | ![Mobile layout](docs/assets/muse-fur-mobile.png) |

Screenshots were taken in headless Chromium with software GL (no GPU). A demo GIF is still to be recorded; see [DEMO-SCRIPT.md](DEMO-SCRIPT.md).

## Architecture
```mermaid
flowchart LR
  U[Owner / team] -->|voice, click| SH[Meta Server shell<br/>servers · channels · Agent Hub]
  MUSE[MUSE voice harness] --> SH
  SH --> AG[Agents & Claw Swarm]
  AG -->|plan / draft| MM[Meta Model API<br/>USD hard spend cap]
  AG -->|classify, short replies| LL[Optional local Llama 3.2]
  AG --> LG[Llama Guard 3 check]
  LG --> C[Commit log<br/>git-for-agents]
  C --> JEV{Jev approval<br/>payload hash}
  JEV -->|approved, unchanged| D[/api/dispatch/]
  JEV -->|changed or rejected| X[Refused]
  D --> META[Meta surfaces<br/>WhatsApp · IG · Messenger · FB · Threads · Ads]
  D --> DB[(SQLite workspace DB<br/>evidence log)]
```

## Built with Llama
MuZe uses the **Meta Model API** for planning and drafting (with a hard spend cap and a token saver), an **optional local Llama 3.2** tier for classification and short replies, and **Llama Guard 3 1B** as a safety check before anything reaches Jev. When a model is not reachable, the app shows *Not connected* rather than fake output.

**Built with Llama.** Llama models are subject to the Llama Community License.

## Quick start
```bash
git clone https://github.com/CodesbyFebin/Meta-Ai-OS && cd Meta-Ai-OS
npm ci                      # Node 20+
cp .env.example .env.local  # optional; every provider stays "Not connected" without keys
npm run dev                 # http://localhost:3000
npm test                    # vitest
npm run build
```
Provider variables are documented in [docs/PROVIDER-ENV.md](docs/PROVIDER-ENV.md). Never commit real keys.

## Verification
### This repo (re-run after re-sequencing)
Run on 2 Nov 2026, about 4:30–4:50 AM IST, on the box (Node 20.19.2, Linux, no GPU), after `npm ci`. Local checks only.

| Check | Result |
|---|---|
| `npx tsc --noEmit` | pass (exit 0) |
| `npm run build` | pass (exit 0); one warning from `@miosa/sdk` ("Critical dependency: the request of a dependency is an expression") |
| `npx vitest run` | 5405 passed, 9 skipped, 4 failed (5418 tests, 424 files). The full run overlapped with a second accidental run on the same machine; re-running the 5 failing files alone left **2 failed tests + 1 file that fails to load**, all in the lab area and the same ones the development repo already lists as failing: `globSync is not a function` on Node 20 (`lab-v2-g*`) and a 30 s timeout in `lab-ledger-retention`. `lab-view` and `legacy-lab` passed alone. |
| Secret scan (gitleaks 8.21.2, all commits) | 7 findings, all reviewed as non-secrets: placeholder values in test files (`xoxb-very-secret-9876`, `apify_api_TESTSECRET123`, `zk_live_abc123`, a dummy UUID) and an empty `.env.example` key. `rg` for `ghp_`, `sk-`, `EAA…`, `LLM_…=`, `AKIA` and private-key headers: no real keys. |
| Route crawl, e2e, a11y | not re-run in this repo; see the development results below |


### Development repo (quoted from [docs/VERIFICATION-REPORT.md](docs/VERIFICATION-REPORT.md), local checks only, 2 Nov 2026 IST)
> | `npx vitest run` (full) | 5376 passed, 9 skipped. 2 tests failed and 1 file failed to load, all in the lab area, which was already failing before this work |
> | Route crawl | 244/244 routes return 200 with 0 stubs on desktop and on mobile |
> | Local swarm e2e | pass. "Run on local swarm" ran the claw-local Llama-3.2-3B in 18–36 s at $0. Llama Guard returned `safe`, a Brain draft was saved, and Jev showed `awaiting_approval`. Nothing was sent. |
> | External sends | BLOCKED by design. Only approved Jev items reach `/api/dispatch`; the Meta credentials are not live here |
> | MUSE fur | Not measured: real-GPU fps. |

The report states it "is not a production-readiness claim". Meta Suite channels without real credentials (Facebook, Threads, Messenger, Ads) show **Not connected**; no live Meta account is wired in this repo.

## Safety model
1. Agents only **propose**. Drafts pass Llama Guard 3, then wait in Jev.
2. Jev approves the canonical hash of the exact payload; tampering after approval is refused (covered by `tests/release-gate1-approval.test.ts`).
3. Only approved, unchanged items reach `/api/dispatch`, and only to a connected sender.
4. MUSE can read and draft; voice approval is refused by design.
5. Spend is capped per workspace and per agent. See [SECURITY.md](SECURITY.md).

## Pre-existing code disclosure
The Meta Global AI Developer Hackathon kicked off on **26 Oct 2026, 9:30 PM IST**. The first commit here, `chore: import pre-existing code (pre-kickoff, Oct 26 2026)`, is the development repo as of commit `1105e64` (26 Oct 2026, 7:35 PM IST), the last commit before kickoff. It includes a FounderOS fork (MIT) and earlier MuzeBOS work. Everything after it was built during the event. Details and ambiguities: [HACKATHON.md](HACKATHON.md).

**History note:** this repo's history was **re-sequenced** from the development repo [CodesbyFebin/MuzeBOS--The-Zero-Trust-Business-OS](https://github.com/CodesbyFebin/MuzeBOS--The-Zero-Trust-Business-OS) (draft PRs #50–#68) into readable commits grouped by area. Commit dates are when this repo was assembled, not backdated. The original granular history stays in the development repo.

## Third-party credits
See [THIRD_PARTY.md](THIRD_PARTY.md) and [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md): FounderOS (MIT), agentshield, ai-employees, founder-skill, ai-agent-onboarding (licences in `vendor/`), three.js (MIT). Meta, Facebook, Instagram, Messenger, WhatsApp, Threads and Llama are trademarks of Meta; this project is not affiliated with or endorsed by Meta.

## Team
**Febin Francis** ([@CodesbyFebin](https://github.com/CodesbyFebin)), Kochi, Kerala, India. Solo, indie track.

## Licence
[MIT](LICENSE), matching the development repo.

<sub>The previous MeTaBos README is kept at [docs/METABOS-README.md](docs/METABOS-README.md).</sub>
