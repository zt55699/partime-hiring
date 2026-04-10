# Work From Home Positions - Landing Page

A single-page web application for recruiting part-time remote workers for AI data annotation tasks.

## Live Demo

https://zt55699.github.io/partime-hiring/

## Features

- **Responsive Design** - Works on desktop, tablet, and mobile devices
- **Three Main Sections**
  - Hero/Intro with key benefits
  - Testimonials from current annotators
  - Application form with validation
- **Google Sheets Integration** - Form submissions are sent to a Google Sheet in real time via Apps Script
- **Anti-Spam Protection** - Honeypot field + server-side validation to block bots
- **Online Support** - Button linking to Telegram for live support
- **No Dependencies** - Pure HTML, CSS, and JavaScript
- **Fast Loading** - Single file, minimal external resources (only Unsplash images)

## Sections

### 1. Introduction
Presents the value proposition: flexible remote work, fair pay ($15-35/hr), no experience required. Includes feature cards highlighting key benefits.

### 2. Stories
Six testimonials from different backgrounds:
- Graduate student
- Stay-at-home parent
- Software developer (side gig)
- Retired teacher
- Freelance writer
- College student

### 3. Application Form
Collects:
- Full name, phone, age, country
- Weekly availability
- Languages spoken

Submissions are stored in a Google Sheet via Google Apps Script webhook.

## Setup

### Google Sheets Integration

1. Create a Google Sheet with headers: `Timestamp | Full Name | Phone | Age | Country | Availability | Languages`
2. Go to **Extensions > Apps Script** and add the webhook script (see `doPost` function)
3. Deploy as a Web App (Execute as: Me, Access: Anyone)
4. Paste the deployment URL into `GOOGLE_SCRIPT_URL` in `index.html`

### Local Development

No build process required. Just open `index.html` in a browser.

```bash
python3 -m http.server 8080
```

## Deployment

Hosted on GitHub Pages. Push to `main` branch to deploy.

## License

MIT
