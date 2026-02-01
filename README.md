# ADV3NT Music Marketplace

**ADV3NT** is a high-performance, hybrid music platform bridging Bitcoin Ordinals (Web3) and traditional event ticketing (Web2.5). Built with **Next.js 15**, **Supabase**, and a custom **Bitcoin HD wallet** infrastructure, it provides artists with a "True Black" monochrome ecosystem to sell limited-edition digital collectibles and real-world event access.

## 🚀 Project Overview

ADV3NT solves the fragmentation between digital ownership and physical experiences:
- **Music (Web3):** Artists create and sell tracks as limited-edition Bitcoin Ordinals using a custom Taproot escrow system.
- **Events (Web2.5):** A robust ticketing engine with QR-based verification, supporting both Stripe (Fiat) and native Bitcoin payments.
- **Experience:** A persistent, high-fidelity audio engine wrapped in a modern, gesture-driven V2 design system.

---

## 🛠 Tech Stack

### Frontend & UI
- **Framework:** Next.js 15.0.7 (App Router)
- **Styling:** Tailwind CSS + custom V2 Design System (Monochrome/True Black)
- **Animation:** Framer Motion (Layout transitions, vinyl record physics)
- **Audio:** Howler.js (Persistent global singleton player)

### Backend & Database
- **Platform:** Supabase (PostgreSQL) with Row Level Security (RLS)
- **Auth:** Supabase Auth + MFA (TOTP) and "Sudo Mode" for sensitive artist operations
- **Async Logic:** `pg_cron` managed job queues for ticket fulfillment and payment verification
- **Search:** GIN Indexes (`pg_trgm`) for high-performance fuzzy search across collections and artists

### Infrastructure & Payments
- **Bitcoin Infrastructure:** Custom HD wallet integration supporting BIP86 Taproot derivation for secure platform escrows.
- **Payments:** Unified revenue engine supporting Stripe and native Bitcoin (1-confirmation enforcement).
- **Notifications:** Transactional email pipeline via Resend.

---

## 🏗 Key Architectural Features

### 1. Proprietary Bitcoin Escrow
A non-custodial secondary market utilizing a **1-of-2 Taproot tree** (Platform leaf + Seller leaf). 
- Allows for trustless listings where sellers maintain refund rights until a purchase is co-signed by the platform.
- Automated funding checks via background job workers.

### 2. Hybrid Ticketing Engine
A "Web2.5" approach to live events:
- **Bouncer Verification:** Two-step "Tap to Confirm" QR verification prevents accidental redemptions.
- **Revenue Engine:** Automated primary sale splits (90/10) with a **Ghost Payee** feature—allowing artists to pay collaborators via email before the collaborator has even created an account.
- **Token-Gating:** Server-side RPCs calculate event discounts based on user-owned digital collectibles.

### 3. V2 "True Black" Design System
A native dark-mode UI focused on minimalism:
- **Persistent Player:** A singleton `AudioProvider` ensures music never stops during route transitions.
- **Mobile-First Navigation:** Gesture-driven "Now Playing" drawers and responsive grid layouts.
- **Vinyl Animation:** Canvas/CSS-based rotating vinyl component for an analog feel in a digital space.

---

## 📁 Directory Structure

```text
/app             # Next.js App Router (Legacy V1 + V2 Prototype)
/components      # V2 UI Primitives, Artwork Cards, and Player Shell
/lib             # Bitcoin ops (escrow/transaction builders), Server Services
/supabase        # SQL migrations, RLS policies, and RPC definitions
/hooks           # Custom logic for Audio, BTC pricing, and Auth Gates
```

---

## 🔒 Security & Compliance

- **Hardened RLS:** Every table is protected by strict Row Level Security with a hardened search path.
- **MFA/Sudo Mode:** Backend enforces AAL2 for sensitive operations, such as modifying payout addresses or disabling security features.
- **Asset Protection:** High-quality master files are stored in private Supabase buckets with on-demand ZIP packaging via a server-side packaging service.

---

**Production repositories are private for security reasons. I’m happy to grant read‑only access under NDA if helpful for technical diligence.**
