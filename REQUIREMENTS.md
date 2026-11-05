# NaviTech (مسار) — Software Requirements Specification (SRS)

| الحقل | القيمة |
|---|---|
| **Project** | NaviTech (مسار) |
| **Document** | Requirements Specification |
| **Standard** | مبني على هيكل IEEE 830 / ISO/IEC/IEEE 29148 (مبسّط للمشروع الأكاديمي) |
| **Version** | 1.0 |
| **Status** | Draft |
| **Scope** | Phase 1 (MVP) + اعتبارات Phase 2 |

---

## 1. Introduction

### 1.1 Purpose
يحدد هذا المستند المتطلبات الوظيفية وغير الوظيفية لمنصة **NaviTech**، وهي منصة ويب لتوجيه طلبة الحاسبات وتكنولوجيا المعلومات والمبتدئين لاختيار مسارهم التقني. المستند هو المرجع الأساسي للتصميم والتطوير والاختبار.

### 1.2 Scope
تقدم المنصة: اختبار ميول **RIASEC**، وترشيح التراكات، و**Taster Labs**، و**Roadmaps**، و**Opportunity Radar**، ولوحة تحكم للأدمن.

### 1.3 Definitions & Abbreviations

| المصطلح | التعريف |
|---|---|
| **Track** | مسار تقني (مثل: Web Development, Data Science, Cybersecurity) |
| **RIASEC** | نموذج Holland للميول المهنية: Realistic, Investigative, Artistic, Social, Enterprising, Conventional |
| **Taster Lab** | تجربة سيناريو عملي مبسّط تحاكي مهمة من تراك معين |
| **Roadmap** | خريطة تعلم مرتبة لتراك معين تتضمن مراحل ومصادر |
| **Opportunity** | منحة أو تدريب أو مسابقة أو فرصة تعلم |
| **Admin** | مستخدم بصلاحيات إدارة المحتوى |
| **MVP** | النسخة الأولى القابلة للاستخدام |

### 1.4 Priority Levels
- **High (H):** ضروري للـ MVP.
- **Medium (M):** مهم ويُنفَّذ إن سمح الوقت.
- **Low (L):** تحسين مستقبلي.

### 1.5 User Classes

| الفئة | الوصف |
|---|---|
| **Visitor** | زائر غير مسجل (يستعرض المحتوى العام) |
| **Student** | مستخدم مسجل (طالب/مبتدئ) |
| **Admin** | مدير المحتوى والفرص |

---

## 2. Functional Requirements (FR)

### 2.1 User Registration & Authentication

| ID | Requirement | Priority |
|---|---|---|
| FR-1.1 | The system **shall** allow a visitor to register using email and password. | H |
| FR-1.2 | The system **shall** validate email format and enforce a minimum password strength policy. | H |
| FR-1.3 | The system **shall** allow registered users to log in and log out securely. | H |
| FR-1.4 | The system **shall** provide a password reset mechanism via email. | M |
| FR-1.5 | The system **shall** collect basic profile data (name, governorate, education level, year of study). | H |
| FR-1.6 | The system **shall** allow users to view and edit their profile information. | M |
| FR-1.7 | The system **should** support social login (e.g., Google). | L |
| FR-1.8 | The system **shall** enforce role-based access control (Student / Admin). | H |

### 2.2 RIASEC Interest Quiz

| ID | Requirement | Priority |
|---|---|---|
| FR-2.1 | The system **shall** provide an interest quiz based on the RIASEC model. | H |
| FR-2.2 | The system **shall** present questions in a paginated or step-by-step flow with a visible progress indicator. | H |
| FR-2.3 | The system **shall** record each user's answers and calculate a score for each of the six RIASEC dimensions. | H |
| FR-2.4 | The system **shall** prevent submission of incomplete quizzes, or clearly warn the user about unanswered questions. | M |
| FR-2.5 | The system **shall** allow users to save progress and resume an unfinished quiz. | M |
| FR-2.6 | The system **shall** allow users to retake the quiz and keep a history of previous attempts. | M |
| FR-2.7 | The quiz questions and scoring weights **shall** be stored in the database, not hard-coded. | H |

### 2.3 Results & Track Recommendation

| ID | Requirement | Priority |
|---|---|---|
| FR-3.1 | The system **shall** display the user's RIASEC profile (top dimensions) after quiz completion. | H |
| FR-3.2 | The system **shall** map the RIASEC profile to a ranked list of recommended tracks using a predefined mapping matrix. | H |
| FR-3.3 | The system **shall** show, for each recommended track, a match percentage and a short explanation of the match. | H |
| FR-3.4 | The system **shall** provide a track details page (description, required skills, career outcomes). | H |
| FR-3.5 | The system **shall** let the user save a selected track as their "Chosen Track." | M |
| FR-3.6 | The system **should** allow results to be exported or shared (PDF or link). | L |

### 2.4 Taster Labs

| ID | Requirement | Priority |
|---|---|---|
| FR-4.1 | The system **shall** provide a catalog of Taster Labs organized by track. | H |
| FR-4.2 | Each Taster Lab **shall** present a simplified real-world scenario with clear objectives and step-by-step tasks. | H |
| FR-4.3 | Each Taster Lab **shall** have an estimated duration and a difficulty level (Beginner only in Phase 1). | M |
| FR-4.4 | The system **shall** record the user's completion status for each Taster Lab. | H |
| FR-4.5 | The system **shall** collect brief post-lab feedback (e.g., enjoyment and interest rating). | M |
| FR-4.6 | The system **shall** use lab completion and feedback to refine track suggestions shown to the user. | L |
| FR-4.7 | Taster Labs **shall** run in the browser without requiring local installation of tools. | H |

### 2.5 Roadmaps

| ID | Requirement | Priority |
|---|---|---|
| FR-5.1 | The system **shall** provide a Roadmap for each supported track, composed of ordered stages. | H |
| FR-5.2 | Each stage **shall** list topics/skills and curated learning resources (title, type, language, link, cost: free/paid). | H |
| FR-5.3 | The system **shall** allow users to mark stages or topics as completed and display overall progress. | H |
| FR-5.4 | The system **shall** allow filtering resources by language (Arabic/English) and cost. | M |
| FR-5.5 | The system **shall** display estimated time per stage. | M |
| FR-5.6 | The Roadmap content **shall** be manageable by Admin without code changes. | H |
| FR-5.7 | The system **should** display a visual (graph or timeline) representation of the Roadmap. | M |

### 2.6 Opportunity Radar

| ID | Requirement | Priority |
|---|---|---|
| FR-6.1 | The system **shall** display a list of opportunities (scholarships, internships, competitions, programs). | H |
| FR-6.2 | Each opportunity **shall** include: title, provider, description, related track(s), governorate/location, deadline, eligibility, and application link. | H |
| FR-6.3 | The system **shall** allow filtering opportunities by **governorate**. | H |
| FR-6.4 | The system **shall** allow filtering opportunities by **track**. | H |
| FR-6.5 | The system **shall** support combining filters (governorate + track + type) and keyword search. | M |
| FR-6.6 | The system **shall** sort opportunities by deadline and automatically hide or flag expired ones. | H |
| FR-6.7 | The system **shall** allow users to bookmark opportunities for later. | M |
| FR-6.8 | The system **should** highlight opportunities that match the user's governorate and chosen track. | M |
| FR-6.9 | The system **should** notify users of upcoming deadlines for bookmarked opportunities. | L |

### 2.7 Admin Panel

| ID | Requirement | Priority |
|---|---|---|
| FR-7.1 | The system **shall** provide a protected Admin Panel accessible only to users with the Admin role. | H |
| FR-7.2 | The Admin **shall** be able to create, read, update, and delete (CRUD) opportunities manually. | H |
| FR-7.3 | The Admin **shall** be able to manage tracks, Roadmaps (stages and resources), and Taster Lab content. | H |
| FR-7.4 | The Admin **shall** be able to manage quiz questions and RIASEC-to-track mapping weights. | M |
| FR-7.5 | The Admin Panel **shall** validate all inputs (required fields, valid dates, valid URLs). | H |
| FR-7.6 | The Admin **shall** be able to archive or deactivate content instead of permanently deleting it. | M |
| FR-7.7 | The Admin Panel **shall** display basic statistics (number of users, quiz completions, most recommended tracks). | L |
| FR-7.8 | The system **should** log Admin actions (audit log). | M |

---

## 3. Non-Functional Requirements (NFR)

### 3.1 Performance & Fast Loading

| ID | Requirement | Priority |
|---|---|---|
| NFR-1.1 | Initial page load (Largest Contentful Paint) **shall** be ≤ 2.5 seconds on a typical 4G connection. | H |
| NFR-1.2 | Standard API responses **shall** return within 500 ms under normal load (95th percentile). | H |
| NFR-1.3 | The system **shall** use server-side rendering or static generation where applicable (Next.js) to improve first load and SEO. | M |
| NFR-1.4 | The system **shall** apply code splitting, lazy loading, and image optimization. | H |
| NFR-1.5 | Listing endpoints (e.g., opportunities) **shall** support pagination and database indexing on filter fields (governorate, track, deadline). | H |
| NFR-1.6 | The system **should** cache static and infrequently changing content (tracks, roadmaps). | M |
| NFR-1.7 | The system **shall** support at least 500 concurrent users without significant degradation (MVP target). | M |

### 3.2 Usability & Responsive UI/UX

| ID | Requirement | Priority |
|---|---|---|
| NFR-2.1 | The interface **shall** be fully responsive across mobile, tablet, and desktop (minimum width 320 px). | H |
| NFR-2.2 | The system **shall** support Arabic with RTL layout, and English as a secondary language where applicable. | H |
| NFR-2.3 | A new user **shall** be able to complete registration and start the quiz in under 3 minutes without external help. | M |
| NFR-2.4 | The UI **shall** follow a consistent design system (colors, typography, components) defined in Figma. | H |
| NFR-2.5 | The system **shall** meet WCAG 2.1 Level AA basics (color contrast, keyboard navigation, alt text, labels). | M |
| NFR-2.6 | The system **shall** provide clear error messages, loading states, and empty states. | H |
| NFR-2.7 | The system **shall** work on the latest two versions of Chrome, Edge, Firefox, and Safari, and on mobile browsers. | H |

### 3.3 Security & Data Protection

| ID | Requirement | Priority |
|---|---|---|
| NFR-3.1 | All communication **shall** use HTTPS/TLS. | H |
| NFR-3.2 | Passwords **shall** never be stored in plain text; they **shall** be hashed using a strong algorithm (e.g., bcrypt/argon2 or via Supabase Auth). | H |
| NFR-3.3 | The system **shall** use secure session/token management (e.g., JWT with expiry, HttpOnly cookies). | H |
| NFR-3.4 | The system **shall** enforce role-based authorization on every Admin endpoint, server-side. | H |
| NFR-3.5 | The system **shall** validate and sanitize all inputs to prevent SQL Injection, XSS, and CSRF. | H |
| NFR-3.6 | The system **shall** use Row Level Security (RLS) so users can access only their own data. | H |
| NFR-3.7 | The system **shall** collect only the minimum personal data necessary and provide a Privacy Policy. | M |
| NFR-3.8 | The system **shall** allow users to request deletion of their account and associated data. | M |
| NFR-3.9 | Secrets and API keys **shall** be stored in environment variables and never committed to the repository. | H |
| NFR-3.10 | The system **should** apply rate limiting on authentication and public API endpoints. | M |
| NFR-3.11 | The system **shall** perform regular automated database backups. | M |

### 3.4 Scalability & Extensibility (Phase 2 AI Integration)

| ID | Requirement | Priority |
|---|---|---|
| NFR-4.1 | The system **shall** follow a modular, layered architecture (Presentation / API / Service / Data) with clear separation of concerns. | H |
| NFR-4.2 | The backend **shall** expose a versioned REST API (e.g., `/api/v1/...`) to allow future clients and services. | H |
| NFR-4.3 | The database schema **shall** be normalized and managed through migrations to support evolution. | H |
| NFR-4.4 | The system **shall** store user interaction data (quiz answers, lab results, roadmap progress) in a structured form suitable for future analytics and ML use. | M |
| NFR-4.5 | The recommendation logic **shall** be isolated in a dedicated service/module so the rule-based engine can be replaced or complemented by an AI/ML model in Phase 2. | H |
| NFR-4.6 | The architecture **should** allow integrating AI features (e.g., an AI career assistant, personalized roadmaps, opportunity matching) without major refactoring. | M |
| NFR-4.7 | The application **shall** be stateless at the API layer to enable horizontal scaling. | M |
| NFR-4.8 | The system **should** be deployable through a CI/CD pipeline (GitHub Actions). | M |

### 3.5 Maintainability & Reliability

| ID | Requirement | Priority |
|---|---|---|
| NFR-5.1 | The codebase **shall** follow a consistent style enforced by linting and formatting tools (ESLint, Prettier). | M |
| NFR-5.2 | The project **shall** follow a Git branching strategy with Pull Request reviews. | H |
| NFR-5.3 | Core business logic (scoring, recommendation) **shall** be covered by automated unit tests. | M |
| NFR-5.4 | The system **shall** target an availability of at least 99% during the demonstration/evaluation period. | L |
| NFR-5.5 | The system **shall** log errors and exceptions in a centralized manner. | M |

---

## 4. Constraints & Assumptions

### 4.1 Constraints
- المشروع أكاديمي، والموارد (الوقت والميزانية) محدودة، لذلك يُعتمد على خدمات ذات طبقات مجانية (Free Tiers) قدر الإمكان.
- إدخال الفرص في Phase 1 يتم **يدويًا** عبر لوحة الأدمن (بدون جمع آلي).
- الاعتماد على الـ Tech Stack المحدد: Next.js, Tailwind CSS, Node.js/Express, PostgreSQL/Supabase.

### 4.2 Assumptions
- المستخدمون لديهم اتصال إنترنت ومتصفح حديث.
- محتوى الـ Roadmaps والـ Taster Labs سيتم إعداده ومراجعته من فريق المشروع.
- نموذج RIASEC ومصفوفة الربط مع التراكات سيتم ضبطهما كقواعد (Rule-Based) في المرحلة الأولى.

---

## 5. Out of Scope (Phase 1)

- التوصيات المبنية على الذكاء الاصطناعي / Machine Learning (مؤجلة إلى Phase 2).
- الجمع الآلي للفرص (Scraping / Aggregation).
- تطبيقات الموبايل Native.
- نظام الشهادات أو الدفع.
- المجتمع والمحادثات بين المستخدمين.

---

## 6. Requirements Traceability (Summary)

| الميزة | Functional | Related NFR |
|---|---|---|
| Authentication | FR-1.x | NFR-3.x |
| RIASEC Quiz | FR-2.x | NFR-2.x, NFR-4.4 |
| Results & Recommendation | FR-3.x | NFR-4.5, NFR-4.6 |
| Taster Labs | FR-4.x | NFR-1.x, NFR-2.x |
| Roadmaps | FR-5.x | NFR-1.6, NFR-2.x |
| Opportunity Radar | FR-6.x | NFR-1.5, NFR-2.x |
| Admin Panel | FR-7.x | NFR-3.4, NFR-3.6 |

---

## 7. Revision History

| Version | Date | Description | Author |
|---|---|---|---|
| 1.0 | — | Initial draft | NaviTech Team |
