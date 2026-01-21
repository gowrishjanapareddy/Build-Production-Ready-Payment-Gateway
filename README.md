# Payment Gateway

A containerized payment-gateway stack with API, background worker, dashboard, and checkout experiences. Includes seeded test credentials and fake payment processing for local development.

## Stack
- Backend API (Node/Express, BullMQ + Redis, Postgres)
- Worker (async jobs for payments/webhooks/refunds)
- Dashboard (React, served on port 3000)
- Checkout page (React demo, served on port 3001)
- Checkout widget (embed-ready package)
- Postgres 15, Redis 7

## Services & Ports
- API: http://localhost:8000
- Dashboard: http://localhost:3000
- Checkout: http://localhost:3001
- Postgres: localhost:5432 (db: payment_gateway, user: gateway_user, pass: gateway_pass)
- Redis: localhost:6379

## Quick Start (Docker)
1) Copy env example if needed: `cp .env.example .env` (optional; defaults work).
2) Build & start: `docker-compose up -d --build`
3) Check health: `curl http://localhost:8000/health`
4) Open dashboard: http://localhost:3000
5) Open checkout demo: http://localhost:3001

## Test Credentials (seeded)
- Merchant email: test@example.com
- API key: key_test_abc123
- API secret: secret_test_xyz789
- Merchant ID: 550e8400-e29b-41d4-a716-446655440000
- Webhook secret: whsec_test_abc123

## Useful API Endpoints
- Health: GET /health
- Orders: POST /api/v1/orders, GET /api/v1/orders/:id, GET /api/v1/orders/:id/public
- Payments: POST /api/v1/payments, GET /api/v1/payments/:id, POST /api/v1/payments/:id/capture, POST /api/v1/payments/public, GET /api/v1/payments
- Refunds: POST /api/v1/payments/:id/refunds, GET /api/v1/refunds/:id
- Webhooks: GET /api/v1/merchant/webhook, POST /api/v1/merchant/webhook, POST /api/v1/merchant/webhook/regenerate, GET /api/v1/webhooks
- Test helpers: GET /api/v1/test/merchant, GET /api/v1/test/jobs/status

## Scripts (backend)
- `npm start` — start API
- `npm run dev` — API with nodemon
- `npm run worker` — start worker

## Notes
- Queue connections use Redis at `REDIS_URL` (default redis://redis:6379 in Docker).
- Fake payment outcomes are controlled by env flags (TEST_PAYMENT_SUCCESS, success rates, processing delays).
- For custom envs, set DATABASE_URL and REDIS_URL appropriately before running.