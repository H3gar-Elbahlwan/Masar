# MASAR — Technical Architecture (Revision 2: complete graduation project)

**Status:** planning only. Nothing here has been implemented, and the approved prototype design is unchanged.
**Companion docs:** `DATABASE_SCHEMA.md`, `IMPLEMENTATION_ROADMAP.md`, `FEATURE_STATUS.md`, `TRACK_CATALOG.md`, `ROADMAP_CONTENT_STRATEGY.md`, `FIGMA_DESIGN_HANDOFF.md`.
**Legend:** **[Confirmed]** stated by the project owner · **[Recommended]** my proposal, needs your approval.

> **What changed in Revision 2.** MASAR is a **complete** graduation project, not a three-track MVP. The platform must cover **19 tracks in 6 categories** with real content for each (`TRACK_CATALOG.md`). Content must be **data-driven** and editable by administrators (§14). Software development (by the project owner, on her laptop, with Claude assisting) and the Figma design (by a teammate, for another course) are **independent workstreams** (§15). Sections 1, 12, 13 were rewritten; sections 10.1, 10.2, 4, 8 were extended; new sections 14 and 15 were added. Everything else is unchanged from Revision 1.

---

## 1. Goals and constraints

**[Confirmed]**
- Deliver a **fully functional multi-track platform**: landing, track exploration and details, RIASEC assessment, recommendations, Taster Labs and interactive scenarios, roadmaps, learning resources, progress, achievements, local opportunities, user profiles, authentication, admin dashboard, English/Arabic, responsive layouts.
- **Preserve the approved prototype** exactly (see the preservation contract in `FEATURE_STATUS.md`). No redesign.
- Track content is **data, not hardcoded in React components**; adding a track or resource must be straightforward.
- Use a **relational** database; support many tracks, categories, multiple roadmaps per track, multiple stages and resources, per-user progress, assessment attempts, labs and attempts, achievements, opportunities, and admin content management.
- Do not fabricate resources or claim unverified resources are verified.

**[Recommended]**
- Prefer managed services and few moving parts, because a small team builds and maintains everything.
- Treat **content production as a first-class workstream** with its own tooling (admin dashboard, import, verification), since it is likely the largest effort.

---

## 2. Stack and decisions

| Layer | Choice | Why |
|---|---|---|
| UI framework | **React 18 + TypeScript** | As requested. A port is required because the prototype is vanilla JS (see §5). |
| Build tool | **Vite** (SPA) | Simple, fast, deploys cleanly on Vercel. See §2.1 for Vite vs Next.js. |
| Routing | **React Router** | Gives every screen a URL and back-button support (the prototype has neither). |
| Server state | **TanStack Query** | Caching, loading/error states, mutations with optimistic updates for task toggles. |
| Styling | **Keep the existing hand-written CSS** (global stylesheet first, split per component later) | There is no Tailwind in the approved prototype. Converting to Tailwind would risk visual drift and violates "do not redesign". |
| Animation | **Keep CSS keyframes + IntersectionObserver** (wrapped in a `useReveal` hook) | These are the "existing animation implementation". A library such as Motion can be added later only where it clearly helps. |
| i18n | **i18next + JSON files** for UI strings; **`*_en` / `*_ar` columns** for database content | Keeps UI text out of components and content editable by admins. |
| Backend | **Supabase** | Postgres, Auth, Storage, Row Level Security, RPC functions, optional Edge Functions. |
| Database | **PostgreSQL** (via Supabase) | Relational model fits the domain. |
| Auth | **Supabase Auth** (email + password; Google optional) | Built-in password reset and email confirmation. |
| Storage | **Supabase Storage** | Only for avatars and, optionally, lab images. Not needed for MVP. |
| Hosting | **Vercel** (frontend) | Preview deployment per pull request. |
| Version control | **Git + GitHub** | Pull-request review fits the team's pair/mob working style. |

### 2.1 Vite SPA or Next.js?
Recommendation: **Vite SPA.** The app is mostly authenticated and interactive; search-engine indexing matters only for the landing page. A SPA is simpler for a student team. If public SEO becomes important later, the landing page and track pages can be moved to Next.js without changing the database. **This is a decision for you to approve** (see §13).

### 2.2 Where I deviate from the brief, and why
1. **"Existing styling framework / animation libraries"** → none exist; the plan keeps the existing CSS approach instead of introducing new frameworks.
2. **Edge Functions** → not planned for MVP. Scoring and progress run as Postgres functions (RPC), which are easier to test and keep all rules next to the data.
3. **Storage** → deferred; no MVP feature needs file uploads.

---

## 3. System overview

```
┌─────────────────────────────┐
│ Browser (React + TS SPA)    │  Vercel (static hosting + preview deploys)
│  • React Router             │
│  • TanStack Query           │
│  • i18next (EN/AR, RTL)     │
└──────────────┬──────────────┘
               │ HTTPS, anon key + user JWT
┌──────────────▼──────────────┐
│ Supabase                    │
│  • Auth (JWT)               │
│  • PostgREST (auto API)     │──► all tables protected by RLS
│  • RPC: submit_quiz,        │──► scoring, grading, XP, achievements
│    submit_lab_answer, ...   │
│  • PostgreSQL               │
│  • Storage (later)          │
└─────────────────────────────┘
```

Rule: **the browser never holds the service-role key.** It uses only the public (anon) key and the signed-in user's token. All authority comes from Row Level Security and security-definer functions.

---

## 4. Proposed frontend structure

```
masar/
├─ src/
│  ├─ app/            # router, providers, layout shell (sidebar / bottom nav / top bar)
│  ├─ pages/          # Home, Explore, TrackDetail, Quiz, Results, Labs, LabPlayer,
│  │                  # Roadmap, StageDetail, Resources, Opportunities, Dashboard, Progress, Achievements,
│  │                  # Saved, Auth, Profile, Settings, Admin/* (tracks, roadmaps, resources, quiz, labs, opportunities, users, import)
│  ├─ components/     # ProgressBar, RadarChart, ProgressRing, RouteHero, Toast, NavItem, ...
│  ├─ features/       # quiz/, labs/, roadmap/, opportunities/, auth/  (hooks + queries per feature)
│  ├─ lib/            # supabase client, i18n setup, reveal hook, format helpers
│  ├─ styles/         # tokens.css, base.css, animations.css  (copied verbatim from prototype)
│  ├─ locales/        # en.json, ar.json
│  └─ types/          # generated DB types
├─ supabase/
│  ├─ migrations/     # SQL migrations (schema, RLS, functions)
│  └─ seed/           # seed data converted from the prototype's mock data
├─ tests/             # unit, RLS, and end-to-end tests
└─ docs/              # these four documents
```

---

## 5. Porting strategy (prototype → React/TS) with zero redesign

1. **Copy, don't rewrite, the CSS.** Move the `<style>` block into `styles/*.css` unchanged.
2. **Port markup 1:1.** Each template-string view becomes a component producing the same DOM and class names.
3. **Replace the global state `S`** with: URL (current page, track slug), TanStack Query (server data), and small local state (quiz step, lab step, filters).
4. **Replace `act()` switch** with ordinary event handlers.
5. **Replace `[en, ar]` pairs** with i18n JSON (UI text) and bilingual DB columns (content).
6. **Verify visually** against the approved prototype after each page is ported (screenshot comparison, EN/AR, dark/light, desktop/mobile).

| Prototype piece | React target |
|---|---|
| `P.home` | `pages/Home` + `RouteHero`, `CodeBars` |
| `P.explore`, `P.track` | `pages/Explore`, `pages/TrackDetail` (`/tracks/:slug`) |
| `P.quiz`, `P.res` | `pages/Quiz`, `pages/Results` (`/results/:attemptId`) + `RadarChart` |
| `P.lab`, `labs()`, `PL()` | `pages/Labs`, `pages/LabPlayer` (`/labs/:slug`) |
| `P.road` | `pages/Roadmap` (`/roadmap/:slug`) |
| `P.opp` | `pages/Opportunities` |
| `P.dash` | `pages/Dashboard` + `ProgressRing` |
| `toast()`, `award()` | `ToastProvider`; awards come from server responses |
| `io` (IntersectionObserver) | `useReveal()` hook |

---

## 6. Data access pattern

- Types generated from the database (`supabase gen types`) so the frontend and schema cannot drift.
- **Reads** of public content go straight to tables (RLS limits them to published rows).
- **Writes with business meaning go through RPC functions**, not direct table writes: quiz submission, lab answers, task completion. This keeps scoring, XP, and achievements out of the browser.
- Task toggling uses an optimistic update (instant UI, rollback on error) to preserve the snappy feel of the prototype.

---

## 7. Authentication and authorization

**Flows:** sign up (email confirmation), log in, log out, password reset (email link → set new password), profile management. Google sign-in is optional.

**Roles:** `user` (default) and `admin`. Roles live in a dedicated `user_roles` table, **not** in the editable profile row, so users can never promote themselves. Admins are created manually (SQL) at first.

**Profiles:** a database trigger creates a `profiles` row when a new auth user is created.

**Guest mode (recommended):** the prototype lets anyone explore and take the quiz without an account. Keep that. Guests' quiz answers/results live in the browser; when they sign up, the app offers to **save them to the new account** (calls the same scoring RPC). Progress features (roadmap, XP, achievements, bookmarks) require login.

**Row Level Security (summary; details in `DATABASE_SCHEMA.md` §6):**
- RLS is enabled on **every** table in the `public` schema.
- Content tables: anyone may read **published** rows; only admins may write.
- Personal tables (attempts, progress, bookmarks): a user can read/write only rows where `user_id = auth.uid()`.
- Derived tables (XP, achievements, recommendations, lab answers): **no direct user writes**; only security-definer functions write them.
- Security-definer functions set `search_path` explicitly and validate every input.

---

## 8. Security checklist

- Anon key only in the frontend; service-role key only in CI/server contexts, never committed.
- Secrets in environment variables (Vercel/GitHub), `.env` ignored by Git.
- Strict input validation in RPC functions; CHECK constraints in the schema.
- Rate limiting on auth endpoints (Supabase defaults) and on RPCs where abuse is plausible (quiz/lab submissions).
- Minimal personal data: email, display name, optional governorate. Publish a short privacy statement; support account deletion (cascade).
- Dependency auditing (`npm audit`) and Dependabot on GitHub.
- Resource and opportunity links: **https only** (enforced by CHECK constraints and validators); open external links with `rel="noopener noreferrer"`; never render admin-entered text as raw HTML.
- Admin actions are recorded in `content_audit_log`; destructive actions require confirmation.
- RLS tests: for every table, automated checks that an anonymous user, a normal user, and an admin can do exactly what the policy says and nothing more.

---

## 9. Environments, deployment, and operations

| Environment | Frontend | Database |
|---|---|---|
| Local | Vite dev server | Supabase CLI (local Docker stack) with migrations + seed |
| Preview | Vercel preview per PR | A shared staging Supabase project |
| Production | Vercel production | Production Supabase project |

- **Migrations** are SQL files in the repo and applied in order; no manual changes in the dashboard.
- **Seed data** is generated from the prototype's mock data so content parity is exact.
- **CI (GitHub Actions):** type-check, lint, unit tests, build on each PR.
- **Backups:** confirm what the chosen Supabase plan provides. **Verify current free-plan terms**, including inactivity pausing and limits, before relying on it for the demo.

---

## 10. Core business logic specification

### 10.1 Career recommendation engine

**What it is:** a transparent matching function, not a psychological test. RIASEC (Holland's model) describes vocational *interests* along six dimensions: Realistic, Investigative, Artistic, Social, Enterprising, Conventional. The model is well-established for interests; **the quiz items and track profiles here are team-authored**, so the output must be presented as *guidance*, not as a validated assessment or a personality type.

**Inputs**
- The user's selected option per question. Each option carries weights `w_R, w_I, w_A, w_S, w_E, w_C` (0–3) and, for the coding question, an optional `coding_affinity` ∈ [0,1].
- Each published track has a profile vector `t = (R, I, A, S, E, C)` (0–5) and `coding_percent` ∈ [0,100].

**Computation (all server-side, in `submit_quiz`)**
1. User vector: `u_j = Σ w_j` over the chosen options.
2. Coding affinity `c_u`: from the coding question (default 0.5 if absent).
3. For each track: `cos = (u·t) / (‖u‖·‖t‖)`.
4. Penalty: `λ · |c_u − coding_percent/100|`, with `λ = 0.25` (configurable).
5. Raw match `m = cos − penalty`.
6. Display *fit index* = `clamp(round((m − 0.25)/0.70 · 100), 40, 97)`. This is a monotonic rescale for readability, **not a probability**.
7. Rank descending; ties broken by track `sort_order`. Return the top 3.

**Explainability.** For each recommended track, store the two dimensions with the largest `u_j · t_j` plus the coding comparison, as **codes** (e.g. `{dims:["I","C"], coding:{user:0.5, track:0.35}}`). The UI renders the sentence in the user's language, so language switching never breaks it.

**Guards and edge cases**
- All questions required (as in the prototype); if `u` is all zeros, return no ranking and prompt the user to explore directly.
- Fewer than three published tracks → return fewer.
- Each result stores `engine_version`, `u`, `c_u`, and the parameters used, so any result can be reproduced and audited.
- Lab reflections are **stored but do not alter rankings in the MVP.** Adjusting scores from unvalidated signals is a Phase-3 experiment.

**Scale problem with 19 tracks [Recommended; needs your decision].** The prototype has 6 quiz questions. That is not enough to separate close neighbors (Data Science vs Machine Learning vs AI; Network Security vs SOC Analysis; Graphic Design vs Motion Graphics). Proposed changes:
1. Expand the question bank to **about 15 to 20 questions** (the length originally planned), including several that probe the *differences* between neighboring tracks.
2. **Two-step recommendation:** first rank the 6 *categories* from the interest scores, then rank tracks *within* the best categories, and show a short "why not the others" note when two tracks score very close.
3. Add a **diversity guard**: if the top 3 are all near-duplicates (same category and similar vectors), show the best track per category first.
4. Run a **user study** (SUS plus satisfaction) before presenting the engine as anything more than guidance.
The track profile values are drafts (`TRACK_CATALOG.md` §7) and must be reviewed.

**Language to avoid:** "your personality type is…", "you will succeed in…". Use "your answers lean toward…", "this track fits your stated interests".

### 10.2 Roadmaps
- A track can have **several roadmaps** (variants such as core or fast-track, each versioned) → ordered **stages** (concept / hands-on / project / checkpoint) → ordered **tasks** (read/video/exercise/practice/project/review; estimated minutes; XP). Each stage also lists **resources** (core or optional) taken from the verified resource library.
- A resource is shown to users only if a person has verified it; the UI shows "verified" and a date **only** when the record proves it (`ROADMAP_CONTENT_STRATEGY.md` §4).
- The user's **starting point** (from scratch / some basics / prior knowledge) is stored per track and only *recommends* where to begin; stages are never locked.
- Completion is stored as one row per completed task. Un-completing deletes the row.

### 10.3 Taster Labs
- A lab has ordered **scenarios** (steps); each step has options.
- **Answer keys and feedback live in a private table.** The client calls `submit_lab_answer(attempt, scenario, option)`; the server records the choice and returns `{is_correct, feedback}`.
- Completing a lab computes `score = correct steps / total steps`, stores the optional reflection ("enjoyed it?"), and awards XP **once per lab**.
- Labs are explicitly **not graded as ability tests**; the score is for learning feedback only.

### 10.4 Progress, XP, achievements
- **Roadmap completion %** = completed tasks ÷ total published tasks (equal weights; weighting by estimated minutes is a possible later change).
- **Stage complete** = all its tasks complete.
- **XP** (prototype values): task 20, stage 100, quiz 50, lab 75. Every award is a row in `xp_events` with a unique key `(user_id, source, source_id)`, so repeating an action can **never** award XP twice (fixes the farming bug).
- **Achievements** are unlocked by database triggers/functions, idempotent by primary key `(user_id, achievement_id)`. MVP set: first discovery, first lab, first stage complete.

### 10.5 Opportunities
- Lifecycle: `draft → review → published → archived`. Only `published` and not-expired items are visible to users.
- Each record: organization, type (internship/training/scholarship/event), mode (online/onsite/hybrid), governorate (null = nationwide/online), related tracks (many-to-many), eligibility, deadline, official apply URL, source URL, **`last_verified_at`**.
- Filters: text search, type, governorate (nationwide items always included), track; default sort by nearest deadline.
- Expiry: queries exclude past deadlines; a scheduled job (or admin action) moves expired items to `archived`.
- Content is entered by admins; automated ingestion (AI agent) stays a later phase with mandatory human review.

---

## 11. Testing strategy

| Level | What | Tool |
|---|---|---|
| Unit | Matching engine (known inputs → expected ranks), XP rules | Vitest / pgTAP |
| Security | RLS matrix per table × role (anon / user / admin) | SQL test scripts in CI |
| Integration | RPC functions against a local database | Supabase CLI + test runner |
| End-to-end | Sign up → quiz → results → roadmap → lab → dashboard | Playwright (EN + AR) |
| Visual | Screenshot comparison against the approved prototype | Playwright screenshots |
| Accessibility | Keyboard navigation, focus order, contrast, screen-reader labels | axe + manual |

---

## 12. Risks and mitigations

| Risk | Mitigation |
|---|---|
| Misconfigured RLS exposes data | RLS on every table, automated RLS tests, review every migration in a PR |
| Visual drift during the port | Preservation contract + screenshot comparison gate per page |
| Content volume: 19 tracks × roadmaps, resources, projects, labs, in two languages | Admin tooling and bulk import first; build content in batches; **publish gate** so only complete tracks are visible; choose a depth target (`ROADMAP_CONTENT_STRATEGY.md` §8) |
| Resources go stale or links break | Verification workflow, re-check interval, user reports, link checker that flags but never "verifies" |
| Copying an external roadmap site would breach its terms | Author roadmaps independently; use external roadmaps only as human-read reference (`ROADMAP_CONTENT_STRATEGY.md` §1) |
| Quiz mistaken for a validated psychometric test | Wording rules (§10.1), evaluation study (SUS + satisfaction), documented limitations |
| Free-plan limits or pausing during the demo | Verify plan terms; keep a seeded local/staging copy for the presentation |
| Scope creep | Milestone gates and an explicit MVP cut (`IMPLEMENTATION_ROADMAP.md`) |

---

## 13. Remaining decisions for the project owner

**Technical**
1. **Vite SPA** (recommended) or Next.js?
2. **Guest mode** with "save my results on sign-up" (recommended) or login required for everything?
3. **Google sign-in** now, or email + password first?
4. **Match score wording:** keep "match %" (documented as a fit index) or switch to bands? Changing it alters approved UI text, so it needs your approval.
5. **Assessment length:** approve expanding to ~15 to 20 questions and the two-step (category then track) recommendation (§10.1)?
6. Does the university or supervisor impose **hosting, data-location, or privacy requirements**?

**Content**
7. **Depth target** per track (lean / standard / deep) and the batch order (`ROADMAP_CONTENT_STRATEGY.md` §8).
8. Approve the **recommended additional tracks** or keep the 19 (`TRACK_CATALOG.md` §4).
9. Who **reviews** track descriptions, RIASEC profiles, and verifies resources? (a second team member, the supervisor, an outside specialist)
10. Should the team **contact roadmap.sh** about linking, or use it only as private reference?

**Design**
11. Confirm the **new screens** proposed for the Figma handoff and the 42-screen total (`FIGMA_DESIGN_HANDOFF.md`); add a "Resources" item to the main navigation?

---

## 14. Content management architecture **[Recommended, driven by confirmed requirements]**

**Principle:** React renders; the database holds content; administrators change content through the admin dashboard, with no code deploy.

```
Authors (team) ─► Spreadsheet / Admin editors ─► Bulk Import (validate → confirm)
                                    │
                                    ▼
          Draft ► In review ► Verified/Published   (per track, roadmap, resource, opportunity)
                                    │
                                    ▼
             Public tables (RLS: published only) ──► React pages
                                    │
                        content_audit_log (who/what/when)
```

- **Admin dashboard** screens: Tracks, Track Editor, Roadmap Editor, Resources Manager, Quiz Manager, Labs and Lab Editor, Opportunities Manager, Users and Roles, Bulk Import (`FIGMA_DESIGN_HANDOFF.md` §3.1 D).
- **Publish gate:** a track becomes visible only when it passes the checklist in `TRACK_CATALOG.md` §8, enforced in the database by `publish_track()`.
- **Versioning:** roadmaps carry a version; progress points at tasks, whose ids stay stable when unchanged, so updates do not erase user progress.
- **Adding a new track** = new rows (track, category link, skills, responsibilities, roadmap, resources, lab link, relations). **No React change.**
- **Bilingual content:** every user-facing text field has `_en` and `_ar` columns; the admin editors flag missing translations.

## 15. Workstreams and responsibilities **[Confirmed]**

| | Workstream A: Software | Workstream B: Figma UI/UX |
|---|---|---|
| Who | The project owner, building on her laptop with Claude assisting (architecture, frontend, backend, database, logic, integration, testing, documentation, deployment preparation) | A separate teammate, manually in Figma, for another academic course |
| Deliverable | The working application | Figma design |
| Dependency | **None on Figma.** The approved interactive prototype is the visual reference | None on software |
| Link between them | `FIGMA_DESIGN_HANDOFF.md` (my only responsibility toward Figma) | |

Rules: software development must never wait for Figma; Claude does not implement the Figma file; if the Figma design later differs from the approved prototype, the **prototype wins for the software** unless you explicitly decide otherwise.
