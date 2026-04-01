# UtilityX Backend

The UtilityX Backend powers a smart peer-to-peer utility marketplace that allows users to buy, sell, and manage digital utilities such as airtime, mobile data, and bill payments.

This service handles authentication, wallet management, marketplace operations, transaction processing, and integrations with external providers.

---

# Overview

The backend is responsible for:

* User authentication and authorization
* Wallet balance and escrow management
* Marketplace listings (P2P trading)
* Trade execution and transaction tracking
* Airtime resale processing
* Utility bill payments (electricity, water, TV)
* Integration with payment and telecom APIs

---

# Tech Stack

* Node.js
* NestJS (recommended) or Express
* PostgreSQL (database)
* Redis (caching, queues)
* REST API

---

# Project Structure

src/
├── modules/
│   ├── auth/              # Authentication (JWT, login, register)
│   ├── users/             # User profile management
│   ├── wallet/            # Wallet logic (balance, escrow)
│   ├── marketplace/       # Listings (create, fetch, expire)
│   ├── trades/            # Trade execution engine
│   ├── airtime/           # Airtime resale flow
│   ├── bills/             # Utility bill payments
│   └── notifications/     # Alerts (email, push, SMS)
│
├── integrations/
│   ├── payments/          # Payment gateways (Paystack, etc.)
│   └── utilities/         # Airtime/data APIs
│
├── database/
│   ├── entities/          # ORM models (User, Wallet, Listing, etc.)
│   ├── migrations/        # DB migrations
│   └── seeds/             # Seed data
│
├── common/
│   ├── guards/            # Auth guards
│   ├── filters/           # Error handling
│   ├── interceptors/      # Logging, response formatting
│   └── utils/             # Helper functions
│
├── config/                # Environment config
├── jobs/                  # Cron jobs (expiry, retries)
└── main.ts                # App entry point

---

# Core Modules Explained

## Auth Module

Handles user registration, login, and JWT authentication.

Endpoints:

* POST /auth/register
* POST /auth/login
* GET /auth/me

---

## Wallet Module

Manages user balances and escrow.

Features:

* Fund wallet
* View balance
* Lock/unlock funds for trades

---

## Marketplace Module

Handles P2P listings.

Features:

* Create listing
* Fetch listings
* Expiry logic (auto-expire based on time)

---

## Trades Module (Core Engine)

Handles the full transaction lifecycle:

Flow:

1. Buyer initiates purchase
2. System checks balance
3. Funds are locked (escrow)
4. Utility API is called
5. If successful:

   * Seller is credited
6. If failed:

   * Buyer is refunded

---

## Airtime Module

Handles airtime-to-cash conversion.

Flow:

1. User submits airtime request
2. System provides recipient number
3. User sends airtime
4. Transaction is verified
5. Wallet is credited

---

## Bills Module

Handles utility payments:

* Electricity
* Water
* TV subscriptions

Flow:
User enters details → backend calls provider API → returns success/token

---

# Database Schema (Core Tables)

users
wallets
listings
trades
transactions
airtime_sales
bill_payments

---

# API Integrations

* Payment Gateway: Paystack (wallet funding)
* Telecom APIs: Reloadly or similar providers

---

# Background Jobs

Located in /jobs/

Includes:

* Expire listings after deadline
* Retry failed transactions
* Send notifications

---

# Running the Project

## Install dependencies

```bash
npm install
```

## Start development server

```bash
npm run start:dev
```

---

# Environment Variables

Create a `.env` file:

```env
DATABASE_URL=
JWT_SECRET=
PAYSTACK_SECRET_KEY=
UTILITY_API_KEY=
REDIS_URL=
```

---

# Responsibilities of Backend

* Ensure transaction reliability
* Maintain data integrity
* Provide secure APIs
* Handle integrations with external services
* Manage escrow and trade execution

---

# MVP Scope

This backend supports the MVP features:

* User authentication
* Wallet funding and balance
* Data/airtime purchase
* Marketplace listings
* Trade execution (escrow logic)
* Airtime resale
* Bill payments

---

# Future Improvements

* Blockchain escrow integration (Stellar Soroban)
* AI-based price recommendations
* Advanced fraud detection
* Real-time notifications (WebSockets)

---

# Contribution

Please follow the CONTRIBUTING.md guidelines when contributing to this project.
