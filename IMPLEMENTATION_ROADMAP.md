# MASAR — Implementation Roadmap (Revision 2: complete graduation project)

**Status:** plan only; nothing has started. **Legend:** **[Confirmed]** from the owner's brief · **[Recommended]** my proposal.

**What changed.** Revision 1 had a three-track MVP cut. That is **removed**. This plan delivers the **complete platform**: 19 tracks, full content model, all approved features, admin dashboard, Arabic and English. It still orders the work intelligently so that something demonstrable exists early and content production can start as soon as its tooling exists.

**How the work is done [Confirmed]:** the project owner develops the application on her laptop with Claude assisting. The Figma design is a separate workstream and **blocks nothing** here. The approved prototype is the visual reference throughout.

**Team rule [from earlier decisions]:** the three teammates work on everything together; changes are reviewed by someone other than the author. Content verification needs a second pair of eyes.

**Sizes** (relative, not calendar time): **S** a couple of sessions · **M** a few sessions · **L** about a week of shared work · **XL** several weeks. Convert to dates once the team knows its weekly capacity.

**Global acceptance rule:** any milestone touching UI is accepted only after screenshot comparison with the approved prototype (EN/AR × dark/light × desktop/mobile).

---

## Recommended implementation order (summary)

| Phase                              | Milestones                     | Outcome                                                                                                |
| ---------------------------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------ |
| **0. Decide and prepare**          | M0, M1                         | Decisions made, repo and tooling ready                                                                 |
| **1. Frontend foundation**         | M2, M3                         | The approved prototype running as a React/TypeScript app, backed by a swappable data layer             |
| **2. Backend foundation**          | M4, M5, M6                     | Supabase environments, full schema with security, authentication                                       |
| **3. Catalog and content tooling** | M7, M8                         | 19-track catalog live; admin dashboard and import/verification tools exist                             |
| **4. Core features**               | M9, M10, M11, M12, M13         | Assessment and recommendations, roadmaps and resources, progress and achievements, labs, opportunities |
| **5. Content production**          | M14 (runs in parallel from M8) | Every track meets the publish gate                                                                     |
| **6. Quality and launch**          | M15, M16, M17, M18             | i18n/RTL QA, security, testing, deployment and demo                                                    |

---

## Milestone details

### M0: Decisions and project preparation · **S**

- **Objectives:** settle the open decisions so they do not block later work.
- **Tasks:** answer the decisions in `TECHNICAL_ARCHITECTURE.md` §13 (Vite vs Next, guest mode, quiz length, depth target, reviewers, added tracks); create the GitHub repo, branch rules, PR template; agree the content-review rule.
- **Dependencies:** none.
- **Deliverables:** decision log; repo with protected `main`.
- **Testing criteria:** every decision has an owner and a recorded answer.

### M1: Tooling and project setup · **S**

- **Objectives:** a clean React + TypeScript project with CI.
- **Tasks:** scaffold Vite + React + TS; ESLint/Prettier; CI (type-check, lint, build); Vercel project with preview deployments; Supabase CLI installed; `.env` handling.
- **Dependencies:** M0.
- **Deliverables:** running empty app, CI green, preview URL.
- **Testing criteria:** a new teammate can run the project from the README; no secrets in the repo.

### M2: React migration of the approved prototype · **L**

- **Objectives:** a **faithful port** of all 9 prototype views with mock data, no visual change.
- **Tasks:** copy CSS verbatim into `styles/`; port markup 1:1 into components; add React Router (URL per page, back button); i18next with EN/AR JSON and RTL switching; port animations (CSS + `useReveal`); port the quiz, radar, lab player, roadmap, dashboard, opportunities.
- **Dependencies:** M1.
- **Deliverables:** the prototype as a React/TS app (still mock data).
- **Testing criteria:** screenshot comparison passes for every screen; all prototype interactions work; deep links work; reduced-motion respected. _(Fixes the known issues in `FEATURE_STATUS.md` §4: reason codes instead of stored strings, hard-coded strings moved to i18n.)_

### M3: Frontend architecture and data layer · **M**

- **Objectives:** a structure that can host 19 tracks and swap mock data for the real backend without rewriting screens.
- **Tasks:** feature folders; typed data-access interface with a **mock adapter** (so frontend work is never blocked by the backend); TanStack Query setup; component extraction (buttons, panels, progress, toasts, modal, drawer, table, form fields) in the existing visual language; error and loading states; accessibility baseline (focus-visible, aria-live toast, radio-group semantics, chart text alternative).
- **Dependencies:** M2.
- **Deliverables:** documented architecture; component library; mock adapter.
- **Testing criteria:** screens render from the adapter; replacing the adapter requires no screen changes; keyboard-only navigation works.

### M4: Supabase configuration and environments · **S**

- **Objectives:** local, staging, and production backends.
- **Tasks:** create projects; local stack via CLI; environment variables; confirm plan limits, backups, and pausing behavior of the chosen plan; secrets handling.
- **Dependencies:** M1.
- **Deliverables:** documented environment setup.
- **Testing criteria:** anon key is the only key in the browser bundle; a fresh clone runs against local Supabase.

### M5: Database schema, RLS, and seed · **L**

- **Objectives:** the full schema from `DATABASE_SCHEMA.md` as migrations, with Row Level Security.
- **Tasks:** migrations in dependency order; RLS on **every** table; `is_admin()`, triggers, constraints; RPC functions skeletons; generate TypeScript types; seed from the prototype data and the 19-track catalog metadata (flagged as draft).
- **Dependencies:** M4.
- **Deliverables:** migrations, seed, generated types.
- **Testing criteria:** migrations apply from scratch; **RLS test matrix** (anonymous / user / admin × every table) passes; lab answer keys are unreadable by non-admins.

### M6: Authentication and profiles · **M**

- **Objectives:** sign up, log in, log out, password reset, profile management.
- **Tasks:** auth pages (screens P05 to P09 in the Figma handoff, built in the existing visual language); session handling; protected and admin routes; profile and settings pages; account deletion; **guest-to-account merge** of quiz results (if approved).
- **Dependencies:** M3, M5.
- **Deliverables:** working auth; profile row auto-created.
- **Testing criteria:** end-to-end flows pass; a signed-out user cannot read private tables; roles cannot be self-assigned; error states in both languages.

### M7: Track catalog integration · **M**

- **Objectives:** Explore, Track Details, and Landing read the catalog from the database.
- **Tasks:** categories, filters, search, relations ("related paths"), responsibilities, prerequisites, roles, skills and tools; per-track URLs; "coming soon" for unpublished tracks.
- **Dependencies:** M3, M5.
- **Deliverables:** database-driven catalog for all 19 tracks (content may still be draft).
- **Testing criteria:** screens match the prototype using seed data; unpublished tracks never appear to users; adding a track by inserting rows requires **no frontend change**.

### M8: Admin dashboard, content tooling, and verification · **XL**

- **Objectives:** let administrators create and manage all content safely, **before** large-scale content authoring.
- **Tasks:** admin shell and guards; Tracks List and Track Editor (tabs); Roadmap Editor (stages, tasks, drag-and-drop, versions); Resources Manager with verification workflow and `resource_checks`; Quiz Manager; Labs List and Lab Editor; Opportunities Manager with workflow; Users and Roles; **Bulk Import with validation** (`validate_import`, `apply_import`); audit log viewer; `publish_track()` publish gate; translation-missing indicators.
- **Dependencies:** M6, M7.
- **Deliverables:** complete admin dashboard.
- **Testing criteria:** a non-admin cannot reach admin screens **or** call admin writes against the API; every admin change appears in the audit log; import rejects bad rows with clear messages; a resource cannot be marked verified without a named person and date; a track failing the gate cannot be published.

### M9: RIASEC assessment and recommendation engine · **L**

- **Objectives:** database-driven quiz and server-side recommendations for 19 tracks.
- **Tasks:** expanded question bank (about 15 to 20, if approved); reviewed track profiles; `submit_quiz`; two-step category/track ranking and diversity guard (if approved); reason codes rendered per language; results URL; guest save flow; unit tests; a small user study plan (SUS, satisfaction).
- **Dependencies:** M7 (tracks), M5; M8 for the question editor.
- **Deliverables:** assessment and results powered by the server.
- **Testing criteria:** fixed inputs give fixed rankings; ties deterministic; all-zero input handled; language switch re-renders the same reasons; users cannot read others' attempts; engine parameters and version stored with every result.

### M10: Roadmaps and learning resources · **L**

- **Objectives:** data-driven roadmaps and the resource library.
- **Tasks:** roadmap and stage pages with core/optional resources and outcomes; start-point choice; several roadmaps per track; Resources library with filters (type, language, difficulty, skill, verified); rate and report resources; bookmarks; unpublished or unverified resources hidden.
- **Dependencies:** M7, M8.
- **Deliverables:** roadmap and resource screens fed by the database.
- **Testing criteria:** changing track or start point never deletes progress; a roadmap update does not erase progress on unchanged tasks; "verified" appears only for verified records; one rating per user per resource.

### M11: Progress tracking, achievements, and dashboard · **M**

- **Objectives:** persistent progress and gamification.
- **Tasks:** `set_task_completed` with optimistic UI; `xp_events` ledger; stage and achievement triggers; Dashboard, Progress, and Achievements pages from real data.
- **Dependencies:** M10.
- **Deliverables:** real progress system.
- **Testing criteria:** progress survives refresh and device change; **un-checking and re-checking a task never awards XP twice**; stage XP and badges awarded exactly once; two tabs stay consistent.

### M12: Taster Labs · **L**

- **Objectives:** database-driven labs with server-side grading for every track that has a lab.
- **Tasks:** `start_lab_attempt`, `submit_lab_answer`, `complete_lab_attempt`; keys in the private table; lab catalog and overview pages; lab-to-track links; port the existing Networking lab; author further labs through the Lab Editor (content work is tracked in M14).
- **Dependencies:** M8, M11.
- **Deliverables:** lab engine plus the first labs.
- **Testing criteria:** answer keys never reach the browser before answering; one answer per step per attempt; XP and achievement once; resume or restart cleanly.

### M13: Local opportunities · **M**

- **Objectives:** the radar with real data and filters.
- **Tasks:** list, search, type, governorate (nationwide included), track filters; details page; save; expiry handling; "last verified" shown; admin workflow already built in M8.
- **Dependencies:** M7, M8.
- **Deliverables:** database-driven opportunities.
- **Testing criteria:** expired and draft items never visible to users; filters combine correctly; saved list is private.

### M14: Content production for all 19 tracks · **XL** (runs in parallel from M8 onward)

- **Objectives:** every track meets the **publish gate** (`TRACK_CATALOG.md` §8).
- **Tasks:** work in batches (suggested order in `ROADMAP_CONTENT_STRATEGY.md` §8): collect and verify resources (team), write stages, projects, labs, roles (with Claude drafting, team reviewing), translate and review Arabic, review RIASEC profiles, enter and review opportunities.
- **Dependencies:** M8 (tools); content for a feature's screens is needed by M10 to M13 for realistic testing.
- **Deliverables:** published tracks; a content tracker showing each track's completeness.
- **Testing criteria:** per track, the gate checklist passes with a second reviewer's sign-off; sampled resources re-opened by a different person; no unverified resource is marked verified.

### M15: Internationalization and RTL QA · **M**

- **Objectives:** full English/Arabic parity.
- **Tasks:** every UI string in i18n; every content field translated and reviewed; RTL layout review on every screen; typography checks (Arabic line-height, no uppercase or letter-spacing); mixed-direction text; terminal blocks stay LTR.
- **Dependencies:** M7 to M13 (continuous), final pass after M14.
- **Deliverables:** i18n audit report.
- **Testing criteria:** no untranslated string in either language; every screen passes RTL review.

### M16: Security hardening and privacy · **M**

- **Objectives:** safe to put real users on.
- **Tasks:** complete RLS matrix; rate limiting on RPCs; dependency audit and secret scanning; link-safety rules; privacy statement; account-deletion cascade test; review every `security definer` function.
- **Dependencies:** M5 to M13.
- **Deliverables:** signed-off security checklist (`TECHNICAL_ARCHITECTURE.md` §8).
- **Testing criteria:** no critical or high findings open; anonymous, user, and admin permissions behave exactly as designed.

### M17: Testing and quality · **L**

- **Objectives:** confidence across the full platform.
- **Tasks:** unit tests (engine, XP rules, validators); integration tests for RPCs; end-to-end flows in EN and AR (Playwright); visual regression against the approved prototype; accessibility pass (keyboard, focus, contrast including lime on light, screen reader labels); performance check on a mid-range phone; content QA report.
- **Dependencies:** M9 to M15.
- **Deliverables:** test suite in CI; test report.
- **Testing criteria:** all suites green; keyboard-only completion of the main flows; no console errors on any screen.

### M18: Deployment and graduation demo · **M**

- **Objectives:** production launch and a safe demonstration.
- **Tasks:** production Supabase setup and migrations; environment variables; domain (optional); backups confirmed; basic monitoring; seed production content; rehearse the demo including a fallback copy; runbook (deploy, roll back, restore).
- **Dependencies:** M16, M17 and enough published tracks.
- **Deliverables:** live URL; runbook; demo script.
- **Testing criteria:** smoke test passes in production; rollback rehearsed once; the demo runs without developer tools open.

---

## Dependency overview

```
M0 → M1 → M2 → M3 ──────────────┐
      └→ M4 → M5 → M6 ─┐        │
               └→ M7 ←─┴────────┘
                  └→ M8 → M9, M10 → M11 → M12
                      │       └→ M13
                      └→ M14 (parallel, long-running)
 M7–M13 → M15, M16 → M17 → M18
```

## Prioritization inside the full scope **[Recommended]**

All approved features are delivered; ordering only decides **what exists first**:

1. The prototype as a real React app (M2, M3): proves nothing was lost.
2. Security and data foundation (M4 to M6): everything else builds on it.
3. Catalog and admin tooling (M7, M8): unlocks content production, the longest task.
4. Assessment, roadmaps, progress, labs, opportunities (M9 to M13).
5. Content batches (M14) continuously, with the publish gate protecting quality.
6. Quality, i18n, security, deployment (M15 to M18).

## Known risks to the schedule

- **Content volume** (M14) is the dominant risk; see the effort model in `ROADMAP_CONTENT_STRATEGY.md` §8.
- **Arabic content review** needs fluent reviewers.
- **Free-plan backend limits** must be verified before the demo.
- **Quiz validity:** expect to iterate on questions and profiles after the first user test.
