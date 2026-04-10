# Work From Home Positions - Landing Page

A single-page web application for recruiting part-time remote workers for AI data annotation tasks.

## Live Demo

- **Landing Page**: https://zt55699.github.io/partime-hiring/
- **Admin Panel**: https://zt55699.github.io/partime-hiring/admin.html

## Features

- **Responsive Design** - Works on desktop, tablet, and mobile devices
- **Three Main Sections**
  - Hero/Intro with key benefits
  - Testimonials from current annotators
  - Application form with validation
- **Google Sheets Integration** - Form submissions stored in a Google Sheet in real time via Apps Script
- **Admin Panel** - Password-protected page to configure settings and view submissions
  - Configure online support URL (stored in Google Sheet Config tab)
  - Configure and view embedded Google Sheet
- **Anti-Spam Protection** - Honeypot field + server-side validation to block bots
- **Online Support** - Button with dynamically configurable URL (defaults to Telegram)
- **No Dependencies** - Pure HTML, CSS, and JavaScript

## Architecture

```
Landing Page (index.html)
  ├── Form submit ──POST──> Google Apps Script ──> Google Sheet (Sheet1)
  └── Load support URL ──GET──> Google Apps Script ──> Google Sheet (Config tab)

Admin Page (admin.html)
  ├── Save support URL ──POST──> Google Apps Script ──> Google Sheet (Config tab)
  ├── Save sheet embed URL ──POST──> Google Apps Script ──> Google Sheet (Config tab)
  └── View submissions via embedded Google Sheet iframe
```

- **Apps Script URL** — Hardcoded in both `index.html` and `admin.html`
- **Support URL & Sheet Embed URL** — Stored in Google Sheet's Config tab, accessible from any browser

## Setup

See `SOP.md` for detailed setup instructions (in Chinese).

### Quick Start

1. Create a Google Sheet with headers: `Timestamp | Full Name | Phone | Age | Country | Availability | Languages`
2. Go to **Extensions > Apps Script**, paste the script code (see SOP.md)
3. Deploy as a Web App (Execute as: Me, Access: Anyone)
4. The Apps Script URL is hardcoded in `index.html` and `admin.html`
5. Log in to the admin panel (default password: `admin123`) to configure support URL and view submissions

### Local Development

No build process required. Just open `index.html` in a browser.

```bash
python3 -m http.server 8080
```

## Deployment

Hosted on GitHub Pages. Push to `main` branch to deploy.

## License

MIT
