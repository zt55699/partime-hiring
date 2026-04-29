# Changelog

## 2026-04-28 — Localize all images and fonts for China access

- Downloaded all 10 YouTube Jobs CDN photos and the 1 Unsplash avatar into `assets/images/` (~1.8MB total) and switched every `<img src>` to a relative path
- Removed Google Fonts (`fonts.googleapis.com` / `fonts.gstatic.com`) — both blocked from mainland China — and replaced Roboto with a system font stack including Chinese fallbacks (`PingFang SC`, `Hiragino Sans GB`, `Microsoft YaHei`)
- Replaced the serif `Roboto Serif` in the featured quote with a Georgia/Songti SC stack
- The page now has zero external CDN dependencies and renders fully offline

## 2026-04-28 — Landing page refactor to YouTube Jobs design

### index.html
- Rewrote the landing page to match the visual language of `youtube.com/jobs`
- **Hero**: diagonal white triangle (clip-path) over a full-bleed photo, dark text inside the white area, red "View openings" CTA
- **Impact stats**: "Help us grow brands and creators all over the world" — centered title plus a 4-column row of large red stat numbers with descriptions
- **Gallery**: horizontally scrollable image carousel ("Give the world a voice"), 5 portrait tiles, overlay prev/next circle buttons pinned to the gallery edges, short centered scroll-progress bar below
- **Featured quote**: "Set the stage" centered serif testimonial with avatar
- **Find your team**: 4 large image cards (2×2) for Ad Campaign Support, Channel Promotion, Influencer Outreach, Performance Analytics
- **Join our team**: numbered hire-process steps + form card on the right
- **Footer**: clean white with multi-column links
- All photography pulled from YouTube Jobs' own CDN (`lh3.googleusercontent.com`) for editorial-quality imagery
- Content updated from video-review tasks to ads / promotion / marketing tasks
- Form fields, honeypot, JS, and `/api/config` + `/api/submit` integration preserved unchanged

### admin.html
- Recolored login overlay, focus state, and login button from teal (`#0f766e`) to YouTube red (`#FF0000` / `#CC0000`) to match the new landing page palette
