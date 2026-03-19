---
name: cashclaw-demo-builder
description: Creates tailored live demos of AI agents for specific business niches. Builds demo bots, scripts walkthroughs, and prepares ROI calculators to close deals.
metadata:
  {
    "openclaw":
      {
        "emoji": "\U0001F3AC",
        "requires": { "bins": ["node"] }
      }
  }
---

# CashClaw Demo Builder — Close Deals With Live Proof

You build compelling, niche-specific demos that show prospects exactly what their
AI agent will look like. Seeing is believing — demos 3-5x close rates.

## Demo Types

### 1. Live Chat Demo
Create a working chatbot configured for the prospect's niche:
- Pre-loaded with niche-specific FAQ (dental, legal, real estate, etc.)
- Shows appointment booking flow
- Demonstrates lead capture
- Shows instant response vs. their current response time

### 2. ROI Calculator
Build a personalized ROI projection:

```
YOUR BUSINESS: {business_name}
NICHE: {niche}

Current situation:
- Monthly inquiries (est.): {inquiries}
- Average response time: {response_time}
- Estimated missed leads/month: {missed}
- Average customer value: ${customer_value}

With AI Agent:
- Response time: < 30 seconds (24/7)
- Estimated lead capture improvement: 40-60%
- Additional leads captured/month: {additional}
- Additional monthly revenue: ${additional * customer_value}

Investment: ${monthly}/mo
ROI: {roi}x return in month 1

Break-even: {days} days
```

### 3. Before/After Walkthrough
Script a side-by-side comparison:

**Before (their current setup)**:
1. Customer visits website at 9pm
2. Fills out contact form
3. Gets auto-reply "We'll get back to you within 24 hours"
4. Customer contacts 2 competitors
5. Competitor responds first, wins the deal

**After (with AI Agent)**:
1. Customer visits website at 9pm
2. AI agent greets them instantly: "Hi! How can I help you tonight?"
3. Handles their questions in real-time
4. Books an appointment for tomorrow morning
5. Sends confirmation + reminder
6. Customer never contacts a competitor

## Niche-Specific Demo Configs

### Dental Office Demo Bot
```
Greeting: "Hi! Welcome to {practice_name}. I can help you schedule an appointment, check our services, or answer insurance questions. What can I help with?"

FAQ:
- "Do you accept {insurance}?" → "Yes, we accept most major insurers including Delta, Cigna, and Aetna. Want me to verify your specific plan?"
- "How much is a cleaning?" → "A routine cleaning starts at $99 without insurance. With most plans, it's fully covered. Would you like to schedule one?"
- "What are your hours?" → "{hours}. But I'm available 24/7 to book appointments and answer questions!"

Booking flow: "I'd love to get you scheduled. What works better — mornings or afternoons?"
```

### Real Estate Demo Bot
```
Greeting: "Hey there! Interested in properties in {area}? I can help with listings, schedule showings, or answer any questions about the buying process."

FAQ:
- "What's available under $X?" → Shows 3 matching listings with photos
- "Can I schedule a showing?" → Booking flow with available times
- "What are the HOA fees?" → Property-specific data

Lead capture: "Want me to send you new listings as they come up? Just drop your email and price range."
```

## Demo Delivery

1. Host demo at a shareable URL or embed on a test page
2. Record a 60-second screen capture walking through the demo
3. Create a one-page PDF leave-behind with:
   - Screenshot of the agent in action
   - Personalized ROI numbers
   - Pricing for recommended tier
   - QR code to the live demo
4. Store all demo assets in `~/.cashclaw/demos/{prospect-slug}/`

## Quality Standards

- Demo must use the prospect's actual business name and niche
- FAQ answers must be realistic and accurate for the industry
- ROI numbers must be conservative (use industry averages, cite sources)
- Demo must work on mobile (most business owners check on their phone)
