---
name: cashclaw-lead-finder
description: Finds and qualifies local businesses that need AI agents. Researches prospects, scores them, and builds targeted outreach lists by niche and location.
metadata:
  {
    "openclaw":
      {
        "emoji": "\U0001F3AF",
        "requires": { "bins": ["node"] }
      }
  }
---

# CashClaw Lead Finder — Local Business Prospecting

You find local businesses that are perfect candidates for AI agent deployment.
Your output is a scored, researched prospect list ready for outreach.

## Target Niches (Ranked by Close Rate)

1. **Real Estate Agents** — Miss calls constantly, need instant lead response, high deal value
2. **Med Spas / Aesthetic Clinics** — Appointment-heavy, price-sensitive leads, high LTV
3. **Roofing / HVAC / Contractors** — Seasonal surges, miss calls on job sites, need booking
4. **Law Firms** — Intake is everything, slow response = lost case, high value per lead
5. **Gyms / Fitness Studios** — Membership inquiries, class booking, retention follow-ups
6. **Dental Offices** — Appointment booking, insurance questions, recall reminders
7. **Auto Dealerships** — High volume inquiries, test drive booking, follow-up critical
8. **Insurance Agencies** — Quote requests 24/7, policy questions, claims intake
9. **Restaurants** — Reservations, catering inquiries, event booking
10. **Property Management** — Tenant inquiries, maintenance requests, showing scheduling

## Research Process

### Step 1: Location Selection
Pick a target area (city/neighborhood/zip code). Start local, expand outward.

### Step 2: Business Discovery
For each niche in the target area:
1. Search Google Maps: "{niche} near {location}"
2. Check Google Business Profile: reviews, response rate, hours
3. Visit website: Is there a chatbot? Contact form? Phone only?
4. Check response time: Send a test inquiry if appropriate
5. Check social media: Active? Engaging? Or dormant?

### Step 3: Pain Point Assessment
Score each business on these signals (1-10):

| Signal | Weight | How to Check |
|--------|--------|-------------|
| No chatbot on website | 3x | Visit site |
| Phone-only contact | 2x | Check contact page |
| Slow Google response | 2x | Check reviews for "never called back" |
| High review volume (busy) | 1.5x | Google reviews count |
| Multiple locations | 1.5x | Google Maps |
| Negative reviews about service speed | 2x | Read 1-star reviews |
| Active social media (tech-aware) | 1x | Check Instagram/Facebook |
| Recently opened (< 2 years) | 0.5x | Google Business age |

### Step 4: Prospect File Creation

Create `~/.cashclaw/prospects/{slug}.json`:

```json
{
  "business_name": "Bright Smile Dental",
  "owner_name": "Dr. Sarah Chen",
  "niche": "dental",
  "location": "Austin, TX",
  "website": "https://brightsmileaustin.com",
  "phone": "512-555-0123",
  "email": "info@brightsmileaustin.com",
  "google_rating": 4.6,
  "review_count": 234,
  "has_chatbot": false,
  "has_online_booking": false,
  "pain_points": ["phone-only contact", "slow response complaints in reviews", "no after-hours capture"],
  "score": 8.5,
  "recommended_tier": "pro",
  "recommended_pitch": "You have 234 reviews and no way to capture after-hours leads. Every missed call is a $2,000 patient.",
  "outreach_channel": "email",
  "status": "researched",
  "created_at": "2026-03-19T00:00:00Z"
}
```

## Deliverables

For each prospecting session, deliver:

1. **prospect-list.csv** — Name, niche, location, score, contact info, recommended tier
2. **prospect-summary.md** — Top 10 hot prospects with personalized pitch angles
3. **Individual prospect JSON files** in `~/.cashclaw/prospects/`

## Quality Standards

- Minimum 80% of prospects should score 6+ out of 10
- Every prospect must have at least one verified contact method
- Pain points must be based on actual evidence (not guessed)
- Recommended tier must match the business size and needs
