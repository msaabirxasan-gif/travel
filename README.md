# SafarLink — Travel Booking & Assistance Platform

> **Your Journey Starts Here.**

A responsive, production-oriented travel agency web application built for customers in **Somalia** and the global **Somali diaspora** (Mogadishu, Hargeisa, Garowe, Nairobi, Dubai, Istanbul, London, Minneapolis, Toronto, Columbus, etc.).

---

## 1. Key Capabilities & Architecture

- **Request-to-Book Flight Assistance**:
  - Flight requirements submission (origin, destination, departure/return dates, passenger breakdown: adults, children, infants, cabin class, flexible dates, diaspora luggage requirements).
  - Every flight inquiry is assigned a unique tracking reference code (`SL-FL-XXXXXX`).
  - Strict compliance: never displays artificial mock seat availability or fake airline booking references. Integrates via a clean service boundary ready for authorized GDS/NDC APIs (Amadeus, Sabre, Duffel).
- **Curated International Travel Packages**:
  - Packages tailored for Somali travelers: 14-Day Premium Umrah Pilgrimage, Istanbul Heritage & Bosphorus Discovery, Dubai Family & Desert Safari, Nairobi Medical & Health Wellness, Zanzibar Coastal Escape, and Kuala Lumpur.
  - Complete day-by-day itineraries, duration, hotel standards, included/excluded services, and USD pricing.
  - Public inquiry modal with instant reference code generation (`SL-PK-XXXXXX`).
  - Full Admin CRUD: create, edit, toggle published status, delete with confirmation modal, and manage itineraries.
- **Visa Consultation & Advisory**:
  - Document consultation request form (`SL-VA-XXXXXX`) for UAE (Dubai), Turkey (e-Visa / sticker), Kenya (eTA), and Saudi Arabia (Umrah).
  - Prominent official regulatory disclaimer that approval/refusal is determined solely by government immigration authorities.
- **Universal Customer Status Tracking**:
  - Lookup by reference number + customer phone or email verification.
  - Multi-stage visual timeline: `New` ➔ `Contacted` ➔ `Quoted` ➔ `Confirmed` ➔ `Completed`.
  - Quoted price in USD and assigned officer notes.
  - Direct 1-tap WhatsApp chat link prefilled with the reference number.
- **Protected Operations Admin Dashboard**:
  - Overview & KPIs: New Inquiries, Confirmed Bookings, Published Packages, Recorded Revenue vs Quoted Pipeline.
  - Real database aggregation clearly distinguishing verified received funds from active quotations.
  - Flight Requests manager with status update, live fare quote entry, agent assignment, and notes.
  - Package Inquiries manager.
  - Bookings & Passenger manifests with passport details.
  - Audit-compliant Payment Ledger with verification workflows (Hormuud EVC Plus, Telesom ZAAD, Dahabshiil, Bank Wire, Credit Card, Cash at office).
  - Customer contact message inbox with status filtering.
  - Financial & Operations Reports with authorized CSV export.
  - Site Settings (configurable business WhatsApp hotline, phone numbers, office address, service fees).
- **Somali & Global Diaspora UX**:
  - Multi-language switcher supporting **English**, **Af-Soomaali**, and **العربية (Arabic)**.
  - Deep navy (`#0A192F`), clean white, and teal accents (`#0D9488`).
  - Pre-seeded with realistic Somali airline routes (MGQ, HGA, GGR, DXB, IST, NBO, JED, MSP, LHR, YYZ).

---

## 2. Technology Stack

- **Frontend**: React 19, TypeScript, Tailwind CSS v4, Lucide React, React Router DOM v7
- **Backend**: Supabase PostgreSQL / Cloud
- **Storage**: Hybrid Data Layer (Supabase PostgreSQL client + persistent offline fail-safe store with pre-seeded data for immediate local evaluation)

---

## 3. Database Schema & Supabase Setup

The database schema and Row Level Security policies are located in `supabase/schema.sql`.

### Tables
1. `profiles`: user profiles and roles (`admin`, `staff`, `customer`).
2. `travel_packages`: curated packages, pricing, durations, image galleries, and publication flags.
3. `package_itineraries`: day-by-day itinerary records linked to packages.
4. `flight_requests`: request-to-book submissions with origin, destination, dates, passengers, and quotes.
5. `package_inquiries`: customer package booking inquiries.
6. `bookings`: confirmed reservations.
7. `booking_passengers`: passenger passport numbers, names, and nationalities.
8. `payments`: audit-compliant financial transactions with verification status and payment methods.
9. `contact_messages`: customer contact submissions.
10. `site_settings`: agency contact details, WhatsApp number, and service fees.
11. `audit_logs`: security and administrative change logs.

### Running Migrations in Supabase
1. Create a project at [supabase.com](https://supabase.com).
2. Go to the **SQL Editor** in the Supabase Dashboard.
3. Copy and paste the entire content of [`supabase/schema.sql`](supabase/schema.sql) and click **Run**.
4. Retrieve your **Project URL** and **Anon Key** from `Project Settings > API`.
5. Add them to your `.env` file:
   ```env
   VITE_SUPABASE_URL=https://your-project.supabase.co
   VITE_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
   ```

---

## 4. Local Development

```bash
# 1. Install dependencies
npm install

# 2. Start local development server
npm run dev

# 3. Compile and build for production
npm run build
```

### Fast Demo Evaluation
- Open the application in your browser (default `http://localhost:5173`).
- In the top bar or on the `/login` page, you can click **"Admin Demo"** or **"Customer Demo"** to evaluate the operations portal instantly without manual registration.

---

## 5. Production Deployment

### Option A: Vercel / Netlify
1. Connect your Git repository.
2. Build Command: `npm run build`
3. Output Directory: `dist`
4. Set Environment Variables:
   - `VITE_SUPABASE_URL`
   - `VITE_SUPABASE_ANON_KEY`

### Option B: Static Host / Docker / Nginx
Serve the compiled `dist/` directory with client-side fallback routing (`try_files $uri /index.html;`).

---

## 6. Regulatory & Ethical Compliance Notice
- SafarLink operates on a Request-to-Book model where ticket availability is independently verified.
- We do not display fake airline PNRs or guarantee foreign sovereign visa approvals.
- Raw credit card PAN details are never collected directly on custom forms.
