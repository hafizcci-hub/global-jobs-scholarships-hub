# Deploy — Global Jobs & Scholarships Hub

## Ahem baat: GitHub Pages static-only hai

**GitHub Pages par full Hub nahi chalta.**

GitHub Pages sirf static HTML / CSS / JavaScript serve karta hai — is mein Python, FastAPI, PostgreSQL, login, database ya background jobs nahi chalte. Is liye:

- `index.html` GitHub Pages par chalega — ye sirf demo landing page hai.
- Full Hub (auth, database, matching, collection, content studio, social posting, analytics) ke liye alag backend hosting chahiye.

Ye dawa na karein ke full backend GitHub Pages par chal raha hai.

## Option A — Static demo on GitHub Pages (is repo ke liye)

1. GitHub par naya repo banayein, masalan `global-jobs-scholarships-hub`.
2. Is folder ki files push karein:
   - `index.html`
   - `README.md`
   - `ARCHITECTURE.md`
   - `DEPLOY.md`
3. Repo Settings → Pages → Source: Deploy from a branch → Branch: `main`, Folder: `/ (root)`.
4. Save karein. Kuch minute mein site live ho jayegi:
   `https://<username>.github.io/global-jobs-scholarships-hub/`
5. Ye sirf demo hai — login, save, apply aur admin is static page par kaam nahi karte.

## Option B — Full Hub live karna (recommended)

Frontend, backend aur database alag-alag host karein, ek hi central database ke sath.

### 1. Frontend — Vercel

- React / TypeScript app ko Vercel par deploy karein.
- Env var: `VITE_API_URL=https://<backend-url>`

### 2. Backend — Railway / Render

- Python FastAPI app ko Railway ya Render par deploy karein.
- Env vars (values yahan na likhein — hosting dashboard mein set karein):
  - `DATABASE_URL` — PostgreSQL connection string
  - `JWT_SECRET` — lamba random secret
  - `GEMINI_API_KEY`
  - `SMTP_HOST`, `SMTP_PORT`, `SMTP_USER`, `SMTP_PASSWORD`, `SMTP_FROM`
  - `TTS_PROVIDER`, `TTS_API_KEY`
  - `IMAGE_PROVIDER`, `IMAGE_API_KEY`
  - `S3_ENDPOINT`, `S3_BUCKET`, `S3_ACCESS_KEY`, `S3_SECRET_KEY`
  - `YOUTUBE_CLIENT_ID`, `YOUTUBE_CLIENT_SECRET`
  - `FACEBOOK_APP_ID`, `FACEBOOK_APP_SECRET`
  - `INSTAGRAM_APP_ID`, `INSTAGRAM_APP_SECRET`
  - `TIKTOK_CLIENT_KEY`, `TIKTOK_CLIENT_SECRET`
  - `LINKEDIN_CLIENT_ID`, `LINKEDIN_CLIENT_SECRET`
  - `WHATSAPP_TOKEN`, `FCM_SERVER_KEY`

### 3. Database — Managed PostgreSQL

- Railway / Render / Neon / Supabase se managed PostgreSQL lein.
- Alembic migrations chalakar schema banayein: `alembic upgrade head`
- Backup aur recovery on rakhein.

### 4. Android — Capacitor / Flutter

- Same backend URL use karein.
- Release build se pehle RTL aur login / CV / search test karein.

## Checklist — live karne se pehle

- [ ] Koi secret repo mein nahi hai — sirf env vars mein hai
- [ ] Pehla account register karke Super Admin bana liya
- [ ] SMTP test kiya — verification email aa raha hai
- [ ] OAuth apps banaye — har platform ke credentials set hain
- [ ] Sample records par "DEMO SAMPLE — not verified" badge hai
- [ ] HTTPS on hai
- [ ] Backup on hai

## Contact

Contact: hafizcci@gmail.com | Facebook: Hafiz Digital Solutions
