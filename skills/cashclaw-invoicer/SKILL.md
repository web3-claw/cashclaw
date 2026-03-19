---
name: cashclaw-invoicer
description: Handles subscription billing, setup fee collection, payment link generation, recurring charges, and automated payment reminders via Stripe. Manages MRR tracking.
metadata:
  {
    "openclaw":
      {
        "emoji": "\U0001F4B3",
        "requires": { "bins": ["node"] }
      }
  }
---

# CashClaw Invoicer — Subscription & Payment Management

You manage all money flow for the AI agent workforce business.
Setup fees, monthly subscriptions, upgrades, and refunds.

## Payment Types

### 1. Setup Fee (One-time)
Charged at deal close:
- Starter: $199
- Pro: $499
- Enterprise: $999
- Reseller: $1,499

### 2. Monthly Subscription
Recurring charge:
- Starter: $297/mo
- Pro: $597/mo
- Enterprise: $997/mo
- Reseller: $1,497/mo

### 3. Add-Ons (One-time)
- Custom training data: $299
- CRM integration: $199
- Additional channel: $99

### 4. Referral Credits
- $100 credit per referred client who signs up

## Stripe Workflow

### New Client
1. Create Stripe Customer with client info
2. Create a Checkout Session for: setup fee + first month
3. Generate payment link
4. On successful payment:
   - Create a Subscription for monthly recurring
   - Log in `~/.cashclaw/earnings.jsonl`
   - Update `~/.cashclaw/dashboard.json` MRR
   - Trigger deployment via `cashclaw-agent-deployer`

### Monthly Recurring
Stripe handles automatic charging. On each successful charge:
- Log in earnings
- Update MRR

### Failed Payment
Day 0: Stripe retries automatically
Day 3: Send friendly reminder
Day 7: Send warning (service pause in 7 days)
Day 14: Pause agent (don't delete — they might come back)
Day 30: Final notice before data deletion

### Upgrade
1. Calculate prorated difference
2. Update Stripe subscription
3. Charge difference immediately
4. Unlock new features via `cashclaw-agent-deployer`
5. Update deployment record

### Refund
14-day satisfaction guarantee on setup fee.
Monthly fees are non-refundable but can cancel anytime.

## MRR Dashboard

Track in `~/.cashclaw/dashboard.json`:

```json
{
  "mrr": 2985,
  "arr": 35820,
  "active_subscriptions": 5,
  "avg_revenue_per_client": 597,
  "churn_rate": 0,
  "ltv_estimate": 7164
}
```

## Invoice Template

Professional PDF invoice with:
- Business name and logo
- Client details
- Line items (setup fee, monthly, add-ons)
- Payment terms
- Stripe payment link
- Support contact info
