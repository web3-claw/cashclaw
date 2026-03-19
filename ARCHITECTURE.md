# CashClaw — Architecture

> AI Agent Workforce Platform for Local Businesses

---

## 1. Project Structure

```
cashclaw/
├── bin/
│   └── cashclaw.js                              # CLI entry point (shebang → src/cli/index.js)
│
├── src/
│   ├── cli/
│   │   ├── index.js                             # Commander program — all CLI commands & routing
│   │   ├── commands/
│   │   │   ├── init.js                          # 5-step interactive setup wizard
│   │   │   ├── audit.js                         # Site audit engine (fetch + HTML parse)
│   │   │   ├── dashboard.js                     # Launch Express dashboard server
│   │   │   └── status.js                        # Agent & pipeline status display
│   │   └── utils/
│   │       ├── config.js                        # Config load/save/defaults (~/.cashclaw/config.json)
│   │       └── banner.js                        # ASCII logo + terminal banner
│   │
│   ├── engine/
│   │   ├── mission-runner.js                    # Mission CRUD, lifecycle, audit trail, proof export
│   │   ├── earnings-tracker.js                  # JSONL-based earnings ledger
│   │   └── scheduler.js                         # Heartbeat — checks pending missions & unpaid invoices
│   │
│   ├── integrations/
│   │   ├── openclaw-bridge.js                   # OpenClaw workspace detection & skill installation
│   │   ├── stripe-connect.js                    # Stripe payment links, invoices, status checks
│   │   └── hyrve-bridge.js                      # HYRVEai marketplace registration & job sync
│   │
│   ├── dashboard/
│   │   ├── server.js                            # Express REST API + static file server
│   │   └── public/
│   │       ├── index.html                       # Dashboard SPA shell
│   │       ├── app.js                           # Frontend (vanilla JS, Canvas chart)
│   │       └── style.css                        # Dark theme UI
│   │
│   └── utils/
│       └── version.js                           # Exports VERSION from package.json
│
├── skills/                                      # 12 OpenClaw skill packages (SKILL.md each)
│   ├── cashclaw-core/                           # Business orchestration brain
│   ├── cashclaw-lead-finder/                    # Find & qualify local business prospects
│   ├── cashclaw-outreach/                       # Personalized sales outreach
│   ├── cashclaw-demo-builder/                   # Build niche-specific live demos
│   ├── cashclaw-agent-deployer/                 # Deploy AI agents for paying clients
│   ├── cashclaw-agent-support/                  # Monitor, report, retain clients
│   ├── cashclaw-invoicer/                       # Billing & Stripe operations
│   │   └── scripts/stripe-ops.js               # Standalone Stripe CLI tool
│   ├── cashclaw-email-outreach/                 # Cold email sequence builder
│   ├── cashclaw-competitor-analyzer/            # Competitor analysis reports
│   ├── cashclaw-landing-page/                   # Landing page generation
│   ├── cashclaw-data-scraper/                   # Web data extraction
│   └── cashclaw-reputation-manager/             # Review monitoring & response
│
├── missions/                                    # 15 JSON mission templates
│   ├── business-assessment.json                 # Free AI readiness assessment
│   ├── outreach-campaign-20.json                # Contact 20 businesses
│   ├── agent-demo-session.json                  # Free live demo
│   ├── agent-starter-deploy.json                # Starter tier deployment ($496)
│   ├── agent-pro-deploy.json                    # Pro tier deployment ($1,096)
│   ├── competitor-analysis-{basic,pro}.json     # Competitor reports
│   ├── data-scrape-{basic,pro}.json             # Data extraction jobs
│   ├── email-outreach-{basic,pro}.json          # Email campaigns
│   ├── landing-page-{basic,pro}.json            # Landing page creation
│   └── reputation-{audit,monthly}.json          # Reputation management
│
├── templates/
│   ├── config.default.json                      # Full default configuration reference
│   ├── invoice.html                             # Mustache-style invoice template
│   └── outreach/                                # 6 niche-specific sales letter templates
│       ├── generic.md
│       ├── real-estate.md
│       ├── med-spa.md
│       ├── contractor.md
│       ├── law-firm.md
│       └── gym.md
│
├── tests/
│   └── cli.test.js                              # Node built-in test runner (550 lines)
│
├── package.json
├── CHANGELOG.md
├── README.md
├── LICENSE                                      # MIT
├── .gitignore
├── .npmignore
└── .github/
    └── FUNDING.yml                              # GitHub Sponsors → web3sonic.com/ai-workforce
```

---

## 2. High-Level System Diagram

```
┌─────────────────────────────────────────────────────────────────────┐
│                          BUSINESS OWNER                             │
│                     (Non-technical reseller)                        │
└────────────────────────────┬────────────────────────────────────────┘
                             │
                    CLI / Dashboard UI
                             │
┌────────────────────────────▼────────────────────────────────────────┐
│                        CASHCLAW CLI                                 │
│                     (bin/cashclaw.js)                               │
│                                                                     │
│  ┌──────────┐  ┌──────────┐  ┌───────────┐  ┌──────────────────┐  │
│  │   init   │  │  status  │  │ dashboard │  │ missions / earn  │  │
│  │  wizard  │  │  display │  │  (Express) │  │ / config / audit │  │
│  └────┬─────┘  └────┬─────┘  └─────┬─────┘  └────────┬─────────┘  │
│       │              │              │                  │             │
│  ┌────▼──────────────▼──────────────▼──────────────────▼──────────┐ │
│  │                      ENGINE LAYER                              │ │
│  │  mission-runner.js  │  earnings-tracker.js  │  scheduler.js   │ │
│  └──────────┬──────────────────────┬───────────────────┬─────────┘ │
│             │                      │                   │            │
│  ┌──────────▼──────────────────────▼───────────────────▼─────────┐ │
│  │                   INTEGRATIONS LAYER                          │ │
│  │  stripe-connect.js  │  openclaw-bridge.js  │  hyrve-bridge.js│ │
│  └──────────┬──────────────────────┬───────────────────┬─────────┘ │
└─────────────┼──────────────────────┼───────────────────┼────────────┘
              │                      │                   │
              ▼                      ▼                   ▼
     ┌────────────────┐   ┌──────────────────┐   ┌──────────────┐
     │   Stripe API   │   │ OpenClaw Agent   │   │  HYRVEai     │
     │   (Payments)   │   │ Platform (local) │   │  Marketplace │
     └────────────────┘   └──────────────────┘   └──────────────┘
                                   │
                          ┌────────▼────────┐
                          │  12 SKILL.md    │
                          │  Skill Packs    │
                          │  (AI Agent      │
                          │   Instructions) │
                          └─────────────────┘
```

---

## 3. Core Components

### 3.1 CLI Layer (`src/cli/`)

| Component | File | Purpose | Technology |
|-----------|------|---------|------------|
| **Program Router** | `index.js` (592 lines) | Defines all CLI commands, subcommands, and flags via Commander.js. Handles `missions`, `earnings`, `config`, and `skills` command groups inline. | Commander ^12 |
| **Init Wizard** | `commands/init.js` (300 lines) | 5-step interactive setup: agent naming, service selection, Stripe connection, OpenClaw detection, HYRVEai registration. | Inquirer ^9 |
| **Site Audit** | `commands/audit.js` (289 lines) | Fetches a URL, parses HTML for SEO signals (title, meta, headings, images, links), and generates a scored report. | Node `fetch()` |
| **Dashboard Launcher** | `commands/dashboard.js` (86 lines) | Starts the Express dashboard server with configurable port and auto-open. | Express ^4.21 |
| **Status Display** | `commands/status.js` (179 lines) | Renders pipeline summary, MRR, active clients, and OpenClaw skill status to terminal. | cli-table3, chalk |
| **Config Manager** | `utils/config.js` (215 lines) | Load, save, merge defaults, get/set nested keys with prototype pollution guard. | fs-extra |
| **Banner** | `utils/banner.js` (51 lines) | ASCII logo and branded terminal banner. | boxen, chalk |

### 3.2 Engine Layer (`src/engine/`)

| Component | File | Purpose |
|-----------|------|---------|
| **Mission Runner** | `mission-runner.js` (329 lines) | Full mission lifecycle: create from template, start, complete, cancel, list, filter by status. Maintains an audit trail array with timestamped entries for every state transition. Supports short ID resolution (first 8 chars of UUID) with ambiguity detection. Exports mission proof as markdown. |
| **Earnings Tracker** | `earnings-tracker.js` (184 lines) | Append-only JSONL ledger. Provides aggregation: total, monthly, weekly, today, by-service, daily totals for N days. Reads entire file into memory for computation. |
| **Scheduler** | `scheduler.js` (139 lines) | Heartbeat loop (default 60s interval). Two checks per tick: flags missions running longer than 2x estimated time, and lists completed missions with unpaid invoices. |

### 3.3 Dashboard (`src/dashboard/`)

| Component | File | Purpose |
|-----------|------|---------|
| **API Server** | `server.js` (257 lines) | Express server with 7 REST endpoints. CORS restricted to localhost. Auto-increments port on collision (up to 10 attempts). Default port: 3847. |
| **Frontend SPA** | `public/app.js` (334 lines) | Vanilla JavaScript dashboard. Canvas-based 30-day earnings bar chart. Auto-refreshes every 30 seconds. |
| **UI Theme** | `public/style.css` (464 lines) | Dark theme — background `#1A1A2E`, orange accent `#FF6B35`, green accent `#16C784`. |

### 3.4 Integrations (`src/integrations/`)

| Component | File | Purpose |
|-----------|------|---------|
| **Stripe Connect** | `stripe-connect.js` (204 lines) | Payment link creation, invoice generation, payment status checks, transaction listing. API version `2024-12-18.acacia`. |
| **OpenClaw Bridge** | `openclaw-bridge.js` (207 lines) | Filesystem-based integration. Detects OpenClaw workspace, lists/installs/uninstalls skill packages by copying directories. No API calls. |
| **HYRVEai Bridge** | `hyrve-bridge.js` (214 lines) | Marketplace agent registration, status sync, job listing, and job acceptance. Graceful degradation when marketplace is unavailable. |

### 3.5 Skill System (`skills/`)

Skills are **documentation-driven instruction sets** for OpenClaw AI agents. Each skill is a directory containing a `SKILL.md` file with YAML frontmatter and structured instructions that teach an AI agent what to do. Skills contain no executable code except `cashclaw-invoicer/scripts/stripe-ops.js`.

**AI Workforce Skills (7):**

| Skill | Purpose |
|-------|---------|
| `cashclaw-core` | Orchestrates the 8-stage sales pipeline (Prospect → Outreach → Demo → Quote → Accept → Deploy → Onboard → Retain) |
| `cashclaw-lead-finder` | Finds and scores local businesses across 10 target niches |
| `cashclaw-outreach` | Sends personalized sales messages using PAIN→PROOF→OFFER framework |
| `cashclaw-demo-builder` | Creates live demos tailored to each prospect's industry |
| `cashclaw-agent-deployer` | Deploys and configures AI agents for paying clients (24h turnaround) |
| `cashclaw-agent-support` | Monitors agent health, sends performance reports, handles churn prevention |
| `cashclaw-invoicer` | Stripe billing: setup fees, subscriptions, payment links, failed payment recovery |

**General Service Skills (5):**

| Skill | Purpose |
|-------|---------|
| `cashclaw-email-outreach` | Cold email sequence builder with personalization |
| `cashclaw-competitor-analyzer` | Competitor website analysis and gap reports |
| `cashclaw-landing-page` | Landing page copy and HTML generation |
| `cashclaw-data-scraper` | Structured web data extraction |
| `cashclaw-reputation-manager` | Online review monitoring and response drafting |

---

## 4. Data Stores

CashClaw uses **filesystem-only storage** — no database. All data lives under `~/.cashclaw/`:

| Path | Format | Purpose | Access Pattern |
|------|--------|---------|---------------|
| `config.json` | JSON | Agent identity, Stripe keys, service tiers, pricing, integrations | Read/write on every command |
| `missions/{uuid}.json` | JSON (one file per mission) | Mission state, steps, client info, payment status, audit trail | Read/write per mission operation |
| `earnings.jsonl` | JSONL (append-only) | Revenue ledger — one JSON object per line | Append on payment; full read for aggregation |
| `ledger.jsonl` | JSONL (append-only) | Stripe operation event log (from `stripe-ops.js`) | Append-only |
| `deployments/{slug}.json` | JSON | Deployed agent configuration records | Write on deploy; read for status |
| `logs/health-{date}.json` | JSON | Daily agent health check results | Write daily; read for reports |

**Design rationale:** Filesystem storage enables fully offline operation, zero infrastructure requirements, and simple backup (copy the directory). The trade-off is no concurrent access safety and O(n) aggregation on earnings.

---

## 5. External Integrations

| Service | File | Auth Method | Purpose |
|---------|------|-------------|---------|
| **Stripe** | `stripe-connect.js`, `stripe-ops.js` | Secret key (env var `CASHCLAW_STRIPE_SECRET_KEY` or `config.stripe.secret_key`) | Payment links, invoices, subscription billing, payment status checks |
| **OpenClaw** | `openclaw-bridge.js` | None (filesystem) | Skill installation/detection in the local OpenClaw agent workspace |
| **HYRVEai** | `hyrve-bridge.js` | Custom headers (`X-Agent-Id`, `X-Agent-Name`) | Marketplace registration, job sync, job acceptance |
| **Target URLs** | `audit.js` | None | Fetches prospect websites for site audit reports |

---

## 6. Deployment & Infrastructure

### Runtime Requirements

| Requirement | Specification |
|-------------|--------------|
| **Node.js** | >= 20.0.0 |
| **Module system** | ESM (`"type": "module"`) |
| **OS** | Any (Linux, macOS, Windows) |
| **Database** | None required |
| **Package manager** | npm |

### Installation Methods

```bash
# Global install
npm install -g cashclaw

# Or run directly
npx cashclaw init
```

### Server Requirements (for hosting AI agents)

| Tier | RAM | vCPU | Storage | Handles |
|------|-----|------|---------|---------|
| Minimum | 4 GB | 2 | 50 GB | 1-5 clients |
| Recommended | 8 GB | 4 | 100 GB | 10+ clients |

### Dashboard Server

- **Port:** 3847 (default), auto-increments on collision up to 10 attempts
- **Binding:** localhost only (CORS restricted)
- **Process:** Foreground Express server, started via `cashclaw dashboard`

### Monitoring

- **Scheduler heartbeat:** 60-second interval, checks overdue missions and unpaid invoices
- **Agent health checks:** Daily logs written to `~/.cashclaw/logs/health-{date}.json`
- **Dashboard auto-refresh:** Frontend polls API every 30 seconds

---

## 7. Security Considerations

| Layer | Measure | Implementation |
|-------|---------|---------------|
| **Config injection** | Prototype pollution guard | `config set` and `POST /api/config` reject `__proto__`, `constructor`, `prototype` keys |
| **API access** | CORS restriction | Dashboard only accepts requests from `localhost` / `127.0.0.1` origins |
| **Sensitive keys** | Write protection | `POST /api/config` blocks modifications to `stripe.secret_key` and `stripe.webhook_secret` |
| **Secret storage** | Environment variable fallback | Stripe keys can be sourced from `CASHCLAW_STRIPE_SECRET_KEY` env var instead of config file |
| **Source control** | Gitignore | `.env`, `.env.local`, `*.log`, `coverage/`, `node_modules/` excluded |
| **Stripe API** | Versioned | Pinned to API version `2024-12-18.acacia` |
| **User-Agent** | Identified | Audit requests identify as `CashClawBot/1.0` |

---

## 8. Development & Testing

### Local Setup

```bash
git clone https://github.com/web3-claw/cashclaw.git
cd cashclaw
npm install
node bin/cashclaw.js init
```

### Test Suite

```bash
npm test
# Runs: node --test tests/cli.test.js
```

**Framework:** Node built-in test runner (`node:test` + `node:assert`)
**Coverage areas (550 lines):**

| Area | Tests |
|------|-------|
| Config | Default values, save/load, nested key access, service type validation |
| Banner | Function exports, output content |
| Missions | 15 template validations, lifecycle transitions (create → start → complete → paid), short ID resolution |
| Earnings | JSONL read/write, empty file handling, aggregation |
| Integrations | Export checks for Stripe, HYRVEai, and OpenClaw modules |
| Engine | Export checks for mission-runner, earnings-tracker, scheduler |
| Templates | `config.default.json` schema validation, `invoice.html` placeholder validation |
| Dashboard | Server creation, port auto-increment (3 concurrent instances) |
| Security | Prototype pollution detection, sensitive key write blocking |
| Skills | All 12 skill directories exist, each contains a `SKILL.md` |

### Code Quality

- **Linting:** Not configured (no ESLint/Prettier)
- **Type checking:** Not configured (no TypeScript)
- **CI/CD:** Not configured

---

## 9. Future Considerations

| Item | Status | Notes |
|------|--------|-------|
| **Database migration** | Planned | Filesystem storage limits concurrency and aggregation performance. SQLite or PostgreSQL would enable multi-user access and faster queries. |
| **Authentication** | Not implemented | Dashboard has no auth. Required before exposing beyond localhost. |
| **WebSocket dashboard** | Not implemented | Currently polls every 30s. WebSocket would enable real-time updates. |
| **CI/CD pipeline** | Not configured | No automated testing or deployment on push. |
| **TypeScript migration** | Not started | All source is vanilla JS with no type annotations. |
| **HYRVEai marketplace** | Stubbed | Integration code exists but marketplace API is not yet live. |
| **Scheduler auto-start** | Not wired | Heartbeat must be invoked programmatically — not started by any CLI command. |
| **Multi-currency** | Partial | Config supports `currency` field but earnings aggregation assumes single currency. |

---

## 10. Glossary

| Term | Definition |
|------|-----------|
| **CashClaw** | The platform — CLI tool, skills, missions, and dashboard for selling AI agents to local businesses |
| **OpenClaw** | The AI agent platform that executes CashClaw skills. CashClaw is a skill pack for OpenClaw. |
| **Skill** | A markdown instruction set (`SKILL.md`) that teaches an OpenClaw AI agent how to perform a specific task |
| **Mission** | An instantiated job from a template — tracks a specific task for a specific client through its lifecycle |
| **Mission Template** | A JSON blueprint defining a service type, pricing, required skills, deliverables, and execution steps |
| **Audit Trail** | A timestamped log of every state change within a mission, stored in the mission's JSON file |
| **MRR** | Monthly Recurring Revenue — total of all active client subscriptions |
| **HYRVEai** | A third-party AI agent marketplace for discovering freelance jobs |
| **Heartbeat** | The scheduler's periodic check loop (default 60s) for overdue missions and unpaid invoices |
| **JSONL** | JSON Lines — one JSON object per line, used for append-only ledgers |
| **Niche** | A target industry vertical (dental, real estate, law firm, etc.) with specific outreach templates |

---

## 11. Project Identification

| Field | Value |
|-------|-------|
| **Project** | CashClaw |
| **Version** | 2.0.0 |
| **Repository** | [github.com/web3-claw/cashclaw](https://github.com/web3-claw/cashclaw) |
| **License** | MIT |
| **Platform** | [web3sonic.com/ai-workforce](https://web3sonic.com/ai-workforce) |
| **Last Updated** | 2026-03-19 |
