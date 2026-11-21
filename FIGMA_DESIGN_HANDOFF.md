# MASAR — UI/UX Design Handoff

> **Document type:** UI/UX design documentation (design handoff)
> **Audience:** the designer building MASAR's interface in Figma, and reviewers of the academic deliverable
> **Scope:** screens, flows, content, responsive behavior, design system, accessibility, and Arabic RTL. Nothing in this document describes engineering, data storage, or system integration.
> **Version:** 2.0 (update of the original handoff; all prior decisions preserved, see [Appendix: Revision Notes](#17-appendix-revision-notes))

MASAR is a guidance platform that helps computer science and IT students discover a suitable career track, follow a structured roadmap, try short hands-on labs, and find real opportunities. Its tone is **guidance, not a verdict**: recommendations are suggestions the learner can always change.

The **approved interactive prototype** is the visual source of truth. Where the prototype shows a screen or component, this document records it and it must be matched. Where it does not, this document gives proposals in the same visual language.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Document Conventions](#2-document-conventions)
3. [Navigation Structure](#3-navigation-structure)
4. [Screen Inventory](#4-screen-inventory)
5. [Shared Screen Patterns](#5-shared-screen-patterns)
6. [Screen Specifications](#6-screen-specifications)
   - [6.1 Public Screens](#61-public-screens)
   - [6.2 Onboarding and Assessment Screens](#62-onboarding-and-assessment-screens)
   - [6.3 Learning App Screens](#63-learning-app-screens)
   - [6.4 Admin Screens](#64-admin-screens)
   - [6.5 System Screens](#65-system-screens)
7. [Sample Content Library](#7-sample-content-library)
   - [7.1 Learning Tracks](#71-learning-tracks)
   - [7.2 Track Details Example](#72-track-details-example)
   - [7.3 Roadmap Example](#73-roadmap-example)
   - [7.4 Learning Resources](#74-learning-resources)
   - [7.5 Assessment Questions and Results](#75-assessment-questions-and-results)
   - [7.6 Taster Labs](#76-taster-labs)
   - [7.7 Progress and Achievements](#77-progress-and-achievements)
   - [7.8 Opportunities](#78-opportunities)
   - [7.9 Admin Dashboard and Management Data](#79-admin-dashboard-and-management-data)
   - [7.10 Sample Learner](#710-sample-learner)
8. [User Flows](#8-user-flows)
9. [Modal and Overlay Specifications](#9-modal-and-overlay-specifications)
10. [Responsive Specifications](#10-responsive-specifications)
11. [Design System](#11-design-system)
    - [11.1 Colors and Themes](#111-colors-and-themes)
    - [11.2 Typography](#112-typography)
    - [11.3 Spacing and Sizing](#113-spacing-and-sizing)
    - [11.4 Radius, Elevation, and Motion](#114-radius-elevation-and-motion)
    - [11.5 Buttons](#115-buttons)
    - [11.6 Inputs and Form Components](#116-inputs-and-form-components)
    - [11.7 Cards and Panels](#117-cards-and-panels)
    - [11.8 Navigation Components](#118-navigation-components)
    - [11.9 Overlays, Alerts, and Toasts](#119-overlays-alerts-and-toasts)
    - [11.10 Tables, Badges, and Progress](#1110-tables-badges-and-progress)
    - [11.11 Component Inventory and Variants](#1111-component-inventory-and-variants)
12. [Accessibility and Interface Consistency](#12-accessibility-and-interface-consistency)
13. [Arabic RTL Requirements](#13-arabic-rtl-requirements)
14. [Completeness Review](#14-completeness-review)
15. [Open Questions and Decisions](#15-open-questions-and-decisions)
16. [Designer Deliverables Checklist](#16-designer-deliverables-checklist)
17. [Appendix: Revision Notes](#17-appendix-revision-notes)

---

## 1. Project Overview

### 1.1 At a glance

| Item | Value | Status |
|---|---|---|
| Unique page-level screens | **42** | Confirmed |
| Reusable templates inside those screens | 6 (see [4.6](#46-reusable-templates)) | Confirmed |
| Modal / overlay designs | 16 (see [Section 9](#9-modal-and-overlay-specifications)) | Confirmed |
| Languages | 2 — English (LTR), Arabic (RTL) | Confirmed |
| Themes | 2 — dark and light | Confirmed |
| Breakpoints | 3 — mobile, tablet, desktop | Confirmed |
| Career tracks | 19 (all use the Track Details and Roadmap templates, so they are **not** separate screens) | Confirmed count; names are [Sample] |

### 1.2 Design principles

| Principle | What it means for the interface | Status |
|---|---|---|
| Guidance, not a verdict | Results and recommendations always show a "you can change this" message and an alternative action | Confirmed |
| Not everything is code | Tracks with low coding level are shown with the same weight as code-heavy tracks | Confirmed (Landing) |
| One accent | Lime is the single primary accent; coral signals urgency only | Confirmed |
| Flat and calm | Thin borders instead of shadows; motion is short and optional | Confirmed |
| Two languages, equal quality | Every component has an LTR and an RTL variant | Confirmed |

### 1.3 Frame plan

| Coverage | Frames | Status |
|---|---|---|
| Minimum: 42 screens × 2 sizes (desktop + mobile), English | **84** | Recommended |
| Tablet for ~12 key screens | ~12 | Recommended |
| Arabic RTL for the same ~12 key screens | ~12 | Recommended |
| Full coverage: 42 screens × 3 breakpoints × 2 languages | 252 | Optional |

**The 12 key screens:** Landing (P01), Explore (P03), Track Details (P04), Log In (P05), Assessment Question (O04), Results (O05), Dashboard (L01), Roadmap (L02), Stage Detail (L03), Lab Step (L07), Opportunities (L11), Admin Tracks List (A02).

**Recommended frame sizes:** mobile 390 × 844 · tablet 820 × 1180 · desktop 1440 × 1024.

---

## 2. Document Conventions

### 2.1 Labels

| Label | Meaning |
|---|---|
| **[Prototype]** | Exists in the approved prototype. Must be matched. |
| **[New]** | Required by the project but not in the prototype. Designed in the same visual language. |
| **[Recommended]** | A suggestion for the designer to accept or change. Not yet approved. |
| **[Sample]** | Illustrative content for layout and realism only. **Not confirmed project information** and may be replaced. |
| **[Open]** | A decision that needs confirmation (collected in [Section 15](#15-open-questions-and-decisions)). |

### 2.2 Sample data policy

- All track names, descriptions, resource titles, provider names, numbers, dates, scores, and learner details in this document are **[Sample]**.
- Samples are written to be consistent across screens (the same track, learner, and dates appear everywhere) so prototypes feel believable.
- Sample deadlines are set relative to **21 November 2026**.
- Provider and organization names in samples are fictional. Replace them before any public use.

### 2.3 Terminology

Use these terms identically in every screen, label, and toast.

| Use | Do not use |
|---|---|
| **Track** (a career direction) | Path, field, major |
| **Roadmap** (the ordered plan for a track) | Curriculum, course plan |
| **Stage** (a section of a roadmap) | Level, module, phase |
| **Task** (a single learning action inside a stage) | Lesson, item |
| **Resource** (external learning material) | Link, material |
| **Taster Lab** / **Lab** (short hands-on scenario) | Simulation, exercise |
| **Assessment** (the interest quiz) | Test, exam |
| **Opportunity** (internship, scholarship, program, competition, event) | Job, offer |
| **Saved** (bookmarked items) | Favorites, bookmarks |
| **XP** (points earned for progress) | Score (reserved for lab and assessment results) |

> **[Open]** The sidebar label in the original document was "Radar" while the mobile bar and screen name were "Opportunities". This document uses **Opportunities** everywhere as the label and "Opportunity Radar" only as an optional page subtitle. See [Section 15](#15-open-questions-and-decisions).

### 2.4 Screen ID scheme

`P` Public · `O` Onboarding and assessment · `L` Learning app · `A` Admin · `S` System. Modals are numbered `M01`–`M16`. Flows are `F01`–`F15`.

---

## 3. Navigation Structure

### 3.1 Learner app

| Area | Items | Status |
|---|---|---|
| **Top bar (all sizes)** | Logo/home · language switch (EN / ع) · theme toggle · account menu (Profile, Settings, Saved, Sign out) when signed in, or Log in / Sign up when not | Confirmed |
| **Desktop sidebar (≥ 900 px)** | Home · Explore · Discover (assessment) · Labs · Roadmap · Opportunities · Dashboard | Prototype |
| Sidebar addition | **Resources** (placed after Roadmap) | New / Recommended |
| **Mobile and tablet bottom bar (< 900 px)** | Home · Explore · Roadmap · Opportunities · Dashboard | Prototype |
| Bottom bar addition | A **More** item opening a sheet with Discover, Labs, Resources, Saved | Recommended |
| **Admin area** | Separate section visible only to administrators: Overview · Tracks · Roadmaps · Resources · Quiz · Labs · Opportunities · Users · Import | New |

### 3.2 Navigation behavior

| Rule | Specification | Status |
|---|---|---|
| Active item | Lime marker (sidebar: edge bar; bottom bar: top bar or filled icon) plus bold label | Prototype |
| Signed-out visitor | Sees Home, Explore, Discover, Labs, Opportunities; opening Dashboard, Roadmap (personal), Saved, Profile, or Settings shows the Log In screen with a "Sign in to continue" note and returns to the requested screen afterwards | Recommended |
| Breadcrumbs | Shown on Track Details, Stage Detail, Lab pages, Opportunity Details, and all Admin editors on desktop; replaced by a Back button on mobile | Recommended |
| Back behavior | Back returns to the previous screen in the flow, never leaves the app | Recommended |
| Assessment and Lab Step | Navigation chrome is minimized (top bar only, no sidebar or bottom bar) to keep focus | Recommended |

### 3.3 Site map

```
Public ─ Landing · About · Explore · Track Details · Login · Sign Up · Forgot/Reset Password · Email Confirmation
Onboarding ─ Welcome · Choose Starting Point · Assessment Intro · Question · Results
App ─ Dashboard · Roadmap · Stage Detail · Resources · Labs (Catalog · Overview · Step · Result)
      · Progress · Achievements · Opportunities (List · Details) · Saved · Profile · Settings
Admin ─ Overview · Tracks (List · Editor) · Roadmap Editor · Resources · Quiz · Labs (List · Editor)
        · Opportunities · Users · Bulk Import
System ─ Not Found · Error / Access Denied
```

---

## 4. Screen Inventory

Screen names link to their full specification in [Section 6](#6-screen-specifications).

### 4.1 Public (9)

| ID | Screen | Purpose | Status |
|---|---|---|---|
| P01 | [Landing](#p01-landing) | Explain the product, show the "not everything is code" bars, how it works, two entry paths | Prototype |
| P02 | [About MASAR](#p02-about-masar) | Mission, how recommendations work, honesty note, team | New |
| P03 | [Explore Tracks](#p03-explore-tracks) | All tracks grouped by category with search and filters | Prototype, extended |
| P04 | [Track Details](#p04-track-details) | Template for every track | Prototype, extended |
| P05 | [Log In](#p05-log-in) | Email and password | New |
| P06 | [Sign Up](#p06-sign-up) | Name, email, password | New |
| P07 | [Forgot Password](#p07-forgot-password) | Request a reset link | New |
| P08 | [Reset Password](#p08-reset-password) | Set a new password | New |
| P09 | [Email Confirmation](#p09-email-confirmation) | "Check your inbox" and "Email confirmed" states | New |

### 4.2 Onboarding and assessment (5)

| ID | Screen | Purpose | Status |
|---|---|---|---|
| O01 | [Welcome](#o01-welcome) | First-run greeting after sign up | New |
| O02 | [Choose Your Starting Point](#o02-choose-your-starting-point) | Two paths: take the assessment or explore tracks | Prototype (two Landing CTAs) |
| O03 | [Assessment Intro](#o03-assessment-intro) | Instructions, time estimate, "optional" message, privacy note | New |
| O04 | [Assessment Question](#o04-assessment-question) | Template: progress, question, 3 option cards, back, slide transition | Prototype |
| O05 | [Assessment Results](#o05-assessment-results) | Top 3 tracks with fit and reasons, RIASEC radar, "guidance, not a verdict" | Prototype |

> "Recommended Career Paths" from the owner's page list is merged into O05 to avoid duplicate content. **[Recommended]**

### 4.3 Learning app (15)

| ID | Screen | Purpose | Status |
|---|---|---|---|
| L01 | [Dashboard](#l01-dashboard) | Progress ring, next step, achievements, relevant opportunities | Prototype |
| L02 | [Roadmap Overview](#l02-roadmap-overview) | Stages and progress, track switcher, starting-point choice | Prototype, extended |
| L03 | [Stage Detail](#l03-stage-detail) | Tasks, resources, project, outcomes, estimated hours | New |
| L04 | [Learning Resources](#l04-learning-resources) | Library with search and filters | New |
| L05 | [Taster Labs Catalog](#l05-taster-labs-catalog) | All labs by category and status | Prototype, extended |
| L06 | [Lab Overview](#l06-lab-overview) | Scenario intro, time, what you will practice | New |
| L07 | [Lab Step](#l07-lab-step) | Template: scenario, optional terminal, 3 options, feedback, next | Prototype |
| L08 | [Lab Result and Reflection](#l08-lab-result-and-reflection) | Score, explanation, reflection, next actions | Prototype |
| L09 | [Learning Progress](#l09-learning-progress) | Per-track progress, history, XP over time | New |
| L10 | [Achievements and Badges](#l10-achievements-and-badges) | All badges, locked and unlocked | New (3 badges appear in the prototype Dashboard) |
| L11 | [Opportunities](#l11-opportunities) | Search, type chips, governorate and track filters, list | Prototype, extended |
| L12 | [Opportunity Details](#l12-opportunity-details) | Full details, eligibility, deadline, apply link, save | New |
| L13 | [Saved Items](#l13-saved-items) | Bookmarked opportunities and resources | New |
| L14 | [Profile](#l14-profile) | Name, avatar, governorate, education level, current track | New |
| L15 | [Settings](#l15-settings) | Language, theme, password change, delete account | New |

### 4.4 Admin (11) — all New

| ID | Screen | Purpose |
|---|---|---|
| A01 | [Admin Overview](#a01-admin-overview) | Counts, items needing review, broken-link reports |
| A02 | [Tracks List](#a02-tracks-list) | Table with status, category, completeness |
| A03 | [Track Editor](#a03-track-editor) | Template: tabs for Basics, Skills, Responsibilities, Prerequisites, Projects, Roles, Relations, Labs |
| A04 | [Roadmap Editor](#a04-roadmap-editor) | Stages and tasks with drag-and-drop, attach resources, versions |
| A05 | [Resources Manager](#a05-resources-manager) | Table with filters and verification status; edit in a modal |
| A06 | [Quiz Manager](#a06-quiz-manager) | Questions, options, weights |
| A07 | [Labs List](#a07-labs-list) | All labs and their status |
| A08 | [Lab Editor](#a08-lab-editor) | Scenario builder: steps, options, correct answer, feedback |
| A09 | [Opportunities Manager](#a09-opportunities-manager) | Table with workflow; edit in a drawer |
| A10 | [Users and Roles](#a10-users-and-roles) | User list and role assignment |
| A11 | [Bulk Import and Validation](#a11-bulk-import-and-validation) | Upload file, validation report, confirm import |

### 4.5 System (2)

| ID | Screen | Purpose |
|---|---|---|
| S01 | [Not Found (404)](#s01-not-found-404) | Friendly message and a way back |
| S02 | [Error and Access Denied](#s02-error-and-access-denied) | Generic failure and "you don't have access" variants |

**Total: 9 + 5 + 15 + 11 + 2 = 42 unique screens.**

### 4.6 Reusable templates

These are reused inside the 42 screens and are not counted as additional screens.

| # | Template | Used by |
|---|---|---|
| 1 | Track Details | P04, for all 19 tracks |
| 2 | Assessment Question | O04, for every question |
| 3 | Lab Step | L07, for every lab step |
| 4 | Track Editor (one layout with tabs) | A03 |
| 5 | Data table | A02, A05, A09, A10 |
| 6 | Detail / form page pattern | A03, A04, A06, A08 |

### 4.7 Modals and overlays (16)

Full specifications are in [Section 9](#9-modal-and-overlay-specifications).

| ID | Modal / overlay | Used from |
|---|---|---|
| M01 | Save my results (guest → sign-up prompt) | O05 |
| M02 | Exit assessment confirmation | O04 |
| M03 | Exit lab confirmation | L07 |
| M04 | Change starting point | L02 |
| M05 | Switch current track confirmation | L02, P03, P04 |
| M06 | Resource quick view | L03, L04 |
| M07 | Rate a resource | L03, L04 |
| M08 | Report a broken or outdated resource | L03, L04 |
| M09 | Stage completed (celebration) | L03 |
| M10 | Achievement unlocked (celebration) | Anywhere |
| M11 | Delete account confirmation | L15 |
| M12 | Sign out confirmation (optional) | Account menu |
| M13 | Resource editor | A05 |
| M14 | Opportunity editor (side drawer) | A09 |
| M15 | Publish / unpublish confirmation | Admin editors |
| M16 | Delete confirmation | Admin |

Also design **toasts** (success, error, info) and **tooltips**.

---

## 5. Shared Screen Patterns

Every screen specification in Section 6 uses these patterns. A screen's own "States" entry lists only what differs.

### 5.1 Page anatomy

| Zone | Specification |
|---|---|
| Top bar | ~58 px, sticky, border-bottom. Contents per [3.1](#31-learner-app) |
| Navigation | Desktop sidebar 220 px (fixed) or mobile bottom bar |
| Page header | Title (H1 or H2), one-line description in muted text, optional primary action on the end side |
| Content | Centered container: 980 px standard, 660 px narrow (assessment, results, lab, roadmap, auth forms), ~1200 px for Admin tables **[Recommended]** |
| Page bottom space (mobile) | ~96 px to clear the bottom bar |

### 5.2 State patterns

| State | Pattern | Status |
|---|---|---|
| **Loading (first load)** | Skeletons that match the final layout (rows for lists, cards for dashboards, stage blocks for roadmap). Layout must not jump when content arrives. A quiet full-page loader only on very first load | Recommended |
| **Loading (action)** | Spinner inside the pressed button; button stays the same width; other controls on the form disabled | Recommended |
| **Empty** | Small illustration or icon, one-line explanation, one primary action (see [Empty states](#53-empty-states)) | Recommended |
| **Success** | Toast for quick actions; inline success message for forms; celebration modal only for stage completion and achievements | Recommended |
| **Error (field)** | Inline message under the field, error color, with an icon; field border changes to error color | Recommended |
| **Error (action)** | Error toast with a **Retry** action | Recommended |
| **Error (page)** | Banner at the top of the content with a **Try again** button; content area keeps its skeleton or last known content | Recommended |
| **Offline** | Banner: "You're offline. Changes will not be saved until you reconnect." | Recommended |

### 5.3 Empty states

| Where | Title | Description | Action |
|---|---|---|---|
| Dashboard, no track chosen | Pick a track to begin | Take the assessment or browse tracks. | **Take the assessment** (primary) · **Explore tracks** (ghost) |
| Saved items | Nothing saved yet | Save opportunities and resources to find them here. | **Browse opportunities** |
| Opportunities, no results | No matches | Try removing a filter. | **Reset filters** |
| Resources, no results | No matches | Try a different search or remove a filter. | **Reset filters** |
| Achievements, none unlocked | Your first badge is one task away | Locked badges show how to unlock them. | **Go to my roadmap** |
| Progress, no activity | Complete your first task | Your history and XP will appear here. | **Open my roadmap** |
| Admin tables | No items yet | Add the first item to get started. | **Add** |

### 5.4 Error states

| Situation | Pattern |
|---|---|
| Form validation | Inline under the field, plus a summary banner at the top of long forms |
| Failed save | Toast with **Retry** |
| Network error | Page banner with **Try again** |
| Page not found | S01 |
| Access denied | S02 |
| Expired session | Modal asking the user to log in again; unsaved input stays visible behind the modal |
| Import validation errors | Row-level problems table in A11 |

### 5.5 Common responsive rules

Detailed behavior is in [Section 10](#10-responsive-specifications). In short:

- Two-column layouts collapse to one column below 760 px.
- Primary actions become full-width on mobile.
- Filters move into a **Filters** bottom sheet on mobile.
- Modals become full-screen sheets on mobile.
- Admin tables become stacked cards on mobile.

---

## 6. Screen Specifications

**How to read each entry.** Entries list purpose, layout and hierarchy, content, actions, inputs, navigation, states, and responsive behavior. Content values marked **[Sample]** are defined in [Section 7](#7-sample-content-library). States not listed follow [Section 5.2](#52-state-patterns). Responsive entries describe only what is specific to the screen; global rules are in [Section 10](#10-responsive-specifications).

### 6.1 Public Screens

#### P01 Landing
**[Prototype]** · Entry point for new visitors.

- **Purpose:** explain MASAR in under a minute and offer two clear entry paths.
- **Layout (top to bottom):** hero → "Not everything is code" bars → How it works (3 steps) → Featured tracks → Taster Labs teaser → Opportunities teaser → Final call to action → Footer.
- **Hero:** two columns on desktop. Text on the start side: H1 (Display), lead paragraph (muted), two buttons. The animated **route graphic** on the end side.
- **Content [Sample]:**
  - H1: "Find the tech path that fits you."
  - Lead: "Answer a few questions, try short labs, and follow a clear roadmap. Guidance, not a verdict."
  - Primary button: **Take the assessment** · Ghost button: **Explore tracks**
  - "Not everything is code" bars: horizontal bars comparing coding level across tracks (e.g., UI/UX Design: low, Cybersecurity Analyst: medium, Backend Development: high) with a caption: "Tech careers range from no code to code-heavy."
  - How it works: **1 Discover** (assessment) · **2 Try** (Taster Lab) · **3 Follow** (roadmap).
- **Actions:** Take the assessment → O02 (or O03 directly); Explore tracks → P03; track cards → P04; Labs teaser → L05; Opportunities teaser → L11.
- **Inputs:** none.
- **States:** bars animate on scroll reveal (600 ms); the route draws once (2400 ms). With reduced motion, all graphics appear static and complete.
- **Responsive:** hero stacks (text first, graphic below, graphic may shrink to ~60% height); both hero buttons become full-width and stacked; the bars section stays full-width with shorter labels truncated by ellipsis plus a visible value.

#### P02 About MASAR
**[New]**

- **Purpose:** build trust by explaining the mission and how recommendations work.
- **Layout:** narrow container. Mission → How recommendations work → Honesty note → Team → Contact.
- **Content [Sample]:**
  - Mission: "MASAR helps students choose a tech direction with confidence, using interests, hands-on trials, and clear roadmaps."
  - How recommendations work: 3 short steps with icons (answer questions → match against track profiles → show reasons you can review).
  - Honesty note (highlighted panel): "MASAR gives guidance, not a verdict. Your results are a starting point; you can change your track at any time."
  - Team: grid of cards (avatar, name, role). **[Open]** real team names and roles.
- **Actions:** **Take the assessment** → O02; **Explore tracks** → P03.
- **Inputs:** none.
- **States:** static page; no empty or error states beyond the global page error.
- **Responsive:** team grid 4 → 2 → 1 columns (desktop, tablet, mobile).

#### P03 Explore Tracks
**[Prototype], extended**

- **Purpose:** browse all 19 tracks and narrow them down.
- **Layout:** page header (title, description, search) → filter row → track list grouped by category (6 groups).
- **Content hierarchy:** category heading (H2) → track rows. Each **track row** shows an index or icon, track name (H3), one-line description (muted), coding-level tag, and a chevron. Prototype rows slide in on hover.
- **Filters:** category (chips), coding level (Low / Medium / High), difficulty (Beginner-friendly / Intermediate / Advanced). Selected chips use lime fill. A **Reset filters** link appears when any filter is active.
- **Inputs and validation:** search field (placeholder "Search tracks, skills, or tools"). Searching is live; no validation. Clearing with the ✕ button restores the list.
- **Actions:** track row → P04; **Set as my track** (secondary, in row overflow or on P04) → M05 if a track is already set.
- **States:** loading = 6 skeleton rows per visible group; empty results = [empty state](#53-empty-states) "No matches" with **Reset filters**; error = page banner.
- **Responsive:** desktop shows filters inline in one row; tablet wraps chips to two rows; mobile shows search plus a **Filters** button opening a bottom sheet with **Apply** and **Reset** buttons; category headings become sticky while scrolling.

#### P04 Track Details
**[Prototype], extended · Template used by all 19 tracks.** Example content: [7.2](#72-track-details-example).

- **Purpose:** give the learner enough information to decide whether to follow the track.
- **Layout (top to bottom):** header (breadcrumb, track name H1, category and coding-level tags, short intro, buttons) → What professionals do → Skills and tools → Prerequisites → Example projects → Roadmap preview → Recommended Taster Lab → Related tracks → Related opportunities.
- **Content hierarchy:** H1 track name; H2 per section; skills as chips; prerequisites as a checklist; projects as 2–3 cards; roadmap preview as a compact stage list with hour estimates.
- **Actions:** **View full roadmap** (primary) → L02 for this track; **Set as my track** (ghost) → M05 or direct confirmation toast if no track set; **Try the lab** → L06; related track card → P04; opportunity card → L12; **Save** icon on opportunity cards.
- **Inputs:** none.
- **States:** loading = skeleton header plus skeleton sections; a section with no content is **hidden**, not shown empty (except Prerequisites, which shows "No prerequisites — you can start today."); error = page banner.
- **Responsive:** single column below 760 px; header buttons stack full-width on mobile; the roadmap preview and related tracks become horizontal scrollers on mobile; a sticky bottom action bar with **View full roadmap** appears on mobile after scrolling past the header **[Recommended]**.

#### P05 Log In
**[New]**

- **Purpose:** return to a saved account.
- **Layout:** narrow container (660 px, form card ~420 px) centered; logo → title → form → links.
- **Content [Sample]:** Title "Welcome back" · Description "Log in to continue your roadmap."
- **Inputs and validation:**

| Field | Rules | Messages |
|---|---|---|
| Email | Required; valid email format | "Enter your email." · "That doesn't look like an email address." |
| Password | Required; show/hide toggle | "Enter your password." |

- **Actions:** **Log in** (primary, full width); **Forgot password?** link → P07; "New to MASAR? **Sign up**" → P06.
- **Result and feedback:** success → returns the learner to the screen they came from, else L01 (or O02 if no track); failure → banner above the form: "Email or password is incorrect. Try again or reset your password." Button returns from loading state.
- **States:** loading button; error banner; disabled button while a request is running.
- **Responsive:** form card becomes full-width with 20 px side padding; keyboard-safe layout so the primary button stays visible above the on-screen keyboard.

#### P06 Sign Up
**[New]**

- **Purpose:** create an account.
- **Layout:** same as P05.
- **Content [Sample]:** Title "Create your account" · Description "Save your results and track your progress."
- **Inputs and validation:**

| Field | Rules | Messages |
|---|---|---|
| Full name | Required; 2–60 characters | "Enter your name." |
| Email | Required; valid format | "That doesn't look like an email address." |
| Password | Required; minimum 8 characters, at least one letter and one number; show/hide toggle; live strength hint | "Use at least 8 characters with a letter and a number." |
| Agreement | Checkbox for terms and privacy, required | "Please accept the terms to continue." |

- **Actions:** **Create account** → P09 ("Check your inbox" state); "Already have an account? **Log in**" → P05.
- **Feedback:** inline validation on blur; password rules checklist updates as the user types.
- **Alternative paths:** if the email is already in use → inline message under email: "An account with this email exists. **Log in** instead?"
- **Responsive:** as P05.
- **[Open]** minimum password rules and whether terms/privacy pages are in scope.

#### P07 Forgot Password
**[New]**

- **Purpose:** request a reset link.
- **Layout:** narrow form card.
- **Content [Sample]:** Title "Reset your password" · Description "Enter your email and we'll send you a link."
- **Inputs:** Email (required, valid format).
- **Actions:** **Send reset link**; **Back to log in** → P05.
- **States:** success replaces the form with a confirmation panel: "If an account exists for this email, a reset link is on its way." (same message whether or not the account exists) with **Resend** (disabled for 30 seconds with a visible countdown) and **Back to log in**.
- **Responsive:** as P05.

#### P08 Reset Password
**[New]**

- **Purpose:** choose a new password from the emailed link.
- **Layout:** narrow form card.
- **Content [Sample]:** Title "Choose a new password".
- **Inputs and validation:** New password (same rules as P06) · Confirm password (must match: "Passwords don't match.").
- **Actions:** **Update password** → success toast "Password updated" → P05.
- **Alternative paths:** expired or used link → error panel: "This link has expired." with **Request a new link** → P07.
- **Responsive:** as P05.

#### P09 Email Confirmation
**[New]** · Two states on one screen.

- **State A, Check your inbox:** envelope icon · title "Check your inbox" · description "We sent a confirmation link to **nour@example.com**. It may take a minute." · buttons **Resend email** (30-second cooldown) and **Change email**.
- **State B, Email confirmed:** check icon · title "Email confirmed" · description "Your account is ready." · primary button **Continue** → O01.
- **State C, Link problem:** warning icon · title "This link isn't valid" · **Resend email**.
- **Responsive:** centered single column in all sizes.

### 6.2 Onboarding and Assessment Screens

#### O01 Welcome
**[New]** · Shown once after the first sign-in.

- **Purpose:** greet the learner and move them into choosing a start.
- **Layout:** narrow, centered: small route graphic → H1 → short paragraph → button.
- **Content [Sample]:** "Welcome, Nour." · "Let's find a direction that fits you. It takes about 5 minutes, and you can change your mind at any time."
- **Actions:** **Let's start** → O02; **Skip for now** (text link) → L01 in empty state.
- **Responsive:** buttons full-width on mobile.

#### O02 Choose Your Starting Point
**[Prototype]** · (two CTAs on Landing; this screen consolidates them.)

- **Purpose:** let the learner pick between guided discovery and direct exploring.
- **Layout:** narrow container; title and description; two large **choice cards** side by side on desktop.
- **Content [Sample]:**
  - Card 1: **Help me choose** — "Take a short assessment about your interests." · tag "About 5 min" · button **Start assessment** → O03.
  - Card 2: **I know what interests me** — "Browse all 19 tracks and pick one." · button **Explore tracks** → P03.
- **States:** hover raises card border to lime; focus ring visible; no selected state because a card click navigates.
- **Responsive:** cards stack vertically on mobile (below 760 px); the first card keeps visual priority (lime border).

#### O03 Assessment Intro
**[New]**

- **Purpose:** set expectations before the questions begin.
- **Layout:** narrow container; title → three info rows → privacy note → buttons.
- **Content [Sample]:**
  - Title: "A few questions about you"
  - Info rows: **10 questions** · **About 5 minutes** · **No right or wrong answers**
  - "Optional" message: "You don't have to take this. You can explore tracks any time."
  - Privacy note: "Your answers are used only to suggest tracks to you." **[Open]** final privacy wording.
- **Actions:** **Begin** (primary) → O04 question 1; **Explore tracks instead** (ghost) → P03; **Back** → O02.
- **Responsive:** buttons stack full-width on mobile.

#### O04 Assessment Question
**[Prototype]** · Template used by every question. Sample questions: [7.5](#75-assessment-questions-and-results).

- **Purpose:** collect one answer at a time with low effort.
- **Layout:** minimal chrome. Top: progress bar and "Question 3 of 10" label, with an **Exit** (✕) icon on the end side. Middle: question text (H2). Below: three **option cards** (A, B, C) stacked vertically. Bottom: **Back** button (ghost) on the start side.
- **Behavior:** tapping an option selects it (selected state) and advances automatically after a short pause (~300 ms) with a slide transition (400 ms; direction reverses in RTL). **Back** returns to the previous question with the earlier answer still selected. On the last question, the button area shows **See my results**.
- **Inputs and validation:** one required answer per question. If the user presses forward without an answer (only possible on the last question's explicit button), show an inline hint: "Choose an option to continue."
- **Actions:** Exit → M02; See my results → O05.
- **States:** loading between last question and results shows a short "Preparing your results…" panel with a progress animation (up to ~2 seconds); error → "We couldn't prepare your results" with **Try again**.
- **Responsive:** option cards full-width on all sizes; question text size steps down one level on mobile; the Back button is sticky at the bottom on mobile.

#### O05 Assessment Results
**[Prototype]**

- **Purpose:** show the top 3 recommended tracks, why they fit, and the learner's interest profile.
- **Layout (narrow container):** title and note → **Top 3 track cards** (rank 1 is visually emphasized) → **RIASEC radar chart** → "How to read this" note → actions.
- **Content hierarchy:** H1 "Your top matches"; honesty note directly below: "These are suggestions, not a verdict. You can explore any track." Each track card shows rank, track name, **fit percentage** with a progress bar, and 2–3 short **reasons** ("You enjoy analyzing patterns", "You prefer structured tasks"). Radar chart shows six axes: Realistic, Investigative, Artistic, Social, Enterprising, Conventional, with a short legend. See [7.5](#75-assessment-questions-and-results) for sample values.
- **Actions:**
  - Card **View track** → P04.
  - **Try a lab for this track** → L06.
  - **Save my results** → M01 for guests; for signed-in users it saves silently and shows a toast "Results saved".
  - **Retake assessment** → O03.
  - **Explore all tracks** → P03.
- **States:** loading = skeleton cards; saved = the Save button becomes a disabled "Saved ✓" state; error = page banner.
- **Responsive:** cards stack; radar chart sits below the cards and scales to the container with axis labels at least 12 px; labels may use short forms on mobile (R, I, A, S, E, C) with a legend list below. Buttons full-width.

### 6.3 Learning App Screens

#### L01 Dashboard
**[Prototype]**

- **Purpose:** show where the learner is and what to do next.
- **Layout (desktop):** greeting header → row with **Progress ring panel** and **Next step panel** → **Achievements panel** → **Relevant opportunities** panel. Container 980 px, two-column grid.
- **Content [Sample]:**
  - Greeting: "Good evening, Nour" · current track tag "Cybersecurity Analyst".
  - Progress ring: **28%** of the roadmap · caption "Stage 2 of 5".
  - Next step: "Next: Linux file permissions · 45 min" with **Continue** button → L03 at that task.
  - Achievements: 3 latest badges (unlocked highlighted) and a **View all** link → L10.
  - Opportunities: 2 cards matched to the current track with deadlines; **See all** → L11.
- **Actions:** Continue → L03; View all → L10; card → L12; track tag → L02.
- **States:** no track chosen = empty state ([5.3](#53-empty-states)); loading = skeleton panels; complete roadmap = ring shows 100% with a "Roadmap complete" message and a **Choose your next track** button.
- **Responsive:** panels stack in the order Next step, Progress ring, Achievements, Opportunities (next step first, because it is the main action); the ring shrinks to ~96 px.

#### L02 Roadmap Overview
**[Prototype], extended** · Example content: [7.3](#73-roadmap-example).

- **Purpose:** show the whole plan for the current track and the learner's position in it.
- **Layout (narrow container):** header with track name and **track switcher** → overall progress bar with hours → vertical **stage list** (each stage is a panel with a number marker, title, hours, task count, status).
- **Stage panel states:** stages are never locked **[Recommended]**; statuses are **Not started**, **In progress** (lime marker, shows "3 of 5 tasks"), **Completed** (check icon, progress bar full).
- **Starting point:** a line "Starting point: From scratch" with a **Change** link → M04.
- **Actions:** stage panel → L03; **Switch track** → M05; **Change** → M04; Resources link → L04.
- **States:** empty (no track chosen) = same empty state as Dashboard; loading = skeleton stage panels; error = banner.
- **Responsive:** same single-column layout at all sizes; stage hours and task counts wrap under the title on mobile; the track switcher becomes a full-width button opening a bottom sheet.

#### L03 Stage Detail
**[New]**

- **Purpose:** let the learner work through a single stage.
- **Layout:** breadcrumb (Roadmap › Stage 2) → stage header (title, estimated hours, progress) → **Tasks** list → **Resources** (Core and Optional groups) → **Stage project** → **Outcomes** ("After this stage you can…") → footer with **Mark stage complete**.
- **Task row:** checkbox, task title, estimated time, linked resource count. Checking a task updates stage progress immediately and shows a toast "Task done · +10 XP".
- **Resource row:** type icon, title, source, language tag, difficulty tag, verified badge, **Save** icon, **Open** (opens external page in a new tab, with an external-link icon), overflow menu (Rate, Report).
- **Actions:** Open resource → external; resource row body → M06; Rate → M07; Report → M08; **Mark stage complete** (enabled when all core tasks are checked) → M09; Next stage → L03 for the next stage.
- **Inputs:** checkboxes only.
- **States:** all tasks done but stage not marked = footer button highlighted with the hint "All tasks done — mark the stage complete"; stage complete = header shows "Completed" badge and button becomes **Go to next stage**; loading = skeleton task rows; empty resources = "No resources attached yet" (rare).
- **Responsive:** the footer action becomes a sticky bottom bar above the bottom navigation; Core and Optional resources become collapsible groups (Core open by default, Optional collapsed) on mobile.

#### L04 Learning Resources
**[New]** · Examples: [7.4](#74-learning-resources).

- **Purpose:** browse and filter all learning resources.
- **Layout:** header with search → filter row → results list (rows) with result count.
- **Filters:** type (video, article, course, book, documentation, practice), language (English, Arabic), difficulty, skill, track, and a **Verified only** switch.
- **Actions:** row body → M06; Save icon; overflow → Rate (M07) / Report (M08); Open → external.
- **Inputs:** search (live, no validation).
- **States:** loading = skeleton rows; empty = "No matches" with **Reset filters**; stale or broken resources show a status badge (see [11.10](#1110-tables-badges-and-progress)).
- **Responsive:** filters collapse into a **Filters** bottom sheet on mobile with an active-filter count badge on the button; result rows keep the title and badges on two lines.

#### L05 Taster Labs Catalog
**[Prototype], extended** · Examples: [7.6](#76-taster-labs).

- **Purpose:** let the learner pick a short hands-on lab.
- **Layout:** header → category chips → lab cards grouped by category.
- **Lab card:** title, one-line scenario, category tag, time (e.g., "10 min"), difficulty tag, status (**Available** or **Coming soon**).
- **Actions:** available card → L06; coming-soon card is non-navigating with a **Notify me** link **[Open]** (only if notifications are in scope).
- **States:** loading = skeleton cards; "Coming soon" cards use reduced emphasis and a tag, never hidden; empty category = hidden.
- **Responsive:** 3 columns desktop → 2 tablet (from 760 px) → 1 mobile.

#### L06 Lab Overview
**[New]**

- **Purpose:** prepare the learner before a lab starts.
- **Layout:** narrow container: title → meta row (time, steps, difficulty) → **Scenario** summary → **What you will practice** (3 bullets) → **Before you start** note → buttons.
- **Actions:** **Start lab** → L07 step 1; **Back to labs** → L05; if the lab was started earlier, **Resume** and **Restart**.
- **States:** coming-soon labs never reach this screen.
- **Responsive:** buttons full-width; the meta row wraps.

#### L07 Lab Step
**[Prototype]** · Template used by every lab step. Example: [7.6](#76-taster-labs).

- **Purpose:** present one decision in a realistic scenario.
- **Layout:** minimal chrome. Top: step progress ("Step 2 of 3") and **Exit** (✕). Then: **scenario text**; optional **terminal block** (monospace, always LTR); question; **three option cards**; **feedback block** (hidden until an answer is chosen); **Next** button.
- **Behavior:** the learner selects one option. The card shows **correct** (success color + check icon + label "Correct") or **incorrect** (error color + cross icon + label "Not quite"), the other cards become disabled, and the feedback block explains why. In the incorrect case the correct option is also highlighted. **Next** appears after answering; the last step shows **See result**.
- **Inputs and validation:** one choice per step; no free text.
- **Actions:** Exit → M03; Next → next step; See result → L08.
- **States:** the terminal block scrolls horizontally if lines are long; reduced motion = no slide transition.
- **Responsive:** terminal text stays 13.6 px with horizontal scroll; the Next button sits in a sticky bottom bar on mobile; on desktop the terminal and the options can sit in one column (narrow container).

#### L08 Lab Result and Reflection
**[Prototype]**

- **Purpose:** show how the learner did, explain, and suggest what to do next.
- **Layout:** narrow container: result header (score, e.g., "2 of 3 correct") → short **summary** → **What you practiced** chips → **Reflection** ("Did you enjoy this?" with three choices: Loved it, It was okay, Not for me) → **Next actions**.
- **Content [Sample]:** "Nice work, Nour. You spotted the scan pattern and chose a safe response." · XP earned "+30 XP".
- **Actions:** **View the Cybersecurity Analyst track** → P04; **Continue my roadmap** → L02; **Try another lab** → L05; **Retry this lab** (ghost).
- **Feedback:** choosing a reflection option shows a toast "Thanks — we'll use this to improve suggestions."
- **States:** a first-ever lab can trigger M10 (Achievement unlocked: Lab Rookie).
- **Responsive:** buttons stack full-width; reflection choices become three full-width rows.

#### L09 Learning Progress
**[New]**

- **Purpose:** show achievement over time.
- **Layout:** header with track selector → summary tiles (Overall progress, Hours logged, XP, Labs completed) → **XP over time** chart → **Per-track progress** list → **History** list (recent activity, grouped by date).
- **Chart:** simple line or bar chart by week; always accompanied by a text summary ("You earned 190 XP in the last 4 weeks") for accessibility.
- **Actions:** history row → relevant task or lab; track row → L02.
- **States:** no activity = empty state; loading = skeleton tiles and chart placeholder.
- **Responsive:** tiles 4 → 2 columns; chart height reduces; history rows show date on its own line.

#### L10 Achievements and Badges
**[New]** · Examples: [7.7](#77-progress-and-achievements).

- **Purpose:** celebrate progress and show what is still to unlock.
- **Layout:** header with unlocked count ("5 of 12 unlocked") and progress bar → filter chips (All, Unlocked, Locked) → badge grid.
- **Badge card:** icon, name, one-line description, unlock date (unlocked) or "how to unlock" with progress (locked).
- **Actions:** badge click opens a small detail popover (description, date).
- **States:** empty (none unlocked) = locked badges shown with hints; loading = skeleton grid.
- **Responsive:** grid 4 → 3 → 2 columns.

#### L11 Opportunities
**[Prototype], extended** · Examples: [7.8](#78-opportunities).

- **Purpose:** find internships, scholarships, programs, competitions, and events.
- **Layout:** header → search → **type chips** (All, Internship, Scholarship, Training program, Competition, Event) → secondary filters (governorate, track, deadline) → results list.
- **Opportunity card:** title, provider, type tag, location (governorate or Remote), **deadline** (coral when within 7 days, with the label "Closes in 6 days"), track tags, **Save** icon.
- **Actions:** card → L12; Save toggles bookmark with toast "Saved" / "Removed from Saved".
- **States:** loading = skeleton cards; empty = "No matches" with **Reset filters**; expired items are hidden by default with a **Show closed** switch.
- **Responsive:** filters collapse into a bottom sheet; cards full-width; deadline wraps under the provider.

#### L12 Opportunity Details
**[New]**

- **Purpose:** give full information and a clear way to apply.
- **Layout:** breadcrumb → header (title, provider, type tag, deadline) → meta grid (location, duration, cost, language) → **About** → **Eligibility** (checklist) → **How to apply** → **Related tracks** → **Similar opportunities**.
- **Actions:** **Apply** (primary, opens the external page in a new tab with an external-link icon and a one-time tip "You'll leave MASAR to apply") ; **Save** (ghost with icon); **Share** **[Recommended]**; **Report a problem** **[Recommended]**.
- **States:** closed opportunity = banner "This opportunity has closed" and **Apply** disabled; saved = filled bookmark; loading = skeleton.
- **Responsive:** meta grid 4 → 2 columns; **Apply** and **Save** in a sticky bottom bar on mobile.

#### L13 Saved Items
**[New]**

- **Purpose:** one place for bookmarked opportunities and resources.
- **Layout:** header → tabs (**Opportunities**, **Resources**) with counts → list.
- **Actions:** item → L12 or M06; remove via the filled bookmark icon with an **Undo** toast.
- **States:** empty per tab (see [5.3](#53-empty-states)); an item that closed or was archived shows a status badge and remains visible.
- **Responsive:** tabs scroll horizontally if needed; list rows as in L11 and L04.

#### L14 Profile
**[New]**

- **Purpose:** edit personal and learning details.
- **Layout:** header with avatar → form sections (**Personal**, **Education**, **Current track**).
- **Inputs and validation:**

| Field | Rules | Messages |
|---|---|---|
| Avatar | Image upload (jpg/png), ≤ 2 MB, or initials fallback | "Choose a JPG or PNG under 2 MB." |
| Full name | Required, 2–60 characters | "Enter your name." |
| Email | Read-only here; change via support **[Open]** | — |
| Governorate | Select from list, optional | — |
| Education level | Select (e.g., Year 1–5, Graduate), optional | — |
| Current track | Select from 19 tracks (change triggers M05) | — |

- **Actions:** **Save changes** (disabled until a change is made) → toast "Profile updated"; **Cancel** reverts.
- **States:** unsaved changes + navigating away shows a leave-confirmation **[Recommended]**; save error = toast with **Retry**.
- **Responsive:** one column; **Save changes** sticky at the bottom on mobile.

#### L15 Settings
**[New]**

- **Purpose:** manage preferences and account safety.
- **Layout:** sections as panels: **Language** · **Theme** · **Password** · **Danger zone**.
- **Content and controls:**
  - Language: segmented control **English / العربية**; switching changes direction immediately and shows a toast.
  - Theme: **Dark / Light / System** **[Open]**.
  - Password: Current password · New password · Confirm new password (rules as P06) · **Update password**.
  - Danger zone: **Delete account** (destructive button) → M11, with a short description of what is lost.
- **States:** password success toast "Password updated"; wrong current password = inline error "Current password is incorrect."
- **Responsive:** panels stack; the segmented controls stay on one line.

### 6.4 Admin Screens

All admin screens are **[New]**, restricted to administrators (non-admins see S02 access denied). They use the Data table and Detail/form templates, a ~1200 px content width on desktop, and the Admin navigation from [3.1](#31-learner-app). Sample values are in [7.9](#79-admin-dashboard-and-management-data).

#### A01 Admin Overview
- **Purpose:** show what needs attention.
- **Layout:** summary tiles (Tracks, Resources, Opportunities, Labs, Users) → **Needs review** list → **Broken or outdated link reports** list → recent activity.
- **Actions:** tile → matching manager; list item → editor for that item.
- **States:** empty needs-review = "Nothing needs review. Nice."; loading = skeleton tiles.
- **Responsive:** tiles 5 → 3 → 2 columns; lists become stacked cards.

#### A02 Tracks List
- **Purpose:** manage all 19 tracks.
- **Layout:** header with **Add track** → search and filters (status, category) → table.
- **Columns:** Name · Category · Status badge · Completeness (progress and "6 of 8 sections") · Updated · row actions.
- **Actions:** row → A03; **Add track** → A03 blank; row menu: Duplicate, Publish/Unpublish (M15), Delete (M16).
- **States:** empty = "No items yet" + **Add track**; loading = skeleton rows; bulk select shows a selection bar.
- **Responsive:** table becomes stacked cards (name, status, completeness) on mobile; filters in a sheet.

#### A03 Track Editor
**Template.**
- **Purpose:** author one track.
- **Layout:** header (track name, status badge, **Save draft**, **Publish**) → **tab bar** (Basics, Skills, Responsibilities, Prerequisites, Projects, Roles, Relations, Labs) → tab content → **completeness checklist** panel on the end side (desktop) or at the top (mobile, collapsible).
- **Inputs and validation:** Basics — Name (required, ≤ 60 characters), Category (required), Coding level (required), Difficulty (required), Short intro (required, ≤ 200 characters with counter). Other tabs use repeatable rows (add, remove, reorder).
- **Actions:** **Publish** requires a complete checklist, otherwise it is disabled with a tooltip "Complete all required sections"; Publish → M15; unsaved changes prompt on exit.
- **States:** saving = button spinner; saved = toast "Draft saved"; tab with errors shows a red dot.
- **Responsive:** tabs become a horizontally scrollable bar; the checklist becomes a collapsible panel; **Save draft** sticky at the bottom.

#### A04 Roadmap Editor
- **Purpose:** build stages and tasks for a track.
- **Entry:** the Admin **Roadmaps** menu item lists tracks and opens this editor for the chosen track; it is also reachable from A03.
- **Layout:** header (track, version, **Save draft**, **Publish**) → stage list with drag handles → each stage expands to task rows → side or sheet for **Attach resources**.
- **Inputs:** Stage title (required, ≤ 60), Stage hours (number, 1–200), Task title (required), Task time (minutes), Core/Optional toggle per resource.
- **Actions:** drag to reorder (also **Move up / Move down** buttons for keyboard use); **Add stage**; **Add task**; **Attach resource** (opens a picker listing verified resources); **Version history** drawer.
- **States:** empty = "No stages yet" + **Add stage**; unpublished changes badge.
- **Responsive:** drag handles remain; Move up/down buttons are visible on mobile; the resource picker is a full-screen sheet.

#### A05 Resources Manager
- **Purpose:** manage learning resources and their verification.
- **Layout:** header with **Add resource** and **Import** (→ A11) → filters (type, language, status, track) → table.
- **Columns:** Title · Type · Language · Difficulty · Verification status badge · Last checked · row actions.
- **Actions:** row or **Add resource** → M13; row menu: Mark verified, Mark stale, Delete (M16).
- **States:** empty, loading; broken-reported rows are highlighted with a status badge.
- **Responsive:** stacked cards; M13 becomes a full-screen sheet.

#### A06 Quiz Manager
- **Purpose:** manage assessment questions and weights.
- **Layout:** question list (numbered, reorderable) → selecting a question opens an edit panel (end side on desktop, full screen on mobile).
- **Inputs:** Question text (required, ≤ 200); three options (each required, ≤ 120); each option has a **dimension** (R, I, A, S, E, C) and **weight** (1–3).
- **Validation:** exactly 3 options; each question must map its options to dimensions; message "Add all three options."
- **Actions:** **Add question**, reorder, **Preview** (opens the O04 view), **Publish quiz** → M15.
- **States:** empty list; unsaved changes marker.
- **Responsive:** list and edit panel become two sequential screens.

#### A07 Labs List
- **Purpose:** see all labs and their status.
- **Layout:** header with **Add lab** → table (Title · Category · Steps · Time · Status badge · Updated).
- **Actions:** row → A08; **Add lab** → A08 blank; row menu: Publish/Unpublish, Delete.
- **States:** statuses: Draft, Published, Coming soon, Archived.
- **Responsive:** stacked cards.

#### A08 Lab Editor
- **Purpose:** build a lab scenario step by step.
- **Layout:** header (title, status, Save draft, Publish) → **Basics** (title, category, time, difficulty, intro) → **Steps** (list) → each step expands to Scenario text, optional Terminal text (monospace field), three options, **Correct option** selector, and **Feedback** text per option → **Preview** panel.
- **Inputs and validation:** every step needs scenario text, three options, a correct option, and feedback for each option ("Add feedback for option B.").
- **Actions:** Add step, reorder, duplicate step, **Preview as learner** (opens L07 layout).
- **Responsive:** Preview becomes a separate full-screen view.

#### A09 Opportunities Manager
- **Purpose:** manage the opportunities workflow.
- **Layout:** header with **Add opportunity** → filters (type, status, deadline) → table.
- **Columns:** Title · Provider · Type · Deadline · Status badge (Draft, In review, Published, Archived) · Updated.
- **Actions:** row or Add → M14 (side drawer); status changes through a **Change status** menu with M15 for publishing.
- **States:** deadlines within 7 days use coral text with an icon; expired items are suggested for archive.
- **Responsive:** stacked cards; the drawer becomes a full-screen sheet.

#### A10 Users and Roles
- **Purpose:** view users and assign roles.
- **Layout:** header with search → table (Name · Email · Role badge (Learner, Editor, Admin) · Joined · Last active).
- **Actions:** row menu: **Change role** (inline select with confirmation), **View profile**. Changing the only remaining Admin is blocked with a message.
- **States:** empty search = "No users match."; role change success toast.
- **Responsive:** stacked cards.

#### A11 Bulk Import and Validation
- **Purpose:** add many items at once safely.
- **Layout:** stepper (**1 Upload · 2 Review · 3 Confirm**) → step content.
- **Step 1:** drop zone and **Choose file** button; accepted types listed; template download link.
- **Step 2:** **validation report**: summary tiles (Rows read, Valid, Warnings, Errors) and a table of row-level problems (Row · Field · Problem). Filter: show only errors.
- **Step 3:** confirmation summary and **Import valid rows** button; **Cancel** returns without changes.
- **Alternative paths:** wrong file type = inline error; all rows invalid = **Import** disabled with explanation; user can **Download error report**.
- **Success:** toast "42 rows imported" and a link to A05.
- **Responsive:** stepper compacts to "Step 2 of 3"; table becomes stacked cards.

### 6.5 System Screens

#### S01 Not Found (404)
**[New]**

- **Purpose:** recover gracefully from a bad link.
- **Layout:** centered: simple route graphic with a broken path → "404" tag → title → description → buttons.
- **Content [Sample]:** "This page took a wrong turn." · "The page you're looking for doesn't exist or was moved."
- **Actions:** **Go home** (primary) → P01 or L01 depending on sign-in; **Explore tracks** (ghost) → P03.
- **Responsive:** same layout, buttons stack.

#### S02 Error and Access Denied
**[New]** · Two variants.

- **Variant A, Something went wrong:** title "Something went wrong" · description "We couldn't load this page. Your progress is safe." · **Try again** (primary) · **Go home** (ghost).
- **Variant B, Access denied:** title "You don't have access" · description "This area is for administrators." · **Go to my dashboard** (primary).
- **Variant C, Session expired:** handled by modal (see [5.4](#54-error-states)).
- **Responsive:** same as S01.

---

## 7. Sample Content Library

> **Everything in this section is [Sample].** It exists so that every screen can be designed with realistic, consistent content. None of it is confirmed project content. Replace it with approved content when available.

### 7.1 Learning Tracks

19 tracks in 6 categories. Coding level: **Low / Medium / High**. Difficulty: **Beginner-friendly / Intermediate / Advanced**.

| Code | Track | Category | Coding level | Difficulty | One-line description |
|---|---|---|---|---|---|
| T01 | Frontend Web Development | Software and Apps | High | Beginner-friendly | Build the parts of websites that people see and use. |
| T02 | Backend Development | Software and Apps | High | Intermediate | Build the logic and services that power applications. |
| T03 | Full-Stack Web Development | Software and Apps | High | Intermediate | Work across both the visible and the hidden sides of web apps. |
| T04 | Mobile App Development | Software and Apps | High | Intermediate | Create apps for phones and tablets. |
| T05 | Game Development | Software and Apps | High | Intermediate | Design and build interactive games. |
| T06 | Data Analysis | Data and AI | Medium | Beginner-friendly | Turn raw data into clear answers and charts. |
| T07 | Data Science | Data and AI | High | Advanced | Use statistics and code to find patterns and make predictions. |
| T08 | Machine Learning Engineering | Data and AI | High | Advanced | Build and deploy systems that learn from data. |
| T09 | Database Administration | Data and AI | Medium | Intermediate | Keep data organized, fast, and safe. |
| T10 | Cybersecurity Analyst | Security | Medium | Intermediate | Watch for threats and respond when something looks wrong. |
| T11 | Penetration Testing | Security | High | Advanced | Test systems for weaknesses before attackers do. |
| T12 | Network Engineering | Networks and Cloud | Medium | Intermediate | Design and maintain the networks that connect everything. |
| T13 | Cloud Computing | Networks and Cloud | Medium | Intermediate | Run applications on flexible, shared infrastructure. |
| T14 | DevOps Engineering | Networks and Cloud | High | Advanced | Automate how software is built, tested, and released. |
| T15 | Embedded Systems and IoT | Networks and Cloud | High | Advanced | Program the small computers inside devices. |
| T16 | UI/UX Design | Design and Quality | Low | Beginner-friendly | Design interfaces that are clear, usable, and pleasant. |
| T17 | Quality Assurance Testing | Design and Quality | Medium | Beginner-friendly | Find problems before users do. |
| T18 | IT Support and Systems Administration | IT Operations | Low | Beginner-friendly | Keep people and systems working. |
| T19 | Technical Project Management | IT Operations | Low | Intermediate | Plan, coordinate, and deliver technology projects. |

**Category counts:** Software and Apps 5 · Data and AI 4 · Security 2 · Networks and Cloud 4 · Design and Quality 2 · IT Operations 2 = **19**.

### 7.2 Track Details Example

**Track:** T10 Cybersecurity Analyst (used in all examples below).

| Section | Sample content |
|---|---|
| Intro | "Cybersecurity analysts monitor systems for threats, investigate suspicious activity, and help organizations respond quickly and calmly." |
| Tags | Security · Coding level: Medium · Intermediate |
| What professionals do | Monitor alerts and logs · Investigate suspicious activity · Write short incident reports · Recommend fixes to teams · Keep up with new threats |
| Skills and tools | Networking basics · Linux · Security fundamentals · Log analysis · Wireshark · Basic scripting |
| Prerequisites | Comfortable using a computer and the internet · Basic English reading for technical documentation · No programming required to start |
| Example projects | **Home network map** (document devices and traffic) · **Packet investigation** (analyze a sample capture) · **Incident report** (write a one-page report for a made-up alert) |
| Roadmap preview | 5 stages, about 150 hours (see 7.3) |
| Recommended lab | "Spot the Suspicious Traffic" (Wireshark, 10 minutes) |
| Related tracks | T12 Network Engineering · T11 Penetration Testing · T18 IT Support and Systems Administration |
| Related opportunities | Security Analyst Summer Internship · Cyber Defense Challenge 2027 (see 7.8) |

### 7.3 Roadmap Example

**Track:** T10 Cybersecurity Analyst · **5 stages · about 150 hours · 25 tasks.**

| Stage | Title | Hours | Tasks |
|---|---|---|---|
| 1 | Computing and Networking Foundations | 30 | 1. How data travels across the internet (1.5 h) · 2. IP addresses and DNS (2 h) · 3. Command line basics (3 h) · 4. Ports and protocols (2 h) · 5. **Project:** map your home network (4 h) |
| 2 | Operating Systems and Linux | 25 | 1. Install a Linux virtual machine (2 h) · 2. Files and folders (2 h) · 3. Linux file permissions (45 min) · 4. Users and processes (2 h) · 5. **Project:** harden a practice machine (4 h) |
| 3 | Security Fundamentals | 30 | 1. The CIA triad (1 h) · 2. Common attacks (3 h) · 3. Passwords and authentication (2 h) · 4. Encryption basics (3 h) · 5. **Project:** write a security checklist (3 h) |
| 4 | Monitoring and Analysis | 35 | 1. Reading logs (3 h) · 2. Packet analysis with Wireshark (4 h) · 3. How alerts and SIEM tools work (3 h) · 4. Incident response steps (2 h) · 5. **Project:** investigate a sample capture (5 h) |
| 5 | Practice and Portfolio | 30 | 1. Practice challenges (6 h) · 2. Write two incident reports (4 h) · 3. Build a portfolio page (4 h) · 4. Prepare for interviews (3 h) · 5. Choose an opportunity to apply for (1 h) |

**Stage outcomes (example, Stage 2):** "After this stage you can use the Linux command line, manage files and permissions, and secure a basic machine."

**Starting points [Sample behavior, Open]:**

| Choice | Meaning | Effect on roadmap |
|---|---|---|
| From scratch | No experience | Starts at Stage 1 |
| I know the basics | Comfortable with computers and some networking | Stage 1 shown as "Skipped, you can revisit"; starts at Stage 2 |
| I'm already practicing | Has hands-on experience | Stages 1–2 shown as skipped; starts at Stage 3 |

**Other tracks, stage titles only [Sample]:**
- **T01 Frontend Web Development:** 1 Web Basics · 2 Styling and Layout · 3 Interactive Pages · 4 Working with Data · 5 Portfolio Project.
- **T06 Data Analysis:** 1 Spreadsheets and Basics · 2 SQL Foundations · 3 Cleaning Data · 4 Visualization · 5 Analysis Portfolio.
- **T16 UI/UX Design:** 1 Design Basics · 2 Research · 3 Wireframes · 4 Prototypes · 5 Case Study.

### 7.4 Learning Resources

Titles are generic and fictional. Languages: EN = English, AR = Arabic. Status: **Verified**, **Needs review**, **Stale**, **Broken**.

| ID | Title | Type | Language | Difficulty | Time | Stage (T10) | Status |
|---|---|---|---|---|---|---|---|
| R01 | How the Internet Works, Illustrated | Video | EN | Beginner-friendly | 25 min | 1 | Verified |
| R02 | شرح عناوين الـ IP والـ DNS ببساطة | Video | AR | Beginner-friendly | 18 min | 1 | Verified |
| R03 | Command Line for Absolute Beginners | Course | EN | Beginner-friendly | 3 h | 1 | Verified |
| R04 | Linux Virtual Machine Setup Guide | Article | EN | Beginner-friendly | 20 min | 2 | Verified |
| R05 | Linux File Permissions Explained | Article | EN | Beginner-friendly | 15 min | 2 | Verified |
| R06 | Security Fundamentals Handbook | Book | EN | Intermediate | 6 h | 3 | Needs review |
| R07 | Common Web Attacks, Visual Guide | Article | EN | Intermediate | 40 min | 3 | Verified |
| R08 | Packet Analysis Basics with Wireshark | Video | EN | Intermediate | 55 min | 4 | Verified |
| R09 | Reading Security Logs Step by Step | Documentation | EN | Intermediate | 30 min | 4 | Stale |
| R10 | Beginner Capture-the-Flag Practice Set | Practice | EN | Intermediate | 4 h | 5 | Broken (reported) |

**Resource row example:** "Linux File Permissions Explained · Article · EN · Beginner-friendly · 15 min · Verified · ★ 4.6 (38)".

### 7.5 Assessment Questions and Results

**10 questions, 3 options each.** Each option is tied to one interest dimension (R Realistic, I Investigative, A Artistic, S Social, E Enterprising, C Conventional). The dimension tag is **admin-only** and never shown to the learner. **[Sample, Open]** final questions, count, and scoring.

| # | Question | Option A | Option B | Option C |
|---|---|---|---|---|
| 1 | You have a free weekend. What sounds most fun? | Taking apart a gadget to see how it works (R) | Solving a tricky puzzle online (I) | Designing a poster for a friend's event (A) |
| 2 | In a group project you usually… | Help teammates who are stuck (S) | Keep the plan and deadlines organized (C) | Pitch the idea to others (E) |
| 3 | Which task would you enjoy most? | Investigating why an app behaves strangely (I) | Building something you can touch or test (R) | Making a design look great (A) |
| 4 | You prefer work that is… | Clear, with defined steps (C) | Creative, with many possible answers (A) | Focused on helping people (S) |
| 5 | When something breaks, you… | Search for the root cause (I) | Try a hands-on fix right away (R) | Ask who else can help (S) |
| 6 | Pick a goal for next year. | Lead a small team (E) | Master a technical skill deeply (I) | Keep everything running smoothly (C) |
| 7 | Which sounds like a good day at work? | Convincing someone to try your idea (E) | Sketching a new interface (A) | Fixing real equipment or networks (R) |
| 8 | How do you like to learn? | Reading and researching on my own (I) | Doing a project with my hands (R) | Discussing with others (S) |
| 9 | You notice a mistake in a report. You… | Correct it carefully and log the change (C) | Explain it kindly to the author (S) | Rework the layout while you're at it (A) |
| 10 | Which headline would you want to write? | "Team launches a new product" (E) | "Researchers find the cause of a bug" (I) | "Company's data stays safe" (C) |

**Sample results for the sample learner (Nour):**

| Dimension | Score (0–100) |
|---|---|
| Realistic | 62 |
| Investigative | 88 |
| Artistic | 35 |
| Social | 41 |
| Enterprising | 48 |
| Conventional | 74 |

| Rank | Track | Fit | Reasons shown |
|---|---|---|---|
| 1 | T10 Cybersecurity Analyst | 91% | You enjoy investigating problems · You like structured, careful work · You're curious about how systems break |
| 2 | T06 Data Analysis | 86% | You like finding patterns · You prefer clear steps and accuracy |
| 3 | T17 Quality Assurance Testing | 82% | You notice details · You like checking that things work |

### 7.6 Taster Labs

| ID | Lab | Category | Time | Steps | Difficulty | Status |
|---|---|---|---|---|---|---|
| LB01 | Spot the Suspicious Traffic (Wireshark) | Security | 10 min | 3 | Beginner-friendly | Available |
| LB02 | Find the Missing Orders (SQL) | Data and AI | 12 min | 3 | Beginner-friendly | Available |
| LB03 | Why Does the Page Break? | Software and Apps | 10 min | 3 | Beginner-friendly | Available |
| LB04 | Fix the Checkout Flow (Figma) | Design and Quality | 15 min | 3 | Beginner-friendly | Available |
| LB05 | Trace the Lost Connection | Networks and Cloud | 12 min | 3 | Intermediate | Coming soon |
| LB06 | Launch Day Traffic Spike | Networks and Cloud | 15 min | 4 | Intermediate | Coming soon |

**Full example: LB01 Spot the Suspicious Traffic.**

- **Overview:** "You're a junior analyst. A colleague says the office network feels slow. You'll read a short packet capture and decide what to do." · **You will practice:** reading packet summaries · spotting scan patterns · choosing a safe response.

**Step 1 of 3**
- Scenario: "You open a capture from the office router. You want to see only the traffic from one laptop."
- Terminal block (always LTR):
  ```
  No.  Time   Source          Destination    Protocol  Info
  1    0.000  192.168.1.23    203.0.113.9    TCP       49152 > 443 [SYN]
  2    0.001  192.168.1.23    203.0.113.9    TCP       49153 > 80  [SYN]
  3    0.001  192.168.1.23    203.0.113.9    TCP       49154 > 22  [SYN]
  ```
- Question: "Which filter shows only traffic from 192.168.1.23?"
  - A. `ip.src == 192.168.1.23` — **Correct.** Feedback: "This filter keeps only packets whose source is that laptop."
  - B. `tcp.port == 192.168.1.23` — Feedback: "Ports are numbers like 80 or 443, not addresses."
  - C. `dns.name == laptop` — Feedback: "DNS filters match names in DNS packets, not a device's traffic."

**Step 2 of 3**
- Scenario: "The filtered list shows the laptop sending hundreds of connection attempts to the same address on many different ports within a second."
- Question: "What does this pattern most likely mean?"
  - A. A port scan — **Correct.** Feedback: "Many attempts to many ports in a short time is a typical scan pattern."
  - B. A normal web page loading — Feedback: "A page usually talks to a few ports, not hundreds."
  - C. A broken keyboard — Feedback: "Keyboards don't create network traffic."

**Step 3 of 3**
- Scenario: "You confirm the laptop is not part of any approved security test."
- Question: "What is the best next action?"
  - A. Delete the capture file — Feedback: "Keep evidence; you'll need it."
  - B. Report it to your team lead with the capture attached — **Correct.** Feedback: "Escalating with evidence lets the team investigate safely."
  - C. Ignore it until it happens again — Feedback: "Waiting can let a real problem grow."

**Result [Sample]:** "2 of 3 correct · +30 XP" · summary "You spotted the scan pattern and chose a safe response." · practiced chips: Packet filters · Scan patterns · Escalation.

**LB02 Find the Missing Orders (SQL), outline:** Step 1 choose the query that lists all orders from yesterday · Step 2 spot why 3 orders don't appear (a filter excludes them) · Step 3 choose the safest way to confirm the fix. Same format as LB01.

### 7.7 Progress and Achievements

**Sample learner progress (T10):**

| Item | Value |
|---|---|
| Overall progress | 28% (7 of 25 tasks done) |
| Current stage | 2 of 5: Operating Systems and Linux (2 of 5 tasks done) |
| Hours logged | 34 h |
| Total XP | 190 XP |
| Labs completed | 1 (LB01) |
| Current next step | "Linux file permissions · 45 min" |

**XP rules [Sample, Open]:** task +10 · project +30 · stage complete +50 · lab +30 · assessment +20.

**XP over the last 4 weeks (Progress chart):** Week 1: 20 · Week 2: 60 · Week 3: 50 · Week 4: 60.

**Recent history:**
- 19 Nov · Completed task "Files and folders" (+10 XP)
- 18 Nov · Completed Stage 1 (+50 XP)
- 15 Nov · Completed lab "Spot the Suspicious Traffic" (+30 XP)
- 12 Nov · Finished the assessment (+20 XP)

**12 badges [Sample, Open]:**

| Badge | How to unlock | Status for sample learner |
|---|---|---|
| First Steps | Complete your first task | Unlocked |
| Explorer | View 5 different tracks | Unlocked |
| Discovery | Finish the assessment | Unlocked |
| Lab Rookie | Finish your first lab | Unlocked |
| Stage Clear | Complete a stage | Unlocked |
| Bookworm | Open 10 resources | Locked (6 of 10) |
| Opportunity Hunter | Save 3 opportunities | Locked (1 of 3) |
| Halfway There | Reach 50% of a roadmap | Locked (28%) |
| Critic | Rate 3 resources | Locked (0 of 3) |
| Lab Explorer | Finish 3 labs | Locked (1 of 3) |
| Roadmap Finisher | Complete a full roadmap | Locked |
| Helper | Report a broken resource | Locked |

The Dashboard shows the three most recent unlocked badges (Stage Clear, Lab Rookie, Discovery).

### 7.8 Opportunities

Providers and details are fictional. Deadlines are relative to 21 November 2026.

| ID | Title | Provider | Type | Location | Deadline | Tracks | Eligibility (summary) |
|---|---|---|---|---|---|---|---|
| OP01 | Security Analyst Summer Internship | Delta Tech Hub | Internship | Cairo | 27 Nov 2026 (**closes in 6 days**, coral) | T10, T11 | Students in year 3 or above; basic networking knowledge |
| OP02 | Cyber Defense Challenge 2027 | Nile Security Club | Competition | Remote | 15 Dec 2026 | T10, T11 | Open to all university students; teams of 3 |
| OP03 | Data Analysis Bootcamp Scholarship | Horizon Learning | Scholarship | Remote | 10 Dec 2026 | T06, T07 | Students and recent graduates; English B1 or above |
| OP04 | Frontend Training Program | Pixel Academy | Training program | Alexandria | 5 Jan 2027 | T01, T03 | No experience required; 8 weeks, part-time |
| OP05 | UI/UX Design Workshop | Craft Studio | Event | Giza | 30 Nov 2026 (**closes in 9 days**) | T16 | Open to all; limited seats |
| OP06 | Cloud Fundamentals Internship | Skyline Systems | Internship | Remote | 20 Jan 2027 | T13, T14 | Students in year 3 or above |
| OP07 | National Student Hackathon | Tech Forward | Competition | Mansoura | 12 Feb 2027 | T01–T05 | Open to all university students |
| OP08 | IT Support Starter Program | Bridge IT | Training program | Cairo | 28 Feb 2027 | T18, T12 | No experience required |

**Opportunity Details example (OP01):**
- **About:** "A 6-week paid internship where you will work with the security team on monitoring, reporting, and practice investigations."
- **Meta:** Location Cairo · Duration 6 weeks · Cost Free · Language English.
- **Eligibility:** Studying computer science or related field · Year 3 or above · Basic networking knowledge · Available full-time for 6 weeks.
- **How to apply:** "Apply on the provider's website. You'll need your CV and a short motivation paragraph."
- **Related tracks:** Cybersecurity Analyst · Penetration Testing.

### 7.9 Admin Dashboard and Management Data

**A01 summary tiles:** Tracks **19** (17 published, 2 drafts) · Resources **142** · Opportunities **38** (6 in review) · Labs **6** (4 published, 2 coming soon) · Users **1,240**.

**Needs review (examples):** 9 resources awaiting verification · 6 opportunities in review · Track "Embedded Systems and IoT" is 5 of 8 sections complete.

**Broken or outdated reports:** R10 Beginner Capture-the-Flag Practice Set (broken, reported 2 times) · R09 Reading Security Logs Step by Step (stale, reported 1 time).

**A02 Tracks List rows:**

| Name | Category | Status | Completeness | Updated |
|---|---|---|---|---|
| Cybersecurity Analyst | Security | Published | 8 of 8 | 14 Nov 2026 |
| Data Analysis | Data and AI | Published | 8 of 8 | 10 Nov 2026 |
| Frontend Web Development | Software and Apps | Published | 8 of 8 | 8 Nov 2026 |
| Embedded Systems and IoT | Networks and Cloud | Draft | 5 of 8 | 19 Nov 2026 |
| Game Development | Software and Apps | Draft | 4 of 8 | 17 Nov 2026 |

**A05 Resources rows:** see [7.4](#74-learning-resources), plus a "Last checked" column (e.g., R05: 2 Nov 2026; R09: 3 Aug 2026).

**A09 workflow example:** OP01 Published · OP02 Published · OP03 In review · OP08 Draft · an expired 2025 item Archived.

**A10 Users rows:**

| Name | Email | Role | Joined | Last active |
|---|---|---|---|---|
| Nour Hassan | nour@example.com | Learner | 12 Nov 2026 | Today |
| Karim Adel | karim@example.com | Editor | 3 Sep 2026 | Yesterday |
| Mariam Saad | mariam@example.com | Admin | 1 Jun 2026 | Today |

**A11 validation report example:** Rows read **42** · Valid **36** · Warnings **3** · Errors **3**.

| Row | Field | Problem |
|---|---|---|
| 7 | Link | Not a valid web address |
| 15 | Language | Must be "English" or "Arabic" |
| 28 | Title | Missing |

### 7.10 Sample Learner

| Field | Value |
|---|---|
| Name | Nour Hassan |
| Email | nour@example.com |
| Governorate | Cairo |
| Education level | Year 3, Computer Science |
| Current track | Cybersecurity Analyst (T10) |
| Starting point | From scratch |
| Language / theme | English / dark |

---

## 8. User Flows

**Flow index.** F01–F09 are the flows from the original document (preserved and expanded). F10–F15 are added to cover interactions the original screens imply.

| ID | Flow | Status |
|---|---|---|
| [F01](#f01-first-visit-with-assessment) | First visit, not sure what to choose | Original |
| [F02](#f02-knows-the-track) | Knows the track | Original |
| [F03](#f03-guest-saves-results) | Guest saves results | Original |
| [F04](#f04-learning-loop) | Learning loop | Original |
| [F05](#f05-taster-lab) | Taster Lab | Original |
| [F06](#f06-opportunities) | Opportunities | Original |
| [F07](#f07-password-reset) | Password reset | Original |
| [F08](#f08-admin-publishes-content) | Admin publishes content | Original |
| [F09](#f09-admin-bulk-import) | Admin bulk import | Original |
| [F10](#f10-returning-learner-logs-in) | Returning learner logs in | New |
| [F11](#f11-switch-current-track) | Switch current track | New |
| [F12](#f12-save-and-unsave-items) | Save and unsave items | New |
| [F13](#f13-profile-and-settings) | Profile and settings | New |
| [F14](#f14-rate-and-report-a-resource) | Rate and report a resource | New |
| [F15](#f15-admin-manages-quiz-labs-opportunities-and-users) | Admin manages quiz, labs, opportunities, and users | New |

Each table lists the **start**, the user's **action**, the **result and feedback**, the **next screen or state**, and **alternatives or errors**.

### F01 First Visit with Assessment
**Path:** Landing → Choose Starting Point → Assessment Intro → Questions → Results → Track Details → Lab → Start roadmap → Roadmap.

| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | P01 Landing | Taps **Take the assessment** | Page transition (450 ms) | O02 | **Explore tracks** → F02 |
| 2 | O02 | Chooses **Help me choose** | Card border turns lime | O03 | **I know what interests me** → P03 |
| 3 | O03 | Reads info, taps **Begin** | Progress bar appears at 0 of 10 | O04 question 1 | **Explore tracks instead** → P03 |
| 4 | O04 | Selects an option | Option shows selected state; auto-advance after ~300 ms with a slide transition | Next question | **Back** → previous question with answer kept; **Exit** → M02 |
| 5 | O04 (last question) | Selects an option, taps **See my results** | "Preparing your results…" panel | O05 | Failure → "We couldn't prepare your results" with **Try again** |
| 6 | O05 | Reviews top 3 and radar, taps **View track** on #1 | Page transition | P04 for that track | **Save my results** → F03; **Retake** → O03 |
| 7 | P04 | Taps **Try the lab** | Page transition | L06 | **View full roadmap** → step 10 |
| 8 | L06 | Taps **Start lab** | Lab begins at step 1 | L07 | Leave → L05 |
| 9 | L07 → L08 | Completes steps (see F05) | Result and reflection | L08 | See F05 |
| 10 | L08 or P04 | Taps **Set as my track** then **Continue my roadmap** | Toast "Cybersecurity Analyst is now your track" | L02 | Guests are prompted to sign up first (M01 pattern) |

### F02 Knows the Track
**Path:** Landing/Explore → Track Details → Roadmap → choose starting point.

| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | P01 or P03 | Taps **Explore tracks** (or a track card) | Track list or details open | P03 / P04 | No matches → "No matches" with **Reset filters** |
| 2 | P03 | Searches or filters, taps a track | Results update live; row slides in on hover | P04 | Mobile: filters in bottom sheet |
| 3 | P04 | Reads details, taps **View full roadmap** | Roadmap opens in preview or full mode | L02 | Guest sees the roadmap as read-only preview with a **Sign up to track progress** banner |
| 4 | L02 | Taps **Change** next to starting point (or picks one on first visit) | M04 opens with three choices | M04 | Close → keeps current choice |
| 5 | M04 | Selects a starting point, taps **Apply** | Stages update; toast "Starting point updated" | L02 | **Cancel** closes without change |
| 6 | L02 | Taps first available stage | Stage opens | L03 | — |

### F03 Guest Saves Results
**Path:** Results → "Save my results" modal → Sign Up → Email Confirmation → Welcome → Dashboard.

| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | O05 (guest) | Taps **Save my results** | M01 opens: "Create a free account to keep your results." | M01 | **Not now** closes; results stay visible this session only |
| 2 | M01 | Taps **Sign up** | Results held for the sign-up journey | P06 | **Log in** link → P05 then back to O05 saved |
| 3 | P06 | Completes the form, taps **Create account** | Button loading; inline validation if needed | P09 state A | Email taken → inline "Log in instead?" |
| 4 | P09 | Opens the emailed link | "Email confirmed" | P09 state B | Invalid or expired link → state C with **Resend email** |
| 5 | P09 | Taps **Continue** | Page transition | O01 | — |
| 6 | O01 | Taps **Let's start** | Welcome shown once | L01 | **Skip for now** → L01 empty state |
| 7 | L01 | Sees the saved top track as current track suggestion | Toast "Your results were saved" | L01 | If no track set, the empty state offers choices |

### F04 Learning Loop
**Path:** Dashboard → next step → Stage Detail → open resource → mark task done → stage complete celebration → Dashboard.

| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | L01 | Taps **Continue** on Next step | Page transition | L03 at the task | No track → empty state |
| 2 | L03 | Taps **Open** on a resource | Opens an external page in a new tab; external-link icon shown | External tab | Broken link → user taps **Report** → F14 |
| 3 | L03 | Returns, checks the task checkbox | Checkbox fills; progress updates; toast "Task done · +10 XP" | L03 | Unchecking removes XP with a toast "Task unmarked" |
| 4 | L03 | Completes the final core task | Footer hint "All tasks done — mark the stage complete" | L03 | Optional tasks never block completion |
| 5 | L03 | Taps **Mark stage complete** | M09 celebration (short, dismissible) | M09 | Reduced motion = static celebration |
| 6 | M09 | Taps **Go to next stage** or **Back to dashboard** | Toast or navigation | L03 (next stage) / L01 | A new badge may trigger M10 first |
| 7 | L01 | Sees updated ring and next step | Progress ring animates (1000 ms) | L01 | — |

### F05 Taster Lab
**Path:** Labs Catalog → Lab Overview → Steps (feedback after each) → Result and Reflection → Roadmap or another lab.

| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | L05 | Taps an **Available** lab card | Page transition | L06 | **Coming soon** card is not clickable |
| 2 | L06 | Taps **Start lab** (or **Resume**) | Step 1 appears | L07 | **Restart** clears progress |
| 3 | L07 | Selects option A, B, or C | Correct: green card, check icon, "Correct", feedback. Incorrect: red card, cross icon, "Not quite", correct option highlighted, feedback | Same step, answered | Other options disabled after answering |
| 4 | L07 | Taps **Next** | Slide transition | Next step | **Exit** → M03: **Leave lab** or **Keep going** |
| 5 | L07 (last) | Taps **See result** | Result screen | L08 | — |
| 6 | L08 | Chooses a reflection option | Toast "Thanks — we'll use this to improve suggestions." | L08 | May trigger M10 (Lab Rookie) |
| 7 | L08 | Taps **Continue my roadmap**, **Try another lab**, or **View track** | Navigation | L02 / L05 / P04 | **Retry this lab** → L06 |

### F06 Opportunities
**Path:** Opportunities → filters → Opportunity Details → Apply (external) / Save → Saved.

| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | L11 | Opens Opportunities | List loads (skeletons first) | L11 | Error → banner with **Try again** |
| 2 | L11 | Taps a type chip, sets governorate or track | List updates; chip turns lime | L11 | No results → "No matches" + **Reset filters** |
| 3 | L11 | Taps a card | Page transition | L12 | Closed items are hidden unless **Show closed** is on |
| 4 | L12 | Taps **Save** | Bookmark fills; toast "Saved" | L12 | Guest → prompt to log in |
| 5 | L12 | Taps **Apply** | Tip "You'll leave MASAR to apply", then opens the external page in a new tab | External tab | Closed opportunity = **Apply** disabled with banner |
| 6 | Account menu | Opens **Saved** | Opportunities tab shows the item | L13 | Empty → "Nothing saved yet" |

### F07 Password Reset
**Path:** Log In → Forgot Password → email → Reset Password → Log In.

| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | P05 | Taps **Forgot password?** | Page transition | P07 | — |
| 2 | P07 | Enters email, taps **Send reset link** | Confirmation panel (same message for every email) | P07 confirmation | Invalid format → inline error |
| 3 | P07 | (Optional) taps **Resend** | Cooldown countdown 30 s | P07 confirmation | — |
| 4 | Email | Opens the link | Reset form | P08 | Expired link → "This link has expired." + **Request a new link** → P07 |
| 5 | P08 | Enters and confirms a new password, taps **Update password** | Toast "Password updated" | P05 | Mismatch → "Passwords don't match." |

### F08 Admin Publishes Content
**Path:** Tracks List → Track Editor → Roadmap Editor → Resources → verification → publish confirmation.

| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | A02 | Taps a track (or **Add track**) | Editor opens | A03 | — |
| 2 | A03 | Fills tabs, taps **Save draft** | Toast "Draft saved"; checklist updates | A03 | Validation error = red dot on tab + inline messages |
| 3 | A03 | Opens **Roadmap** link | Roadmap editor opens | A04 | Unsaved changes prompt |
| 4 | A04 | Adds stages and tasks, attaches resources | Rows added; drag to reorder | A04 | Attach picker shows only verified resources by default |
| 5 | A05 | Marks attached resources verified | Status badge changes to Verified | A05 | Stale or broken resources show warning in A04 |
| 6 | A03 | Taps **Publish** (enabled when checklist is complete) | M15 opens listing what will go live | M15 | Disabled button with tooltip when incomplete |
| 7 | M15 | Taps **Publish** | Toast "Track published"; status badge = Published | A02 | **Cancel** closes |

### F09 Admin Bulk Import
**Path:** Bulk Import → upload → validation report → fix or confirm → Resources Manager.

| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | A05 | Taps **Import** | Stepper step 1 | A11 | — |
| 2 | A11 | Drops or chooses a file | File name and size shown | A11 step 2 | Wrong type = inline error |
| 3 | A11 | Reviews the validation report | Tiles show Rows, Valid, Warnings, Errors; table lists problems | A11 step 2 | **Download error report**; **Show only errors** |
| 4 | A11 | Fixes the file and re-uploads, or accepts valid rows | Report refreshes | A11 step 3 | All rows invalid = **Import** disabled |
| 5 | A11 | Taps **Import valid rows** | Progress then toast "36 rows imported" | A05 | **Cancel** discards without changes |

### F10 Returning Learner Logs In
| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | Any public page | Taps **Log in** | Page transition | P05 | — |
| 2 | P05 | Enters email and password, taps **Log in** | Button loading | L01 (or the screen they came from) | Wrong credentials = banner "Email or password is incorrect." |
| 3 | L01 | Sees their dashboard | Greeting by name | L01 | No track = empty state |

### F11 Switch Current Track
| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | L02, P03, or P04 | Taps **Switch track** / **Set as my track** | M05 opens: "Switch to Data Analysis?" with a note "Your progress in Cybersecurity Analyst is kept." | M05 | **Cancel** closes |
| 2 | M05 | Taps **Switch track** | Toast "Data Analysis is now your track" | L02 for the new track | Earlier progress remains available under L09 |

### F12 Save and Unsave Items
| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | L04, L03, L11, L12 | Taps the bookmark icon | Icon fills; toast "Saved" | Same screen | Guest = login prompt |
| 2 | L13 | Taps the filled bookmark | Item leaves list; toast "Removed from Saved" with **Undo** | L13 | **Undo** restores; empty list shows empty state |

### F13 Profile and Settings
| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | Account menu | Opens **Profile** | Form shows current values | L14 | — |
| 2 | L14 | Edits fields, taps **Save changes** | Toast "Profile updated" | L14 | Invalid field = inline message; save failure = toast with **Retry** |
| 3 | Account menu | Opens **Settings** | Panels | L15 | — |
| 4 | L15 | Switches language | Direction and text change instantly; toast "Language updated" | L15 | — |
| 5 | L15 | Taps theme choice | Theme changes instantly | L15 | — |
| 6 | L15 | Updates password | Toast "Password updated" | L15 | Wrong current password = inline error |
| 7 | L15 | Taps **Delete account** | M11 asks to type "DELETE" to confirm | M11 | **Cancel** closes; confirm → P01 with toast "Account deleted" |

### F14 Rate and Report a Resource
| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | L03 or L04 | Opens resource overflow menu, taps **Rate** | M07: 1–5 stars and optional comment | M07 | **Cancel** closes |
| 2 | M07 | Selects stars, taps **Submit** | Toast "Thanks for your rating" | Same screen | No stars = inline "Choose a rating." |
| 3 | L03 or L04 | Taps **Report** | M08: reason (Link broken, Outdated, Wrong language, Other) and optional note | M08 | **Other** requires a note |
| 4 | M08 | Taps **Send report** | Toast "Report sent. Thank you." | Same screen | Failure = toast with **Retry** |

### F15 Admin Manages Quiz, Labs, Opportunities, and Users
| # | Start | User action | Result and feedback | Next | Alternative / error |
|---|---|---|---|---|---|
| 1 | A06 | Edits a question and its option weights, taps **Save** | Toast "Question saved" | A06 | Missing option = inline "Add all three options." |
| 2 | A07 → A08 | Opens a lab, edits steps, taps **Preview as learner** | L07 layout preview | A08 | Missing feedback = "Add feedback for option B." |
| 3 | A09 | Opens or adds an opportunity in the drawer (M14), saves | Drawer closes; toast "Opportunity saved" | A09 | Missing deadline = inline error |
| 4 | A09 | Changes status to **Published** | M15 confirmation; badge updates | A09 | **Cancel** closes |
| 5 | A10 | Changes a user's role | Confirmation, then toast "Role updated" | A10 | Last admin cannot be demoted |
| 6 | Any admin table | Deletes an item | M16 confirmation, then toast | Same table | **Cancel** closes |

---

## 9. Modal and Overlay Specifications

### 9.1 Global rules **[Confirmed from original; details Recommended]**

| Rule | Specification |
|---|---|
| Width | 480 px on desktop; 640 px for editors; full-screen sheet on mobile |
| Drawer | Opens from the **end** side (right in LTR, left in RTL), 480 to 560 px wide; full-screen sheet on mobile **[Recommended]** |
| Scrim | 60% of the background color. Click outside closes, unless there are unsaved changes |
| Structure | Header (title + close), body, footer. Primary action on the **end** side (right in LTR, left in RTL) |
| Destructive actions | Use the error color and ask for confirmation |
| Focus | Trapped inside; `Esc` closes; focus returns to the trigger |
| Celebrations | Short, dismissible, respect reduced motion |
| Mobile bottom sheets | For short choices (filters, switcher): slide up, drag handle, max height 85% of the screen |

### 9.2 Modal catalog

| ID | Title | Body content [Sample] | Buttons (primary on end side) | Result |
|---|---|---|---|---|
| M01 | Save your results | "Create a free account to keep your results and start your roadmap." | **Sign up** (primary) · **Log in** · **Not now** | → P06 / P05 / closes |
| M02 | Leave the assessment? | "Your answers so far will be lost." | **Leave** (destructive ghost) · **Keep going** (primary) | Leaves to O02 / stays |
| M03 | Leave this lab? | "Your progress in this lab will be lost." | **Leave lab** · **Keep going** (primary) | Leaves to L05 / stays |
| M04 | Change starting point | Three radio cards: From scratch · I know the basics · I'm already practicing, each with a one-line explanation | **Apply** (primary) · **Cancel** | Updates L02 |
| M05 | Switch current track | "Switch to Data Analysis? Your progress in Cybersecurity Analyst is kept." | **Switch track** (primary) · **Cancel** | Updates current track |
| M06 | Resource quick view | Title, type, source, language, difficulty, time, verified badge, short description | **Open resource** (primary) · **Save** · **Close** | Opens external page / saves |
| M07 | Rate this resource | 5-star control, optional comment (≤ 200 characters with counter) | **Submit** (primary) · **Cancel** | Toast "Thanks for your rating" |
| M08 | Report a problem | Reason radios (Link broken, Outdated, Wrong language, Other), optional note (required for Other) | **Send report** (primary) · **Cancel** | Toast "Report sent. Thank you." |
| M09 | Stage completed | Celebration graphic, "Stage 2 complete", XP earned, a note about what comes next | **Go to next stage** (primary) · **Back to dashboard** | Navigates |
| M10 | Achievement unlocked | Badge icon, name, description, "+XP" if any | **Nice!** (primary) · **View all badges** | Closes / → L10 |
| M11 | Delete your account? | Explains what is lost (profile, progress, saved items). Field: type DELETE to confirm | **Delete account** (destructive, disabled until text matches) · **Cancel** | → P01 + toast |
| M12 | Sign out? (optional) | "You'll need to log in again to continue." | **Sign out** (primary) · **Cancel** | → P01 |
| M13 | Resource editor (640 px) | Fields: Title, Link, Type, Language, Difficulty, Time, Skills, Tracks, Verification status | **Save** (primary) · **Cancel** | Toast "Resource saved" |
| M14 | Opportunity editor (drawer) | Fields: Title, Provider, Type, Location, Deadline, Tracks, Eligibility, How to apply, Link, Status | **Save** (primary) · **Cancel** | Toast "Opportunity saved" |
| M15 | Publish or unpublish | Summary of what changes and who will see it | **Publish** / **Unpublish** (primary) · **Cancel** | Status badge updates |
| M16 | Delete this item? | Names the item; "This can't be undone." | **Delete** (destructive) · **Cancel** | Removes item + toast |

### 9.3 Toasts and tooltips

| Element | Specification | Status |
|---|---|---|
| Toast types | Success, error, info (and warning if the warning color is approved) | Prototype (success); others New |
| Placement | Bottom center on mobile above the bottom bar; bottom end corner on desktop | Recommended |
| Duration | Success and info about 4 seconds; error stays until dismissed or acted on | Recommended |
| Content | Icon + one short sentence + optional action (**Undo**, **Retry**). Never color-only | Recommended |
| Stacking | Max 3 visible; newest on top | Recommended |
| Tooltip | Appears on hover and on keyboard focus; short text (≤ 8 words); never holds essential information | Recommended |

---

## 10. Responsive Specifications

### 10.1 Breakpoints **[Confirmed]**

| Name | Width | Navigation | Layout |
|---|---|---|---|
| Mobile | 360 to 699 px | Bottom bar | Single column; track rows 3 columns |
| Tablet | 700 to 899 px | Bottom bar | Track rows 4 columns from 700 px; two-column grids only from 760 px (700–759 stays single column) |
| Desktop | ≥ 900 px | Sidebar (220 px) | Container 980 px (narrow 660 px; Admin ~1200 px) |

**Frame sizes [Recommended]:** mobile 390 × 844 · tablet 820 × 1180 · desktop 1440 × 1024.

> **Clarification.** The original document listed track rows as "3 columns on mobile → 4 columns from 700 px" and two-column grids "from 760 px". Both are kept; this means tablet widths 700–759 px show four-column track rows but single-column panel grids.

### 10.2 Layout behavior by breakpoint

| Area | Desktop (≥ 900) | Tablet (700–899) | Mobile (360–699) |
|---|---|---|---|
| Navigation | Fixed sidebar + top bar | Bottom bar + top bar. A landscape tablet ≥ 900 uses the sidebar | Bottom bar (5 items + More) + top bar |
| Content width | 980 px (narrow 660, Admin ~1200) | Fluid with 20 px side padding | Fluid with 20 px side padding |
| Grids | Up to 3–4 columns | Two columns from 760 px | One column |
| Breadcrumbs | Visible | Visible | Replaced by Back button |
| Primary action | Inline at the end of the header | Inline | Full-width; sticky bottom bar on L03, L07, L12, L14, A03 |
| Filters | Inline row | Inline, wrapped | **Filters** bottom sheet with Apply and Reset |
| Modals | 480 / 640 px centered | 480 / 640 px centered | Full-screen sheet |
| Drawers | 480–560 px from the end edge | Same | Full-screen sheet |
| Tables (Admin) | Full table | Table with horizontal scroll if needed | Stacked cards, one per row |
| Charts | Full size | Scale to container | Reduced height; text summary below; shortened axis labels |

### 10.3 Collapsible and scrolling behavior

| Element | Behavior | Status |
|---|---|---|
| Resource groups on L03 (Core, Optional) | Mobile: collapsible, Core open and Optional closed; desktop: both open | Recommended |
| Completeness checklist (A03) | Desktop: side panel; mobile: collapsible panel at the top | Recommended |
| Track Details sections | Roadmap preview and related tracks scroll horizontally on mobile | Recommended |
| Category headings (P03) | Sticky on mobile | Recommended |
| Top bar | Sticky on all sizes | Prototype |
| Bottom bar | Fixed; hides while scrolling down on long pages and returns on scroll up | Recommended |
| Terminal block | Horizontal scroll inside the block; page never scrolls sideways | Recommended |
| Wide content (tables, code) | Scrolls inside its own container | Recommended |
| Page padding | ~96 px bottom space on mobile to clear the bottom bar | Prototype |

### 10.4 Navigation changes

- **Desktop → mobile:** the sidebar's seven items become the five-item bottom bar plus a **More** sheet (Discover, Labs, Resources, Saved).
- **Admin on mobile:** the Admin menu becomes a full-screen menu opened from a menu button in the top bar (a bottom bar is not used in Admin).
- **Account menu:** dropdown on desktop; full-width sheet on mobile.
- **Language and theme controls:** remain in the top bar on all sizes; on very narrow widths the language switch shows "ع / EN" in a compact form.

### 10.5 Screen groups at a glance

| Group | Desktop | Tablet | Mobile |
|---|---|---|---|
| Landing | Two-column hero | Two-column hero from 760 px | Stacked hero, full-width buttons |
| Explore and Opportunities | Inline filters, list | Wrapped filters | Search + Filters sheet |
| Track Details | One column in narrow container, sections stacked | Same | Sticky bottom action bar; scrollers for previews |
| Assessment and Labs | Narrow container, no side nav | Same | Full width; sticky bottom action |
| Dashboard | Two-column panel grid | Two columns from 760 px | Single column, Next step first |
| Roadmap and Stage | Narrow container | Same | Collapsible resource groups |
| Auth | Form card centered | Same | Full-width form |
| Admin | Wide tables, side panels | Tables with scroll | Stacked cards, full-screen sheets |

---

## 11. Design System

All values in 11.1–11.4 marked **[Prototype]** are approved and must not change. Values marked **[Recommended]** fill gaps the prototype did not define.

### 11.1 Colors and Themes

#### Palette **[Prototype]**

| Token | Dark | Light | Use |
|---|---|---|---|
| `bg` | `#0A1C20` | `#F5F2EA` | Page background (with a subtle dotted grid) |
| `s1` (surface) | `#10282D` | `#FFFFFF` | Panels, nav, inputs |
| `s2` (surface 2) | `#173439` | `#EAE5D8` | Selected states, progress track, badges |
| `bd` (border) | `rgba(220,240,230,.12)` | `rgba(10,28,32,.15)` | All borders |
| `tx` (text) | `#E9F1EC` | `#0E2A2E` | Primary text |
| `mu` (muted) | `#8FA8A6` | `#566D6C` | Secondary text |
| `br` (brand lime) | `#C6F36B` | `#C6F36B` | Primary buttons, active markers |
| `brt` (brand text/accent) | `#C6F36B` | `#2F6B12` | Brand-colored text, bars, icons |
| `on` (on-brand text) | `#0A1C20` | `#0A1C20` | Text on lime |
| `co` (coral) | `#FF7A59` | `#D8502B` | Logo dot, urgent deadlines |
| `ok` (success) | `#5EE0A0` | `#1E9E6A` | Correct answers |
| `er` (error) | `#FF6B6B` | `#D44A4A` | Wrong answers, errors |

**[New] Warning color** (not in the approved palette; needs approval): `#F5B74A` dark / `#B7791F` light. Used for "Needs review" and "Stale" status and warning alerts only.

#### Semantic use

| Meaning | Token | Always paired with |
|---|---|---|
| Primary action, active, selected | `br` / `brt` | Fill or marker plus label |
| Urgency (deadline ≤ 7 days) | `co` | Clock icon and text "Closes in N days" |
| Success / correct | `ok` | Check icon and text |
| Error / incorrect | `er` | Cross or alert icon and text |
| Warning / needs review | warning | Warning icon and text |
| Information | `tx` or `brt` | Info icon |

#### Themes

| Rule | Specification | Status |
|---|---|---|
| Theme set | Dark and Light, switchable from the top bar and Settings | Prototype |
| Text on light backgrounds | Use `brt` (dark green), never `br` (lime), for text and thin icons. Lime on the light background has a contrast of only 1.14:1 | Prototype (practice confirmed) |
| Lime fills | `br` is used as a **fill** with `on` text in both themes (contrast 13.7:1) | Prototype |
| Dotted grid | Subtle on `bg` in both themes; disabled behind dense tables and forms | Recommended |
| Images and graphics | Route graphic, radar chart, and illustrations use tokens so both themes work | Recommended |
| Default theme | **[Open]** dark, light, or follow system | Open |

#### Contrast reference (calculated against WCAG 2.x; text needs 4.5:1, large text and meaningful icons 3:1)

| Pair | Dark theme | Light theme | Notes |
|---|---|---|---|
| `tx` on `bg` / `s1` / `s2` | 15.2 / 13.4 / 11.5 | 13.5 / 15.1 / 12.0 | Pass |
| `mu` on `bg` / `s1` / `s2` | 6.9 / 6.1 / 5.2 | 4.9 / 5.5 / **4.4** | Light theme: do not use `mu` for small text on `s2` |
| `brt` on `bg` / `s1` / `s2` | 13.7 / 12.1 / 10.4 | 5.8 / 6.5 / 5.2 | Pass |
| `on` on `br` | 13.7 | 13.7 | Pass |
| `co` on `bg` / `s1` | 6.8 / 6.0 | **3.7 / 4.1** | Light theme: icon or large/bold text only; keep message text in `tx` |
| `ok` on `bg` / `s1` | 10.5 / 9.3 | **3.1 / 3.4** | Light theme: icon, border, or large text only |
| `er` on `bg` / `s1` | 6.3 / 5.6 | **3.9 / 4.3** | Light theme: icon, border, or large text only; message text in `tx` |
| Warning on `bg` / `s1` | 9.8 / 8.6 | **3.3 / 3.6** | Same rule as above |

**Rule:** in the light theme, coral, success, error, and warning colors are used for icons, borders, fills, and large or bold text. Small message text beside them uses `tx`. This keeps the approved palette unchanged while meeting contrast.

### 11.2 Typography

#### Fonts **[Prototype]**

| Role | Font | Weights |
|---|---|---|
| English headings | Space Grotesk | 500, 700 |
| English body | Inter | 400, 500, 600 |
| Arabic headings | Cairo | 500, 700, 800 |
| Arabic body | IBM Plex Sans Arabic | 400, 500 |
| Code / terminal | System monospace | Regular |

#### Scale **[Prototype]**

| Style | Size / line-height | Notes |
|---|---|---|
| Display / H1 | 37 to 67 px, fluid with screen width / 1.05 | Tracking −3%. Arabic: line-height 1.3, tracking 0 |
| H2 | 24 px / 1.3 | Bold |
| H3 | 17.6 px | Semibold |
| Body | 16 px / 1.7 | |
| Lead | 17.6 px | Muted |
| Small | 13.6 px | |
| Tag / label | 11.5 px, uppercase, +8% tracking | English only; supporting text only, never the sole carrier of meaning |
| Code / terminal | 13.6 px | Always LTR |

#### Usage rules **[Recommended]**

- One H1 per screen. Headings do not skip levels.
- Line length 60–75 characters for body paragraphs; narrow container (660 px) enforces this.
- Left/start alignment for body text; center only for hero, empty states, auth headers, and celebrations.
- Button labels use the body font at weight 600 (English) or 500 (Arabic).
- Numbers inside tables use tabular figures where the font supports them.

### 11.3 Spacing and Sizing

| Token | Value | Use | Status |
|---|---|---|---|
| Scale | 4, 8, 12, 16, 20, 24, 32, 48 px | All spacing | Recommended (normalizes the prototype) |
| Panel padding | 18 px in the prototype → use **16 or 20 px** from the scale | Cards, panels | Recommended |
| Gap between items | 10 px in the prototype → use **8 or 12 px** | Lists, grids | Recommended |
| Container side padding | 20 px | Mobile and tablet | Prototype |
| Section spacing | 32 px (mobile) / 48 px (desktop) | Between page sections | Recommended |
| Top bar height | ~58 px | | Prototype |
| Sidebar width | 220 px | | Prototype |
| Bottom bar height | 64 px plus device safe area | | Recommended |
| Minimum touch target | 44 × 44 px | All tappable elements | Recommended |
| Control height | Large 48 · Default 44 · Small 36 px | Buttons, inputs, selects | Recommended |
| Container widths | 980 px standard · 660 px narrow · ~1200 px Admin | | Prototype / Recommended (Admin) |
| Icon sizes | 16, 20, 24 px | | Recommended |

### 11.4 Radius, Elevation, and Motion

| Token | Value | Status |
|---|---|---|
| Radius: panels / option cards | 14 px | Prototype |
| Radius: buttons | 12 px | Prototype |
| Radius: chips / tags / pills | 99 px | Prototype |
| Radius: small controls (inputs, selects, checkboxes) | 8 to 10 px | Prototype |
| Radius: modals and drawers | 14 px (inner edge only for drawers) | Recommended |
| Elevation | **Flat.** Borders instead of shadows. Hover/active uses border color and 2 to 4 px movement | Prototype |
| Overlay layer | Modals, drawers, popovers, and toasts use a 1 px border in `bd` plus the scrim; no decorative shadows | Recommended |
| Easing | Ease curve (0.2, 0.7, 0.2, 1) | Prototype |
| Durations | Page enter 450 ms · quiz slide 400 ms · scroll reveal 600 ms · progress fill 1000 ms · route draw 2400 ms | Prototype |
| Small interactions | Hover, pressed, toast enter: 150–250 ms | Recommended |
| Reduced motion | All animations are disabled or replaced by instant changes when the user asks for reduced motion | Prototype |

### 11.5 Buttons

| Variant | Appearance | Use | Status |
|---|---|---|---|
| **Primary** | Lime fill (`br`), `on` text, radius 12 | One per view or per modal footer | Prototype |
| **Ghost** | Transparent, `bd` border, `tx` text | Secondary actions | Prototype |
| **Destructive** | `er` border and text (ghost style); filled `er` only inside confirmation modals | Delete, leave | New |
| **Text link** | `brt` text, underline on hover/focus | Tertiary navigation | New |
| **Icon button** | 44 px square target, 20 px icon, tooltip or visible label nearby | Close, bookmark, overflow | New |

| Property | Specification | Status |
|---|---|---|
| Sizes | Large 48 · Default 44 · Small 36 px height | Recommended |
| Padding | 20 px horizontal (default) | Recommended |
| Hover | Lifts 2 px (primary); border highlight (ghost) | Prototype |
| Pressed | Scale to about 97% | Recommended |
| Disabled | 40% opacity, no hover effect | Recommended |
| Loading | Spinner replaces the leading icon; label remains; width does not change | Recommended |
| Focus | See [12.3](#123-focus-and-interactive-states) | Recommended |
| Icon use | Optional leading icon; directional icons mirror in RTL | Recommended |

**Component structure:** one **Button** component with variant, size, state, icon, and direction properties.

### 11.6 Inputs and Form Components

| Component | Specification | Status |
|---|---|---|
| Text input | `s1` fill, `bd` border, radius 8–10, 44 px height, 16 px text | Prototype (basic) |
| Search input | Text input with leading search icon and a trailing clear (✕) button when filled | Prototype |
| Select | Same as text input with trailing chevron; menu opens as a popover (desktop) or bottom sheet (mobile) | Prototype (basic) |
| Textarea | Same styling; shows a character counter when a limit exists | New |
| Password input | Text input with show/hide toggle; stays LTR in RTL | New |
| Checkbox / radio / switch | Off, on, disabled, focus. Lime fill when on; 44 px target including label | New |
| Segmented control | 2–3 options (language, theme); selected = lime fill | New |
| File upload / drop zone | Dashed `bd` border; states: default, drag-over (lime border), uploading, error | New |
| Form field wrapper | Label above, input, helper text, then error text | New |
| Option card (A/B/C) | Full-width radio-style card, radius 14 | Prototype |

**Field states:** default · hover · focus · filled · error · success · disabled · read-only.

**Form rules [Recommended]**

- Labels are always visible above fields; placeholders are examples only.
- Required fields are the default; mark **optional** fields with "(optional)" text instead of asterisks.
- Validate on blur, then on change after the first error. Never validate an empty field before the user leaves it.
- Error text: icon + sentence that says what to do ("Enter your email."), directly under the field, linked to the field for screen readers.
- Long forms add an error summary at the top with links to each field.
- Submit buttons are never disabled just because the form is empty; they validate and explain. (Exception: confirmation fields such as "type DELETE".)
- The primary submit button sits at the end of the form; on mobile it is full-width.

### 11.7 Cards and Panels

| Component | Description | Variants / states | Status |
|---|---|---|---|
| **Panel** | `s1` fill, `bd` border, radius 14, 16–20 px padding | Default; interactive (hover border lime-tinted); selected (`s2` fill) | Prototype |
| **Track row** | Index/icon, name, description, tag, chevron | Default, hover (slides in), focus | Prototype |
| **Track card** | Compact track summary (Landing, related tracks) | Default, hover, focus | New (derived from Track row) |
| **Choice card** | Large card for two-path choices (O02) | Default, hover, focus | New |
| **Option card** | A/B/C answers | Default, hover, selected, correct, incorrect, disabled | Prototype |
| **Lab card** | Title, scenario, time, difficulty, status | Available, coming soon, completed | Prototype / New |
| **Opportunity card** | Title, provider, tags, deadline, save | Default, urgent deadline, closed, saved | Prototype / New |
| **Resource row** | Type icon, title, meta, badges, actions | Default, saved, stale, broken | New |
| **Badge card** | Icon, name, description | Locked (reduced emphasis, shows progress), unlocked | Prototype |
| **Stat tile** | Number, label, optional trend | Default | New |
| **Terminal block** | Monospace text in a darker `s2` panel, always LTR | Default, scrollable | Prototype |
| **Feedback block** | Explanation after an answer | Correct, incorrect, neutral | Prototype |

### 11.8 Navigation Components

| Component | Specification | Status |
|---|---|---|
| Top bar | ~58 px, sticky, border-bottom; logo, language, theme, account | Prototype |
| Sidebar item | Icon + label; states: default, hover, active (lime marker), focus | Prototype |
| Bottom bar item | Icon + short label; same states; active label bold | Prototype |
| More sheet | Bottom sheet with 4 items (Discover, Labs, Resources, Saved) | Recommended |
| Account menu | Dropdown (desktop) / sheet (mobile): Profile, Settings, Saved, Sign out | New |
| Tabs | Default, active (lime underline), disabled; scrollable on mobile | New |
| Breadcrumb | Text links with separators; last item is plain text | Recommended |
| Stepper | Done (check), current (lime), upcoming (muted); used in A11 | New |
| Pagination | Previous, page numbers, next; active = lime fill | New |
| Filter chip | Default, selected (lime), hover, focus | Prototype |

### 11.9 Overlays, Alerts, and Toasts

| Component | Specification | Variants |
|---|---|---|
| Modal | See [Section 9](#9-modal-and-overlay-specifications) | Standard (480 px), editor (640 px), confirm, celebration |
| Drawer | End-side panel, 480–560 px | Editor |
| Bottom sheet | Mobile only, 85% max height, drag handle | Filters, pickers, More |
| Popover / dropdown | `s1` panel with border; closes on `Esc` and outside click | Menu, select options |
| Tooltip | Short helper, on hover and focus | Default |
| Alert / banner | Full-width panel with icon, message, optional action and dismiss | Info, success, warning, error |
| Toast | Short confirmation with optional action | Success, info, error (warning optional) |

**Alert anatomy:** icon (24 px) · title (optional, semibold) · message (≤ 2 lines) · action (optional text link). Left/start border accent in the semantic color. Text uses `tx`.

### 11.10 Tables, Badges, and Progress

#### Data table (Admin) **[New]**

| Property | Specification |
|---|---|
| Header | `s2` fill, small semibold text; sortable columns show an arrow, and the sort direction is announced to screen readers |
| Rows | 52 px height; hover shows `s2`; selected row has lime marker and `s2` fill |
| Cells | Text truncates with ellipsis; full text in tooltip; numbers right-aligned (mirrored in RTL) |
| Actions | Row menu (overflow icon) at the end; primary action = click row |
| Footer | Result count and pagination |
| Empty | Centered empty state inside the table area |
| Mobile | Stacked cards: title, status badge, two key facts, overflow menu |

#### Status badges **[New]**

Every badge has **icon + text**, never color alone.

| Status | Where | Color |
|---|---|---|
| Draft | Tracks, labs, opportunities | Muted outline |
| In review / Needs review | Opportunities, resources | Warning |
| Published | Tracks, labs, opportunities | Success |
| Archived | Opportunities, labs | Muted fill (`s2`) |
| Verified | Resources | Success |
| Stale | Resources | Warning |
| Broken | Resources | Error |
| Coming soon | Labs | Muted outline |
| Closed | Opportunities | Muted fill |
| Role: Learner / Editor / Admin | Users | Neutral outline (Admin uses lime outline) |

#### Chips and tags

- **Chip** (interactive filter): pill, selectable, lime when selected. **Tag** (non-interactive label): small outlined pill. Do not style tags like chips.

#### Progress indicators

| Component | Specification | Status |
|---|---|---|
| Progress bar | `s2` track, `brt` fill, 8 px height, fills start→end (right→left in RTL); label with percentage or count | Prototype |
| Progress ring | Ring with centered percentage; 0%, partial, complete (check) | Prototype |
| Fit bar (results) | Progress bar with percentage label | Prototype |
| Stepper | See navigation | New |
| Skeleton | Line, card, row, tile shapes in `s2`, subtle shimmer (off for reduced motion) | New |
| Spinner | 20 px, inside buttons or small areas | New |
| Rating stars | 5 stars, filled/empty, keyboard operable | New |
| Avatar | Image or initials, sizes 32 / 40 / 96 | New |

### 11.11 Component Inventory and Variants

**Reusable component?** Yes = one master component. **Variants** = properties to define.

| Component | Reusable | Variants / properties | States to design | Status |
|---|---|---|---|---|
| Button | Yes | Variant (primary, ghost, destructive, text, icon) · size · icon | default, hover, pressed, focus, disabled, loading | Prototype (primary, ghost); others New |
| Chip / filter chip | Yes | Selected on/off · with count | default, hover, selected, focus | Prototype |
| Tag | Yes | Neutral, coding-level, category | default | Prototype |
| Status badge | Yes | One per status | default | New |
| Panel | Yes | Static, interactive, selected | default, hover, selected | Prototype |
| Top bar | Yes | Signed in/out · LTR/RTL · desktop/mobile | default | Prototype |
| Sidebar item, bottom-nav item | Yes | Active on/off | default, hover, active, focus | Prototype |
| Track row / Track card | Yes | Row vs card | default, hover, focus | Prototype |
| Option card | Yes | Quiz vs lab | default, hover, selected, correct, incorrect, disabled | Prototype |
| Choice card | Yes | — | default, hover, focus | New |
| Lab card | Yes | Available, coming soon, completed | default, hover | Prototype / New |
| Opportunity card | Yes | Default, urgent, closed, saved | default, hover | Prototype / New |
| Resource row | Yes | Saved, stale, broken | default, hover | New |
| Task row with checkbox | Yes | Core / optional | default, hover, done | Prototype |
| Badge card | Yes | Locked / unlocked | default, hover | Prototype |
| Stat tile | Yes | With/without trend | default | New |
| Progress bar / ring | Yes | Size · with label | 0%, partial, complete | Prototype |
| Radar chart | Yes | 6 axes; full vs compact labels | with data | Prototype |
| Route hero graphic | One-off | Static for reduced motion | animated, static | Prototype |
| Terminal block | Yes | — | default, scrollable | Prototype |
| Feedback block | Yes | Correct, incorrect, neutral | default | Prototype |
| Text input / search / select / textarea | Yes | Type · size | default, hover, focus, filled, error, success, disabled | Prototype (basic); errors New |
| Checkbox, radio, switch | Yes | — | off, on, disabled, focus | New |
| Segmented control | Yes | 2 or 3 options | default, selected, focus | New |
| Form field wrapper | Yes | With helper, with error, with counter | default, error, success | New |
| File drop zone | Yes | — | default, drag-over, uploading, error | New |
| Tabs | Yes | Scrollable | default, active, disabled | New |
| Breadcrumb / stepper / pagination | Yes | — | default, active | New |
| Dropdown / account menu | Yes | Desktop menu, mobile sheet | closed, open | New |
| Modal / drawer / bottom sheet | Yes | Standard, editor, confirm, celebration | open, closing | New |
| Tooltip | Yes | — | default | New |
| Alert / banner | Yes | Info, success, warning, error | default | New |
| Toast | Yes | Success, info, error | enter, visible, exit | Prototype (success); others New |
| Data table | Yes | Row density · selectable | default, sorted, row hover, selected, empty | New |
| Skeleton | Yes | Line, card, row, tile | loading | New |
| Avatar | Yes | Image, initials · size | default | New |
| Rating stars | Yes | Read-only, interactive | default, hover, selected | New |
| Page header | Yes | With/without action, breadcrumb | default | New (pattern) |

All **[New]** components follow the same visual language: flat surfaces, thin borders, lime as the single primary accent, coral for urgency only.

**Iconography [Open]:** the prototype's icon style is not documented. Recommended: one outline icon set at 24 px grid with 1.5–2 px stroke, consistent corner treatment, filled variant only for selected states (bookmark, active nav). Directional icons mirror in RTL; others do not (see [Section 13](#13-arabic-rtl-requirements)).

---

## 12. Accessibility and Interface Consistency

### 12.1 Text readability and contrast

- Body text is 16 px minimum with 1.7 line-height; supporting text is never below 13.6 px, except uppercase tags (11.5 px) which only repeat information found elsewhere.
- Meet the contrast values in [11.1](#111-colors-and-themes): 4.5:1 for text, 3:1 for large text, icons, and component borders that carry meaning.
- Follow the light-theme rule: coral, success, error, and warning colors are not used for small text.
- Do not place text over the dotted grid in tables or forms; do not place text over images.
- Support text zoom to 200% without horizontal scrolling or overlapping content (except tables and terminal blocks, which scroll inside their own container).
- Arabic text keeps its larger line-height and has no letter-spacing.

### 12.2 Clear button labels

| Guideline | Good | Avoid |
|---|---|---|
| Start with a verb that says the result | "Save my results" · "View full roadmap" | "Submit" · "Click here" |
| Say what happens next | "Mark stage complete" | "Done" |
| Same action, same label everywhere | **Set as my track** on every screen | "Choose track" in one place and "Select" in another |
| Destructive actions name the object | "Delete account" · "Delete resource" | "OK" · "Yes" |
| Pair cancel with a clear opposite | "Keep going" / "Leave lab" | "Cancel" / "OK" when meaning is unclear |
| Icon-only buttons have a text name | Tooltip + accessible name "Save opportunity" | Unlabeled icons |
| External links say so | "Apply (opens provider's site)" with icon | Plain "Apply" with no hint |

### 12.3 Focus and interactive states

- Every interactive element has a **visible focus ring**: 2 px lime with 2 px offset in dark theme, `brt` in light theme **[Recommended; the prototype has none]**. The ring must be visible against every surface.
- Focus order follows reading order (mirrored in RTL).
- Hover is never the only way to discover a control or its information.
- States (default, hover, focus, pressed, disabled, selected) are defined in [Section 11.11](#1111-component-inventory-and-variants); disabled is 40% opacity and is not focusable unless it explains itself through a tooltip.
- Correct and incorrect answers use border color **plus icon plus text label** ("Correct", "Not quite").
- Selected items use fill or marker plus a checkmark or "selected" label, not color alone.

### 12.4 Consistent spacing and alignment

- Use only the spacing scale in [11.3](#113-spacing-and-sizing).
- All pages start with the same header pattern: title, one-line description, optional primary action at the end side.
- Align primary actions to the end side of forms, modals, and headers (right in LTR, left in RTL).
- Keep icon size and stroke consistent; align icons to the text baseline center.
- Same component = same padding, radius, and border everywhere; do not create one-off variants.
- Lists of cards use equal heights per row in a grid.

### 12.5 Form feedback and validation

- Errors appear next to the problem, in text, with an icon; they say **how to fix it**.
- Never clear what the user typed after an error (except passwords on a failed log in).
- Success is confirmed with a toast or inline message; destructive success also offers **Undo** where possible.
- Loading states keep the layout stable and tell the user an action is running.
- Time-limited actions (resend email) show a visible countdown.

### 12.6 Keyboard-friendly interaction

| Pattern | Behavior |
|---|---|
| Tab / Shift+Tab | Moves through controls in reading order |
| Enter / Space | Activates buttons, toggles checkboxes and switches |
| Option cards (quiz, lab) | Behave as a radio group: arrow keys move between A, B, C; Enter or Space selects; Back and Next are reachable by Tab |
| Chips | Arrow keys within a group; Space toggles |
| Tabs | Arrow keys switch tabs; Home/End jump |
| Menus and dropdowns | Arrow keys navigate; Enter selects; `Esc` closes and returns focus |
| Modals and drawers | Focus trapped; `Esc` closes; focus returns to trigger |
| Drag-and-drop (A04, A06) | Always provide **Move up / Move down** buttons as an alternative |
| Skip link | "Skip to content" as the first focusable element |

### 12.7 Motion and sensory

- Respect reduced-motion preferences: no slide transitions, route drawing, or confetti; use instant changes.
- Do not rely on sound. Do not flash content.
- Charts always have a text summary (e.g., radar: "Your highest interests: Investigative, Conventional, Realistic").

### 12.8 Arabic RTL layout consistency

- Every component is built with an RTL variant and checked on the 12 key screens (see [Section 13](#13-arabic-rtl-requirements)).
- Alignment, order of columns, icon direction, progress direction, and the primary-action side all mirror together; do not mirror half of a layout.

### 12.9 Interface consistency checklist

- [ ] Same terminology from [2.3](#23-terminology) on every screen
- [ ] One primary button per view
- [ ] Same header pattern on all pages
- [ ] Spacing from the scale only
- [ ] Every interactive element has all required states
- [ ] Every list and table has loading, empty, and error states
- [ ] Every form has validation messages
- [ ] Every icon-only button has an accessible name
- [ ] Contrast checked in both themes
- [ ] RTL variant checked

---

## 13. Arabic RTL Requirements

### 13.1 Rules **[Prototype / Confirmed from original]**

1. **Mirror the layout:** sidebar on the right, text right-aligned, progress bars fill from right to left, the quiz slide transition reverses direction, arrows `→` become `←`.
2. **Do not mirror** logos, the route illustration, charts' data order where meaning would change, media icons, or numbers. Icons that imply direction (arrows, back) do mirror.
3. **Type:** Arabic uses Cairo (headings) and IBM Plex Sans Arabic (body). Increase line-height (about 1.3 on large headings, 1.7 on body). **No letter-spacing and no uppercase styling** on Arabic.
4. **Mixed text:** English technical terms (Wireshark, SQL, Figma) stay Latin inside Arabic sentences. Check punctuation placement at direction changes.
5. **Numbers:** the prototype uses Western digits (0 to 9) in both languages. Keep consistent unless the owner decides otherwise (see [Open Questions](#15-open-questions-and-decisions)).
6. **Terminal/code blocks** stay left-to-right and left-aligned, even in the Arabic UI.
7. **Text expansion:** Arabic strings are often shorter in characters but taller in line height; design buttons and chips to flex, not fix widths.
8. **Forms:** labels on the right, inputs flow right-to-left; email and password fields stay LTR.
9. **Radar chart** axis labels are translated; keep legible at mobile size.
10. Build each component with an **RTL variant** (Figma variables/modes help); verify at least the 12 key screens listed in [1.3](#13-frame-plan).

### 13.2 Mirror or not

| Element | Mirror in RTL? |
|---|---|
| Sidebar, top bar order, bottom bar order | Yes |
| Page header action position | Yes (moves to the left) |
| Primary button in modal footers | Yes (left side) |
| Progress bars, rings fill direction | Bars yes; ring direction clockwise stays (it is a circle) **[Recommended]** |
| Slide transitions | Yes |
| Chevrons, back and next arrows, breadcrumb separators | Yes |
| Checkmarks, search icon, bookmark, clock, external-link icon | No (the external-link icon may mirror to point toward the end side) |
| Logo, route illustration, radar chart geometry | No |
| Numbers, dates, percentages | No; keep Western digits unless decided otherwise |
| Email, password, URL, terminal, code | No; remain LTR and left-aligned within RTL layouts |
| Table columns | Yes (first column on the right) |
| Toast position | Bottom corner on the **end** side (left in RTL) |
| Drawer | Opens from the **end** side (left in RTL) |
| Tabs and steppers | Yes |
| Star rating | Fills from the start (right in RTL) |

### 13.3 Sample Arabic strings **[Sample, needs native-speaker review]**

| English | Arabic |
|---|---|
| Home | الرئيسية |
| Explore | استكشاف |
| Roadmap | خريطة الطريق |
| Opportunities | الفرص |
| Dashboard | لوحة التحكم |
| Log in | تسجيل الدخول |
| Sign up | إنشاء حساب |
| Take the assessment | ابدأ الاختبار |
| View full roadmap | عرض خريطة الطريق كاملة |
| Save my results | احفظ نتائجي |
| Set as my track | اجعله مساري |
| Continue | متابعة |
| Cancel | إلغاء |
| Guidance, not a verdict | إرشاد وليس حكمًا |

Final Arabic terminology for **Taster Labs**, **Assessment**, **Stage**, and **Resources** is **[Open]**.

---

## 14. Completeness Review

### 14.1 Screen coverage

| Group | Expected | Specified in Section 6 | Check |
|---|---|---|---|
| Public (P01–P09) | 9 | 9 | ✅ |
| Onboarding and assessment (O01–O05) | 5 | 5 | ✅ |
| Learning app (L01–L15) | 15 | 15 | ✅ |
| Admin (A01–A11) | 11 | 11 | ✅ |
| System (S01–S02) | 2 | 2 | ✅ |
| **Total** | **42** | **42** | ✅ |

### 14.2 Flow coverage

- [x] F01–F09 (all original flows) documented step by step
- [x] Assessment, track selection, roadmap navigation, learning tasks, labs, saving items, opportunities, profile settings, admin management covered (F01–F15)
- [x] Alternative paths and error states listed for each flow

### 14.3 Design system, responsive, RTL, themes

- [x] Colors in both themes with contrast values
- [x] Typography, spacing, radius, elevation, motion
- [x] Buttons, inputs, cards, navigation, overlays, tables, badges, progress
- [x] Component inventory with variants and states
- [x] Three breakpoints with behavior for desktop, tablet, mobile
- [x] Navigation, modal, drawer, table, and scrolling adaptations
- [x] RTL rules, mirror table, and sample strings
- [x] Accessibility guidance
- [ ] **Not yet possible without owner input:** final track list, assessment content, XP rules, Arabic terminology, team content (see [Section 15](#15-open-questions-and-decisions))

### 14.4 Corrected or clarified in this version

| Item | Before | Now |
|---|---|---|
| Nav label for Opportunities | "Radar" in sidebar, "Opportunities" elsewhere | One label: **Opportunities** (subtitle "Opportunity Radar" optional) |
| Tablet grid behavior | "Two-column grids from 760" inside a 700–899 tablet range | Clarified in [10.1](#101-breakpoints-confirmed) |
| Admin "Roadmaps" menu vs Roadmap Editor | Both listed without a link | "Roadmaps" lists tracks and opens the Roadmap Editor (A04) for the chosen track |
| Recommendations voice | "my suggestion" | Neutral **[Recommended]** label |
| Light-theme use of accent colors | Only lime on light was noted | Full contrast rule for coral, success, error, warning |

---

## 15. Open Questions and Decisions

The items below are **not confirmed** and should be decided by the project owner. Until then, sample content and recommendations stay labeled as such.

| # | Topic | Question | Affects |
|---|---|---|---|
| 1 | Track list | What are the final names, categories, coding levels, and difficulty of the 19 tracks? (7.1 is a sample) | P03, P04, A02, all sample content |
| 2 | Product name | Which name is displayed in the UI (MASAR in English, مسار in Arabic)? Is a logo/wordmark file available? | Top bar, Landing, About |
| 3 | Palette scope | Is the approved dark-teal and lime palette the single final palette for **all** screens, including Landing? | All |
| 4 | Default theme | Default dark, default light, or follow the device? Does Settings include "System"? | L15, all |
| 5 | Warning color | Is `#F5B74A` dark / `#B7791F` light approved? | Alerts, badges |
| 6 | Navigation labels | Confirm **Opportunities** (not "Radar"), and **Resources** in the sidebar | Navigation |
| 7 | Assessment | Number of questions, wording, scoring method, and privacy text? | O03, O04, A06 |
| 8 | Starting points | Are the three choices and their effect on the roadmap correct? | L02, M04 |
| 9 | XP and badges | XP values, the 12 badges, and the names of the 3 badges in the prototype Dashboard? | L01, L09, L10 |
| 10 | Resources and providers | Which resources and providers are real? Who verifies them and how often? | L03, L04, A05 |
| 11 | Arabic numerals | Western digits or Arabic-Indic digits in the Arabic UI? | RTL |
| 12 | Arabic terminology | Official Arabic names for Taster Labs, Assessment, Stage, Resources | RTL, all copy |
| 13 | Account rules | Password rules, whether terms and privacy pages are designed, and how email changes | P06, L14, L15 |
| 14 | Guest access | Exactly what can a guest do (read-only roadmap, results held for the session)? | Flows F01–F03 |
| 15 | Admin roles | Do Editors exist? What can Editors do compared with Admins? | A10 |
| 16 | Labs | Is "Notify me" for coming-soon labs in scope? Final lab list? | L05 |
| 17 | Opportunities scope | Is the audience limited to one country (governorate filter)? Final governorate list and filters? | L11, L14 |
| 18 | About page | Real team names, roles, and contact method | P02 |
| 19 | Icons and illustration | Approved icon set and illustration style | All |
| 20 | Sign-out confirmation | Is M12 wanted at all? | Account menu |
| 21 | Delete confirmation word | Type "DELETE" in both languages, or a localized word in Arabic? | M11 |
| 22 | Frame coverage | Recommended 84 + key tablet and RTL frames, or the full 252? | Deliverables |

---

## 16. Designer Deliverables Checklist

**[Recommended]** — a suggested set of deliverables for the designer to accept or change.

- [ ] **Styles and variables:** colors (dark + light), typography, spacing, radius, effects, motion notes
- [ ] **Component library** with all states (see [11.11](#1111-component-inventory-and-variants)), LTR and RTL
- [ ] **42 screens** at desktop and mobile (English)
- [ ] **Tablet** for the 12 key screens
- [ ] **Arabic RTL** for the 12 key screens
- [ ] **16 modals**, toasts, tooltips
- [ ] **Empty, loading, and error states** for every list, table, and form
- [ ] **Clickable prototype** for flows F01 to F04 at minimum (F05–F09 recommended)
- [ ] **Accessibility pass:** contrast in both themes, focus states, touch targets
- [ ] **"Design decisions" page** for the course submission
- [ ] **Open questions** from Section 15 reviewed with the owner

---

## 17. Appendix: Revision Notes

**Preserved from the original document (unchanged):** the 42-screen inventory and IDs, the 16 modal list, the navigation model, the site map, the color palette (both themes), typography, radius, elevation, motion values, breakpoints and container widths, component list, interactive states, RTL requirements, and the frame planning numbers.

**Expanded:** full specifications for all 42 screens; sample content library; 15 user flows (9 original plus 6); modal catalog; responsive specifications; complete design system; accessibility guidance; completeness review; open questions.

**Removed:** statements about the software implementation roadmap and development timing. They are outside the scope of this UI/UX document.

**Added as Recommended (not approved):** the warning color (already proposed in the original), focus ring, control sizes, bottom bar height, toast behavior, empty-state copy, sample Arabic strings, and all **[Sample]** content.
