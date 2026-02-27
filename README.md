# Zion Shores - Wave Booking App

A full-stack mobile app for booking surf sessions at the three world-class waves at Zion Shores surf park in Washington, Utah.

## Architecture

```
ZionShores/
├── App.tsx                    # Expo entry point
├── src/
│   ├── screens/               # 6 screens (Login, SignUp, Home, WaveDetail, BookingConfirmation, Bookings, Profile)
│   ├── components/            # Reusable UI (WaveCard, SessionSlot, Button, GradientBackground)
│   ├── services/              # Supabase, Auth, Bookings, Payments, Conditions
│   ├── hooks/                 # useAuth context
│   ├── navigation/            # React Navigation (tabs + stack)
│   ├── constants/             # Theme colors, wave data, pricing
│   └── types/                 # TypeScript interfaces
├── admin/                     # React web admin panel (Vite)
│   └── src/pages/             # Dashboard, Users, Bookings, WaveConditions
├── server/                    # Express API for Stripe payments
└── supabase/migrations/       # Database schema SQL
```

## Three Waves

| Wave | Skill Level | Capacity | Width | Height Range |
|------|------------|----------|-------|-------------|
| PerfectSwell Zion | Advanced | 20/session | 200ft | 3-8 ft |
| UNIT Dynamic Wave | Intermediate | 16/session | 164ft | 2-5 ft |
| UNIT Standing Wave | Beginner | 12/session | 60ft | 1-6 ft |

## Pricing

| Wave | Owner | Renter | Local |
|------|-------|--------|-------|
| PerfectSwell Zion | $100/hr | $200/hr | $200/hr |
| UNIT Dynamic Wave | $50/hr | $50/hr | $50/hr |
| UNIT Standing Wave | $50/hr | $50/hr | $50/hr |

## Priority Booking System

| Tier | Role | Booking Window |
|------|------|---------------|
| 1 (Highest) | Property Owner | 30 days ahead |
| 2 | Property Renter | 7 days ahead |
| 3 | Washington, UT Local | 1 day ahead |

Sessions: 5 per wave per day (7 AM - 12 PM), 1 hour each.
No general public access — only Owners, Renters, and verified Locals.

## Setup

### 1. Supabase

1. Create a project at [supabase.com](https://supabase.com)
2. Go to SQL Editor and run `supabase/migrations/001_initial_schema.sql`
3. Copy your project URL and anon key

### 2. Environment Variables

```bash
cp .env.example .env
# Fill in your Supabase URL, keys, and Stripe keys
```

### 3. Mobile App (Expo)

```bash
cd ZionShores
npm install
npx expo start
```

Scan QR code with Expo Go app, or press `w` for web.

### 4. Admin Panel

```bash
cd admin
npm install
npm run dev
# Opens at http://localhost:3001
```

### 5. Payment Server

```bash
cd server
npm install
npm run dev
# Runs at http://localhost:3002
```

### 6. Stripe

1. Create account at [stripe.com](https://stripe.com)
2. Get test keys from Dashboard > Developers > API keys
3. Add to `.env`

## Replit Setup

The project includes `.replit` and `replit.nix` for one-click deployment:

1. Upload the `ZionShores/` folder to a new Replit
2. Set environment variables in Replit Secrets
3. Click Run — the app starts in web mode

## User Flows

### Sign Up
1. Choose role (Owner / Renter / Local)
2. Enter name, email, password
3. Locals must upload ID for address verification

### Book a Wave
1. Browse 3 waves on home screen with live conditions
2. Tap wave → see details, specs, features
3. Pick date (limited by your booking window tier)
4. Pick available time slot
5. Review summary → Pay via Stripe
6. Get confirmation with booking ID

### Admin Panel
- Dashboard: User counts, booking stats, revenue
- Users: View all users, approve/reject local verifications, view ID docs
- Bookings: Filter by date and wave, view all booking details
- Wave Conditions: Update height, water temp, crowd level, open/closed status

## Tech Stack

- **Mobile**: React Native (Expo), TypeScript
- **Backend**: Supabase (PostgreSQL, Auth, Storage, RLS)
- **Payments**: Stripe
- **Admin**: React, Vite, React Router
- **API**: Express.js (Stripe integration)
