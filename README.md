# 💳 Payment Gateway Project

A full-stack **payment gateway simulation** that demonstrates real-world payment flows including payment creation, capture, refunds, background processing, and webhook retries.
The system includes a backend API, merchant dashboard, and an embeddable checkout widget.

> ⚠️ This project is for **learning and demonstration purposes only**. No real payments are processed.

---

## 📌 Features

* Payment creation & capture
* UPI and Card payment simulation
* Refund processing
* Webhook delivery & retry mechanism
* Background job processing using queues
* Merchant dashboard
* Embeddable checkout widget
* Fully Dockerized setup

---

## 📁 Project Structure

```text
payment-gatewayy/
├── backend/                # Node.js / Express API & Worker
│   ├── src/
│   ├── Dockerfile
│   ├── Dockerfile.worker
│   └── package.json
├── checkout-widget/        # React Checkout Widget
│   ├── src/
│   ├── webpack.config.js
│   └── package.json
├── dashboard/              # React Merchant Dashboard
│   ├── public/
│   ├── src/
│   └── package.json
├── database/               # Database initialization
│   └── init.sql
├── docker-compose.yml
└── README.md
```

---

## 🧩 Services Overview

| Service         | Container Name   | Port (Host:Internal) | Description                             |
| --------------- | ---------------- | -------------------- | --------------------------------------- |
| PostgreSQL      | `payment_db`     | `5432:5432`          | Stores users, transactions, and refunds |
| Redis           | `redis_gateway`  | `6379:6379`          | Job queues and caching                  |
| API             | `payment_api`    | `8000:8000`          | Main backend service                    |
| Worker          | `gateway_worker` | —                    | Processes async jobs and webhooks       |
| Checkout Widget | `checkout_cdn`   | `3001:3001`          | Serves checkout widget                  |

---

## ⚙️ Environment Variables

Configured in `docker-compose.yml` for API and Worker services.

| Variable                       | Default              | Description                        |
| ------------------------------ | -------------------- | ---------------------------------- |
| `NODE_ENV`                     | `development`        | Application environment            |
| `PORT`                         | `8000`               | API server port                    |
| `DATABASE_URL`                 | `postgresql://...`   | PostgreSQL connection              |
| `REDIS_URL`                    | `redis://redis:6379` | Redis connection                   |
| `TEST_MODE`                    | `"true"`             | Enables simulated payment behavior |
| `WEBHOOK_RETRY_INTERVALS_TEST` | `"true"`             | Short retry intervals for testing  |

---

## 🚀 Getting Started

### Prerequisites

* Docker
* Docker Compose

### Run the project

```bash
docker-compose up --build
```

### Access Services

* API: `http://localhost:8000`
* Checkout Widget: `http://localhost:3001`

---

## 📚 API Reference

**Base URL**

```
http://localhost:8000/api/v1
```

---

## 🔐 Authentication

All API requests require the following headers:

```http
x-api-key: YOUR_API_KEY
x-api-secret: YOUR_API_SECRET
```

---

## 💰 Payments

### Create Payment

`POST /payments`

```json
{
  "amount": 1000,
  "currency": "INR",
  "method": "card",
  "order_id": "order_12345",
  "vpa": "test@upi"
}
```

**Response**

```json
{
  "id": "pay_12345...",
  "status": "pending"
}
```

---

### Capture Payment

`POST /payments/:id/capture`

```json
{
  "id": "pay_12345...",
  "captured": true
}
```

---

## 🔄 Refunds

### Create Refund

`POST /payments/:id/refunds`

```json
{
  "amount": 500,
  "reason": "Customer request"
}
```

---

### Get Refund

`GET /refunds/:id`

---

## 🌐 Webhooks

### List Webhooks

`GET /webhooks`

### Retry Webhook

`POST /webhooks/:id/retry`

---

## 🛠️ Tech Stack

* **Backend:** Node.js, Express
* **Frontend:** React
* **Database:** PostgreSQL
* **Queue:** Redis, BullMQ
* **Containerization:** Docker, Docker Compose

---

## 📎 Use Cases

* Learning payment gateway architecture
* Understanding async job processing
* Webhook handling & retry logic
* Full-stack system design reference

---

## 📄 License

MIT License

---

## 🙌 Author

**Murali Nadipena**
GitHub: [https://github.com/23MH1A42B1](https://github.com/23MH1A42B1)
