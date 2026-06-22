# Peec AI

> Visualize how much B2B pipeline your company is losing in AI-search — and what fixing it is worth.

![Next.js](https://img.shields.io/badge/Next.js-15-black?logo=next.js)
![React](https://img.shields.io/badge/React-19-61DAFB?logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript)
![Tailwind](https://img.shields.io/badge/Tailwind-3-38BDF8?logo=tailwindcss)
![Framer Motion](https://img.shields.io/badge/Framer_Motion-11-black?logo=framer)
![GCS](https://img.shields.io/badge/Deployed-GCS-4285F4?logo=google-cloud)

## What it is

Peec AI is a high-fidelity **frontend prototype** built during **BigHack Berlin 2026**. It demonstrates a product concept: show a B2B company how visible it is in ChatGPT and Perplexity searches, how competitors compare, and what recovering that visibility gap is worth in annual revenue. All data is driven by a hard-coded mock JSON dataset — there is no live data pipeline or backend. It is an honest UI showcase of the product vision.

## Features

- **AI-search visibility score** — animated gauge showing your share-of-voice across tracked prompts vs. the category leader
- **Competitor gap breakdown** — per-prompt table of which rivals outrank you and by how many percentage points
- **Revenue forecast** — pessimistic / optimistic EUR lift scenarios per prompt, rolled up to a total pipeline number
- **Simulated analysis flow** — multi-step animated pipeline (crawl → analyse → score) on the `/analyse` route, giving the feel of a live backend job
- **Paid-media upsell card** — state-machine offer card that walks through estimate → sending → received → accepted stages
- **Content-plan view** — recommended actions with rationale and evidence signals, tied back to revenue lift per prompt

## Tech stack

| Layer | Choice |
|---|---|
| Framework | Next.js 15 (static export, `output: "export"`) |
| UI | React 19, TypeScript, Tailwind CSS 3 |
| Animation | Framer Motion 11 |
| Icons | Lucide React |
| Hosting | Google Cloud Storage (static files) |
| CI/CD | Google Cloud Build (`cloudbuild.yaml`) |

## How it works

The entire app is a static Next.js export. On `next build`, all routes are pre-rendered to HTML/JS/CSS in `/out` and uploaded to a GCS bucket via Cloud Build.

The "analysis" the user sees is simulated: the `/analyse` route runs a timed, animated sequence of steps, then navigates to `/report`. The report reads from `Data/Mock.json` — a single structured file containing visibility scores, competitor data, prompt-level revenue scenarios, and recommended actions. No API calls, no server.

The `lib/peec.ts` module types and slices that mock JSON. `lib/paidMedia.ts` manages the offer card's client-side state machine via `localStorage`.

## Status

Hackathon demo — **BigHack Berlin 2026**. Static front-end, mock data only. Not production-ready; no real data ingestion or authentication.

## Running locally

```bash
npm install
npm run dev        # starts Next.js with Turbopack on http://localhost:3000
```

To build the static export:

```bash
npm run build      # outputs to /out
```
