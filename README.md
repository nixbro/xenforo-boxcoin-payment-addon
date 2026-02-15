# XenForo Boxcoin Crypto Payment Add-on — Accept Bitcoin, Ethereum & 30+ Cryptocurrencies

![Boxcoin Payment Integration for XenForo](https://raw.githubusercontent.com/nixbro/xenforo-boxcoin-payment-addon/main/%7B4F05B99A-1C15-4CA2-84D3-03254BC34431%7D.png)

[![XenForo 2.1+](https://img.shields.io/badge/XenForo-2.1%2B-blue?style=flat-square)](https://xenforo.com)
[![PHP 7.2+](https://img.shields.io/badge/PHP-7.2%2B-777BB4?style=flat-square&logo=php&logoColor=white)](https://php.net)
[![Boxcoin](https://img.shields.io/badge/Boxcoin-Powered-00a885?style=flat-square)](https://boxcoin.dev)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)

**XenForo payment add-on that auto-upgrades user groups when Boxcoin cryptocurrency payments complete. Encrypted checkouts, hardened webhook pipeline, full transaction logging. Zero fees, self-hosted, no third-party services.**

Built by [Nixnode](https://nixnode.dev) | Contact: [@nixnode on Telegram](https://t.me/nixnode)

---

## Why This XenForo Crypto Payment Add-on?

Most crypto payment solutions for forums cost $50–$200+ in license fees, lock you into third-party processors that take a cut of every transaction, and can freeze your funds without warning. This add-on is different:

- **Zero transaction fees** — Boxcoin runs on your own server
- **No third-party payment processors** — no KYC, no account freezes, no volume limits
- **Self-hosted & decentralized** — you control everything
- **Production-grade security** — encrypted checkouts, hardened webhooks, full audit trail

> Want this on your forum? **[Message me on Telegram](https://t.me/nixnode)**

---

## Features

### Automatic XenForo User Group Upgrades
Members pay with cryptocurrency and their primary user group is updated instantly upon payment confirmation. Map any XenForo user group to a USD price — support as many membership tiers as you need.

### Encrypted Checkout URLs
Every checkout link is cryptographically secured. The add-on encrypts the user ID and target group into the payment reference using Boxcoin's built-in `bxc_encryption()`, preventing tampering and ensuring the right user gets the right upgrade.

### Secure Webhook Processing
A dedicated callback controller handles Boxcoin's real-time payment notifications with a multi-step validation pipeline:
- Timing-safe secret verification (`hash_equals`)
- Payment amount validation against server-side configuration (tamper-proof)
- Duplicate transaction detection to prevent double-processing
- Target group existence checks before any database writes
- All error details logged server-side only — webhook callers receive opaque responses

### Accept Bitcoin, Ethereum, and 30+ Cryptocurrencies
Powered by Boxcoin's on-premises payment engine — accept BTC, ETH, DOGE, USDT, USDC, BNB, LTC, SHIB, LINK, BCH, ALGO, BAT, and all ERC-20 / BEP-20 tokens. No third-party payment processors, no transaction fees, no KYC.

### Conversation Notifications
Optionally send a private conversation to the user when their upgrade completes, letting them know their new membership is active. Configure which admin account sends the notification.

### Flexible Multi-Tier Group Pricing
Define pricing for any number of user groups with a simple `groupId:price` format. Run a $10 VIP tier and a $50 Premium tier simultaneously — no limits.

### Full Transaction Logging & Audit Trail
Every processed payment is recorded in a dedicated database table with the complete webhook payload, user ID, group assignment, amount, currency, and timestamps — full audit trail for accounting and dispute resolution.

### Guest Protection
Only registered, logged-in members can access checkout URLs. Guests are blocked at the controller level, preventing invalid payment references.

---

## How It Works

```
1. Member clicks "Upgrade" on your forum
         ↓
2. Add-on encrypts userId-groupId and redirects to Boxcoin payment page
         ↓
3. Member pays with Bitcoin, Ethereum, or any supported crypto
         ↓
4. Boxcoin confirms payment on blockchain → sends webhook to your forum
         ↓
5. Add-on validates: secret → status → duplicates → amount → group
         ↓
6. User group upgraded → transaction logged → member notified
```

The entire flow is automatic and completes within seconds of blockchain confirmation.

---

## Architecture

Clean two-controller design — no templates, no cron jobs, no admin controllers. Minimal footprint, small attack surface.

| Controller | Purpose |
|---|---|
| **Pay Controller** | Validates group & price, encrypts user identity, redirects to Boxcoin |
| **Callback Controller** | Receives webhook, validates payment, upgrades user group, logs transaction |

---

## XenForo Admin Panel Configuration

All settings managed through **ACP > Options > Boxcoin**:

| Setting | Description |
|---|---|
| **Boxcoin Path** | Absolute server path to your Boxcoin installation |
| **Boxcoin Pay URL** | Public URL to Boxcoin's `pay.php` |
| **Group Prices** | User group-to-price mappings (e.g., `5:10\|6:25`) |
| **Send Alert** | Toggle conversation notifications on upgrade |
| **Alert User ID** | Admin user ID that sends notification conversations |

---

## Security

| Measure | Description |
|---|---|
| **Encrypted references** | User and group IDs encrypted via `bxc_encryption()` before leaving your server |
| **Server-side price validation** | Amounts verified against ACP config, not URL parameters |
| **Timing-safe verification** | `hash_equals()` prevents timing attacks on webhook secret |
| **Duplicate detection** | Boxcoin transaction ID checked before processing |
| **Opaque error responses** | No internal details exposed — errors go to XenForo server log only |
| **CSRF-exempt endpoint** | Properly configured for machine-to-machine webhook communication |
| **Integer comparison** | Amounts converted to cents to avoid floating-point precision issues |

---

## Requirements

| Requirement | Version |
|---|---|
| XenForo | 2.1.0+ |
| PHP | 7.2+ |
| [Boxcoin](https://boxcoin.dev) | Installed on the same server |

---

## Supported Cryptocurrencies

Bitcoin (BTC), Ethereum (ETH), Dogecoin (DOGE), Tether (USDT), USD Coin (USDC), BNB, Litecoin (LTC), Shiba Inu (SHIB), Chainlink (LINK), Bitcoin Cash (BCH), Algorand (ALGO), Basic Attention Token (BAT), and all ERC-20 / BEP-20 tokens.

---

## Custom XenForo Add-on Development

This add-on was designed and built from scratch by **Nixnode** — a full-stack developer experienced in building SaaS platforms, custom integrations, and production-grade software.

Need a custom XenForo add-on? Payment integrations, automation workflows, API connectors, or entirely new features — built to your exact specifications.

**[Message me on Telegram @nixnode](https://t.me/nixnode)** | [nixnode.dev](https://nixnode.dev)

---

## License

This project is licensed under the [MIT License](LICENSE).

---

*Version 1.2.0 | Built by [Nixnode](https://nixnode.dev)*
