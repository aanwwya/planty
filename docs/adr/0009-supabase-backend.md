---
status: accepted
---

# Supabase is the v1 backend

Rootly uses Supabase for Postgres, authentication, photo storage, Row-Level Security, and PostGIS.

The domain is relational (Owners, Plants, Species, care logs, Growth Entries, reports, blocks), privacy is enforced per row, and discovery needs geographic queries. Postgres plus RLS matches those needs directly, and Supabase Auth supports Google, Apple, and email one-time codes. Firebase's document model would complicate relational queries and privacy rules; a custom API would add work before validation. The trade-off is vendor lock-in, limited by the fact that the data layer is standard Postgres.
