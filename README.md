### Hey, I'm Alper 👋

Recent software engineering graduate. I build backend systems and full-stack apps — mostly Node.js and React Native — and I'd rather understand *why* something works than just get it working.

---

What I've been building — [Expiry](https://github.com/AlperKaanSahin/expiry)

A marketplace app for near-expiry groceries — shops list discounted products before they go to waste, customers pick them up with a QR code. Solo project, backend to mobile UI, still in active development.

The part I'm most proud of isn't a feature — it's a mistake I fixed. I originally modeled customer/shop-owner/admin as separate app "modes" and wired navigation with ad-hoc state and imperative `navigate()` calls. It worked until it didn't — race conditions, wrong screens on notification taps, flicker between views. I ended up rebuilding it around a proper separation: identity (who you are), permissions (what you're allowed to do), and workspace (which experience you're currently in). Same account, instant switching, no re-login. It's a small thing conceptually but it's the difference between code that happens to work and code you can reason about.

A few other things in there:

* Event-driven notifications (order/shop status changes → in-app notification + real push via FCM, same event bus), including tap-to-navigate routing that respects the workspace model above
* Found and fixed a real database race condition: two concurrent requests could both reserve the last unit of stock. Fixed with row-level locking (`SELECT ... FOR UPDATE`) instead of a naive read-then-write
* Two-step pagination for the one endpoint where filtering depends on an aggregate (available stock), so I'm not loading full tables into memory
* JWT auth with refresh token rotation, rate limiting, and a couple of security bugs I found and fixed along the way (a missing auth check on a shop route, a user-enumeration issue in password reset)
* Centralized error handling (custom `AppError` class + async wrapper) across the whole API, so internal errors never leak implementation details to clients
* CI via GitHub Actions for both backend and mobile app — dependency validation, Expo config checks, and unit tests (Jest) for the business logic I trust least, like the stock-locking above

Still working on: Iyzico payment integration is architecturally done (submerchant model, checkout flow) but blocked on a business registration requirement on their end — and expanding test coverage beyond the highest-risk logic.

---

### Stack

Node.js · Express · Sequelize · MySQL · React Native (Expo) · JWT · Firebase Cloud Messaging · Jest · GitHub Actions

---

### Elsewhere

[LinkedIn](https://www.linkedin.com/in/alper-kaan-şahin-3341a228a/)
