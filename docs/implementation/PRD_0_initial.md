# As Intended — Product Requirements Document (PRD)

**Version:** 1.0
**Date:** 2025-10-03
**Owner:** (you)
**Status:** Approved for implementation planning (Chrome-only MVP)

---

## 0) One-paragraph summary

**As Intended** is a Chrome extension + web app that intercepts visits to attention-trap sites with a **blocking intent modal**, records a privacy-minimized **activity log** while you browse, and then either **intervenes in real time** or **reports a session summary** based on whether your actions align with your stated intent. It delivers **positive reinforcement** on success, configurable **personality** (Playful default, Neutral optional), and a paid SaaS dashboard for insights, settings, and billing.

---

## 1) Goals & Non-Goals

### 1.1 Goals

* G1: Reduce unintentional feed consumption by forcing an explicit **intent declaration** at entry.
* G2: **Track and classify** session behavior vs. intent with minimal, containerized content capture.
* G3: **Follow-up modes**: (a) Intervention (real-time nudge), (b) Summary (end-of-session report).
* G4: **Reward success** with lightweight, configurable reinforcement.
* G5: Provide **metrics** (e.g., intent completion rate, time-to-completion, aligned vs. non-aligned time).
* G6: Launch a **subscription** product from day one with a **7-day full refund** guarantee.

### 1.2 Non-Goals (MVP)

* N1: No native mobile apps.
* N2: No Firefox/Safari/Edge builds.
* N3: No site-specific API integrations (DOM-only approach).
* N4: No heavy content processing of full post text (privacy: containerize/minimize).

---

## 2) Scope (MVP)

* Platform: **Chrome Extension (Manifest V3)** + **SaaS web app**.
* Works by default on **any site** matching configurable “attention-trap” patterns (e.g., `twitter.com`, `linkedin.com`, `reddit.com`, `instagram.com`, `facebook.com`, `youtube.com`, `tiktok.com`, etc.), with **user-controlled allow/deny lists**.
* Two personality modes: **Playful (default)**, **Neutral**.
* Two follow-up modes: **Intervention** or **Summary** (user-selectable).
* **Timeboxing** optional per session (default off).
* Billing: **subscription from day one**, **7-day full refund**.

---

## 3) User Experience & Flows

### 3.1 Onboarding

1. Install extension from Chrome Web Store.
2. First open of any tracked site → **blocking modal** appears.
3. User creates account (email + magic link) or logs in.
4. 7-day paid guarantee starts immediately after first login; subscription required to continue past day 7.

### 3.2 Blocking Intent Modal (Core)

* Appears on initial navigation to a **tracked** site.
* **Free-text intent input** + **quick suggestions** (chips): `Reply to DM`, `Grab a link`, `Post update`, `Search`, `Check mentions`.
* **LLM clarity validation**:

  * If vague → input gives light shake animation + message:

    * Playful: *“Hmm, that’s foggy. What’s the mission, captain?”*
    * Neutral: *“Intent too vague. Provide a specific goal or dismiss As Intended.”*
* **Primary actions**:

  * `Start with this intent` (records intent; session active)
  * `Dismiss for now` (modal closes; **agent inactive** for this session)
* Optional **timebox** selector (off by default): `3m · 5m · 10m · custom`.

### 3.3 Intervention Mode (if enabled)

* **Live activity classifier** evaluates events vs. intent:

  * If **off-intent** pattern persists beyond a threshold (configurable), show **nudge overlay**:

    * Playful: *“Feed vortex detected. Still on mission ‘reply to Sam’?”* [Continue] [Return to intent]
    * Neutral: *“Detected off-intent activity. Intent: ‘reply to Sam’. Continue?”* [Continue] [Return]
* If intent is **fulfilled** (completion conditions met) → **success toast**:

  * Playful: *“🎉 Mission accomplished in 1m 42s. Doom dodged.”*
  * Neutral: *“Intent completed. Duration: 1m 42s.”*
* On **timebox expiry**:

  * Screen-cover modal: *“Timebox ended. Did you finish?”* [Mark complete] [Add 2 min] [Dismiss]

### 3.4 Summary Mode (if enabled)

* No live nudges.
* On navigation away/tab close/long idle → show **session summary** (popup or page):

  * Intent, status (Completed / Not completed), time to completion, aligned time %, off-intent episodes, suggested improvements.

### 3.5 Extension Popup (mini dashboard)

* Today: intents started, completed, average time-to-completion, aligned %.
* Last 7 days sparkline for aligned vs. off-intent minutes.
* Quick toggles: follow-up mode, personality, site enable/disable.
* Button to **Open full dashboard**.

### 3.6 Web App (full dashboard)

* **Home:** rolling metrics, streaks, recent intents, completion rate.
* **Sessions:** table + drill-down to activity log.
* **Settings:** personality, follow-up mode defaults, timebox defaults, site lists.
* **Billing:** subscription status, invoices, **refund within 7 days** self-serve.
* **Security & Data:** export/delete data, retention controls.

---

## 4) Functional Requirements (IDs)

### 4.1 Intent Capture & Validation

* **FR-I1:** Show blocking modal on first load of tracked site.
* **FR-I2:** Accept **free-text** intent; support quick suggestions.
* **FR-I3:** Validate intent clarity via LLM; reject vague intents with actionable message.
* **FR-I4:** Allow `Dismiss for now` which **disables** agent for this session (until tab closed or site changed).

### 4.2 Session Tracking & Classification

* **FR-S1:** Session starts when intent accepted; ends on site leave/tab close/30-min idle.
* **FR-S2:** Content script collects **privacy-minimized events** (routes, click role, scroll regions, focus areas, limited keystroke metadata but **no raw message/post content**).
* **FR-S3:** Extension **summarizes** events into **ActivityLogItem**(s) (see Data Model).
* **FR-S4:** Background service **streams** items to backend over secure channel with **back-pressure** and offline queue.

### 4.3 Alignment Engine

* **FR-A1:** Backend computes alignment in near-real-time using hybrid rules: heuristics + LLM for ambiguous cases.
* **FR-A2:** Detect **intent fulfillment** via site-agnostic signals (e.g., compose→submit, open DM→send) + intent text mapping.
* **FR-A3:** In **Intervention mode**, trigger overlay on sustained off-intent behavior (threshold configurable: default 20 seconds of continuous feed scrolling or 2 off-intent actions).
* **FR-A4:** In **Summary mode**, generate end-of-session report only.

### 4.4 Reinforcement & Messaging

* **FR-R1:** Show **success toast** when intent fulfilled.
* **FR-R2:** Personality modes affect copy only (Playful/Neutral), not logic.
* **FR-R3:** Timebox reminders when enabled.

### 4.5 Sites & Targeting

* **FR-T1:** Default tracked domains include major attention traps but **works on any domain** unless explicitly excluded.
* **FR-T2:** User can maintain **Allow list** (never intercept) and **Track list** (always intercept).
* **FR-T3:** Per-site overrides (e.g., LinkedIn off during work hours).

### 4.6 Accounts & Billing

* **FR-B1:** Auth via **email + magic link** (passwordless).
* **FR-B2:** Subscription required beyond day 7; **automatic full refund** if user cancels within 7 days.
* **FR-B3:** Stripe for billing; sync subscription status to extension.

### 4.7 Data Portability & Privacy

* **FR-P1:** User can export their data (JSON) and request deletion.
* **FR-P2:** Data minimization: store **containers**(roles/selectors, event types, hashed text tokens), not raw content.
* **FR-P3:** Configurable retention (default 90 days for detailed events; aggregates retained).

---

## 5) Non-Functional Requirements (NFRs)

* **NFR-1 Performance:** Modal must appear within **200 ms** post DOMContentLoaded.
* **NFR-2 Reliability:** Offline buffering with retry; no event loss under normal usage.
* **NFR-3 Privacy:** No transmission of raw message/post text; LLM prompts receive **only containerized descriptors**.
* **NFR-4 Security:** TLS 1.2+, signed JWT between extension and backend; CSP in web app; OWASP-level hardening.
* **NFR-5 Accessibility:** Modal keyboard navigable; focus traps; ARIA roles; WCAG AA.
* **NFR-6 Observability:** Structured logs, metrics, traces (OpenTelemetry).
* **NFR-7 Maintainability:** Typed code (TS/Python), linting, tests, migrations, infra as code.

---

## 6) Architecture

### 6.1 High-Level

* **Client (Chrome Extension, MV3)**

  * **Content scripts** injected on tracked domains.
  * **Background service worker**: event bus, policy, networking.
  * **Extension popup**: mini dashboard + quick settings.
* **Backend (FastAPI, Python 3.11+)**

  * Ingest API (events, sessions).
  * Alignment engine (rules + LLM).
  * Auth & billing webhooks.
  * Aggregation & analytics jobs.
* **Web app (SvelteKit 5, TS, Tailwind)**

  * Dashboard, sessions, settings, billing UI.
* **Data (PostgreSQL + JSONB)**

  * Normalized tables + JSONB activity logs.
  * Alembic migrations.

### 6.2 Extension Components

* **manifest.json (MV3)**: permissions: `scripting`, `storage`, `activeTab`, `webNavigation`, host permissions for tracked domains.
* **Content script responsibilities:**

  * Detect URL patterns, key UI regions (feed, composer, DM).
  * Instrument events: `click`, `scroll`, `input`, `visibilitychange`, route changes.
  * **Redact** text; send **containers**: role (e.g., `button[aria-label=Compose]`), area (`#feed`/`[data-testid=primaryColumn]`), action type (`CLICK`, `SCROLL`, `NAVIGATE`), keypress **category** (e.g., `typing in composer`), not content.
* **Background service worker:**

  * Shows **blocking modal** via `chrome.scripting.executeScript` + injected UI or via CSS overlay.
  * Session lifecycle; offline queue (IndexedDB).
  * Throttled batching of ActivityLogItem(s) to backend; JWT auth.
  * Receives alignment signals for live interventions.

### 6.3 Backend Modules (FastAPI)

* **Auth**: magic link (email), JWT sessions.
* **Ingest**: `/v1/events/batch`, `/v1/sessions/start`, `/v1/sessions/end`.
* **Alignment engine**:

  * **Rules layer** (deterministic): route in messages area, click on send button → likely fulfillment for “reply/send”. Long scroll in feed → off-intent.
  * **LLM layer** (only when ambiguous): map intent text ↔ observed actions. Prompt receives **container summaries** only.
* **Analytics**: nightly jobs to compute aggregates (completion rate, aligned minutes, time-to-completion).
* **Billing**: Stripe webhooks; enforce access window; 7-day refund flow.

---

## 7) Data Model

### 7.1 TypeScript (client) — canonical shapes

```ts
type Intent = {
  id: string;
  text: string;            // user-entered free text
  createdAt: string;       // ISO
  timeboxSec?: number;     // optional
};

type ActivityLogItem = {
  ts: string;              // ISO
  route: string;           // path + minimal query (redacted)
  area: 'FEED' | 'COMPOSER' | 'DM' | 'PROFILE' | 'SEARCH' | 'OTHER';
  action: 'NAVIGATE' | 'SCROLL' | 'CLICK' | 'TYPE' | 'SUBMIT' | 'HOVER';
  elementRole?: string;    // e.g., 'button:compose', 'tab:messages', 'link:post'
  contentHash?: string;    // optional short hash of snippet if needed (never raw)
  dwellMs?: number;        // e.g., continuous feed scroll dwell
};

type AlignmentSignal = {
  intentAligned: boolean;       // current state
  intentFulfilling: boolean;    // this event likely fulfills intent
  reason?: string;
};
```

### 7.2 PostgreSQL schema (key tables)

```sql
-- users
CREATE TABLE app_user (
  id UUID PRIMARY KEY,
  email CITEXT UNIQUE NOT NULL,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  personality_mode TEXT NOT NULL DEFAULT 'PLAYFUL', -- PLAYFUL | NEUTRAL
  followup_mode TEXT NOT NULL DEFAULT 'INTERVENTION', -- INTERVENTION | SUMMARY
  retention_days INT NOT NULL DEFAULT 90
);

-- subscriptions
CREATE TABLE subscription (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES app_user(id) ON DELETE CASCADE,
  status TEXT NOT NULL, -- ACTIVE | TRIAL | CANCELED | PAST_DUE
  started_at TIMESTAMPTZ NOT NULL,
  renewed_at TIMESTAMPTZ,
  provider TEXT NOT NULL, -- 'stripe'
  provider_ref TEXT NOT NULL
);

-- site settings
CREATE TABLE site_rule (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES app_user(id) ON DELETE CASCADE,
  pattern TEXT NOT NULL,       -- e.g., '*.twitter.com'
  mode TEXT NOT NULL,          -- TRACK | ALLOW | BLOCK
  hours_json JSONB             -- optional per-hour overrides
);

-- sessions
CREATE TABLE session (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES app_user(id) ON DELETE CASCADE,
  domain TEXT NOT NULL,
  started_at TIMESTAMPTZ NOT NULL,
  ended_at TIMESTAMPTZ,
  intent_text TEXT NOT NULL,
  timebox_sec INT,
  mode TEXT NOT NULL,            -- INTERVENTION | SUMMARY
  status TEXT NOT NULL,          -- COMPLETED | NOT_COMPLETED | DISMISSED
  completion_at TIMESTAMPTZ,
  aligned_ms BIGINT NOT NULL DEFAULT 0,
  off_intent_ms BIGINT NOT NULL DEFAULT 0
);

-- activity logs (append-only)
CREATE TABLE activity_log (
  id BIGSERIAL PRIMARY KEY,
  session_id UUID REFERENCES session(id) ON DELETE CASCADE,
  ts TIMESTAMPTZ NOT NULL,
  route TEXT,
  area TEXT,
  action TEXT,
  element_role TEXT,
  content_hash TEXT,
  dwell_ms INT,
  alignment_json JSONB           -- {intentAligned, intentFulfilling, reason}
);

-- aggregates (for fast dashboard)
CREATE TABLE daily_aggregate (
  user_id UUID NOT NULL REFERENCES app_user(id) ON DELETE CASCADE,
  day DATE NOT NULL,
  intents_started INT NOT NULL,
  intents_completed INT NOT NULL,
  aligned_ms BIGINT NOT NULL,
  off_intent_ms BIGINT NOT NULL,
  PRIMARY KEY (user_id, day)
);
```

---

## 8) APIs (FastAPI)

### 8.1 Auth

* `POST /v1/auth/magic/start` → `{ email }` → 204
* `POST /v1/auth/magic/verify` → `{ token }` → `{ jwt, user }`

### 8.2 Sessions

* `POST /v1/sessions/start`
  Req: `{ domain, intent: { text, timeboxSec? }, mode }`
  Res: `{ sessionId }`
* `POST /v1/sessions/end`
  Req: `{ sessionId, endedAt }` → 204

### 8.3 Events

* `POST /v1/events/batch`
  Req: `{ sessionId, items: ActivityLogItem[] }`
  Res: `{ signals?: AlignmentSignal[] }`  *(optional streaming back of nudges)*

### 8.4 Alignment (server internal)

* `POST /v1/alignment/evaluate`
  Req: `{ sessionId, intentText, window: ActivityLogItem[] }`
  Res: `{ intentAligned, intentFulfilling, reason }`

### 8.5 Dashboard

* `GET /v1/metrics/today` → mini dashboard numbers
* `GET /v1/metrics/weekly` → aligned vs. off-intent series
* `GET /v1/sessions` (paginated)
* `GET /v1/sessions/{id}` (with sampled activity log)

### 8.6 Billing

* `POST /v1/billing/subscribe`
* `POST /v1/billing/cancel`
* `POST /v1/billing/refund` (auto-approve if within 7 days)
* `POST /v1/billing/webhook/stripe` (webhook)

---

## 9) LLM Usage & Prompts

### 9.1 Intent Clarity Validation (client-initiated, server-executed)

* **Input:** intent text only.
* **System prompt (essence):**

  * “You validate if an intent is **specific and actionable** within a single session on a social site. Reject vague intents (‘browse’, ‘check stuff’). Accept intents with clear targets (‘Reply to Sam’s DM’, ‘Copy link to my last tweet’). Output: `OK | VAGUE` and short reason.”

### 9.2 Alignment Disambiguation (server-initiated)

* **Input:** `intentText`, last N **containerized** events (areas/actions/roles, no raw content).

* **System prompt (essence):**

  * “Determine if the user’s last actions align with the stated intent. Treat prolonged feed scrolling as off-intent unless explicit search or navigation to target area occurs. Output: `intentAligned`, `intentFulfilling`, `reason` (<= 100 chars).”

* **Data minimization:** Never send raw post text or message contents; only roles, areas, and hashed fingerprints if absolutely required.

* **Rate limiting & cost:** Evaluate every **2–4 seconds** only when rules layer is uncertain; rules cover ≥80% cases.

---

## 10) Heuristics (Rules Layer) — Site-agnostic

* **Composer flow:** area=`COMPOSER` + `TYPE` → `SUBMIT` ⇒ fulfillment for intents containing *post*, *publish*, *reply*, *send*.
* **DM flow:** navigate to messages area → **CLICK** on conversation item → **TYPE** → **SUBMIT** ⇒ fulfillment for intents containing *reply*, *DM*, *message*.
* **Link retrieval:** open post detail (route change with post identifier) + **CLICK** on share/copy role or context menu → `COPY` event if detectable ⇒ fulfillment for intents containing *copy link*, *share*.
* **Off-intent patterns:** continuous **SCROLL** in `FEED` area for > 20s or 2+ successive `CLICK` on random feed items not tied to intent keywords ⇒ off-intent.

---

## 11) Configuration & Policies

* **Personality:** `PLAYFUL` (default) or `NEUTRAL`.
* **Follow-up mode:** `INTERVENTION` (default) or `SUMMARY`.
* **Timebox:** optional per session; default off; presets 3/5/10 minutes.
* **Dismissal:** if user dismisses modal, agent remains inactive until tab closes or domain changes.
* **Sites:** global defaults + user allow/track lists; pattern syntax supports wildcards.

---

## 12) UI Specifications (key elements)

### 12.1 Modal

* **Layout:** Title, intent input, suggested chips, timebox dropdown, actions.
* **Keyboard:** Enter to confirm; Esc to dismiss; focus trapped.
* **Validation:** shake + inline error on `VAGUE`.

### 12.2 Nudge Overlay (Intervention)

* **Non-blocking** small card bottom-right; auto-hide on return to intent area; CTA to “Return to intent”.

### 12.3 Success Toast

* 2–3 seconds, top-right; includes **intent text** and **duration**.

### 12.4 Popup

* Four tiles (Today): `Intents`, `Completed`, `Aligned %`, `Avg time`.
* Sparkline (7 days).
* Toggles for personality & mode.

---

## 13) Metrics & KPIs

* **Primary:** Intent completion rate (%), average time-to-completion (sec), aligned vs off-intent minutes (per day).
* **Secondary:** Dismiss rate (%), intervention acceptance rate, time spent in feed pre- vs post-install.
* **Business:** Conversion to paid (%), 7-day refund rate, weekly retention.

---

## 14) Security, Privacy, Compliance

* **PII:** email only; no social credentials.
* **Storage:** JWT in extension storage; rotate regularly.
* **Event redaction:** never store raw messages/posts; keep role/selector hashes.
* **GDPR:** export/delete endpoints; DPA with processors (LLM, Stripe).
* **Transport:** HTTPS; HSTS; JWT audience/expiry checks.

---

## 15) Testing & Acceptance Criteria (samples)

* **AC-1 Modal timing:** On first navigation to `twitter.com`, modal appears ≤200 ms after DOMContentLoaded.
* **AC-2 Dismissal:** After `Dismiss`, no further interventions until tab close.
* **AC-3 Vague intent:** Input “check stuff” → validation returns VAGUE → shake + error.
* **AC-4 Fulfillment:** Intent “Reply to Sam”; user opens messages, types, sends → success toast appears; session `status=COMPLETED`.
* **AC-5 Off-intent nudge:** Intent “Copy link to my post”; user scrolls feed 25s → nudge overlay appears.
* **AC-6 Privacy:** No network payload contains raw message text (automated test inspects payloads).
* **AC-7 Data export:** User can download JSON with sessions, aggregates, redacted logs.
* **AC-8 Billing:** Cancel within 7 days triggers full refund automatically.

---

## 16) Deployment & Ops

* **Environments:** dev, staging, prod.
* **CI/CD:** lint + typecheck + tests + Alembic migrations.
* **Monitoring:** uptime, API latency, error rates, LLM call volume/costs.
* **Feature flags:** intervention thresholds, default sites.

---

## 17) Roadmap

* **MVP (this PRD):** Chrome, modal, intervention/summary modes, basic heuristics, LLM clarity & alignment fallback, popup + dashboard, Stripe billing.
* **V1.1:** Per-site heuristics packs, richer timeboxing UX, keyboard-only quick intents.
* **V1.2:** Team accounts (shared policies), Slack/Email weekly reports.
* **V2:** Firefox/Edge ports; optional local-only mode (no LLM) with reduced accuracy.

---

## 18) Open Questions (flagged for implementation planning)

* **OQ-1:** Should we maintain **site-specific adapters** (Twitter/X, LinkedIn, etc.) to increase fulfillment accuracy?
* **OQ-2:** Minimal **LLM vendor set** and model selection (cost vs. latency)?
* **OQ-3:** What’s the **default tracked domain list** shipped at install (to balance surprise vs. value)?
* **OQ-4:** Sampling strategy for activity logs (e.g., compress repetitive scroll events) to control storage/cost.

---

## 19) Copy (Playful vs Neutral) — Examples

* **Vague intent error:**

  * Playful: “That’s fog. What’s the mission?”
  * Neutral: “Intent too vague. Specify a concrete goal.”
* **Nudge:**

  * Playful: “Feed trap sprung. Still on ‘grab link’?”
  * Neutral: “Detected off-intent scrolling. Continue?”
* **Success:**

  * Playful: “🎉 Mission accomplished in {duration}. Doom dodged.”
  * Neutral: “Intent completed. Duration {duration}.”

---

## 20) Tech Stack (locked)

* **Extension:** TypeScript, MV3, IndexedDB (queue), Vite build.
* **Web App:** **SvelteKit 5 (rune mode)** + TypeScript + Tailwind.
* **Backend:** **FastAPI (Python 3.11+)**, Uvicorn/Gunicorn, Pydantic v2.
* **DB:** **PostgreSQL** (JSONB), **Alembic** migrations.
* **Queues/Jobs:** Celery or asyncio background tasks (simple first), later Redis if needed.
* **Billing:** Stripe.
* **Observability:** OpenTelemetry + Prometheus/Grafana or vendor.

---

### Appendix A — Event → Activity mapping (illustrative)

| Raw event                                           | Containerized mapping | Area        | Action |
| --------------------------------------------------- | --------------------- | ----------- | ------ |
| Click `button[data-testid=SideNav_NewTweet_Button]` | `button:compose`      | COMPOSER    | CLICK  |
| Scroll `#react-root [data-testid=primaryColumn]`    | `region:feed`         | FEED        | SCROLL |
| Click `a[href*="/messages"]`                        | `tab:messages`        | DM          | CLICK  |
| Keydown in `div[contenteditable]`                   | `editor:composer`     | COMPOSER    | TYPE   |
| Submit form `aria-label="Send"`                     | `button:send`         | DM/COMPOSER | SUBMIT |

---

This PRD is deliberately concrete on system behavior, data handling, and UI, with explicit IDs for traceability in an implementation plan. It assumes Chrome-only MVP, free-text intents with LLM validation, hybrid alignment (rules first, LLM fallback), privacy-minimized event capture, and a paid SaaS with 7-day refunds.
