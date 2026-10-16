# Hoplink

A personal cloud shortcut hub with Supabase email/password authentication and owner-scoped cloud data.

## Features

- Email/password sign-up and sign-in, password reset, and sign-out
- Private, cloud-synced shortcuts
- Add, edit, delete, favorite, and open links
- Custom categories, emoji icons, accent colors, and descriptions
- Search, category/favorite filters, and grid/list layouts
- JSON import/export for backups
- Responsive layout for desktop and mobile
- Keyboard shortcuts: `N` adds a shortcut, `/` focuses search, and `Esc` closes dialogs

## Run locally

The app is preconfigured for the dedicated Hoplink Supabase project. From the repository root, run:

```bash
python -m http.server 8000
```

Then open http://localhost:8000. One-time publishing setup: open repository **Settings → Pages**, choose **GitHub Actions** as the build and deployment source, then open **Actions** and re-run the latest `Deploy Hoplink to GitHub Pages` workflow. The GitHub Actions API for this connection cannot enable the Pages site automatically. After that, pushes to `main` will deploy the root directory. The expected site URL is `https://bradleysouciercomputer.github.io/hoplink/`.

## Supabase

The `supabase/schema.sql` schema is already applied to the Hoplink project. It creates `public.hoplink_shortcuts`, enables RLS, grants data access to authenticated users, and includes four owner-scoped policies for reading, creating, updating, and deleting rows.

The app uses the project's publishable key, which is intended for browser use. Never put a `service_role` key or `sb_secret_` key in front-end code. RLS policies are required to protect user data.

For deployment, add your public site URL to Supabase **Authentication → URL Configuration → Redirect URLs**. If email confirmation is enabled, users will need to verify their email before signing in.

To use a different Supabase project, replace the project configuration in `index.html` and run `supabase/schema.sql` in that project's SQL editor.
