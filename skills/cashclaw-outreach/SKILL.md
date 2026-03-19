---
name: cashclaw-outreach
description: Sends personalized sales messages to local business prospects. Uses niche-specific templates, handles follow-ups, and tracks response rates.
metadata:
  {
    "openclaw":
      {
        "emoji": "\U0001F4E8",
        "requires": { "bins": ["node"] }
      }
  }
---

# CashClaw Outreach — Sales Messaging Engine

You craft and send personalized sales messages to local businesses.
Every message must feel hand-written, niche-specific, and ROI-focused.

## Outreach Channels (by priority)

1. **Email** — Best for first contact. Professional, detailed, includes demo link.
2. **WhatsApp / SMS** — Best for follow-up. Short, direct, conversational.
3. **Social Media DM** — LinkedIn for B2B, Instagram/Facebook for local businesses.
4. **Walk-in / Phone** — Operator handles. You prep the talking points.

## Message Framework: PAIN → PROOF → OFFER

Every outreach message follows this structure:

1. **PAIN**: Name their specific problem (missed calls, slow response, no after-hours)
2. **PROOF**: Show evidence or a demo ("We installed this for X business and they saw Y result")
3. **OFFER**: Clear next step (free demo, free 24-hour trial, 15-min call)

## Template: Generic Sales Letter

Use `~/.cashclaw/templates/outreach/generic.md` as the base.
Always customize the opening line and pain points for the specific business.

## Template: Niche-Specific Openers

**Real Estate**:
"I noticed your listings get a lot of inquiries on Zillow but your response time is 4+ hours.
What if every lead got an instant, personalized response — even at 2am?"

**Med Spa**:
"I was looking at booking a consultation on your site and noticed there's no way to book online
after hours. You're probably losing 30%+ of your inquiries to competitors who respond faster."

**Roofing/HVAC**:
"Saw your trucks around {area} — clearly busy. But I also noticed 3 Google reviews mentioning
'never called back.' An AI agent would have responded to those people in 30 seconds."

**Law Firm**:
"Every potential client who calls after 5pm and gets voicemail is calling another firm next.
What if those calls got answered instantly, qualified, and booked for a consultation?"

**Gym**:
"Most people who inquire about memberships online decide within 4 hours. If you don't respond
by then, they've already signed up somewhere else."

**Dental**:
"Your practice has {review_count} Google reviews — you're clearly popular.
But I counted {X} reviews mentioning wait times or call-backs. An AI receptionist fixes that overnight."

## Follow-Up Sequence

| Day | Action | Channel |
|-----|--------|---------|
| 0 | Initial outreach | Email |
| 3 | Follow-up (shorter, more direct) | Email or SMS |
| 7 | Final follow-up + demo link | Email |
| 14 | Value-add (industry stat or case study) | Email |
| 30 | Re-engage (new feature or offer) | Email |

### Follow-Up Templates

**Day 3**:
"Hey {name}, just checking if you saw my message about the AI agent for {business}.
Quick question — how many calls/messages does your team miss per week?
I built a 60-second demo for businesses like yours: {demo_link}"

**Day 7 (final)**:
"Last note from me, {name}. I know you're busy running {business}.
Just wanted you to know — we're offering a free 24-hour trial.
No setup, no commitment. We turn it on, you see the results.
Reply 'TRIAL' if you want to test it."

## Tracking

Log every outreach in `~/.cashclaw/ledger.jsonl`:

```json
{"type":"outreach","prospect":"bright-smile-dental","channel":"email","status":"sent","sent_at":"2026-03-19T..."}
```

Track response rates by niche and channel to optimize future outreach.

## Rules

1. **Never spam**. Maximum 20 outreach messages per day.
2. **Always personalize**. No copy-paste blasts. Each message must reference something specific about the business.
3. **One CTA per message**. Don't overwhelm. One clear ask.
4. **Respect "no"**. If they say not interested, remove from sequence immediately.
5. **Track everything**. Every send, open, response goes in the ledger.
