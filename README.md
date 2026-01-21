# Local Payment Gateway Platform

A fully dockerized **payment gateway development environment** featuring an API service, async worker, admin dashboard, and checkout experiences. Built for **local testing and learning**, with seeded demo credentials and simulated payment flows.

---

## Technology Overview
- **Backend API**: Node.js + Express
- **Async Processing**: BullMQ with Redis
- **Database**: PostgreSQL 15
- **Worker Service**: Handles payments, refunds & webhooks
- **Admin Dashboard**: React app (Port 3000)
- **Checkout Demo**: React-based checkout UI (Port 3001)
- **Embeddable Checkout Widget**
- **Infrastructure**: Docker & Docker Compose

---

## Running Services & Ports
| Service | URL / Port |
|-------|------------|
| API Server | http://localhost:8000 |
| Dashboard | http://localhost:3000 |
| Checkout Demo | http://localhost:3001 |
| PostgreSQL | localhost:5432 |
| Redis | localhost:6379 |

**Postgres Credentials**
- DB Name: `payment_gateway`
- Username: `gateway_user`
- Password: `gateway_pass`

---

## Getting Started (Docker)
1. *(Optional)* Copy environment file:
   ```bash
   cp .env.example .env
   ```
2. Build and start all services:
   ```bash
   docker-compose up -d --build
   ```
3. Verify API health:
   ```bash
   curl http://localhost:8000/health
   ```
4. Launch dashboard: http://localhost:3000
5. Open checkout demo: http://localhost:3001

---

## Demo Merchant Credentials (Preloaded)
- **Merchant Email**: test@example.com
- **API Key**: key_test_abc123
- **API Secret**: secret_test_xyz789
- **Merchant UUID**: 550e8400-e29b-41d4-a716-446655440000
- **Webhook Secret**: whsec_test_abc123

> These credentials are for **local testing only**.

---

## API Reference (Common Routes)
### System
- `GET /health` — Service health check

### Orders
- `POST /api/v1/orders`
- `GET /api/v1/orders/:id`
- `GET /api/v1/orders/:id/public`

### Payments
- `POST /api/v1/payments`
- `POST /api/v1/payments/:id/capture`
- `POST /api/v1/payments/public`
- `GET /api/v1/payments/:id`
- `GET /api/v1/payments`

### Refunds
- `POST /api/v1/payments/:id/refunds`
- `GET /api/v1/refunds/:id`

### Webhooks
- `GET /api/v1/merchant/webhook`
- `POST /api/v1/merchant/webhook`
- `POST /api/v1/merchant/webhook/regenerate`
- `GET /api/v1/webhooks`

### Testing Utilities
- `GET /api/v1/test/merchant`
- `GET /api/v1/test/jobs/status`

---

## Backend Scripts
Located in the backend service:
- `npm start` — Start API server
- `npm run dev` — API with live reload
- `npm run worker` — Run background worker

---

## Development Notes
- Redis connection defaults to `redis://redis:6379` inside Docker
- Payment results are **mocked** using environment flags
- Delays and success rates are configurable for testing scenarios
- For non-Docker usage, ensure `DATABASE_URL` and `REDIS_URL` are set correctly

---

## 📦 Purpose
This project is designed for **learning, experimentation, and demo use** — not for production payment processing.

Happy hacking! 💳⚙️

