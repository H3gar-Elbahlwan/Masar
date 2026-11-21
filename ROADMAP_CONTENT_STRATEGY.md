# MASAR — Roadmap & Learning-Resource Content Strategy (Revision 2)

**Legend:** **[Confirmed]** from the owner's brief · **[Recommended]** my proposal · **[Verified fact]** something I actually checked on the date shown.

**Core rules [Confirmed]**
1. Do not fabricate links.
2. Do not claim a resource is verified unless a person checked it.
3. Roadmaps and resources are **data**, editable without changing frontend code.
4. Do not assume anything about external sources beyond what has been provided and checked.

---

## 1. The external reference: roadmap.sh

You named **roadmap.sh** ("Developer Roadmaps") as the external roadmap reference. On **21 Nov 2026** I read its homepage and its Terms of Use. This section records only what I actually saw.

### 1.1 What it covers **[Verified fact]**
The homepage lists community-created roadmaps in three groups: **role-based** (31), **skill-based** (62), and **best practices** (5), plus lesson packs, videos, guides and newsletters. Role-based entries relevant to MASAR include: Backend, Frontend, Full Stack, Cyber Security, DevOps, Data Analyst, AI and Data Scientist, Machine Learning, AI Engineer, Network Engineer, QA, Game Developer, Android, iOS, UX Design, Product Design, SEO. Skill-based entries relevant to MASAR include: Cloud Computing, AWS, Linux, Python, SQL, Computer Science, Power BI, Flutter, React Native, and others.

It is **developer-focused**. The homepage listing I reviewed did **not** show dedicated roadmaps for graphic design, motion graphics, video editing, content creation, or a general digital-marketing track (only SEO). The full `/roadmaps` page may list more; I did not review it.

### 1.2 Its Terms of Use **[Verified fact, not legal advice]**
The Terms (last updated 27 March 2025) say the site is for **personal, non-commercial use only**, and that you must not **reproduce, distribute, modify, create derivative works of, republish, download, or store** material from it. They also prohibit using robots or automated processes to access or copy the site, **including scraping to train AI**, and they restrict linking to the homepage only.

I could not open the project's GitHub repository, so **I did not check whether the underlying roadmap source files carry a different license.** Do not assume they are free to reuse.

### 1.3 What this means for MASAR **[Recommended]**
| Do | Don't |
|---|---|
| Read it as a human, to understand which topics practitioners consider important | Scrape, download, import, or mirror its roadmaps, topic trees, or text |
| Write MASAR's stages and tasks **in your own structure and words**, grounded in primary sources | Copy its structure node-for-node or paste its descriptions |
| Cite it in your project report as an inspiration/reference | Deep-link to its inner pages or embed them without permission |
| If you want to link or reuse anything, ask its operators in writing first and keep the reply | Assume a GitHub license applies to the website content |

Also: because MASAR is a graduation project, "non-commercial" may fit, but **copying/derivatives are still not permitted** under the stated terms, so the safe path is independent authoring.

### 1.4 Coverage map: where roadmap.sh helps as a topic reference **[Verified fact for the listing; mapping is mine]**
| MASAR track | Related entry on the homepage listing |
|---|---|
| Software Development | Partial: Computer Science, Python, Data Structures & Algorithms, Software Architect |
| Web Development | Frontend, Backend, Full Stack, HTML, CSS, JavaScript |
| Mobile Development | Android, iOS, Flutter, React Native |
| Computer Networking | Network Engineer |
| Cloud Computing | Cloud Computing, AWS |
| DevOps | DevOps |
| Network Security | Partial: Cyber Security |
| SOC Analysis | None dedicated (Cyber Security is general) |
| Penetration Testing | None dedicated |
| Data Analysis | Data Analyst, SQL, Power BI |
| Data Science | AI and Data Scientist |
| Artificial Intelligence | AI Engineer |
| Machine Learning | Machine Learning |
| UI/UX Design | UX Design, Product Design |
| Graphic Design | None |
| Motion Graphics | None |
| Video Editing | None |
| Content Creation | None |
| Digital Marketing | Partial: SEO |

**Consequence:** for **at least 7 of the 19 tracks** (SOC, Penetration Testing, Graphic Design, Motion Graphics, Video Editing, Content Creation, and most of Digital Marketing) another credible research base is needed. Ask your supervisor and instructors where they would look.

---

## 2. Source policy **[Recommended]**

### 2.1 Source tiers
| Tier | Examples of *types* (no specific sources are endorsed here) |
|---|---|
| 1 | Official documentation and standards; vendor/product documentation |
| 2 | University courses, established learning platforms, recognized certification bodies |
| 3 | Reputable community material (maintained guides, well-known educators) |

### 2.2 Selection rubric (score each candidate 1 to 5, record the scores)
Credibility · Beginner fit · Clarity · Recency (is it still accurate?) · Accessibility (free? needs account? works in Egypt?) · Language (Arabic availability) · Practical value · License/terms for linking. A candidate enters the catalog only if it passes your threshold (suggested: no score below 3, credibility ≥ 4).

### 2.3 Language plan
Arabic resources matter for your audience. Flag each resource's language, and where no good Arabic resource exists say so rather than padding the list. Searching for Arabic resources is a **team task**; I will not invent any.

### 2.4 Candidate lists
The team collects candidate URLs. Paste them to me and I can help score them against the rubric, group them into stages, and draft descriptions. **I will not supply URLs from memory**, because I cannot verify they still exist.

---

## 3. Data model summary **[Confirmed fields, Recommended structure]**

Full definitions are in `DATABASE_SCHEMA.md`. In short:

```
career_tracks ─┬─ roadmaps (several per track: variant, version, status)
               │      └─ roadmap_stages ─┬─ roadmap_tasks
               │                          └─ stage_resources ── learning_resources ── resource_skills ── skills
               ├─ track_projects          (authored practical projects)
               ├─ track_responsibilities, track_roles, track_prerequisites
               └─ lab_tracks ── labs
```

### 3.1 Resource fields **[Confirmed]** → columns
| Required field | Column / table |
|---|---|
| Title | `title_en`, `title_ar` (at least one required) |
| Description | `description_en`, `description_ar` |
| Source URL | `url` (https only) |
| Provider | `provider` |
| Resource type | `resource_type`: `official_docs`, `video_course`, `article`, `interactive_platform`, `practical_project`, `certification` |
| Language | `language`: `en`, `ar`, `other` |
| Difficulty level | `difficulty` 1 to 3 |
| Estimated duration | `est_minutes` |
| Related skills | `resource_skills` (many-to-many) |
| Related roadmap stage | `stage_resources` (many-to-many; a resource can serve several stages) |

Added by me **[Recommended]**: `verification_status`, `verified_at`, `verified_by`, `last_reviewed`, `is_free`, `requires_account`, `notes`.

### 3.2 Roadmap structure
- A track can have **several roadmaps** (variants such as "core", "fast track", "Arabic-first"), each with a version number.
- Stage types: `concept`, `hands_on`, `project`, `checkpoint`.
- Each stage: goal, outcomes ("after this stage you can…"), recommended prerequisites (never a hard lock), estimated hours, tasks, resources.
- Task types: read, video, exercise, practice, project, review (as in the prototype).

---

## 4. Verification workflow **[Recommended]**

```
candidate → in_review → verified → published
                 │          └→ stale (re-check due) → verified | broken | retired
                 └→ rejected
```

| Status | Meaning | Visible to users? |
|---|---|---|
| `candidate` | Collected, not yet reviewed | No |
| `in_review` | Someone is checking it | No |
| `verified` | A named person opened it, confirmed it matches the description, level, and language, and recorded the date | Yes, once published |
| `stale` | Re-check date passed | Yes, with no "verified" badge until re-checked |
| `broken` / `retired` | Link dead or content unsuitable | No |

**Rules**
- The words "verified" and a verification date appear in the UI **only** when a person has actually done the check and the record shows who and when.
- Every check is logged (`resource_checks`: who, when, result, notes).
- An automated link checker may flag broken links (HTTP status), but **automation never sets `verified`**.
- Suggested re-check interval: every 90 days (adjust to your capacity).
- Users can report a broken or outdated resource; reports enter the review queue.

---

## 5. Authoring pipeline: update content without touching code **[Recommended]**

1. **Collect** candidates in the team's shared spreadsheet using the template below.
2. **Score** each against the rubric (§2.2).
3. **Import** through the admin Bulk Import screen (CSV/JSON). The importer **validates before saving**: required fields present, https URLs, allowed enum values, known skill and stage references, no duplicate URLs, both languages present where required.
4. **Review** in the admin Resource Manager: a second person verifies and sets `verified`.
5. **Attach** resources to stages and tasks in the Roadmap Editor (drag to reorder, mark "core" vs "optional").
6. **Publish** a roadmap version. Previous versions stay in history; users' progress is kept because progress points at tasks, and tasks keep stable ids across versions where possible.
7. **Changelog:** every change is written to an audit log (who, what, when).

### 5.1 Import template (illustrative; values are placeholders, **not real sources**)
```json
{
  "resource": {
    "title_en": "TO_BE_PROVIDED",
    "title_ar": "TO_BE_PROVIDED",
    "description_en": "TO_BE_PROVIDED",
    "url": "https://TO_BE_PROVIDED",
    "provider": "TO_BE_PROVIDED",
    "resource_type": "official_docs | video_course | article | interactive_platform | practical_project | certification",
    "language": "en | ar | other",
    "difficulty": 1,
    "est_minutes": 60,
    "skills": ["skill-slug"],
    "stages": [{"track": "computer-networking", "roadmap": "core", "stage": 1, "is_core": true}]
  }
}
```

---

## 6. Roadmap design template (per track) **[Recommended]**

A track roadmap should answer, for a complete beginner: *what do I learn, in what order, how do I know I can move on, and what do I build?*

| Stage | Purpose | Typical content |
|---|---|---|
| 1. Orientation | Understand the field and vocabulary | Intro reading/video, glossary, a short Taster Lab |
| 2. Foundations | Core concepts | Core resources, small exercises |
| 3. Core skills | Daily-work skills | Hands-on practice with the common tools |
| 4. Applied practice | Solve realistic problems | Guided exercises, a checkpoint |
| 5. Portfolio project | Show the skills | One practical project with a rubric |
| 6. Next steps | Specialize and apply | Related tracks, certifications to consider, local opportunities |

Not every track needs exactly 6 stages; keep **4 to 6**. Each stage lists outcomes, estimated hours, tasks, and resources with core/optional marking. Avoid vague advice such as "practice a lot": every task says what to do and how to know it is done.

---

## 7. Practical projects and Taster Labs **[Recommended]**
- **Projects** (`track_projects`) are authored by the team: brief, deliverable, acceptance criteria, difficulty, estimated hours, skills practiced. External project platforms are separate resources of type `practical_project`.
- **Labs:** one lab per track as the target; scenarios are authored in the admin Lab Editor with answer keys kept private (see schema). Labs are learning feedback, not ability tests.

---

## 8. Effort model (read this before committing to scope) **[Recommended]**

Content is the largest workload in the project, not the code. A rough model for **depth per track**:

| Depth target | Stages | Tasks | Resources | Total resources, 19 tracks |
|---|---|---|---|---|
| Lean | 4 | ~12 | ~18 | ~340 |
| Standard (suggested) | 5 | ~20 | ~30 | ~570 |
| Deep | 6 | ~30 | ~50 | ~950 |

Every resource must be found, scored, opened, and verified by a person; every stage, project, and lab must be written and reviewed in two languages. For three students this is substantial. Options: a **lean** depth for all 19 tracks first, then deepen priority tracks; or fewer tracks at standard depth. Because you asked for all tracks to be meaningful, I recommend **lean-to-standard depth for all 19**, built in batches, with the publish gate (`TRACK_CATALOG.md` §8) deciding what is visible at the demo.

**Suggested production order (batches):**
1. Tracks that already have prototype content: Networking, Data Analysis, UI/UX, Web, Digital Marketing.
2. Cybersecurity category (3), reusing the phishing-triage lab idea.
3. Programming: Software Development, Mobile.
4. Data & AI: Data Science, AI, Machine Learning.
5. Network & Infrastructure remaining: Cloud, DevOps.
6. Design and Digital Media remaining: Graphic, Motion, Video, Content.

---

## 9. Who does what
| Team (people) | Claude (assistant) |
|---|---|
| Finds candidate sources, opens and verifies every link, decides what is credible, searches for Arabic resources, reviews all content | Drafts descriptions, outcomes, stage structures, project briefs, lab scenarios; scores candidates you paste; writes validators/importers; reviews consistency between EN and AR text |

## 10. Open decisions
1. Depth target (lean / standard / deep) and how many batches before the demo.
2. Re-check interval for resources.
3. Whether to contact roadmap.sh's operators about linking, or treat it purely as private research.
4. Who is the second reviewer for each batch.
5. Other research references (supervisor, instructors, course syllabi) to cover the 7 tracks without a dedicated external roadmap.
