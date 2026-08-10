### Hey, I'm Alper 👋

Recent software engineering graduate. I build backend systems and full-stack apps — mostly Node.js and React Native — and I'd rather understand *why* something works than just get it working.

---

### What I've been building — [Expiry](https://github.com/AlperKaanSahin/expiry)

A marketplace app for near-expiry groceries — shops list discounted products before they go to waste, customers pick them up with a QR code. Solo project, backend to mobile UI, still in active development.

The part I'm most proud of isn't a feature — it's a mistake I fixed. I originally modeled customer/shop-owner/admin as separate app "modes" and wired navigation with ad-hoc state and imperative `navigate()` calls. It worked until it didn't — race conditions, wrong screens on notification taps, flicker between views. I ended up rebuilding it around a proper separation: identity (who you are), permissions (what you're allowed to do), and workspace (which experience you're currently in). Same account, instant switching, no re-login. It's a small thing conceptually but it's the difference between code that *happens* to work and code you can reason about.

A few other things in there:
- Event-driven notifications (order/shop status changes → in-app notification + real push via FCM, same event bus)
- Two-step pagination for the one endpoint where filtering depends on an aggregate (available stock), so I'm not loading full tables into memory
- JWT auth with refresh token rotation, rate limiting, and a couple of security bugs I found and fixed along the way (a missing auth check on a shop route, a user-enumeration issue in password reset)

Still working on: real payment integration (Iyzico), a few pre-launch security passes, and yes — actual tests.

---

### Stack

Node.js · Express · Sequelize · MySQL · React Native (Expo) · JWT · Firebase Cloud Messaging

---

### Elsewhere

[LinkedIn](https://www.linkedin.com/in/alper-kaan-şahin-3341a228a/)
