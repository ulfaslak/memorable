# [Project Name] — Product Requirements Document (PRD)

**Version:** 1.0
**Date:** [YYYY-MM-DD]
**Owner:** [Your name/team]
**Status:** [Draft / Approved for implementation planning]

---

## 0) One-paragraph summary

[Provide a concise elevator pitch that captures: What is it? Who is it for? What problem does it solve? What's the core value proposition? Include key technical constraints if relevant (e.g., "web app", "CLI tool", "mobile-first", etc.)]

---

## 1) Goals & Non-Goals

### 1.1 Goals

* G1: [Primary user/business outcome]
* G2: [Key technical capability or feature set]
* G3: [Important UX goal or constraint]
* G4: [Metric or success criteria]
* G5: [Additional strategic goal]

### 1.2 Non-Goals (MVP)

* N1: [What you explicitly won't build in MVP]
* N2: [Platform/feature explicitly out of scope]
* N3: [Integration or capability deferred]
* N4: [Complexity/feature excluded for simplicity]

---

## 2) Scope (MVP)

* **Platform:** [Web app / Desktop app / CLI / Mobile / Browser extension / API / etc.]
* **Target users:** [Who will use this? Demographics, roles, context]
* **Core functionality:** [3-5 bullet points of must-have features]
* **Technical constraints:** [Language requirements, deployment targets, performance needs]
* **Timeline:** [If relevant: MVP in X weeks, followed by...]

---

## 3) User Experience & Flows

### 3.1 [Flow Name: e.g., Onboarding]

1. [Step 1: User action]
2. [Step 2: System response]
3. [Step 3: Next action]
4. [Expected outcome]

### 3.2 [Flow Name: e.g., Core Workflow]

* **Entry point:** [How user initiates]
* **Main actions:** [Key steps in the flow]
* **Exit/completion:** [How flow ends]
* **Error handling:** [What happens when things go wrong]

### 3.3 [Additional Flows]

[Repeat for each major user journey: authentication, main feature use, settings, etc.]

---

## 4) Functional Requirements (IDs)

### 4.1 [Feature Category 1: e.g., Authentication]

* **FR-A1:** [Specific requirement with acceptance criteria]
* **FR-A2:** [Another requirement]
* **FR-A3:** [Another requirement]

### 4.2 [Feature Category 2: e.g., Core Feature]

* **FR-C1:** [Specific requirement]
* **FR-C2:** [Another requirement]

### 4.3 [Feature Category 3: e.g., Data Management]

* **FR-D1:** [Specific requirement]
* **FR-D2:** [Another requirement]

### 4.4 [Additional Categories]

[Continue with: UI/UX requirements, integrations, admin features, etc.]

---

## 5) Non-Functional Requirements (NFRs)

* **NFR-1 Performance:** [Latency, throughput, or speed requirements with numbers]
* **NFR-2 Reliability:** [Uptime, error rates, recovery expectations]
* **NFR-3 Security:** [Auth requirements, data protection, compliance needs]
* **NFR-4 Scalability:** [Expected load, growth projections]
* **NFR-5 Accessibility:** [WCAG level, keyboard navigation, screen readers, etc.]
* **NFR-6 Observability:** [Logging, monitoring, alerting needs]
* **NFR-7 Maintainability:** [Code quality, testing, documentation standards]

---

## 6) Architecture

### 6.1 High-Level

* **[Component 1: e.g., Frontend]**
  * [Technology choice]
  * [Key responsibilities]
  * [Major libraries/frameworks]

* **[Component 2: e.g., Backend]**
  * [Technology choice]
  * [Key responsibilities]
  * [API design approach]

* **[Component 3: e.g., Database]**
  * [Technology choice]
  * [Schema approach]
  * [Migration strategy]

* **[Additional Components: e.g., Workers, Cache, CDN]**
  * [As needed for your architecture]

### 6.2 [Detailed Component Breakdown]

[For each major component, describe:]
* **Responsibilities:** [What it does]
* **Technologies:** [Specific choices with versions]
* **Interfaces:** [How it communicates with other components]
* **Key patterns:** [Design patterns, architectural decisions]

---

## 7) Data Model

### 7.1 [Language] (client/server) — canonical shapes

```[language]
// Primary entities with field descriptions
type [EntityName] = {
  id: [type];           // [description]
  [field]: [type];      // [description]
  [field]: [type];      // [description]
};

// Additional types, enums, interfaces
```

### 7.2 Database schema (if applicable)

```sql
-- [Table description]
CREATE TABLE [table_name] (
  id [type] PRIMARY KEY,
  [field] [type] [constraints],
  [field] [type] [constraints],
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- [Additional tables]
-- [Indexes]
-- [Constraints]
```

---

## 8) APIs (if applicable)

### 8.1 [API Category 1: e.g., Authentication]

* `[METHOD] /v1/[endpoint]`
  * Req: `{ [fields] }`
  * Res: `{ [fields] }`
  * Auth: [required/optional]

### 8.2 [API Category 2: e.g., Core Resources]

* `[METHOD] /v1/[endpoint]`
  * [Request/response format]
  * [Query parameters]
  * [Error responses]

### 8.3 [Additional Categories]

[Webhooks, WebSockets, GraphQL schemas, etc.]

---

## 9) External Integrations (if applicable)

### 9.1 [Integration Name: e.g., Payment Provider]

* **Purpose:** [Why this integration]
* **API:** [Which API/SDK]
* **Authentication:** [How auth works]
* **Key operations:** [What you'll call]
* **Error handling:** [How to handle failures]
* **Costs:** [Pricing model if relevant]

### 9.2 [Additional Integrations]

[LLMs, analytics, email, SMS, etc.]

---

## 10) Business Logic & Rules

[If your app has complex business logic, document it here:]

* **Rule 1:** [Condition] → [Action]
* **Rule 2:** [Calculation or validation logic]
* **Rule 3:** [State transitions]

[Examples: pricing calculation, eligibility rules, workflow state machines, etc.]

---

## 11) Configuration & Settings

* **[Setting category 1]:** [Options available, defaults, where configured]
* **[Setting category 2]:** [Options available, defaults, where configured]
* **Environment-specific:** [What varies between dev/staging/prod]

---

## 12) UI Specifications (if applicable)

### 12.1 [UI Element 1: e.g., Main Dashboard]

* **Layout:** [Grid, sections, components]
* **Key interactions:** [Click, hover, drag behaviors]
* **Responsive behavior:** [Mobile, tablet, desktop differences]

### 12.2 [UI Element 2: e.g., Forms]

* **Validation:** [Client vs server, error display]
* **Accessibility:** [Labels, ARIA, keyboard navigation]

### 12.3 [Design System References]

* **Colors:** [Palette or reference to design file]
* **Typography:** [Font families, sizes, weights]
* **Spacing:** [System used: 4px/8px grid, etc.]
* **Components:** [Button variants, input styles, etc.]

---

## 13) Metrics & Success Criteria

### 13.1 Product Metrics

* **Primary:** [Main KPI with target]
* **Secondary:** [Supporting metrics]
* **User behavior:** [Engagement, retention metrics]

### 13.2 Technical Metrics

* **Performance:** [Response time targets, throughput]
* **Reliability:** [Uptime, error rates]
* **Quality:** [Test coverage, bug density]

### 13.3 Business Metrics (if applicable)

* **Conversion:** [Sign-ups, purchases, etc.]
* **Revenue:** [MRR, ARPU, etc.]
* **Growth:** [User acquisition, retention rates]

---

## 14) Security, Privacy, Compliance

* **Authentication:** [Method: OAuth, magic link, passwords, etc.]
* **Authorization:** [RBAC, ABAC, scopes, etc.]
* **Data protection:** [Encryption at rest/in transit]
* **PII handling:** [What personal data is collected, how it's protected]
* **Compliance:** [GDPR, HIPAA, SOC2, etc. requirements]
* **Security practices:** [OWASP, penetration testing, etc.]

---

## 15) Testing & Acceptance Criteria

* **AC-1:** [Specific testable criterion with measurable outcome]
* **AC-2:** [Another criterion]
* **AC-3:** [Another criterion]

[Include: functional tests, performance tests, security tests, user acceptance tests]

---

## 16) Deployment & Operations

* **Environments:** [dev, staging, production]
* **CI/CD:** [Build, test, deploy pipeline]
* **Hosting:** [Cloud provider, services used]
* **Monitoring:** [APM, logs, alerts]
* **Backup & recovery:** [Strategy and RTO/RPO]
* **Rollback strategy:** [How to undo deployments]

---

## 17) Roadmap (Optional)

* **MVP (this PRD):** [Key features for initial launch]
* **V1.1:** [First iteration improvements]
* **V1.2:** [Second iteration]
* **V2:** [Major future version]

---

## 18) Open Questions

* **OQ-1:** [Unresolved technical decision]
* **OQ-2:** [Product direction question]
* **OQ-3:** [Integration or vendor selection]
* **OQ-4:** [Performance or scalability unknown]

[These should be resolved during implementation planning]

---

## 19) Tech Stack (Recommended/Required)

* **[Frontend/Client]:** [Framework + version, key libraries]
* **[Backend/Server]:** [Framework + version, key libraries]
* **[Database]:** [Primary DB + version]
* **[Cache/Queue]:** [Redis, RabbitMQ, etc.]
* **[Infrastructure]:** [Cloud provider, container orchestration]
* **[Observability]:** [Logging, monitoring, tracing tools]
* **[Development]:** [Testing frameworks, linters, formatters]

---

## Appendix A — [Additional Details]

[Use appendices for:]
* Detailed data transformations
* Algorithm specifications
* Third-party API mappings
* UI mockups or wireframe references
* Research findings
* User interview summaries

---

## Notes on Using This Template

**Completeness > Brevity:** A detailed PRD prevents costly rework during implementation.

**Traceability:** Use requirement IDs (FR-X1, NFR-Y2, AC-Z3) so implementation tasks can reference specific requirements.

**Stakeholder Alignment:** Share this PRD with all stakeholders before implementation begins.

**Living Document:** Update the PRD when significant decisions change scope or approach.

**AI-Friendly:** The more specific this PRD, the better the AI agent can generate implementation plans and code that matches your vision.

---

**This PRD should be detailed enough that a developer unfamiliar with the project could understand what to build, why, and how it should work.**
