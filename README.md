# Studywell · CFA Level I

A responsive static app for CFA Level I study planning. Signed-in users store progress privately in Supabase; GitHub Pages serves the app. Google Calendar integration is optional and requires a Google OAuth web client ID.

## Repository layout

- `site/` — published web app and public browser configuration
- `supabase/migrations/` — per-user progress table and row-level security
- `.github/workflows/pages.yml` — publishes `site/` to GitHub Pages

## Setup

See [SETUP.md](SETUP.md). The Supabase project and private per-user data table are provisioned. Never put a Supabase secret/service-role key, password, or OAuth client secret in `site/config.js`. The browser uses only a publishable key with row-level security enabled.
