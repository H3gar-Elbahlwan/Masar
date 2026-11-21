# MASAR — Feature Scope & Implementation Plan

**Document status:** Project planning document  
**Revision:** 2 (reframed from the proposed technical audit)  
**Purpose:** Record the confirmed scope of MASAR, describe the planned feature set, and separate confirmed requirements from recommendations that still need approval.

> **Important status note:** MASAR's coded prototype and full application implementation have not yet been created. This document therefore describes the intended project scope and implementation targets. It does not claim that pages, features, tests, or technical architecture have already been implemented or audited.

---

## 1. Project status and scope

MASAR is planned as a bilingual career-exploration and learning platform. The complete project scope includes career-track exploration, assessment and recommendations, learning roadmaps and resources, practical labs, progress tracking, opportunities, user accounts, and administration tools.

The project is intended to be delivered as a **complete project**, not as an MVP limited to a small subset of features.

The work is expected to move through distinct stages:

1. **Planning and requirements:** define the complete feature scope, content model, and project documentation.
2. **UI/UX design:** design the required screens, components, states, and responsive layouts; document the intended user flows.
3. **Interactive prototype:** connect the designed screens and interactions so the user experience can be tested.
4. **Software implementation:** build the application and implement its data, authentication, persistence, and business logic.
5. **Testing and refinement:** verify functionality, responsiveness, accessibility, bilingual behavior, and data integrity.

The existence of a requirement in this document does not mean that the feature has already been designed, prototyped, or implemented.

---

## 2. Technical direction and implementation considerations

The final technical architecture is to be established during the software implementation stage. The following are planning considerations, not findings from an audit of an existing codebase:

- The implementation should use a maintainable project structure rather than placing the entire application in a single source file.
- Reusable UI components and a consistent styling system should be used.
- Navigation should support direct routes and appropriate browser history behavior.
- Application state that must survive refreshes or sessions should be persisted.
- Content should be data-driven and manageable through the administration experience.
- English and Arabic content should be supported, including correct RTL behavior for Arabic.
- Authentication, authorization, and protected administrative actions should be implemented securely.
- Automated tests should cover important business logic and user journeys.

### 2.1 Architecture decisions still to be finalized

The following are recommendations and should not be treated as approved decisions unless the project owner confirms them:

- Using Vite with a React and TypeScript single-page application.
- Using Supabase for authentication, database services, and server-side operations.
- Implementing recommendation scoring through a server-side function.
- Providing a guest mode.
- Introducing a content publishing gate and a content-verification workflow.

The implementation team should select and document the final stack before development begins.

---

## 3. Complete feature scope

The table below describes the intended state of the complete project. These are **planned features**, not claims about an existing implementation.

| Feature | Planned scope |
|---|---|
| Landing Page | Introduce MASAR and guide visitors toward exploring career tracks or starting the assessment. |
| Career Track Exploration | Browse and filter 19 career tracks organized across 6 categories. |
| Track Details | Present the complete information defined by the approved 17-item track content template. |
| RIASEC Career Assessment | Provide an assessment that helps identify the user's interests and career preferences. |
| Career Recommendations | Recommend suitable tracks and explain the reasons behind the recommendations. |
| Taster Labs | Provide practical introductory activities across career tracks, with a target of approximately one lab per track. |
| Interactive Scenarios | Let users make decisions in practical scenarios and receive feedback. |
| Learning Roadmaps | Provide meaningful, track-specific roadmaps; multiple roadmaps may be appropriate for a track. |
| Learning Resources | Provide a searchable resource library with the approved metadata fields and resource types. |
| Progress Tracking | Track learning progress and completion persistently. |
| Achievements | Award achievements and badges based on defined, consistent rules. |
| Local Opportunities | Display relevant opportunities using real, appropriately verified information. |
| User Profiles | Allow users to view and manage their profile and settings. |
| Authentication | Support account registration, login, and password recovery. |
| Admin Dashboard | Allow authorized administrators to manage tracks, roadmaps, resources, assessments, labs, opportunities, users, and content imports. |
| Arabic and English | Support both languages across the interface and project content, including Arabic RTL layout. |
| Responsive Layouts | Support mobile, tablet, and desktop screen sizes. |

---

## 4. Content model and data requirements

### 4.1 Career tracks

- The complete starting catalog contains **19 tracks across 6 categories**.
- The approved starting list and category mapping should be maintained in `TRACK_CATALOG.md`.
- The Cybersecurity area is intended to be represented by three separate tracks, as specified in the catalog.
- Each track should follow the approved **17-item content template**.
- Track content should be stored in a structured, data-driven format so it can be updated without rewriting page layouts.

The track content should be reviewed for accuracy and consistency before publication. Do not invent facts, prerequisites, career responsibilities, salary claims, or external links.

### 4.2 Learning resources

The resource library should support the **ten approved metadata fields** and **six approved resource types** defined in the project requirements.

Resource records should be searchable and filterable using the approved metadata. Resource links must not be fabricated. A resource must not be described as verified unless it has actually passed the project's verification process.

### 4.3 Roadmaps

- Roadmaps should be specific to the relevant track and learner stage.
- Each roadmap should contain meaningful stages, tasks, and learning resources.
- Multiple roadmaps may be created for a track when different learning goals or starting levels require them.
- `roadmap.sh` is an external reference for roadmap research; MASAR roadmaps should be authored independently and should not be copied from an external site.

### 4.4 Assessment and recommendations

- The assessment should be based on the approved RIASEC approach.
- The current scope calls for a question bank capable of distinguishing between the 19 tracks.
- Approximately 15–20 questions is a recommendation, not a confirmed fixed requirement unless approved.
- Recommendation results should be explainable to users.
- The scoring approach and final recommendation logic must be documented and tested before release.

### 4.5 Opportunities

- Opportunities should be managed through the admin experience.
- Records should include accurate information and valid destination links.
- Verification status should reflect an actual review process.
- Search, filters, and sorting should be designed around the approved opportunity data model.

---

## 5. Functional and quality requirements

The following requirements should guide design, implementation, and testing.

### 5.1 Bilingual experience

- Provide English and Arabic interface content.
- Support correct RTL layout and reading order in Arabic.
- Translate user-facing content, not only navigation labels.
- Avoid hard-coded English-only labels in otherwise Arabic experiences.

### 5.2 Responsive behavior

The application should be designed and tested for:

- Mobile screens.
- Tablet screens.
- Desktop screens.

Responsive behavior must be verified using actual browser/device testing during implementation. It should not be marked as complete based only on reading CSS or reviewing a design.

### 5.3 Accessibility

The implementation should include an accessibility review covering, at minimum:

- Keyboard navigation and visible focus states.
- Appropriate semantic HTML and accessible names.
- Screen-reader announcements for dynamic feedback where needed.
- Text alternatives or equivalent descriptions for meaningful charts and visualizations.
- Accessible form controls and assessment options.
- Sufficient color contrast in both light and dark themes.
- Respect for reduced-motion preferences.

### 5.4 Data integrity and security

- User progress and achievements should not be vulnerable to repeated client-side actions that grant duplicate rewards.
- Sensitive assessment answers or grading logic should not be exposed unnecessarily in client code.
- Authentication and authorization must be enforced appropriately.
- Administrative features must be restricted to authorized roles.
- Persistent records and important actions should be validated on the server side.

### 5.5 Testing

The completed application should be tested through appropriate methods, including:

- Unit tests for important logic.
- Database and authorization tests, including row-level security where applicable.
- End-to-end tests for major user journeys.
- Responsive and cross-browser checks.
- Accessibility checks.
- Visual comparison against the approved design and prototype.

No tests are claimed to have been run at this planning stage.

---

## 6. Implementation milestones

The following sequence is a proposed way to organize the work. Exact task ownership and dates can be added by the team.

| Milestone | Focus | Expected outcome |
|---|---|---|
| 1 | Requirements and project documentation | Approved scope, track catalog, content model, and project documents. |
| 2 | UI/UX design | Complete screen designs, reusable components, design system, and responsive specifications. |
| 3 | Interactive prototype | Connected user flows and testable interactions based on the approved designs. |
| 4 | Application foundation | Selected technical stack, project structure, routing, shared components, and localization foundation. |
| 5 | Core career discovery | Track catalog, track details, assessment, and recommendations. |
| 6 | Learning experience | Roadmaps, resource library, labs, scenarios, and learning progress. |
| 7 | User experience and engagement | Authentication, profiles, achievements, and persistent user data. |
| 8 | Opportunities and administration | Opportunity workflows and administrative content management. |
| 9 | Quality assurance | Functional, security, accessibility, bilingual, responsive, and end-to-end testing. |
| 10 | Release preparation | Final content review, fixes, and deployment preparation. |

---

## 7. Confirmed requirements vs. recommendations

This section is intended to prevent proposals from being mistaken for approved requirements.

### 7.1 Confirmed project scope

The following items are recorded as confirmed by the project owner:

- The project is intended to cover the complete scope, not only an MVP.
- The project has two independent workstreams.
- The starting catalog contains 19 tracks across 6 categories.
- Each track uses a 17-item content template.
- Learning resources use the ten specified metadata fields and six specified resource types.
- Content should be data-driven and manageable by administrators.
- External links must not be fabricated.
- Content must not be falsely labeled as verified.
- `roadmap.sh` is an external reference for roadmap research.
- A Figma handoff document is part of the project documentation.
- The project documentation includes revised documents and three additional documents.

### 7.2 Recommendations requiring approval

The following are proposals and are **not confirmed requirements** unless the project owner approves them:

- Vite with React and TypeScript.
- Guest mode.
- An expanded assessment and a two-step recommendation process.
- A publishing gate for content.
- A formal content-verification workflow.
- Specific content-depth targets beyond the approved content template.
- Six optional additional tracks.
- Additional screens proposed in the Figma handoff.
- Independently authoring roadmaps rather than copying an external roadmap.

---

## 8. Related project documents

The following documents support the project and should be kept consistent with this plan:

- `FIGMA_DESIGN_HANDOFF.md` — UI/UX design requirements, screen inventory, user flows, design system, and responsive behavior.
- `TRACK_CATALOG.md` — the 19-track starting catalog and its 6 categories.
- `TECHNICAL_ARCHITECTURE.md` — the technical architecture, once the implementation decisions have been reviewed and approved.

If any additional documents are created, their purpose and status should be stated clearly.

---

## 9. Document maintenance

Update this document as the project progresses.

When reporting status, distinguish clearly between:

- **Planned:** included in the agreed project scope but not yet completed.
- **In Design:** currently being designed.
- **Prototyped:** represented in the interactive prototype.
- **In Development:** currently being implemented in code.
- **Implemented:** completed in the application.
- **Tested:** verified through the relevant test process.
- **Approved:** explicitly reviewed and accepted by the project owner.

Do not mark a feature as implemented, tested, or approved solely because it is described in this document.
