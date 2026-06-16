# OSP Sales University

**Recruit, train, certify, and develop elite sales professionals through OSP Sales University.**
A branded recruiting system, AI coaching platform, sales academy, reporting center, and student development OS — built for the OSP vision. *My Team. My Family. My OSP.*

The entire app is one self-contained React component (`OSPSalesUniversity.jsx`) so it builds clean and can't break on a missing import.

---

## 1. Run locally

```bash
npm install
npm run dev      # http://localhost:5173
npm run build    # production build → dist/
npm run preview  # preview the production build
```

Requires Node 18+.

## 2. Add AI keys (optional)

The app ships with a clean AI service abstraction (`OSP_AI`) covering `generateText`, `roleplayResponse`, `scoreRoleplay`, `generateRecruitingPost`, `generateLessonContent`, `generateReportInsight`, `generateMarketingCopy`, and `generateCoachingPlan`.

- **No key →** every AI feature runs in **Demo AI Mode** with strong mock responses (clearly badged in the UI).
- **Key present →** AI features call the live model automatically.

Set in `.env` (local) or in Vercel env vars:

```
VITE_ANTHROPIC_API_KEY=sk-ant-...
# or
VITE_OPENAI_API_KEY=sk-...
```

> ⚠️ **Security:** a browser-only build exposes any client key. For production, proxy AI calls through a serverless function (e.g. a Vercel Function) and keep the key server-side. The abstraction is structured so you can swap the fetch target without touching the UI.

See `.env.example` for all variables.

## 3. Deploy to Vercel

1. Push this folder to a GitHub repo.
2. In Vercel: **Add New → Project → Import** the repo.
3. Framework preset: **Vite**. Build command `npm run build`, output dir `dist` (already set in `vercel.json`).
4. Add any env vars from `.env.example` under **Settings → Environment Variables**.
5. **Deploy.**

## 4. Connect OSPSU.com

1. Vercel project → **Settings → Domains → Add** → enter `ospsu.com` and `www.ospsu.com`.
2. At your domain registrar, add the DNS records Vercel shows:
   - `A` record for `ospsu.com` → Vercel's IP, **or** an `ALIAS/ANAME` to `cname.vercel-dns.com`.
   - `CNAME` for `www` → `cname.vercel-dns.com`.
3. Wait for DNS to propagate; Vercel issues SSL automatically.
4. Set `www.ospsu.com` as the primary domain so canonical/OG URLs match `index.html`.

Metadata (title, description, Open Graph, Twitter, canonical) already points at `https://www.ospsu.com/`.

## 5. Test credentials

Login → one-click role buttons (password is `password`):

| Role | Email |
|------|-------|
| Super Admin | `admin@ospsu.com` |
| Recruiter / Manager | `manager@ospsu.com` |
| Sales Student / Agent | `student@ospsu.com` |

## 6. What's live vs. demo

**Fully operational (no external services):**
- Landing page + aptitude gate; **landing signups persist to `localStorage` and appear in the Recruiting pipeline**.
- Recruiting Command Center: pipeline moves, applicant profiles/notes, job posts (create/edit/duplicate/archive), AI job generator, campaigns, interviews + scorecards, landing-page manager, reports with **real CSV export**.
- Courses + video lessons/transcripts, timed Tests + certificates, Sales Drills roleplay + scoring, Badge vault, Leaderboard + profiles, Board Room, Tasks, Resources, Profile.

**Live if a key is provided, otherwise demo:**
- All AI features (AI Coach, Recruiting AI, etc.) via the `OSP_AI` abstraction.

**Demo / mock until external credentials are wired:**
- Emails (welcome, certificate, recruiting) are previewed/logged, not sent — add an email provider to go live.
- External job-board posting is an integration-ready workflow (copy optimized post / mark as posted / track source), not live API posting.
- Persistence is `localStorage` (browser). Add a database for multi-device/multi-user persistence.

## 7. Replace the OSP logo

The brandmark is a placeholder component, `<OSPLogo />` / `<Logo />`, in `OSPSalesUniversity.jsx`. To use the official logo:

1. Drop the file in a `public/` folder, e.g. `public/osp-logo.png`.
2. In the `Logo` component, replace the gold "OSP" tile with:
   ```jsx
   <img src="/osp-logo.png" alt="OSP" style={{ height: dim }} />
   ```
3. Replace the favicon `<link rel="icon">` in `index.html` with `public/favicon.png`, and add `public/og-image.png` for social sharing.

## 8. Future integrations

- **Auth + database:** Supabase (logins + persistence across devices/users).
- **Live AI proxy:** serverless function holding the OpenAI/Anthropic key.
- **Email/SMS:** Resend (email) + Twilio (text) for invites, reminders, certificates.
- **Job boards:** Indeed/ZipRecruiter/LinkedIn posting APIs.
- **Video hosting:** Mux/Vimeo for real OSP TV and course lessons.

---

© One Source Provider · OSP Sales University · Founded by Dean Elali · Dearborn, MI
