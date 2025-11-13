# Okecbot: Distributed System Architecture

## 1.0 Introduction

This document offers a comprehensive overview of the Okecbot distributed system architecture. Its main objective is to describe how the various component repositories and services interact to deliver a complete, privacy-focused browser profile AI agent manager to a secure peer-to-peer marketplace for browser automation contractual services.

This is a foundational guide for any contributor in the Okecbot GitHub organisation. Whether you're extending the browser AI agent desktop app or optimizing the marketplace, understanding the full picture ensures every change strengthens the deliberate chain.

## 2.0 Architectural Philosophy

Okecbot system follows a deliberately decoupled architecture where components communicate via REST APIs, secure WebSockets, and encrypted sync protocols. This design delivers:

- **Local Execution by Default**: 99.9% of automation runs on the user's machine — zero data leaves unless explicitly synced to user-controlled storage (Drive, SFTP, etc.).
- **Separation of Concerns**: Each repository has one clear responsibility.
- **Scalability**: Horizontal scaling for web services; vertical scaling for desktop (1,000 profiles on a single laptop).
- **Resilience**: Failure in one component (e.g., marketplace outage) never breaks local automation.

## 3.0 System Components & Repositories

The Okecbot ecosystem is composed of the following core components, each in its own repository within the organisation.

### 3.1 okecbot-desktop-app (Private)
- **Responsibility**: A native desktop application that runs browser profile AI agent locally.
- **Technology**: Node.js + Electron Js + custom Chromium.
- **Key Features**:
  - Advanced Stealth Features (retained browser sessions, proxy rotation, fingerprint spoofing, captcha solvers)
  - Advanced browser profile AI agents for multiple profiles (Max 250P/ 500P/ 1000P — 250/500/1,000 profiles)
  - AI Task Execution (Gemini/OpenAI/Claude/Grok API integration)
  - Manual Workflow Mode: Visual recorder + drag-and-drop scripting
  - Sync & Backup: Google Drive, iCloud, Dropbox, custom SFTP (end-to-end encrypted)

- **Input**: API key, user generated browser profiles, workflows and proxies.
- **Output**: Executed automations, local logs, synced profiles

### 3.2 okecbot-web-api (Private)
- **Responsibility**: Central nervous system — authentication, billing, marketplace logic, license validation.
- **Technology**: Pure OOP PHP 8.3 + MySQL 8.0 + MongoDB 7.0 + Redis 7.2
- **URL**: api.okecbot.com
- **Key Features**:
  - Webhook delivery for instant bot deployment
  - Hardware-bound license keys + JWT
  - Tier management (250P/ 500P/ 1000P)
  - Marketplace escrow + 10% commission
  - Abuse detection + rate limiting
- **Input**: Requests from desktop, web clients, marketplace
- **Output**: JSON responses, database persistence

### 3.3 okecbot-marketplace-client (Private)
- **Responsibility**: P2P marketplace for automation services and leased sessions.
- **Technology**: Vanilla PHP + Tailwind CSS + Alpine.js
- **URL**: p2p.okecbot.com
- **Key Features**:
  - Gig listing: Custom workflows, engagement boosts, ad revenue packages
  - Leased sessions: Rent logged-in accounts (Instagram, TikTok, etc.) — zero password sharing
  - Escrow + timed leases (hourly/daily/weekly)
  - One-click "Deploy to Desktop" with secure token
  - Merchant dashboard with /merchant/withdraw

### 3.4 okecbot-web-home (Private)
- **Responsibility**: Marketing and brand showcase.
- **Technology**: Vanilla PHP + Tailwind CSS
- **URL**: www.okecbot.com
- **Features**: 
  - Display the features of the okecbot browser AI agent desktop app.
  - Display products and services.
  - Display pricing.
  - Display contact information.
  - Display legal information.

### 3.5 okecbot-web-admin-client (Private)
- **Responsibility**: Internal admin portal for support and operations.
- **Technology**: Vanilla PHP + Tailwind CSS
- **URL**: admin.okecbot.com
- **Features**: User lookup, license management, dispute resolution, live support queue

### 3.6 okecbot-web-user-client (Private)
- **Responsibility**: User control panel.
- **Technology**: Vanilla PHP + Alpine.js
- **URL**: dashboard.okecbot.com
- **Features**:
  - API key management (create/revoke)
  - Connected devices (accept/disconnect computers)
  - Referral earnings view
  - Virtual account funding for marketplace purchases
  - Live support tickets/chat


### 3.7 okecbot-compile-assets (Public)
- **Responsibility**: Build resources and binaries for compiling desktop app from source.

### 3.8 okecbot-public-library (Public)
- **Responsibility**: Knowledge base, docs, SDKs, examples.

## 4.0 Data Flow Example (Typical User Journey)

1. **User Launches Desktop App**
   - App validates license against okecbot-web-api → unlocks tier (e.g., Max 2G = 500 profiles)
   - Loads groups from local + synced backup (Drive/SFTP)

2. **User Funds Virtual Account**
   - In dashboard.okecbot.com → funds via Paystack/Stripe → virtual account balance increases
   - In the browser AI agent desktop app → user can use the virtual account balance to purchase higher tier plans (e.g., 250P, 500P, 1000P)
- In the browser AI agent desktop app → user can purchase proxies directly from okecbot
- In the browser AI agent desktop app → user can purchase leased profiles or automation gigs on the p2p market place

3. **User Buys Leased Session or Workflow**
   - Browses p2p.okecbot.com → purchases (e.g., "100 Instagram accounts — 24h lease")
   - Payment from virtual account → 10% commission deducted
   - Secure token + session files pushed to desktop via WebSocket and sftp.

4. **User Runs Automation**
   - User launches desktop app, selects proxy chain/pool, browser workflows and browser profile groups
   - AI engine uses Gemini/OpenAI to interact with the workflows and execute the automation as a real user would.

5. **Seller Withdraws Earnings**
   - In p2p.okecbot.com/merchant/withdraw → requests payout
   - okecbot-web-api releases escrow → bank/PayPal

6. **Support Interaction**
   - User opens ticket in dashboard → live chat to admin.okecbot.com
   - Support views session (with permission) → resolves

## 5.0 System Integration Points

### 5.1 Authentication & Licensing
- Desktop → okecbot-web-api (hardware-bound key + JWT)
- Web clients → session cookies + 2FA
- Marketplace requires active license + virtual account balance

### 5.2 Real-time Communication
- Desktop ↔ Marketplace: WebSocket for instant deployment
- Dashboard ↔ Admin: Server-Sent Events for live support

### 5.3 Sync & Backup
- Desktop → User-chosen storage APIs (zero-knowledge encryption)

### 5.4 Error Handling & Monitoring
- Local logs + optional cloud upload
- Sentry for crashes; custom alerts for failed deployments



*Last updated: November 07, 2025*  
*Okecbot — Built by DCSSP, Abuja, Nigeria | RC: 2006105*