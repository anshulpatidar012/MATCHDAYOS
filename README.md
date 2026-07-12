# Matchday OS — GenAI Stadium Intelligence for FIFA World Cup 2026

A GenAI-enabled prototype that enhances stadium operations and fan experience during the FIFA World Cup 2026 — covering multilingual fan assistance, real-time crowd management, transportation, sustainability, accessibility, and operational intelligence for organizers and volunteers.

**Live demo:** _add your deployed link here_

## The Problem

World Cup stadiums pack 60,000+ fans from dozens of countries into a few hours of high-density movement — through gates, concourses, transit hubs, and back out again. Language barriers, accessibility gaps, and slow human-only decision-making all create friction and risk during exactly the moments (kickoff, halftime, final whistle) when things move fastest.

## The Solution

Matchday OS is a single-page control-room and fan-facing prototype with four modules:

### 1. Fan Assistant (Multilingual Wayfinding)
A GenAI concierge, grounded in the venue's real gate map, accessible routes, and services, that answers fan questions in whatever language they type in — no translation app or dropdown menu needed. Escalation-aware: medical, security, or lost-child queries are flagged to route to a human steward rather than answered by the model.

### 2. Crowd Command (Real-Time Decision Support)
A live stadium-bowl visualization mapping simulated turnstile/concourse sensor data onto the venue's actual sections. A single click sends current occupancy data to an LLM, which drafts a plain-language flow recommendation for the control room — which sections are at risk, what rerouting or staffing action to take, and a preventative step for the next 15 minutes.

### 3. Transit & Sustainability
Forecasted shuttle/metro load with GenAI-drafted push notifications when a line crosses capacity, plus a sustainability tracker where a vision-assisted model reviews (simulated) waste-station imagery to flag mis-sorted recycling and coach volunteers in real time.

### 4. Accessibility & Operational Intelligence
Step-free route planning, live captioning of announcements, sensory-friendly routing, auto-generated volunteer briefings, incident-log summarization from radio chatter, and automated shift handoff notes.

## Tech Stack

- **Frontend:** Single-file HTML/CSS/JS (no build step, deploys anywhere static)
- **GenAI:** Anthropic Claude API (`claude-sonnet-4-6`) called directly from the client for the Fan Assistant chat and the Crowd Command flow-recommendation generator
- **Visualization:** Hand-drawn SVG stadium-bowl diagram driven by live occupancy data (no charting library)
- **Data:** Simulated sensor/ticketing/transit feeds standing in for real IoT and turnstile integrations

## Running Locally

No build step required.

```bash
git clone <your-repo-url>
cd matchday-os
# open index.html directly in a browser, or serve it:
python3 -m http.server 8000
# then visit http://localhost:8000
```

> **Note:** The Fan Assistant chat and "Generate AI Flow Recommendation" button call `https://api.anthropic.com/v1/messages` directly from the browser. Outside of the Claude.ai artifact environment (where this call is proxied automatically), you'll need to run these calls through your own backend with your Anthropic API key rather than calling the API directly from client-side JS — never ship a raw API key in frontend code.

## Deploying

This is a static site — any static host works:

- **GitHub Pages:** Settings → Pages → Deploy from branch → `main` / root
- **Netlify:** drag-and-drop the folder at [app.netlify.com/drop](https://app.netlify.com/drop)
- **Vercel:** `vercel deploy` from the project folder

## Roadmap

- Replace simulated sensor data with real turnstile/IoT feeds
- Add a lightweight backend proxy for the Claude API calls (auth, rate limiting, logging)
- Multi-venue support (one control room, many stadiums)
- Push notification integration for transit rerouting alerts
- Accessibility audit with real wheelchair-using fans and Deaf/HoH advisory group

## License

MIT
