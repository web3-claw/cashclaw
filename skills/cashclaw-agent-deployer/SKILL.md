---
name: cashclaw-agent-deployer
description: Deploys and configures AI agents for client businesses. Handles channel setup, training data, integrations, and go-live testing.
metadata:
  {
    "openclaw":
      {
        "emoji": "\U0001F680",
        "requires": { "bins": ["node"] }
      }
  }
---

# CashClaw Agent Deployer — Ship AI Agents to Clients

You handle the technical deployment of AI agents for paying clients.
Speed matters — deploy within 24 hours of payment.

## Deployment Checklist

### Phase 1: Gather Info (Hour 0-2)
- [ ] Client's business name, address, phone, email
- [ ] Services/products they offer with pricing
- [ ] Business hours
- [ ] Top 20 FAQ from their customers
- [ ] Appointment types and durations (if booking needed)
- [ ] Current tools: CRM, calendar, phone system
- [ ] Brand voice: formal, casual, friendly, professional
- [ ] Any specific instructions or rules

### Phase 2: Configure Agent (Hour 2-8)
- [ ] Set up agent identity (name, personality, knowledge base)
- [ ] Load FAQ and service information
- [ ] Configure greeting message per channel
- [ ] Set up appointment booking (if included)
- [ ] Configure lead capture fields
- [ ] Set up notification system (email/SMS to business owner for new leads)
- [ ] Configure business hours behavior (in-hours vs. after-hours responses)
- [ ] Set up escalation rules (when to hand off to human)

### Phase 3: Channel Setup (Hour 8-16)
- [ ] **Web Chat Widget**: Generate embed code, test on client's site
- [ ] **WhatsApp Business** (if included): Connect number, set up greeting
- [ ] **SMS** (if included): Configure Twilio or similar
- [ ] **Facebook Messenger** (if included): Connect page
- [ ] Test each channel end-to-end

### Phase 4: Integration Setup (Pro/Enterprise only)
- [ ] CRM integration (HubSpot, Salesforce, GoHighLevel, etc.)
- [ ] Calendar sync (Google Calendar, Calendly, etc.)
- [ ] Email notifications for new leads
- [ ] Webhook setup for custom workflows

### Phase 5: Testing (Hour 16-20)
- [ ] Test 10 common customer scenarios
- [ ] Test appointment booking flow
- [ ] Test lead capture and notification
- [ ] Test escalation to human
- [ ] Test after-hours behavior
- [ ] Mobile test (phone browser)
- [ ] Load test (5 simultaneous conversations)

### Phase 6: Go Live (Hour 20-24)
- [ ] Deploy to production
- [ ] Send client access credentials
- [ ] Send embed code with installation instructions
- [ ] Verify agent is responding on all channels
- [ ] Send go-live confirmation to client

## Client Handoff

After deployment, send:

```
Your AI agent is LIVE! Here's everything you need:

AGENT NAME: {agent_name}
CHANNELS ACTIVE: {channels}

Web Chat:
- Embed this code on your website: {embed_code}
- Or share this link: {chat_url}

{if_whatsapp}
WhatsApp:
- Your AI agent is responding on: {whatsapp_number}
{/if_whatsapp}

Dashboard:
- View conversations: {dashboard_url}
- View leads captured: {leads_url}

You'll get an email/SMS notification every time a new lead is captured.

First 72 hours: I'm monitoring your agent closely.
If anything needs adjusting, I'll fix it proactively.

Day 7: I'll send you your first performance report.

Questions? Just message me anytime.
```

## Deployment Records

Create `~/.cashclaw/deployments/{client-slug}.json`:

```json
{
  "client": "bright-smile-dental",
  "tier": "pro",
  "deployed_at": "2026-03-19T00:00:00Z",
  "channels": ["web_chat", "whatsapp"],
  "agent_id": "",
  "status": "active",
  "monthly_fee": 597,
  "next_billing": "2026-04-19",
  "performance": {
    "leads_captured": 0,
    "conversations": 0,
    "appointments_booked": 0,
    "avg_response_time_seconds": 0
  }
}
```

## Tier-Specific Deployment

| Feature | Starter | Pro | Enterprise |
|---------|---------|-----|-----------|
| AI Agents | 1 | 2 | Unlimited |
| Web Chat | Yes | Yes | Yes |
| WhatsApp | OR | AND | AND |
| SMS | No | Yes | Yes |
| Appointment Booking | Basic | Advanced | Custom |
| CRM Integration | No | Yes | Yes |
| Custom Workflows | No | No | Yes |
| White-Label | No | No | Yes |
| Setup Time | < 12h | < 24h | < 48h |
