# Agent Collab Viz — overnight MVP

## Goal
Ship a **deployed** multi-agent collaboration visualization by morning (Asia/Saigon ~08:00–10:00 Fri Oct 30 2026) that eason can open in a browser.

## UI reference (Flinzu office)
- Dark theme "office floor" board (2D is fine for MVP; isometric 3D nice-to-have)
- Zones: QUEUE/ROUTER, workers, REVIEW
- Agents as cards/avatars with status tags + confidence
- Top bar: LIVE, working / needs you / queued counts, optional cost
- Bottom: TEAM table + ACTIVITY log
- Human gate: when `needs_human`, red "needs you" + approve | edit | decline
- Decision panel: show choice options + confidence bars (next_worker)

## Event contract
Implement against `event-schema-v0.1.json` (attached).
- Bus fields only: actor / task / decision / artifact_ref
- Statuses: queued → running → waiting_approval → done | failed | blocked
- edit|approve|decline emit NEW events (never mutate)

## Stack (architect decision)
- Viz is **language-agnostic frontend** + event bus consumer
- Prefer: TypeScript + Vite/React (or Next), WebSocket or SSE from a small Go or Node event mock
- Demo mode: replay canned fee-backend pipeline events (merchant_config → settle → recharge_review → tg_notify) so the board moves without real services
- Deploy publicly (Vercel / Cloudflare Pages / similar). **Must return a live HTTPS URL.**

## Out of scope tonight
- Real fee microservices, Redis/MQ/ClickHouse wiring
- Jev decision model integration
- Full 3D isometric polish

## Done when
1. Public URL loads the board
2. Demo replay shows agents moving + at least one waiting_approval that can be approved in UI
3. Events conform to the schema
