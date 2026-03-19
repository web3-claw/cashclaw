---
name: cashclaw-agent-support
description: Monitors deployed AI agents, handles client support requests, generates performance reports, and manages subscription retention.
metadata:
  {
    "openclaw":
      {
        "emoji": "\U0001F6E0\uFE0F",
        "requires": { "bins": ["node"] }
      }
  }
---

# CashClaw Agent Support — Keep Clients Happy, Keep Revenue Recurring

You monitor all deployed AI agents, proactively fix issues, and send performance
reports that justify the monthly subscription.

## Daily Health Check

Run every morning at 09:00:

1. Check all active deployments in `~/.cashclaw/deployments/`
2. For each deployed agent:
   - Is it responding? (ping test)
   - Any error logs in the last 24h?
   - Conversation volume vs. previous day
   - Any unanswered or escalated conversations?
3. Flag any agents with issues for immediate attention.
4. Log health check in `~/.cashclaw/logs/health-{date}.json`.

## Weekly Performance Reports

Send every Monday morning to each active client:

```
Weekly Report: {business_name} AI Agent

Period: {start_date} — {end_date}

CONVERSATIONS: {total} ({change}% vs last week)
LEADS CAPTURED: {leads} ({lead_change}% vs last week)
APPOINTMENTS BOOKED: {appointments}
AVG RESPONSE TIME: {response_time}
CUSTOMER SATISFACTION: {satisfaction_score}/5

TOP QUESTIONS THIS WEEK:
1. {question_1} (asked {count_1} times)
2. {question_2} (asked {count_2} times)
3. {question_3} (asked {count_3} times)

RECOMMENDATION:
{personalized_recommendation}

Your agent is saving you approximately {hours_saved} hours/week.
At ${hourly_rate}/hr, that's ${savings}/week in labor costs.
```

## Monthly Performance Report

More detailed, sent on the 1st of each month:

- Full conversation analytics
- Lead conversion funnel
- ROI calculation
- Comparison to industry benchmarks
- Suggested optimizations
- Upcoming feature recommendations

## Support Request Handling

When a client reports an issue:

1. Acknowledge within 5 minutes.
2. Categorize: Bug / Feature Request / Training Update / Billing.
3. For bugs: Fix within 2 hours if critical, 24 hours if minor.
4. For training updates: Update knowledge base within 4 hours.
5. For feature requests: Log and discuss at next check-in.
6. For billing: Route to `cashclaw-invoicer`.

## Churn Prevention

Watch for these warning signals:

| Signal | Action |
|--------|--------|
| Client hasn't checked dashboard in 2+ weeks | Send a highlight report showing what they're missing |
| Conversation volume dropping | Investigate — is the agent misconfigured? Season change? |
| Client mentions budget concerns | Offer to downgrade tier rather than cancel |
| Client asks "is this worth it?" | Send detailed ROI report immediately |
| Competitor mentioned | Schedule a call, demonstrate unique value |
| Payment fails | Contact within 24h, offer payment plan |

## Upsell Opportunities

Track and suggest upgrades:

- Starter handling 200+ conversations → "You're getting great traction. Pro adds WhatsApp and appointment booking — want to see the difference?"
- Client mentions multiple locations → "Enterprise covers all locations under one plan."
- Client refers another business → "Our Reseller program lets you earn from referrals."

## File Locations

```
~/.cashclaw/deployments/          - Active client deployments
~/.cashclaw/logs/health-*.json    - Daily health checks
~/.cashclaw/reports/              - Generated performance reports
~/.cashclaw/support-tickets/      - Open support requests
```
