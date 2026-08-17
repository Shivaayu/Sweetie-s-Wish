# Sweetie's Wish — Version 0.8

Persistent short-link preparation and branding cleanup.

- Keeps the seven games, effects, sounds, bloom atmosphere, mobile polish, saved form draft, and multilingual architecture intact.
- Replaces remaining old brand wording with `Sweetie’s Wish`.
- Replaces the old long self-contained share URL as the intended production flow with a persistent short-link architecture.
- Adds a Supabase Edge Function + Postgres schema under `../supabase/` for real share storage.
- Production links use a random 10-character slug such as `#wish=Q7k3mA91Zx`; the wish data is stored server-side instead of being packed into the URL.
- Human-friendly share codes look like `SW-ANAYA-A7K4` and resolve through the same backend.
- Keeps the old offline packing path only as a fallback while the backend is not configured.
- Version is now `0.8`.

See `../SUPABASE_SETUP.md` for the one-time backend setup. A real Supabase project is required before short links can work across different devices.
