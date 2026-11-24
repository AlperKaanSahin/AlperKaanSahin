### Hey, I'm Alper

Recent software engineering graduate. I build backend systems, mobile apps, and lately games — mostly working with Node.js, React Native, C#, and Unity. I'd rather understand *why* something works than just get it working.

---

### What I've been building

**[Expiry](https://github.com/AlperKaanSahin/expiry)**

A marketplace app for near-expiry groceries — shops list discounted products before they go to waste, customers pick them up with a QR code. Solo project, backend to mobile UI, still in active development.

The part I'm most proud of isn't a feature — it's a mistake I fixed. I originally modeled customer/shop-owner/admin as separate app "modes" and wired navigation with ad-hoc state and imperative `navigate()` calls. It worked until it didn't — race conditions, wrong screens on notification taps, flicker between views. I ended up rebuilding it around a proper separation: identity (who you are), permissions (what you're allowed to do), and workspace (which experience you're currently in). Same account, instant switching, no re-login. It's a small thing conceptually, but it's the difference between code that happens to work and code you can reason about.

A few other things in there:

- Built the real payment flow on Iyzico's marketplace model — hosted checkout, per-shop submerchant onboarding, and escrow-style payouts that only release once the buyer confirms delivery by QR code. Added webhook signature verification (HMAC, independent of the checkout callback path) as a second, asynchronous line of defense against forged "payment succeeded" requests
- Event-driven notifications (order/shop status changes → in-app notification + real push via FCM, same event bus), including tap-to-navigate routing that respects the workspace model above
- Found and fixed a real database race condition: two concurrent requests could both reserve the last unit of stock. Fixed with row-level locking (`SELECT ... FOR UPDATE`) instead of a naive read-then-write
- Two-step pagination for the one endpoint where filtering depends on an aggregate (available stock), so I'm not loading full tables into memory
- JWT auth with refresh token rotation and rate limiting, plus a self-audit that turned up (and fixed) two real issues: an authorization gap that let a buyer skip QR verification and self-confirm their own delivery, and an upload endpoint trusting the client's claimed file type instead of the file's actual content
- Centralized error handling (custom `AppError` class + async wrapper) across the whole API, so internal errors never leak implementation details to clients
- CI via GitHub Actions for both backend and mobile — dependency validation, Expo config checks, and Jest unit tests focused on the logic I trust least, like the stock-locking and payment flow above

Still working on: Iyzico integration is fully working end-to-end in sandbox (submerchant onboarding, checkout, escrow payouts, webhook verification) — what's left is switching to live merchant credentials for production. Also continuing to expand test coverage beyond the highest-risk logic.

---

**[Forest Builder](https://github.com/AlperKaanSahin/ForestBuilder)**

A 3D mobile incremental game I'm building with Unity and C#. The core loop is simple: harvest resources, collect and sell them, buy upgrades, and gradually progress through the world.

I started this project to learn Unity and game development by building an actual game rather than a collection of small tutorials or prototypes. I'm taking it feature by feature, trying to understand the problems that appear as the game grows and designing around them when it makes sense.

So far I've built a generic resource system for Wood and Stone, procedural resource clusters inside hexagonal regions, inventory and selling, resource unlocks, and a reusable progression system for upgrades such as carrying capacity, harvesting power, and movement speed.

The next stages are focused on expanding the progression loop with new regions, resources, and eventually workers and automation. The goal is to take it beyond a learning project and release it as a real mobile game.

---

### Stack

**Backend & Mobile:** Node.js · Express · Sequelize · MySQL · React Native (Expo) · JWT · Firebase Cloud Messaging

**Game Development:** C# · Unity · URP

**Testing & Tools:** Jest · GitHub Actions · Git · Visual Studio

---

### Elsewhere

[LinkedIn](https://www.linkedin.com/in/alper-kaan-şahin-3341a228a/)
