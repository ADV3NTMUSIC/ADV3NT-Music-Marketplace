This README is designed to provide a professional overview of the **ADV3NT Music Marketplace**, highlighting its unique hybrid architecture and sophisticated tech stack based on your `CLAUDE.md`.

***

# ADV3NT Music Marketplace

**ADV3NT** is a high-performance, hybrid music platform that bridges the gap between Bitcoin Ordinals (Web3) and traditional event ticketing (Web2.5). Built with **Next.js 15**, **Supabase**, and native **Bitcoin** integration, it provides artists with a "True Black" monochrome ecosystem to sell limited-edition digital collectibles and real-world event access.

## 🚀 Project Overview

ADV3NT solves the fragmentation between digital ownership and physical experiences:
- **Music (Web3):** Artists mint and sell tracks as limited-edition Bitcoin Ordinals using a custom Taproot escrow system.
- **Events (Web2.5):** A robust ticketing engine with QR-based verification, supporting both Stripe (Fiat) and native Bitcoin payments.
- **Experience:** A persistent, high-fidelity audio engine wrapped in a modern, gesture-driven V2 design system.

---

## 🛠 Tech Stack

### Frontend
- **Framework:** Next.js 15.0.7 (App Router)
- **Styling:** Tailwind CSS + Custom V2 Design System (Monochrome/True Black)
- **Animation:** Framer Motion (Layout transitions, vinyl animations)
- **Components:** Radix UI primitives
- **Audio:** Howler.js (Persistent global player)

### Backend & Database
- **Platform:** Supabase (PostgreSQL)
- **Auth:** Supabase Auth with MFA (TOTP) + Sudo Mode for sensitive actions
- **Database Logic:** Row Level Security (RLS), GIN Indexes for fuzzy search, and `pg_cron` for background job processing
- **Storage:** Supabase Storage with strict RLS for private high-quality audio assets

### Blockchain & Payments
- **Bitcoin:** LaserEyes + `bitcoinjs-lib`
- **Escrow:** 1-of-2 Taproot tree (Platform + Seller leaves) for trustless secondary listings
- **Payments:** Stripe integration for fiat; native Bitcoin (1-confirmation enforcement) for crypto

---

## 🏗 Key Architectural Features

### 1. Hybrid Ticketing System
A "Web2.5" approach to events. While the platform leverages blockchain for music, ticketing uses a high-speed database engine for discovery and fulfillment.
- **Bouncer Verification:** Two-step "Tap to Confirm" QR verification prevents accidental redemptions.
- **Revenue Engine:** Automated primary sale splits (90/10) with a "Ghost Payee" feature to pay collaborators via email before they even create an account.

### 2. Taproot Escrow Marketplace
A non-custodial secondary market for Ordinals.
- Uses **BIP86** path derivation.
- Platform co-signs transactions only after 1-block confirmation is verified by a background `pg_cron` job.

### 3. V2 Design System (The "True Black" Aesthetic)
A native dark-mode UI focused on minimalism and performance:
- **Persistent Player:** A singleton `AudioProvider` ensures music never stops during navigation.
- **Physics-Based UI:** Framer Motion used for slide-up drawers, vinyl record rotations, and snap-physics carousels.

---

## 📁 Directory Structure

```text
/app             # Next.js App Router (Main & V2 Prototype)
/components      # V2 UI Primitives, Cards, and Audio Player
/lib             # Bitcoin scripts, Escrow utils, and Server Services
/supabase        # SQL migrations and RLS policies
/hooks           # Custom logic for Audio, BTC Pricing, and Auth Gates
```

---

## 🛠 Development

### Quick Start
```bash
npm install
npm run dev              # Start local development
npm run generate-keys    # Setup HD wallet keys for escrow
```

### Database Updates
```bash
npx supabase gen types typescript --project-id <id> > src/types/supabase.ts
```

---

## 🔒 Security & Compliance

- **Hardened RLS:** All tables utilize Row Level Security with a hardened search path.
- **MFA/Sudo Mode:** Step-up authentication required for changing payout addresses or disabling security features.
- **Asset Protection:** High-quality master files are stored in private buckets with on-demand ZIP packaging via a backend service.

---

**Production repositories are private for security reasons. I’m happy to grant read‑only access under NDA if helpful for technical diligence.**
