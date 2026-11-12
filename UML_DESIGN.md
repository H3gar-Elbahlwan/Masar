# NaviTech (مسار) — UML Design

> الرسومات مكتوبة بـ **Mermaid.js** وبتتعرض تلقائيًا على GitHub. ولو عاوز تعرضها في أي مكان تاني، الصقها في [mermaid.live](https://mermaid.live) وصدّرها كصورة.

---

## 1. Use Case Diagram

Mermaid مفيهوش نوع Use Case رسمي، فبنستخدم `flowchart` بشكل مرادف: الـ Actors برّه حدود النظام، والـ Use Cases جوّه (`System Boundary`).

```mermaid
flowchart LR
    %% ===== Actors =====
    Student(["👤 Student / User"])
    Admin(["🛠️ Admin"])

    %% ===== System Boundary =====
    subgraph NaviTech["NaviTech System"]
        direction TB

        subgraph AUTH["Authentication"]
            UC1(["Register"])
            UC2(["Login / Logout"])
            UC3(["Manage Profile"])
        end

        subgraph QUIZ["RIASEC Quiz"]
            UC4(["Take RIASEC Quiz"])
            UC5(["View Results & Recommended Tracks"])
            UC6(["Choose Track"])
        end

        subgraph LABS["Taster Labs"]
            UC7(["Browse Taster Labs"])
            UC8(["Complete Taster Lab"])
            UC9(["Submit Lab Feedback"])
        end

        subgraph ROAD["Roadmaps"]
            UC10(["View Roadmap & Resources"])
            UC11(["Track Roadmap Progress"])
        end

        subgraph RADAR["Opportunity Radar"]
            UC12(["Browse Opportunities"])
            UC13(["Filter by Governorate / Track"])
            UC14(["Bookmark Opportunity"])
        end

        subgraph ADM["Admin Panel"]
            UC15(["Manage Opportunities (CRUD)"])
            UC16(["Manage Tracks & Roadmaps"])
            UC17(["Manage Taster Labs"])
            UC18(["Manage Quiz Questions"])
        end
    end

    %% ===== Student interactions =====
    Student --- UC1
    Student --- UC2
    Student --- UC3
    Student --- UC4
    Student --- UC5
    Student --- UC6
    Student --- UC7
    Student --- UC8
    Student --- UC10
    Student --- UC11
    Student --- UC12
    Student --- UC14

    %% ===== Admin interactions =====
    Admin --- UC2
    Admin --- UC15
    Admin --- UC16
    Admin --- UC17
    Admin --- UC18

    %% ===== Include / Extend =====
    UC4 -. "«include»" .-> UC5
    UC8 -. "«extend»" .-> UC9
    UC12 -. "«include»" .-> UC13
    UC4 -. "«precondition»" .-> UC2
```

### شرح الـ Use Case Diagram

| العنصر | التوضيح |
|---|---|
| **Student / User** | المستخدم المسجّل. بيعمل الكويز ويشوف الترشيحات ويجرب Labs ويتابع Roadmap ويتصفح الفرص. |
| **Admin** | مدير المحتوى. بيدخل ويعدل الفرص والتراكات والـ Roadmaps والـ Labs وأسئلة الكويز يدويًا. |
| **«include»** | علاقة إجبارية: أخذ الكويز يستدعي دايمًا عرض النتيجة. وتصفح الفرص بيتضمن إمكانية الفلترة. |
| **«extend»** | علاقة اختيارية: بعد إنهاء الـ Lab المستخدم **ممكن** يرسل Feedback، مش لازم. |
| **Login** | مشترك بين الـ Student والـ Admin، والصلاحيات بتتفرق بعدها بالـ Role. |

---

## 2. Class Diagram

```mermaid
classDiagram
    direction LR

    class User {
        +UUID id
        +String name
        +String email
        -String passwordHash
        +String governorate
        +String educationLevel
        +Role role
        +UUID chosenTrackId
        +DateTime createdAt
        +register() void
        +login() Token
        +updateProfile() void
        +takeQuiz() QuizResult
        +chooseTrack(trackId) void
        +bookmarkOpportunity(oppId) void
    }

    class Admin {
        +manageOpportunities() void
        +manageTracks() void
        +manageRoadmaps() void
        +manageTasterLabs() void
        +manageQuizQuestions() void
    }

    class QuizResult {
        +UUID id
        +UUID userId
        +int realistic
        +int investigative
        +int artistic
        +int social
        +int enterprising
        +int conventional
        +String hollandCode
        +DateTime takenAt
        +calculateScores() void
        +getRecommendedTracks() List~Track~
    }

    class Track {
        +UUID id
        +String name
        +String description
        +List~String~ requiredSkills
        +List~String~ careerOutcomes
        +Map riasecWeights
        +getRoadmap() Roadmap
        +getTasterLabs() List~TasterLab~
    }

    class TasterLab {
        +UUID id
        +UUID trackId
        +String title
        +String scenario
        +int durationMinutes
        +String difficulty
        +start() void
        +complete() void
    }

    class Roadmap {
        +UUID id
        +UUID trackId
        +String title
        +String estimatedDuration
        +getStages() List~RoadmapStage~
        +calculateProgress(userId) float
    }

    class RoadmapStage {
        +UUID id
        +String title
        +int stageOrder
        +List~Resource~ resources
        +markCompleted(userId) void
    }

    class Opportunity {
        +UUID id
        +String title
        +String provider
        +String description
        +String type
        +String governorate
        +Date deadline
        +String applyLink
        +Boolean isActive
        +isExpired() Boolean
        +matches(governorate, trackId) Boolean
    }

    %% ===== Relationships =====
    Admin --|> User : inherits
    User "1" --> "0..*" QuizResult : takes
    User "*" --> "0..1" Track : chooses
    User "*" --> "*" Opportunity : bookmarks
    QuizResult "*" --> "*" Track : recommends
    Track "1" *-- "1" Roadmap : has
    Roadmap "1" *-- "1..*" RoadmapStage : contains
    Track "1" o-- "0..*" TasterLab : offers
    Track "*" -- "*" Opportunity : relevantTo
    Admin "1" --> "0..*" Opportunity : manages
```

> **ملحوظة:** أضفنا `TasterLab` و`RoadmapStage` فوق الكيانات الستة المطلوبة، لأنهم ضروريين لتمثيل Taster Labs وتفاصيل الـ Roadmap. لو عاوزه مبسط جدًا، تقدر تشيلهم وتحتفظ بالستة الأساسيين.

---

## 3. شرح العلاقات بين الـ Classes

### 3.1 جدول العلاقات

| العلاقة | النوع | الـ Multiplicity | التفسير |
|---|---|---|---|
| `Admin` ← `User` | **Inheritance** (Generalization) | — | الأدمن هو User بصلاحيات إضافية، فبيرث كل خصائصه (email, login, ...) ويضيف دوال الإدارة. |
| `User` → `QuizResult` | Association | 1 إلى 0..* | المستخدم الواحد ممكن يعمل الكويز أكتر من مرة، فيبقى عنده عدة نتائج (History). |
| `QuizResult` → `Track` | Association | * إلى * | نتيجة الكويز بتفرز عدة تراكات مرشحة، والتراك الواحد ممكن يظهر في نتايج ناس كتير. |
| `User` → `Track` | Association | * إلى 0..1 | المستخدم يختار تراك واحد كحد أقصى كـ Chosen Track، والتراك ممكن يختاره ناس كتير. |
| `Track` ◆— `Roadmap` | **Composition** | 1 إلى 1 | الـ Roadmap مالهاش معنى من غير التراك، ولو التراك اتمسح بتتمسح معاه. |
| `Roadmap` ◆— `RoadmapStage` | **Composition** | 1 إلى 1..* | المراحل جزء لا يتجزأ من الـ Roadmap. |
| `Track` ◇— `TasterLab` | **Aggregation** | 1 إلى 0..* | التراك بيضم عدة Labs، لكن الـ Lab ممكن يتنقل أو يتعاد استخدامه كمحتوى مستقل. |
| `Track` — `Opportunity` | Association | * إلى * | الفرصة الواحدة ممكن تناسب أكتر من تراك، والتراك عنده فرص كتير. |
| `User` → `Opportunity` | Association | * إلى * | عمل Bookmark: مستخدمين كتير ممكن يحفظوا نفس الفرصة. |
| `Admin` → `Opportunity` | Association | 1 إلى 0..* | الأدمن بيدخل ويدير الفرص يدويًا. |

### 3.2 تحويلها لجداول في قاعدة البيانات

علاقات **Many-to-Many** بتتحول لجداول وسيطة (Junction Tables):

- `quiz_result_tracks` (quiz_result_id, track_id, match_percentage)
- `opportunity_tracks` (opportunity_id, track_id)
- `user_bookmarks` (user_id, opportunity_id)
- `user_roadmap_progress` (user_id, stage_id, completed_at)

---

## 4. أسئلة متوقعة في السكشن (Q&A Prep)

**س1: ليه Admin بيرث من User؟**
لأن الأدمن في الأصل مستخدم مسجّل (بيسجل دخول ولديه بروفايل)، وبيضيف عليه صلاحيات إدارة. الوراثة بتمنع تكرار الكود. وفي التنفيذ الفعلي بنستخدم حقل `role` في جدول واحد (`users`) بدل جدولين.

**س2: إيه الفرق بين Composition و Aggregation عندكم؟**
الـ Composition (زي Track → Roadmap) يعني الجزء بيموت بموت الكل. الـ Aggregation (زي Track → TasterLab) يعني الجزء له وجود مستقل نسبيًا.

**س3: ليه QuizResult كلاس منفصل مش جزء من User؟**
لأن المستخدم ممكن يعيد الاختبار، فمحتاجين نحتفظ بالتاريخ. كمان ده بيفيد في Phase 2 لأن البيانات دي هتتحول لـ Dataset للـ AI.

**س4: إزاي النظام بيرشح التراكات؟**
كل Track عنده أوزان RIASEC (`riasecWeights`). بنحسب تطابق بين درجات المستخدم وأوزان التراك (مثلًا Cosine Similarity أو مجموع الأوزان)، ونرتب التراكات تنازليًا بنسبة التطابق. ده Rule-Based في Phase 1، ومعزول في Service مستقلة عشان نبدله بـ AI في Phase 2.

**س5: إزاي الفلترة بالمحافظة والتراك بتشتغل؟**
`Opportunity` فيها حقل `governorate`، وعلاقة Many-to-Many مع `Track`. الفلترة عبارة عن Query بشرط على المحافظة وJoin على جدول `opportunity_tracks`، مع Indexes على الحقول دي للأداء.

**س6: فين Taster Labs في الـ Use Case؟**
المستخدم بيتصفحها ويكملها (`Complete Taster Lab`)، وبعدها اختياريًا بيرسل Feedback (`extend`)، والنتيجة بتتسجل لتحسين الترشيحات مستقبلًا.

**س7: ليه استخدمتوا `flowchart` للـ Use Case؟**
لأن Mermaid ما بيدعمش Use Case Diagram رسمي. المحتوى مطابق لمعايير UML، ولو الدكتور طلب الشكل الكلاسيكي (بيضاوي + Stick Figure) نرسمه في Draw.io أو Figma بنفس الـ Actors والـ Use Cases.
