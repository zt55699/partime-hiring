# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Single-page recruiting landing page (`index.html`) plus password-protected admin (`admin.html`) backed by a Flask API (`app.py`). Two-file frontend, no build step, no JS framework.

## Architecture

```
Browser ──HTTPS──▶ Caddy (:443) ──▶ Gunicorn 127.0.0.1:8080 ──▶ app.py (Flask)
  GET  /, /admin.html        → static files from STATIC_DIR
  POST /api/submit           → append row to data/submissions/YYYY-MM-DD.xlsx
  GET  /api/config           → returns {support_url, support_icon}
  POST /api/config           → auth required, partial update
  GET/DELETE /api/files[...] → auth required, list/download/delete daily xlsx
```

- Auth: `Authorization: Bearer <password>`; server SHA-256s and compares against `PASSWORD_HASH` in `app.py`. Default password `admin123`. To rotate: `echo -n "newpw" | sha256sum`, replace `PASSWORD_HASH`, restart.
- Submissions are written to one Excel file per UTC-date with a `write_lock` (single-worker gunicorn assumed). Headers in `HEADERS` constant must match the form fields in `index.html`.
- Honeypot: form sends a `website` field; non-empty → silently return success.
- Config persists to `data/config.json`; the admin UI stores the password in `sessionStorage` and sends it on every authed call.

## Key files

- `app.py` — Flask backend (all API routes, auth decorator, file I/O).
- `index.html` — landing page; calls `/api/submit` and `/api/config`. Auto-prefixes a saved support URL with `https://` if scheme missing (avoids relative-link breakage).
- `admin.html` — admin UI; logs in by POSTing to `/api/config` to verify the password server-side, then calls authed endpoints with the stored bearer.
- `DEPLOYMENT.md` — full server runbook (SSH, filesystem layout, ops, incidents). Read this before touching deploy.
- `README.md` and `SOP.md` describe the **legacy** Google Sheets / Apps Script architecture that has been replaced by the Flask backend. Treat them as historical unless explicitly migrating back.

## Common commands

```bash
# Run backend locally (binds to :80, may need sudo)
pip install flask openpyxl gunicorn
python3 app.py

# Or just serve static frontend without backend
python3 -m http.server 8080
```

No tests, no linter, no build.

## Deploying

Two independent deploy targets — pick the right one:

1. **GitHub Pages** (`https://zt55699.github.io/partime-hiring/`) — auto-deploys on push to `main`. Frontend-only; the Pages copy of `index.html`/`admin.html` will hit `/api/...` paths that don't exist there, so Pages is effectively a preview of the static shell.
2. **Production server** (`https://amadw.com`) — separate VM running Flask + Caddy. Deploy via `scp` per `DEPLOYMENT.md`. Static HTML changes are live immediately; `app.py` changes require re-running `/mnt/partime-hiring/start.sh`. The host has a failing read-only system disk — see DEPLOYMENT.md "Known Issues" before any ops work.

When changing the form schema, update **all three**: the form fields in `index.html`, the `required`/row construction in `app.py:submit`, and `HEADERS` in `app.py`.
