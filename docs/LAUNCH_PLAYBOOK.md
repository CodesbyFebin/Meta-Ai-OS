# Launch playbook (whitehat only)

Everything here is a **draft for the maintainer to post personally**. Nothing in this
repo posts anywhere automatically. Rules for every channel:

- No bought stars, vote rings, bots, sockpuppets or "upvote my post" requests. GitHub,
  Hacker News, Product Hunt and Reddit all detect and penalise these, and they can get the
  repo or account flagged.
- Never claim numbers you have not measured (users, stars, benchmarks, uptime).
- Say clearly that MuZeBOS is a **single-operator preview**, live Meta sending needs the user's
  own credentials, and paid AI routes are opt-in.
- Disclose that you are the maker in every post.

## Part 1. 20 growth tactics

### How GitHub Trending works (what is publicly known)
GitHub does not publish the formula. Public statements and observation suggest it ranks
repos by **recent star velocity relative to their usual rate**, per language and per time
window (daily/weekly/monthly), with filtering for spam. Practical consequence: a burst of
genuine attention within ~24–48 hours matters more than a slow trickle, so concentrate
launches on the same day or two, and make sure the repo is ready *before* traffic arrives.

| # | Tactic | Why it works | Notes |
|---|---|---|---|
| 1 | Make the first screen convert | Visitors decide in seconds | README value line in the first 160 chars, social preview uploaded, About description + topics set (done in this PR, except the image upload) |
| 2 | Record a 30–60 s demo GIF/video | Posts with motion get more clicks | Follow `DEMO-SCRIPT.md`; show the Jev "changed payload is refused" moment |
| 3 | Deploy the docs/pitch page to GitHub Pages | Gives every channel a link that works | Pages is configured but returns 404 today |
| 4 | Green CI badge before launch | Signals the code builds | Fixed in this PR; confirm on `main` |
| 5 | Seed 5–8 good first issues | Turns visitors into contributors | Created alongside this PR |
| 6 | Cut a tagged release | Release badge, "Releases" sidebar, watchers get notified | `v0.1.0` |
| 7 | Concentrate the launch in one 48 h window | Trending rewards velocity | HN + Reddit + X + dev.to on day 1, Product Hunt on day 1 or 2 |
| 8 | Show HN (Tue–Thu, ~8–10 AM US Eastern = ~5:30–7:30 PM IST) | Highest-intent developer audience | Title must start with "Show HN:"; something people can run; be in the thread for hours |
| 9 | r/selfhosted | Exact audience for self-hosted apps | Read the sidebar rules first; self-promo usually only allowed for open-source with a clear write-up |
| 10 | r/LocalLLaMA | Interest in local Llama/WebLLM/Ollama workflows | Lead with the local-model and Llama Guard angle, not the business pitch |
| 11 | r/opensource, r/SideProject, r/nextjs, r/IndieHackers-style communities | Broader dev audiences | One post per community, spaced out, tailored copy; follow each sub's rules |
| 12 | dev.to article | Ranks well in Google, long tail traffic | Technical: "Binding human approval to a payload hash" |
| 13 | Hashnode post (canonical URL set to dev.to or your blog) | Second audience without duplicate-content penalty | Set the canonical URL |
| 14 | X / Twitter thread with GIF | Developer reach, quote-tweets | 6–8 posts, GIF in the first |
| 15 | LinkedIn post | Founder/SMB audience in India | Focus on GST/UPI + approvals |
| 16 | Awesome-list PRs | Durable backlinks and discovery | Only lists whose criteria you meet. Example: awesome-selfhosted requires a project to be released more than 4 months ago, so wait. Check each list's CONTRIBUTING first |
| 17 | Product Hunt launch | Big single-day spike | 12:01 AM Pacific (~12:30–1:30 PM IST); kit below |
| 18 | Answer questions where they're asked | Durable trust | Only answer genuinely relevant threads, disclose you're the maker, no link-dropping |
| 19 | GitHub Discussions + "Show and tell" | Keeps visitors engaged after launch | Pin a welcome post and a roadmap post |
| 20 | Post-launch changelog cadence | Returning visitors and watchers | Ship small releases weekly with honest notes; each release notifies watchers |

Measure only what you can see: GitHub Insights → Traffic (views, clones, referrers), stars,
issues and PRs opened by others. Do not publish projected numbers.

## Part 2. Product Hunt kit

**Name:** MuZeBOS
**Tagline (≤60 chars):** `AI workers draft, you approve. Self-host or cloud.` (50)
**Expansion (use in description, not the name field):** Meta AI Zero Trust Business Open Server
**Website:** use the GitHub repo until workeragent.cloud resolves (PLANNED); cloud tier is not live, so say "self-host today, cloud coming soon"
**Alternates:** `AI agents draft. You approve the exact payload.` (47) · `Open-source AI workspace with approval-gated agents` (52)

**Topics:** Open Source, Artificial Intelligence, Productivity, Developer Tools, SaaS

**Description (≤260 chars):**
> MuZeBOS (Meta AI Zero Trust Business Open Server) is an open-source business OS. AI agents draft inbox replies, posts, ads and invoices; nothing is sent until you approve the exact payload. Free local Llama by default. Preview, MIT.

**Maker first comment:**
> Hi Product Hunt 👋 I'm Febin, a solo developer from Kochi, India.
>
> I built MuZeBOS because I didn't want an AI agent sending messages or invoices on my behalf without me seeing *exactly* what goes out. So in MuZeBOS every agent action becomes a commit with a diff, and the approval is bound to a hash of the exact payload: if anything changes after you approve, the send is refused.
>
> What works today: the Discord-style workspace, the commit log and approval gate, SQLite invoicing/GST/inventory/CRM modules, and local Llama via Ollama or WebLLM. What it is not (yet): production-ready, and live WhatsApp/Instagram sending needs your own Meta app credentials.
>
> It's MIT and runs with `npm ci && npm run dev`. I'd love feedback on the approval UX, and good first issues are open if you want to contribute.

**Gallery shot list (1270×760 recommended):**
1. Social preview / hero: "Agents propose. You approve the exact payload."
2. Meta Server shell: brands as servers, channels, agent member list.
3. Commit console: an agent draft shown as a diff with author and status.
4. Jev approval: approve → shipped; edited payload → "Refused".
5. Business module: invoice with GST, approval-bound.
6. Model routing panel: local Llama connected, paid routes off.
7. Mobile layout.
8. Demo video (30–60 s) as the first gallery item if available.
Every shot must be a real screenshot of the running app; label sample data as DEMO.

**Launch-day checklist:**
- [ ] Day −7: PH maker profile complete; "coming soon" page optional; README, GIF, social preview, release all live.
- [ ] Day −1: test `npm ci && npm run dev` on a clean machine; CI green; docs page live.
- [ ] 12:01 AM PT (~12:30–1:30 PM IST depending on US DST): launch goes live; post the first comment immediately.
- [ ] Share the PH link with your own network as a normal announcement ("we launched, feedback welcome"). Never ask for upvotes or share vote links in groups.
- [ ] Reply to every comment within the first hours; log bugs as issues and link them.
- [ ] Post the HN/Reddit/X drafts the same day (tactic 7).
- [ ] Day +1: thank-you post with honest results from Insights; triage issues.

## Part 3. Channel drafts

### Show HN
**Title:** `Show HN: MuZeBOS – zero-trust, self-hosted AI workspace where agents can't send without approval`
**Body:**
> MuZeBOS (MIT) is a Next.js + SQLite workspace for small businesses. AI agents draft inbox replies, posts, ads and invoices. Each action is stored as a commit, and approval is bound to a canonical hash of the exact payload, so editing after approval makes /api/dispatch refuse the send. There is no auto-approve path, and the voice assistant can draft but not approve.
>
> Models default to local Llama (Ollama llama3.2:3b or WebLLM in the browser) with an optional Llama Guard 3 check. Paid routes are opt-in with spend caps.
>
> Limits: single-operator preview, not production-ready; Meta channels need your own app credentials. Built during the Meta hackathon on top of some pre-existing code (disclosed in HACKATHON.md).
>
> Repo: https://github.com/CodesbyFebin/Meta-Ai-OS. I'd especially like criticism of the approval model.

### r/selfhosted
**Title:** `MuZeBOS: self-hosted (Node + SQLite) business workspace with approval-gated AI agents [open source, preview]`
**Body:** what it is (2 lines) · how to run (`npm ci && npm run dev`, no keys needed) · where data lives (local SQLite) · what's not done · "I'm the developer, feedback welcome". Add a screenshot.

### r/LocalLLaMA
**Title:** `Using llama3.2:3b + Llama Guard 3 1B as a local drafting tier behind a human approval gate`
**Body:** routing design (WebLLM → Ollama → optional OpenRouter), why drafts are hashed before approval, measured latency only if you measure it on your hardware and say which hardware, link to repo.

### dev.to / Hashnode article outline
**Title:** `Binding human approval to a payload hash: how MuZeBOS keeps AI agents from sending things you didn't see`
1. The problem with "approve" buttons when the payload can change.
2. Canonical JSON → hash → approval record; dispatch rechecks.
3. Code walk-through (link `tests/release-gate1-approval.test.ts`).
4. Local Llama tier and Llama Guard.
5. Limits and roadmap. Tags: `opensource`, `ai`, `nextjs`, `selfhosted`.

### X thread
1. "I built an open-source AI business workspace where agents can draft anything but send nothing until you approve the exact payload. 🧵 [GIF]"
2. "Every agent action is a commit: author, diff, status."
3. "Approval = hash of the payload. Change one character after approving and dispatch refuses it."
4. "Runs local Llama via Ollama or in-browser WebLLM. Paid models are opt-in with caps."
5. "SQLite invoicing, GST, inventory, CRM included. Self-hosted, MIT."
6. "Preview, not production. Meta channels need your own credentials."
7. "Repo + good first issues: https://github.com/CodesbyFebin/Meta-Ai-OS"

### LinkedIn
> Shipped an open-source preview of MuZeBOS, a self-hosted AI business workspace for founders and small agencies. Agents draft replies, posts and GST invoices; nothing is sent until a human approves the exact payload. Built solo in Kochi during the Meta Global AI Developer Hackathon. It's early (single-operator preview), and I'd value feedback from anyone running a small business on WhatsApp and Instagram. Repo: https://github.com/CodesbyFebin/Meta-Ai-OS

### Awesome-list PR description template
> Adds MuZeBOS: open-source (MIT) self-hosted AI business workspace with payload-bound human approval for agent actions. Node.js/SQLite. I'm the maintainer. I checked the list's inclusion criteria: [state each one].
