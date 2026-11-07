# Maharashtra Desha CRM - fixes (Nov 2026)

## STEP 1 - run the database migration (required)
Supabase dashboard > SQL Editor > New query > paste the contents of
`supabase/migrations/20261107120000_pricing_grid_payments_fixes.sql` > Run.
(It also repairs old quick-bookings whose advance was lost, and backfills payment history.)

## STEP 2 - set your trip prices
Trips tab > hover a trip card > pencil icon (Edit trip) > fill the price table:
one row per package option (e.g. "Mumbai", "Pune", "Sleeper train"), columns Quad / Triple / Double (per person),
Couple (per COUPLE), Single (per person). Add the peak surcharge per person and tick GST included or not.
Old passengers with Rs 0 need Edit passenger (pencil) once so their price recalculates.

## What changed
- Quick Booking: advance is split across passengers and saved as payments; price from trip grid;
  "Fixed total" mode for family/couple deals; discount per person; payment date; balance due date;
  seat check; fuzzy trip match (kokan = Konkan) by name + date; asks before creating duplicate trips.
- Paste parser: "Name -25", "Name (25)", "Name, 25"; date ranges (24/12/26-28/12/26); two phone numbers;
  sharing (quad/triple/double/couple/single); payment date; Rs.12,000/- amounts.
- Trips: Edit Trip, price grid editor, per-trip Revenue / Collected / Due on every card, seat warning.
- Payments tab: Add Payment (installments) with history, delete entry; receipts list every installment.
- Leads: Convert creates ALL passengers (pax), discount, optional fixed group total, saves advance as payments; booked-trips match by phone fixed.
- Calendar: trips created there get a price too (edit later in Trips).
- Branding: Trailhead -> Maharashtra Desha everywhere; sample GSTIN/address cleared (set yours in Settings).
- Optional login: set VITE_REQUIRE_LOGIN=true in .env, create a user in Supabase > Authentication,
  log in, THEN run supabase/OPTIONAL_lock_database_after_login.sql (locks the database to logged-in users).
