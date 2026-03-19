<p align="center">
  <img src="cover.jpeg" alt="CashClaw - AI Agent Workforce for Local Businesses" width="100%" />
</p>

<p align="center">
  <a href="#what-is-cashclaw">What is CashClaw?</a> &middot;
  <a href="#quick-start">Quick Start</a> &middot;
  <a href="#how-it-works">How It Works</a> &middot;
  <a href="#service-tiers">Tiers</a> &middot;
  <a href="#target-niches">Niches</a> &middot;
  <a href="#dashboard">Dashboard</a> &middot;
  <a href="#commands">Commands</a>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/cashclaw"><img src="https://img.shields.io/npm/v/cashclaw?color=crimson&label=npm" alt="npm version" /></a>
  <a href="https://github.com/web3-claw/cashclaw/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue" alt="license" /></a>
  <a href="https://github.com/web3-claw/cashclaw/stargazers"><img src="https://img.shields.io/github/stars/web3-claw/cashclaw?style=social" alt="stars" /></a>
</p>

---

> *"We deployed CashClaw on Monday. By Friday, we had 3 demos booked and closed our first $597/mo client."*

---

## What is CashClaw?

CashClaw is a set of **OpenClaw skills** that turn your AI agent into a **local business sales machine**.

Your agent finds local businesses that need AI. Sends personalized outreach. Books demos. Closes deals. Deploys AI agents for clients. Collects payment. Manages recurring subscriptions. Sends performance reports. Upsells. Handles support.

**You build the machine once. CashClaw sells for you.**

It is not a SaaS. It is not a dashboard. It is a skill pack that plugs into any OpenClaw-compatible agent and gives it the ability to **prospect, sell, deploy, and manage AI agent workforces** for local businesses — autonomously.

```
No cold calling. No manual demos. No invoicing headaches.
Just an agent, a Stripe account, and CashClaw.
```

## Quick Start

```bash
npx cashclaw init
```

CashClaw will:

1. Create your `~/.cashclaw/` workspace
2. Set up the sales pipeline
3. Connect to Stripe (optional, add later)
4. Install all 7 skills into your OpenClaw agent
5. Print your first dashboard

```bash
# Or install globally
npm install -g cashclaw
cashclaw init
```

## How It Works

### The Sales Pipeline

```
PROSPECT → OUTREACH → DEMO → QUOTE → ACCEPT → DEPLOY → ONBOARD → RETAIN
```

1. **Prospect**: CashClaw finds local businesses that need AI agents (no chatbot, slow response, phone-only contact)
2. **Outreach**: Sends personalized sales messages with niche-specific pain points
3. **Demo**: Builds a live demo tailored to the prospect's business
4. **Quote**: Sends a professional proposal with ROI projection
5. **Accept**: Collects payment via Stripe (setup fee + first month)
6. **Deploy**: Configures and deploys AI agents for the client's business
7. **Onboard**: Walks client through their new AI agent, monitors first week
8. **Retain**: Monthly performance reports, recurring billing, upsells

### Revenue Model

| What | Amount |
|------|--------|
| Starter Setup Fee | $199 (one-time) |
| Starter Monthly | $297/mo |
| Pro Setup Fee | $499 (one-time) |
| Pro Monthly | $597/mo |
| Enterprise Setup Fee | $999 (one-time) |
| Enterprise Monthly | $997/mo |
| Reseller Setup Fee | $1,499 (one-time) |
| Reseller Monthly | $1,497/mo |

**5 Pro clients = $2,985 MRR = $35,820/year**

## Service Tiers

### Starter — $297/mo
- 1 AI agent
- 1 channel (web chat OR WhatsApp)
- Lead capture & auto-responses
- Basic FAQ handling
- Email notifications for new leads

### Pro — $597/mo
- 2 AI agents
- Multi-channel (web + WhatsApp + SMS)
- Appointment booking
- CRM integration
- Follow-up sequences
- Weekly performance reports

### Enterprise — $997/mo
- Unlimited AI agents
- All channels
- Custom workflows
- Priority support
- White-label option
- Dedicated account management

### Reseller — $1,497/mo
- Everything in Enterprise
- Resell rights
- Keep 100% commission on sub-clients
- Reseller dashboard
- Sales training materials

## Target Niches

CashClaw comes with niche-specific outreach templates and demo configurations:

| Niche | Why They Need AI | Avg Deal Value |
|-------|-----------------|----------------|
| Real Estate | Miss leads after hours, 78% go to first responder | $8,000-15,000/commission |
| Med Spas | Can't book consultations at 9pm, high LTV clients | $2,000-5,000/client |
| Roofing/HVAC | On job sites, miss calls, "never called back" reviews | $3,000-15,000/job |
| Law Firms | Intake is everything, voicemail = lost case | $5,000-50,000/case |
| Gyms | 67% of inquiries die in inbox within 4 hours | $600-1,200/year LTV |
| Dental | Appointment-heavy, insurance questions, recall reminders | $2,000-4,000/patient LTV |
| Auto Dealers | High volume, test drive booking, follow-up critical | $1,500-3,000/sale |
| Insurance | Quote requests 24/7, policy questions never stop | $500-2,000/policy |

## Available Skills

| Skill | Purpose |
|-------|---------|
| `cashclaw-core` | Business brain — orchestrates the entire sales pipeline |
| `cashclaw-lead-finder` | Finds and scores local businesses that need AI agents |
| `cashclaw-outreach` | Sends personalized sales messages with follow-up sequences |
| `cashclaw-demo-builder` | Creates live demos tailored to each prospect's niche |
| `cashclaw-agent-deployer` | Deploys and configures AI agents for paying clients |
| `cashclaw-agent-support` | Monitors agents, sends performance reports, handles support |
| `cashclaw-invoicer` | Stripe subscriptions, setup fees, recurring billing |

## Commands

```bash
# Setup & Status
cashclaw init                                # Interactive setup wizard
cashclaw status                              # Pipeline, MRR, active clients
cashclaw dashboard [-p PORT] [--no-open]     # Launch web dashboard

# Pipeline
cashclaw missions list [--status STATUS]     # List all pipeline items
cashclaw missions create <template> -c NAME  # Create from template
cashclaw missions start <id>                 # Move to next stage
cashclaw missions complete <id>              # Mark complete
cashclaw missions show <id>                  # View details

# Earnings
cashclaw earnings [-n LIMIT]                 # MRR, revenue, breakdown

# Config
cashclaw config show                         # View config
cashclaw config set <key> <value>            # Update setting

# Skills
cashclaw skills [--install]                  # List/install skills
```

## Mission Templates

```bash
cashclaw missions create business-assessment -c "Bright Smile Dental"
cashclaw missions create outreach-campaign-20 -c "Austin Real Estate"
cashclaw missions create agent-demo-session -c "Peak Roofing"
cashclaw missions create agent-starter-deploy -c "FitZone Gym"
cashclaw missions create agent-pro-deploy -c "Chen Law Group"
```

## Dashboard

```bash
cashclaw dashboard
```

Opens a local web dashboard showing:
- Pipeline funnel (prospects → demos → quotes → clients)
- MRR and revenue trends
- Active client list with agent status
- Outreach tracking and response rates
- Upcoming follow-ups and renewals

## The Math

```
10 prospects contacted per day
= 200 per month
× 5% demo rate = 10 demos
× 30% close rate = 3 new clients
× $597 avg monthly = $1,791 new MRR

Month 1: $1,791 MRR
Month 3: $5,373 MRR
Month 6: $10,746 MRR
Month 12: $21,492 MRR ($257K ARR)

All from an AI agent that works while you sleep.
```

## License

MIT — do whatever you want with it.

---

**Your next sales rep isn't human. It's AI.**
