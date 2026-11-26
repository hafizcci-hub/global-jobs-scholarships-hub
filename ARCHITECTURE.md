# Architecture — Global Jobs & Scholarships Hub

## Stack

- **Frontend:** React, TypeScript, Tailwind CSS — responsive, RTL / LTR, light / dark
- **Backend:** Python, FastAPI, REST API
- **Database:** PostgreSQL
- **ORM:** SQLAlchemy
- **Migrations:** Alembic
- **Background jobs:** Celery + Redis
- **AI:** Google Gemini API (configurable, env var se)
- **Media:** FFmpeg, configurable TTS provider, configurable image generation provider
- **Storage:** S3-compatible object storage
- **Android:** Flutter / Capacitor — same backend aur central database
- **Auth:** JWT, OAuth integrations, salted + hashed passwords

> GitHub Pages par sirf static demo chalta hai. Full backend is repo mein nahi chalta — dekhein `DEPLOY.md`.

## Folder structure (target)

```
global-jobs-scholarships-hub/
├── frontend/                 # React + TypeScript + Tailwind
│   ├── src/
│   │   ├── pages/            # Home, Jobs, Scholarships, Detail, Dashboard, Admin
│   │   ├── components/       # Cards, Filters, Forms, Charts, Calendar
│   │   ├── i18n/             # en, ur, ar, pa, skr, ps + RTL
│   │   └── lib/              # API client, auth, matching helpers
├── backend/                  # Python FastAPI
│   ├── app/
│   │   ├── api/              # auth, users, opportunities, sources, content, social, analytics
│   │   ├── models/           # SQLAlchemy models
│   │   ├── services/         # matching, collection, content, notifications
│   │   ├── connectors/       # RSS, JSON API, website, CSV, manual
│   │   └── workers/          # Celery tasks
│   ├── alembic/              # migrations
│   └── requirements.txt
├── mobile/                   # Flutter / Capacitor (Android-ready)
├── docs/
│   ├── README.md
│   ├── ARCHITECTURE.md
│   └── DEPLOY.md
└── index.html                # Static demo landing page (GitHub Pages)
```

## PostgreSQL schema plan

### Users

- `users` — id, email, password_hash, role, status, created_at, updated_at
- `user_profiles` — user_id FK, full_name, mobile, date_of_birth, gender, country, province, district, city, nationality, profile_picture
- `user_roles` — role name, description
- `permissions` — role, module, action
- `education_records` — user_id FK, level (Matric / Intermediate / Bachelor / Master / MPhil / PhD / Diploma), institution, year, grade
- `work_experiences` — user_id FK, designation, organization, start_date, end_date, description
- `skills` — id, name
- `user_skills` — user_id FK, skill_id FK, level
- `user_preferences` — user_id FK, interests (jobs / scholarships / internships / fellowships), job types, preferred countries / cities / industries / education levels / salary / languages (JSON / join tables)
- `user_documents` — user_id FK, type (CV), file_key, extracted_text, confirmed_at
- `user_saved_opportunities` — user_id FK, opportunity_id FK, saved_at

### Opportunities

- `opportunities` — id, title, type (job / scholarship / internship / fellowship), category, organization_id FK, country, province, district, city, qualification, experience, age_limit, salary_or_funding, deadline, status, verification_status, source_id FK, quality_score, created_at, updated_at
- `job_details` — opportunity_id FK, employment_mode, job_type, vacancies, age_limit, nationality_requirement
- `scholarship_details` — opportunity_id FK, degree_level, funding_type (fully / partial), tuition_coverage, stipend, accommodation, travel_allowance, ielts / toefl
- `organizations` — id, name, logo_key, website, type
- `opportunity_skills` — opportunity_id FK, skill_id FK
- `opportunity_sources` — opportunity_id FK, source_url, apply_url, official_website
- `opportunity_status_history` — opportunity_id FK, old_status, new_status, changed_by, changed_at

### Data collection

- `data_sources` — id, name, type (website / api / rss), url, category, country, region, frequency, enabled, connector_key
- `source_categories` — id, name
- `collection_jobs` — id, source_id FK, status, started_at, finished_at, error
- `collection_logs` — job_id FK, level, message, created_at
- `raw_imports` — id, source_id FK, raw_payload, normalized_json, quality_score, status (pending / approved / rejected / duplicate)
- `duplicate_records` — raw_import_id FK, matched_opportunity_id FK, reason
- `verification_records` — opportunity_id FK, verified_by, decision, note, decided_at

### AI

- `ai_matching_results` — user_id FK, opportunity_id FK, match_percent, eligibility_status, matched_criteria, missing_requirements, explanation, computed_at
- `ai_generated_content` — opportunity_id FK, type, language, body, status, created_by
- `content_translations` — content_id FK, language, body
- `content_media` — content_id FK, media_type, format, storage_key, provider_status

### Social media

- `social_accounts` — id, platform, display_name, handle, account_id, scopes, oauth_status, created_by
- `content_approvals` — content_id FK, status (Draft / Pending Review / Approved / Rejected / Scheduled / Publishing / Published / Failed), decided_by, decided_at, note
- `publishing_schedules` — content_id FK, account_id FK, scheduled_at, language, country, region, category, status
- `social_publications` — schedule_id FK, platform, publication_id, publication_url, published_at, status, error_message
- `social_analytics` — publication_id FK, views, reach, likes, shares, comments, recorded_by, recorded_at

### Geography

- `countries` — id, name, code
- `regions` — id, country_id FK, name, type (province / state)
- `cities` — id, region_id FK, name, district

### System

- `languages` — code, name, rtl (true / false)
- `notifications` — user_id FK, type, title, body, read_at, created_at
- `application_tracker` — user_id FK, opportunity_id FK, status (Interested / Saved / Applied / Interview / Selected / Rejected / Withdrawn), application_date, notes, reminder_date
- `audit_logs` — user_id FK, action, entity, entity_id, created_at
- `system_settings` — key, value

## Rules

- Har foreign key indexed hai, timestamps har table mein hain.
- Expired opportunities auto-expire hote hain, delete nahi hote.
- Unverified opportunities kabhi publish nahi hote — Review Queue se guzarte hain.
- AI eligibility ki guarantee nahi deta — hard rules aur soft match alag hain.
- Secrets kabhi code mein nahi — sirf environment variables.
- Ek hi central database — koi disconnected ya duplicate database nahi.
