# Global Jobs & Scholarships Hub

> Har masle ka digital hal — Hafiz Digital Solution

## Short summary / Mukhtasar khulasa

Global Jobs & Scholarships Hub ek platform hai jo berozgari aur ghurbat kam karne mein madad karta hai. Ye logon ko national aur international jobs, scholarships, fellowships aur internships se connect karta hai.

The Global Jobs & Scholarships Hub connects people with national and international jobs, scholarships, fellowships, internships and educational funding.

**Live Hub (Muse Space):** Phase 1–7 complete hain — full platform Muse Space mein chal raha hai. Ye GitHub repo us ka GitHub-ready package hai, is mein static demo aur documentation hai.

## Phase 1–7 — kya ban gaya hai

- **Phase 1 — Foundation:** Responsive homepage, Jobs / Scholarships / International / Remote listings, search aur filters, opportunity detail with AI match score aur official Apply link, User Dashboard, Admin Dashboard, English / Urdu with RTL, light / dark theme, navy-and-gold brand.
- **Phase 2 — Backend / Auth:** Real registration, login / logout, password reset, email verification (placeholder), 8 roles — Super Admin, Admin, Data Manager, Content Manager, Social Media Manager, Regional Admin, Registered User, Guest User. Full profile, multiple education records, work experience, skills, preferences, CV upload (PDF / DOCX) with AI extraction aur review-and-confirm step. Audit logs. Pehla registered account Super Admin banta hai — koi default password nahi hai.
- **Phase 3 — Data Collection Engine:** 20 sources ka directory (FPSC, PPSC, HEC, Rozee.pk, LinkedIn, Indeed, UN Careers, Chevening, DAAD, Fulbright aur bhi), connectors (RSS, JSON API, website listing, CSV import, manual entry), test connection, collection jobs / logs / retry, duplicate detection, data validation, quality score 0–100, Admin Review Queue — bina verify ke kuch publish nahi hota.
- **Phase 4 — Matching v2 + Regional + Notifications:** Hard eligibility alag, soft match % alag. For You page, Regional Engine (Pakistan ke 7 provinces / territories, 43 cities, plus worldwide), deduplicated in-app notifications, Application Tracker with 7 statuses.
- **Phase 5 — AI Content Studio:** 9 content types (Facebook, Instagram, Carousel, Reels, TikTok, YouTube Shorts, Detailed Video, LinkedIn), 7 languages, images 1:1 / 4:5 / 16:9, video packs 9:16 / 1:1 / 16:9 with voiceover text, SRT subtitles, captions, hashtags. Full approval workflow.
- **Phase 6 — Social Media Center:** YouTube, Facebook, Instagram, TikTok, LinkedIn, OAuth status, publishing adapters, schedule / publish / retry, Publishing Calendar (daily / weekly / monthly).
- **Phase 7 — Analytics + Android-ready:** Real analytics events, charts, CSV / Excel export, Apply click aur completed application alag, Android-ready plan (Capacitor / Flutter, same backend).

## Kya test ho chuka hai / What is tested

Full end-to-end test pass hua hai — ~45 server action checks plus browser probe, zero console errors.

Tested aur pass:
- Registration, login, password reset, suspend par login block, staff gating
- Profile, education, CV upload aur AI extraction (8 fields)
- Matching v2, regions, save / tracker, notifications aur preferences
- Content Studio, video pack, image spec, approval → schedule → publish attempt
- Collection Engine, duplicate detection, CSV import, source connection test
- Analytics — Apply click ko application nahi gina gaya
- Browser mein Home, Jobs, Detail, Dashboard, Admin, Studio, Social, Calendar, Analytics — Urdu RTL aur dark mode bhi

**Note:** Is repo ka `index.html` sirf static demo hai. Full Hub ka live test Muse Space mein hua hai.

## Abhi bhi kya chahiye — credentials / What still needs credentials

Ye cheezein placeholder hain, live kaam ke liye credentials chahiye honge. Koi secret is repo mein nahi hai, aur kabhi commit na karein.

- **SMTP** — email verification aur password reset ke liye
- **Google Gemini API** — AI matching aur content generation ke liye
- **TTS provider** — multilingual voiceover audio ke liye
- **Image generation provider** — promotional graphics ke liye
- **S3-compatible storage** — media files ke liye
- **OAuth app credentials** — YouTube, Facebook, Instagram, TikTok, LinkedIn par live posting ke liye
- **WhatsApp Business + Android push (FCM)** — notifications ke liye

Environment variables mein rakhein, kabhi frontend code ya GitHub mein secret na likhein.

## Demo data — ahem

Is repo aur live Hub ke sample records par **"DEMO SAMPLE — not verified"** badge hai. Ye live jobs nahi hain, sirf UI testing ke liye hain. Real records Admin panel se add karein.

## Files

- `index.html` — static demo landing page (GitHub Pages ke liye)
- `README.md` — ye file
- `ARCHITECTURE.md` — FastAPI / PostgreSQL schema aur folder structure
- `DEPLOY.md` — GitHub Pages aur full deployment guide

## Contact

Contact: hafizcci@gmail.com | Facebook: Hafiz Digital Solutions
