# FRONTEND_DESIGN.md

# 1. Brand Snapshot

**Project name:** Apogee  
**Tagline:** Mission control for your placement journey.  
**Product promise:** Apogee turns a student's resume, interviews and tests into one Launch Readiness Score that students can improve and trainers can monitor at scale.

**Wordmark + orbit glyph:** Set “apogee” in lowercase Space Grotesk. Replace the “o” with a thin orbit ring and place a small signal-orange dot at its upper-right edge to mark the peak. Keep the mark compact enough for the telemetry bar and large enough to anchor the Launch Gate.

**Rationale:** “ANALOG MISSION CONTROL” makes Apogee feel like a working flight-operations console rather than a generic space-themed website. Dark ink surfaces frame the live data, warm paper cards feel like printed mission briefs, and signal orange marks the one action that moves the user forward. Phosphor green is reserved for live/healthy states, never decoration. Fine registration marks, orbit arcs, stamped status labels and instrument-like gauges connect the space metaphor to real placement tasks: readiness, attempts, skill gaps, and batch health. The result should feel engineered, legible and calm under pressure.

**How this will look to judges**
- A coherent, recognizable interface with a clear “mission control” identity—not a stock space template.
- The resume-to-interview-to-readiness story is visually obvious in the student journey.
- Trainer analytics look like operational tools, and remain readable on a phone.

# 2. Design Tokens

## Colour tokens

| Name | Token | Hex | Use | Do / don't |
|---|---|---|---|---|
| Ink | `--color-ink` | `#0E1116` | Main page background | Use as the default canvas; don't put long body copy on it without contrast. |
| Panel | `--color-panel` | `#161B22` | Raised cards, nav and work areas | Use for grouped controls; don't confuse it with paper cards. |
| Paper | `--color-paper` | `#F2EBDD` | Briefing cards, result summaries and selected reading areas | Use dark ink text on it; don't use white text on paper. |
| Signal | `--color-signal` | `#FF5A1F` | Primary CTA and critical active selection | One primary CTA per screen; don't use as a general chart colour. |
| Phosphor | `--color-phosphor` | `#3DFFA2` | Live/OK states, connected indicators, successful completion | Only live or healthy; don't use for ordinary decoration. |
| Amber | `--color-amber` | `#FFB547` | Warnings, caution, secondary highlights | Pair with a label/icon; don't rely on colour alone. |
| Steel | `--color-steel` | `#8B98A9` | Muted text, dividers, borders and inactive scales | Check contrast for small text; don't use for primary body copy on ink. |
| Ice | `--color-ice` | `#BFE3FF` | Rare informational links and informational emphasis | Keep rare; don't compete with signal orange. |

## Typography

Use Google Fonts: **Space Grotesk** for headings, **Inter** for body copy, and **JetBrains Mono** for IDs, metrics, timestamps and micro-labels. Chakra Petch is an acceptable fallback display face only if Space Grotesk is unavailable.

| Role | Size | Weight | Line height | Notes |
|---|---:|---:|---:|---|
| Display | 48–64px | 600–700 | 1.0–1.08 | Landing headline or wow moment only; scale down on mobile. |
| H1 | 36px desktop / 30px mobile | 600–700 | 1.1 | One per page. |
| H2 | 28px / 24px mobile | 600 | 1.15 | Major sections. |
| H3 | 22px | 600 | 1.2 | Cards and subsections. |
| H4 | 18px | 600 | 1.25 | Compact panel titles. |
| Body | 16px | 400 | 1.5 | Main instructions and descriptions. |
| Small | 14px | 400–500 | 1.4 | Secondary copy, helper text. |
| Mono label | 11–12px | 500–700 | 1.35 | Uppercase, letter-spacing 0.08–0.14em. |
| Metric | 28–48px | 600 | 1.0–1.1 | JetBrains Mono or Space Grotesk; use tabular numerals. |

## Spacing, shapes and layers

- **Spacing:** 4px base. Use 4, 8, 12, 16, 24, 32, 40, 48, 64 and 80px. Keep form groups at 16–24px and page sections at 24–40px.
- **Radii:** 2px default; 4px maximum for cards and controls. Stamp badges may be slightly angled; never use large pill-shaped cards.
- **Borders:** 1px solid steel at low contrast on dark surfaces; ink/steel edge on paper cards. Use 1px crosshair registration marks in the corners of major cards.
- **Shadows:** hard offset shadows, e.g. 4px 4px 0px rgba(0,0,0,.35); paper cards may use 3px 3px 0 ink. Avoid diffuse floating shadows and glass effects.
- **Z-index:** base 0; surface 10; sticky nav/telemetry 20; dropdown 30; toast 40; modal/backdrop 50.
- **Breakpoints:** mobile baseline 375px; tablet layout at 768px; desktop layout at 1280px. At 375px, no horizontal page scrolling. At 768px, allow two-column layouts where content remains readable. At 1280px, use a 12-column grid and a content max-width around 1440px.
- **Texture:** very faint grain/scanlines on dark surfaces only. Keep opacity low enough that small text remains crisp.
- **Orbit motif:** thin concentric arcs behind headers or in card corners; never place busy line art behind body text.
- **Registration marks:** four tiny L-shaped corner marks on key cards and the login panel. They are structural marks, not decorative borders.

## Tailwind CSS v4 theme

```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;600;700&family=Space+Grotesk:wght@400;500;600;700&display=swap');

@theme {
  --color-ink: #0E1116;
  --color-panel: #161B22;
  --color-paper: #F2EBDD;
  --color-signal: #FF5A1F;
  --color-phosphor: #3DFFA2;
  --color-amber: #FFB547;
  --color-steel: #8B98A9;
  --color-ice: #BFE3FF;
  --font-display: "Space Grotesk", "Chakra Petch", sans-serif;
  --font-body: "Inter", sans-serif;
  --font-mono: "JetBrains Mono", monospace;
}
```

Plain CSS variables for non-Tailwind use:

```css
:root {
  --ink: #0E1116;
  --panel: #161B22;
  --paper: #F2EBDD;
  --signal: #FF5A1F;
  --phosphor: #3DFFA2;
  --amber: #FFB547;
  --steel: #8B98A9;
  --ice: #BFE3FF;
  --font-display: "Space Grotesk", "Chakra Petch", sans-serif;
  --font-body: "Inter", sans-serif;
  --font-mono: "JetBrains Mono", monospace;
}
```

Google Fonts link tags:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;600;700&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
```

# 3. Layout and Navigation

## App shell

1. **TelemetryBar** across the top: Apogee wordmark + orbit glyph, current UTC time, connection dot with text (“SYSTEMS NOMINAL” or “RECONNECTING”), and the active workspace label (“STUDENT FLIGHT DECK” or “COMMAND CENTER”). Do not invent a live clock value in static mockups; show `UTC // 14:32:08` as sample UI data.
2. **Primary navigation:** desktop left rail below the telemetry bar; mobile compact top row with a menu button and a bottom navigation strip for the most-used student destinations. Keep navigation consistent across pages.
3. **Main content:** responsive max-width container, PageHeader, then page-specific cards/panels. Prefer paper cards for key briefing/results and dark panels for editors, chat, tables and navigation.
4. **Footer:** small mono text: `APOGEE // PLACEMENT OPERATIONS` and a build/environment label such as `DEMO ENVIRONMENT`. No marketing footer links are needed.

## Navigation by role

- **Student:** Mission Control (S2), Test Arena (S3), Interview Room (S5), Resume Lab (S6), Code Lab (S7). Debrief (S4) is reached after a test attempt. Mission Control links to Streaks/Leaderboard, Study Plan and Study Library sections when those F7/F9/F10 extras are built.
- **Trainer:** Command Center (S8) with Tests, Batches and Students tabs. Trainers do not see student-only Code Lab or Interview Room as primary navigation.
- **Admin:** Command Center (S8) with extra user/batch management actions. Admin accounts are seeded according to the PRD.
- **Launch Gate (S1):** public route; after login, `student` goes to S2 and `trainer`/`admin` goes to S8. If a user opens a page outside their role, redirect to their own dashboard.

## Responsive rules

- Mobile-first at 375px: stack cards, keep one main CTA visible, use full-width form controls and a sticky bottom action only where useful (Test Arena submit and Interview Room answer action).
- Tablet at 768px: use two columns for dashboard metrics and result panels; keep tables horizontally scrollable with the key identity/score columns sticky if possible.
- Desktop at 1280px: left navigation rail (220–248px), content area, and optional right summary rail for the Interview Room or Resume Lab. Never let dense tables shrink to unreadable text.
- Respect reduced-motion settings. Motion is reserved for the readiness score count-up, a restrained status blink, typewriter headline on first landing, and slow orbit rotation on the wow screen.

# 4. Component Library

All components use the exact palette and sharp 2–4px corners. Every interactive component must have visible keyboard focus and a disabled state. If an item is loading, explain what is happening instead of showing a spinner alone.

| Component | Purpose and variants | States | Plain-language props | Used on |
|---|---|---|---|---|
| **Button** | Primary signal-orange; secondary outlined steel; quiet text; destructive outline | Default, hover (slight lift), focus ring ice, disabled, loading with label | `label`, `variant`, `disabled`, `loading`, `onClick`, optional icon | S1–S8 |
| **BriefingCard** | Warm paper card for a key summary, score or result; dark ink text | Default, hover only if clickable, focus if interactive | `title`, `eyebrow`, `children`, `stamp`, `onClick` | S2, S4, S6 |
| **PanelCard** | Dark raised surface for tools, tables, chat and forms | Default, hover for selectable panels, focus for interactive cards | `title`, `children`, `footer`, `variant` | S1–S8 |
| **StatusStamp** | Slightly rotated stamped label: `NOMINAL`, `IN REVIEW`, `ATTENTION`, `BASIC MODE` | Good/phosphor, warning/amber, neutral/steel, error/signal | `label`, `tone`, `rotation`, `icon` | S1–S8 |
| **GaugeRadial** | Instrument-like radial gauge with tick marks and a clear number | Normal, count-up, low/medium/high bands; accessible text equivalent | `value`, `max`, `label`, `subLabel`, `tone` | S2, S4, S6, S8 |
| **SegmentedBar** | Rectangular segmented progress indicator, not a soft rounded progress pill | Empty, partial, complete, warning | `value`, `max`, `segments`, `label`, `tone` | S2–S8 |
| **DataTable** | Crew roster and attempts table with readable columns | Loading skeleton rows, empty, error, sorted, row focus | `columns`, `rows`, `sort`, `onRowClick`, `emptyMessage` | S4, S8 |
| **FormField** | Label, control, helper/error copy, optional character/file info | Default, focus, invalid, disabled, success | `label`, `name`, `value`, `hint`, `error`, `required`, `onChange` | S1, S6, S8 |
| **Modal** | Confirm submit, end interview, assignment and destructive actions | Open, closing, busy, validation error | `title`, `description`, `confirmLabel`, `onConfirm`, `onClose` | S3, S5, S8 |
| **Toast** | Brief saved/error confirmation | Success, warning, error, informational; dismissible | `message`, `tone`, `duration`, `onDismiss` | S1–S8 |
| **OrbitLoader** | Orbit ring animation with textual progress status | Loading, reduced-motion static ring, timeout/retry | `label`, `detail` | S1–S8 |
| **EmptyState** | Helpful empty panel with one next action | First-use, filtered-empty | `title`, `description`, `actionLabel`, `onAction` | S2–S8 |
| **ErrorState** | Honest recoverable error with retry or fallback note | Network, permission, AI fallback, upload error | `title`, `description`, `retryLabel`, `onRetry` | S1–S8 |
| **TelemetryBar** | Brand, UTC sample/current clock, connection state, workspace | Nominal, waking server, disconnected | `workspace`, `connectionState`, `utcTime`, `user` | S1–S8 |
| **Navbar** | Role-aware desktop rail, mobile menu and student mobile shortcuts | Active, collapsed, menu open, role-filtered | `role`, `activePage`, `onNavigate`, `mobileOpen` | S2–S8 |
| **PageHeader** | Page title, one-sentence mission brief, optional ID/status | Default, with action, with breadcrumb | `title`, `description`, `eyebrow`, `action`, `status` | S2–S8 |
| **LaunchReadinessSummary** | Score, radial gauge, coverage note and next action | Initial score, updated score, incomplete data | `readinessScore`, `areasIncluded`, `previousScore`, `nextAction` | S2, S8 |
| **KeywordTag** | Missing/matched resume terms | Missing/signal outline, matched/phosphor outline, neutral | `keyword`, `state` | S5, S6 |
| **ChatMessage** | Interviewer and student messages with clear speaker labels | Normal, generating, fallback-generated | `speaker`, `message`, `timestamp`, `state` | S5 |
| **QuestionPalette** | Numbered question navigation and answered/unanswered state | Current, answered, unanswered, flagged | `questions`, `currentIndex`, `answers`, `onSelect` | S3 |
| **QuestionOption** | Large accessible MCQ answer row | Default, hover, selected, correct/incorrect in review, disabled | `label`, `selected`, `state`, `onSelect` | S3, S4 |
| **TopicAccuracy** | Topic-level result bars with score and comparison | Normal, weak topic, missing comparison | `topic`, `accuracy`, `batchAverage` | S4, S8 |
| **ResumeDropzone** | PDF upload with clear accepted file rules | Idle, dragging, selected, uploading, invalid type, too large, failed | `file`, `status`, `onFileSelect`, `onRemove` | S6 |
| **ResumeLineDiff** | Shows original resume line and proposed rewrite | Needs attention, improved, accepted/copied | `originalLine`, `suggestedLine`, `reason`, `onCopy` | S6 |
| **InterviewRoundSelector** | HR, Technical and Behavioral setup cards | Selected, unselected, disabled/loading | `round`, `selectedRound`, `onSelect`, `focusKeywords` | S5 |
| **CodeEditorPanel** | Editor-like code area, language picker, stdin and output panes | Editing, running, output, error, runner unavailable | `language`, `code`, `input`, `output`, `onRun`, `onSubmit` | S7 |
| **BatchWeakTopics** | Compact batch insight bars for common weak topics | Loading, populated, no attempts | `topics`, `batchName`, `onTopicSelect` | S8 |
| **StreakPatch** | Mission patch and days-in-orbit count | Active streak, streak at risk, earned badge | `streakCount`, `badges`, `points` | S2 |
| **StudyModuleRow** | Library module with completion state and company-track tag | Not started, in progress, complete | `title`, `topic`, `companyTrack`, `completed`, `onToggle` | S2 when F9 ships |

## Component interaction rules

- Primary button text describes the real action: “Analyze resume”, “Start interview”, “Submit test”. Only one primary orange CTA per visible screen.
- Focus outlines use `--color-ice`; never remove the browser outline without replacing it.
- Loading states use a label such as “Waking up the training server…” or “Scoring your answers…”.
- Errors say what failed and what the user can do. AI failure should switch to the PRD's fallback and show `BASIC MODE`, not block the journey.
- Tables, gauges and bars need text labels so colour is never the only way to understand the value.
- Use CSS/SVG for radial gauges and orbit diagrams; use a chart library only if a complex chart cannot be made clearly with CSS/SVG. Do not add a chart dependency just for decoration.

# 5. Page Specifications

The PRD inventory contains exactly eight pages: S1, S2, S8, S3, S4, S5, S6 and S7. Keep those IDs and names. S5 includes the Interview Report state; S6 includes the Resume Builder tab only when F8 is built. Do not create extra routes for reports, library or study plan.

## S1 — Launch Gate

**Purpose / user goal:** Authenticate or create an account, choose a role during sign-up, and enter the correct workspace.

**Layout, top to bottom**
- TelemetryBar with `PUBLIC ACCESS // APOGEE`.
- Two-column desktop composition: left paper briefing panel with wordmark, tagline and concise explanation; right dark login panel with tabs `LOG IN` / `SIGN UP`. Stack on mobile with form first after a compact brand header.
- Login fields: Email, Password. Sign-up adds Full name, Email, Password and Role (`Student`, `Trainer`). Admin is not self-selectable; admin accounts are seeded.
- Footer note: `SESSION TOKEN ISSUED AFTER AUTHENTICATION`.

**Exact sample copy**
- Headline: `Your next placement starts with a systems check.`
- Body: `Prepare with a clearer picture of your skills. Analyze your resume, practice interviews and tests, then track your Launch Readiness Score.`
- Button: `Log in to Apogee`
- Sign-up button: `Create account`
- Error: `Access not cleared. Check your email and password, then try again.`
- Success: `Identity verified. Routing to your workspace…`

**Components:** TelemetryBar, PanelCard, BriefingCard, FormField, Button, StatusStamp, OrbitLoader, Toast, ErrorState.

**Data / backend actions:** `User.name`, `User.email`, `User.role`, `User.batchId`, `User.readinessScore`. `API: see API_CONTRACT` for sign-up, login, current-user/session and logout. Never send or display `passwordHash`.

**States**
- Loading: `Verifying credentials…` and OrbitLoader.
- Empty: blank fields with example-format hints, not prefilled passwords.
- Error: incorrect password, duplicate email or server unavailable; preserve typed email.
- Success: route `student` to S2; `trainer` or `admin` to S8.

**Navigation:** S1 → S2 for student; S1 → S8 for trainer/admin. Logout from protected pages returns to S1.

**Memorable visual moment:** The wordmark sits like an insignia on warm paper, with a registration-marked access panel and a small orange “launch” action.

## S2 — Mission Control

**Purpose / user goal:** Give a student one clear view of readiness and the next best action.

**Layout, top to bottom**
- PageHeader: `MISSION CONTROL`, subtitle `Mission brief: close the largest skill gap before your next placement drive.`
- Main top row: large paper LaunchReadinessSummary on the left; dark “Recommended next action” panel on the right. On mobile, score first, then action.
- Next row: assigned Tests table/list with title, topic, duration and status; StreakPatch with `days in orbit`, points and badges.
- Lower sections: recent activity and compact `YOUR ORBIT / BATCH ORBIT` leaderboard preview. When F9/F10 are built, include tabs/sections for `Study Plan` and `Study Library`; do not show nonfunctional tabs before then.
- Readiness breakdown note: `Based on 2 of 4 areas` if data is incomplete, per PRD.

**Exact sample copy/data**
- `AARAV SHARMA // STUDENT FLIGHT DECK`
- Launch Readiness Score: **54 / 100**
- Status stamp: `PRE-LAUNCH`
- Next action: `Resume Lab: compare your resume with the Backend Intern role at NovaPay.`
- CTA: `Open Resume Lab`
- Assigned test: `SQL Fundamentals Check`, topic `SQL`, `20 min`, status `DUE`
- Assigned test: `Data Structures Sprint`, topic `DSA`, `15 min`, status `COMPLETED`
- Streak: `3 DAYS IN ORBIT`; points `240`; level `CADET`
- Recent activity: `Resume analysis not yet recorded`; `Last test: Data Structures Sprint · 72%`
- Batch leaderboard preview: `CSE-A 2027`, `Your rank: 8 / 12`.

**Components:** TelemetryBar, Navbar, PageHeader, LaunchReadinessSummary, GaugeRadial, BriefingCard, PanelCard, StatusStamp, SegmentedBar, StreakPatch, DataTable, EmptyState, OrbitLoader, Toast.

**Data / backend actions:** `User.name`, `User.role`, `User.batchId`, `User.readinessScore`, `User.streakCount`, `User.points`, `User.lastActiveDate`; `Test.title`, `Test.topic`, `Test.durationMinutes`, `Test.assignedBatchIds`; `TestAttempt.score`, `TestAttempt.submittedAt`, `InterviewSession.createdAt`, `ResumeReport.atsScore`, `PointsEvent.reason`, `PointsEvent.points`. `API: see API_CONTRACT` for dashboard summary, assigned tests, activity, leaderboard and optional study plan/library.

**States**
- Loading: skeleton gauge and list rows, plus `Loading your flight data…`.
- Empty: `No tests assigned yet. Your trainer will publish the next mission here.`
- Error: preserve shell and show retry card; do not fake a new readiness score.
- Success: after an activity, animate score from 54 to 61 if that is the returned server result; never hard-code that transition outside the demo mock.

**Navigation:** S2 → S3 to open an assigned test; S2 → S5 to start an interview; S2 → S6 to analyze resume; S2 → S7 for code practice. S4 returns to S2.

**Memorable visual moment:** A large, instrument-like readiness gauge with tick marks and an orange needle; the number is the focus, not a decorative space illustration.

## S8 — Command Center

**Purpose / user goal:** Trainers monitor readiness and weak topics, create tests, assign them to batches and export useful reports. Admins also manage batches and users.

**Layout, top to bottom**
- TelemetryBar and PageHeader: `COMMAND CENTER`, subtitle `Crew status, assessment readiness and batch-level gaps.`
- Tabs: `Tests`, `Batches`, `Students`; retain the same page route and update the active panel.
- Top metric strip: students in selected batch, average Launch Readiness Score, tests assigned, students below threshold.
- Main desktop two-column area: left `CREW ROSTER` DataTable; right `BATCH WEAK TOPICS` with bars for `Docker / Containers`, `SQL Joins`, `REST API Design`.
- Tests tab: create-test form (`Title`, `Topic`, `Duration (minutes)`), question add form, CSV upload area showing accepted/rejected row counts, batch selector and `Assign test`.
- Batches tab: batch list with name, year and trainer; Admin sees `Create batch`.
- Students tab: searchable roster with name, batch, readiness score, latest weak topics and last activity. Admin additionally sees `Add user`.
- Export action: `Export readiness CSV`.

**Exact sample copy/data**
- `MS. PRIYA NAIR // TRAINER CONSOLE`
- Batch: `CSE-A 2027`; roster count `12`; average readiness `58`; below threshold (`< 50`) `3`.
- Crew row: `Aarav Sharma` · `CSE-A 2027` · `61` · `Docker / Containers, SQL Joins` · `Today`
- Weak topics: `Docker / Containers — 7 students`; `SQL Joins — 6 students`; `REST API Design — 4 students`.
- CSV result: `22 questions added · 2 rows rejected. Review the rejected rows before assigning.`
- Test form sample: `Backend Readiness Check`, topic `Backend`, duration `25`.
- Admin label: `DR. ROHAN KULKARNI // PLACEMENT OPERATIONS`.

**Components:** TelemetryBar, Navbar, PageHeader, PanelCard, BriefingCard, StatusStamp, DataTable, BatchWeakTopics, GaugeRadial, SegmentedBar, FormField, Button, Modal, Toast, OrbitLoader, EmptyState, ErrorState.

**Data / backend actions:** `User.name`, `User.email`, `User.role`, `User.batchId`, `User.readinessScore`, `Test.title`, `Test.topic`, `Test.durationMinutes`, `Test.createdBy`, `Test.assignedBatchIds`, `Question.testId`, `Question.text`, `Question.options`, `Question.correctIndex`, `Question.topic`, `Question.difficulty`, `Batch.name`, `Batch.year`, `Batch.trainerId`, `TestAttempt.score`, `TestAttempt.topicAccuracy`, `TestAttempt.tabSwitchCount`, `TestAttempt.submittedAt`. `API: see API_CONTRACT` for roster, batch metrics, test CRUD, CSV import, assignment, admin user/batch management and CSV export.

**States**
- Loading: roster skeleton and `Syncing crew telemetry…`.
- Empty: `No students in this batch yet. Add students or select another batch.`
- Error: show which operation failed; don't discard a completed CSV parse summary.
- Success: after assignment show `Test assigned to CSE-A 2027. Students in this batch will see it in Mission Control.`

**Navigation:** S8 tabs remain within S8; row detail can open a student summary panel within this page. Logout returns to S1.

**Memorable visual moment:** A dense but readable crew roster beside batch weak-topic bars, giving judges the “one student's gap becomes a batch insight” payoff.

## S3 — Test Arena

**Purpose / user goal:** Complete a timed multiple-choice test, see remaining time and submit safely.

**Layout, top to bottom**
- PageHeader: `TEST ARENA`, test title and metadata.
- Test list state: paper briefing row for each assigned `Test` with topic, duration and `Start test`.
- Active test state: narrow launch countdown header with time remaining, question progress and status stamp `IN PROGRESS`; question text in a paper card; four large option rows; question palette in a right panel on desktop and collapsible strip on mobile.
- Bottom action row: `Previous`, `Mark for review` (if supported by implementation), `Next`, and one primary `Submit test`.
- Confirmation modal warns about unanswered questions. At zero, auto-submit and show `Countdown reached zero. Your answers are being submitted.`

**Exact sample copy/data**
- Test: `SQL Fundamentals Check`; `20 MINUTES`; `12 QUESTIONS`; topic `SQL`.
- Question 1: `Which SQL clause filters grouped rows after aggregation?`
- Options: `A. WHERE`, `B. ORDER BY`, `C. HAVING`, `D. DISTINCT`.
- Question labels: `QUESTION 01 / 12`, `ANSWER SAVED`, `TIME REMAINING`.
- Warning: `3 questions are unanswered. Submit anyway?`

**Components:** TelemetryBar, Navbar, PageHeader, PanelCard, BriefingCard, StatusStamp, SegmentedBar, QuestionPalette, QuestionOption, Button, Modal, Toast, OrbitLoader, ErrorState.

**Data / backend actions:** `Test.title`, `Test.topic`, `Test.durationMinutes`, `Question.text`, `Question.options`, `Question.topic`, `Question.difficulty`, `TestAttempt.answers`, `TestAttempt.timePerQuestion`, `TestAttempt.tabSwitchCount`, `TestAttempt.submittedAt`. Never expose `Question.correctIndex` before submission. `API: see API_CONTRACT` for assigned test list, start test with shuffled questions, save/submit answers and optional Focus Guard tab-switch event.

**States**
- Loading: `Preparing your test and randomizing questions…`.
- Empty: `No assigned tests are waiting. Return to Mission Control or check with your trainer.`
- Error: network error with retry; retain locally selected answers while possible.
- Success: submitted/auto-submitted state with disabled answers and route to S4.

**Navigation:** S3 → S4 after submit; S3 → S2 via navigation only before an attempt starts or after confirming exit.

**Memorable visual moment:** The countdown resembles a launch timer: large mono numerals, tick marks and a precise progress strip—not a generic quiz card.

## S4 — Debrief

**Purpose / user goal:** Understand the test result, topic weaknesses and performance compared with the batch.

**Layout, top to bottom**
- PageHeader: `DEBRIEF // TEST ATTEMPT`, test name and submission timestamp.
- Top row: paper score card with score and accuracy; adjacent batch comparison card labelled `YOUR ORBIT / BATCH ORBIT`.
- Middle: topic accuracy bars for each topic, time-per-question list and a `Weak areas to revisit` paper card.
- Lower: question review list showing chosen answer and correct answer after submission. Use `Question.correctIndex` only in this post-submit view.
- Main CTA: `Return to Mission Control`.

**Exact sample copy/data**
- `SQL Fundamentals Check`
- Score: `72 / 100`; accuracy `9 / 12`; batch average `68`.
- Topic rows: `SQL Basics — 83%`; `Joins — 50%`; `Aggregation — 67%`.
- Time note: `Question 04 took 01:42 — slower than your median of 00:38.`
- Weak-area recommendation: `Review SQL joins, then retry a short practice set.`
- Status stamp: `DEBRIEF COMPLETE`.

**Components:** TelemetryBar, Navbar, PageHeader, BriefingCard, PanelCard, GaugeRadial, SegmentedBar, TopicAccuracy, DataTable, QuestionOption, StatusStamp, Button, EmptyState, ErrorState.

**Data / backend actions:** `TestAttempt.userId`, `TestAttempt.testId`, `TestAttempt.answers`, `TestAttempt.timePerQuestion`, `TestAttempt.score`, `TestAttempt.topicAccuracy`, `TestAttempt.submittedAt`; `Test.title`, `Test.topic`; batch average returned by backend. `API: see API_CONTRACT` for attempt report and batch average.

**States**
- Loading: `Calculating topic accuracy and batch comparison…`.
- Empty: `No completed attempt selected. Choose a completed test from Mission Control.`
- Error: show attempt result if available, but state that batch comparison could not load.
- Success: all charts have text values and a clear next action.

**Navigation:** S4 → S2. The page can link to S3 only if the product later supports retakes; do not invent a retake feature now.

**Memorable visual moment:** Two clearly labelled “orbits” compare personal accuracy and batch average, while a single amber marker identifies the largest gap.

## S5 — Interview Room (wow page)

**Purpose / user goal:** Run an adaptive text mock interview based on HR, Technical or Behavioral round; optionally target Resume Lab gaps; then inspect the Interview Report.

**Layout, top to bottom**
- Setup state: PageHeader `INTERVIEW ROOM`; InterviewRoundSelector cards for `HR`, `Technical`, `Behavioral`; toggle/checkbox `Base questions on my resume gaps` when a ResumeReport exists; display focus keywords.
- Active interview desktop: main chat panel around 2/3 width and right-side `SESSION TELEMETRY` panel with round, question count, focus keywords and elapsed time. Mobile stacks chat first and keeps the answer form anchored at the bottom without covering the latest message.
- Chat uses speaker labels `APOGEE INTERVIEWER` and `AARAV SHARMA`; messages are rectangular, not bubbles with large rounded corners. A clear typing/generating state appears while the next question is prepared.
- Answer form: multiline text area and `Send answer`; separate `End interview` secondary action with confirmation modal.
- Report state within the same page: score four skills out of 10, at least two strengths, two weaknesses and a comment per answer; include `Interview Report` heading and a `Return to Mission Control` action.

**Exact sample copy/data**
- Setup helper: `Choose a round. Apogee will ask 4–5 questions and follow up on your answers.`
- Round: `TECHNICAL`
- Focus keywords from ResumeReport: `Docker`, `REST API`, `SQL joins`
- Interviewer: `Tell me about a project where you used Docker. What problem did it solve?`
- Student answer: `I used Docker once.`
- Adaptive follow-up: `What was the container running, and how did you start it?`
- Status: `FOLLOW-UP GENERATED FROM YOUR ANSWER`
- Report skills: `Communication 6/10`; `Technical Depth 4/10`; `Problem Solving 5/10`; `Structure of Answers 5/10`.
- Strengths: `You stayed on the question`; `You identified a relevant tool.`
- Weaknesses: `Explain what the container ran`; `Describe the outcome with a concrete example.`
- Fallback badge if needed: `BASIC MODE — using the practice question bank`.

**Components:** TelemetryBar, Navbar, PageHeader, InterviewRoundSelector, PanelCard, BriefingCard, ChatMessage, FormField, Button, StatusStamp, SegmentedBar, Modal, Toast, OrbitLoader, ErrorState.

**Data / backend actions:** `InterviewSession.userId`, `InterviewSession.round`, `InterviewSession.messages`, `InterviewSession.report`, `InterviewSession.focusKeywords`, `InterviewSession.createdAt`; optional `ResumeReport.missingKeywords`, `ResumeReport.matchedKeywords`. `API: see API_CONTRACT` for create session, next question/follow-up, end session/report, and readiness score update.

**States**
- Loading: `Preparing your interview brief…`; while waiting for a response, `Reviewing your answer for a useful follow-up…`.
- Empty: setup screen before a round is selected.
- Error: AI outage switches to seeded question-bank fallback and shows `BASIC MODE`; if the backend itself is unreachable, keep the draft answer visible and offer retry.
- Success: after 4–5 questions, report includes four skill scores, at least two strengths, two weaknesses and a comment per answer.

**Navigation:** S5 → S6 to inspect/fix resume gaps; S5 → S2 after report. Start from S6 via `Interview me on these gaps`, preselect Technical and pass focus keywords.

**Memorable visual moment:** The interviewer follow-up visibly refers to the student's own sentence. The side telemetry panel connects those exact gaps to the final skill report.

## S6 — Resume Lab

**Purpose / user goal:** Upload a text-based PDF resume, optionally paste a job description, and get specific ATS-style feedback and line-level rewrites. The Resume Builder tab appears only when F8 is implemented.

**Layout, top to bottom**
- PageHeader `RESUME LAB`, subtitle `A precise review of your resume against the role you want.`
- Input state: left/upper paper `Resume intake` card with PDF dropzone; job description text area labelled `Optional job description`; one primary CTA `Analyze resume`.
- Result state: large ATS score gauge with `BASIC MODE` stamp when AI fallback was used; matched and missing keyword groups; section feedback for Education, Skills, Projects and Experience; ResumeLineDiff cards with original text, suggested rewrite and a short reason.
- CTA beside missing keywords: `Interview me on these gaps` routes to S5 with the focus keywords.
- Builder tab, only when F8 exists: form and two-template preview (`Template A`, `Template B`) with `Download PDF`. Do not display a dead tab during the MUST-only build.

**Exact sample copy/data**
- Job target: `Backend Intern at NovaPay`
- ATS score: `61 / 100`
- Missing keywords: `REST API`, `Docker`, `SQL joins`
- Matched keywords: `Python`, `Git`, `Data Structures`
- Section feedback: `Education — clear degree and graduation date`; `Skills — add role-specific backend tools`; `Projects — describe the result, not just the task`; `Experience — add measurable outcomes where accurate`.
- Original line: `Worked on backend APIs for college project.`
- Suggested rewrite: `Built and tested backend API endpoints for a college project; add the actual framework, scope and measured outcome if available.`
- Basic-mode note: `Basic mode: rules-based checks are available; AI rewrite suggestions may be limited.`

**Components:** TelemetryBar, Navbar, PageHeader, BriefingCard, PanelCard, ResumeDropzone, FormField, Button, GaugeRadial, KeywordTag, SegmentedBar, StatusStamp, ResumeLineDiff, Modal, Toast, OrbitLoader, EmptyState, ErrorState.

**Data / backend actions:** `ResumeReport.userId`, `ResumeReport.resumeText` (never expose in logs), `ResumeReport.jobDescription`, `ResumeReport.atsScore`, `ResumeReport.sectionFeedback`, `ResumeReport.missingKeywords`, `ResumeReport.matchedKeywords`, `ResumeReport.lineSuggestions`, `ResumeReport.createdAt`. `API: see API_CONTRACT` for PDF upload/analyze, latest report, and optional builder export. Use multipart form upload; the AI key stays on the backend.

**States**
- Loading: `Reading your PDF and checking role keywords…`; allow for slow first request.
- Empty: no file selected; explain `PDF only · text-based PDFs · add a job description for keyword matching`.
- Error: wrong file type, unreadable PDF, upload failure; preserve pasted job description and offer retry.
- Success: score, four section feedback areas, keyword match/miss lists and at least one real-line suggestion. If AI fails, show rules-based score with `BASIC MODE`.

**Navigation:** S6 → S5 with focus keywords; S6 → S2. Optional Builder tab stays inside S6.

**Memorable visual moment:** The original resume line and stronger rewrite are shown as a marked-up mission document, with missing keywords stamped in signal orange.

## S7 — Code Lab

**Purpose / user goal:** Choose a seeded coding problem, write code in Python, Java, C++ or JavaScript, run with custom input and submit against hidden test cases.

**Layout, top to bottom**
- PageHeader `CODE LAB`, subtitle `Write, run and verify a solution in a controlled environment.`
- Desktop three-column workbench: left problem list; center editor and language selector; right input/output and test results. On mobile, use tabs `Problem`, `Editor`, `Output` and keep `Run code` available without horizontal scrolling.
- Problem header shows difficulty tag and statement. Editor uses a dark panel and mono text; don't try to recreate every VS Code feature.
- Controls: `Run code` (secondary) and one primary `Submit solution`.
- Results panel lists `TEST 01`, `TEST 02` etc. with pass/fail, runtime in milliseconds and a plain-language error when the runner is unavailable.

**Exact sample copy/data**
- Problem: `Two Sum`
- Difficulty: `EASY`
- Statement: `Given an array of integers and a target, return the indices of two numbers that add up to the target.`
- Sample input: `nums = [2, 7, 11, 15], target = 9`
- Sample output: `[0, 1]`
- Language: `Python`
- Demo result: `4 / 5 tests passed · 18 ms`
- Runner fallback: `The code runner is unavailable. You can inspect the seeded demo result, or try again shortly.`

**Components:** TelemetryBar, Navbar, PageHeader, PanelCard, BriefingCard, StatusStamp, FormField, Button, CodeEditorPanel, SegmentedBar, DataTable, Toast, OrbitLoader, EmptyState, ErrorState.

**Data / backend actions:** `CodingProblem.title`, `CodingProblem.statement`, `CodingProblem.difficulty`, `CodingProblem.sampleInput`, `CodingProblem.sampleOutput`, `CodeSubmission.userId`, `CodeSubmission.problemId`, `CodeSubmission.language`, `CodeSubmission.code`, `CodeSubmission.testsPassed`, `CodeSubmission.testsTotal`, `CodeSubmission.runtimeMs`, `CodeSubmission.submittedAt`. `API: see API_CONTRACT` for seeded problems, run code, submit solution and submission history. User code must be sent to the hosted code-runner through the backend; never execute arbitrary code in the frontend or the app server.

**States**
- Loading: `Loading the problem set…` and `Starting the code runner…`.
- Empty: `No practice problems are available yet. Try again after the problem set is seeded.`
- Error: show compiler/runtime errors as readable text; runner outage offers the demo result as a clearly labelled fallback.
- Success: pass/fail by hidden test case, total and runtime.

**Navigation:** S7 → S2. Do not add a separate route for each problem.

**Memorable visual moment:** A compact flight-console workbench with crisp editor boundaries and test-case status stamps—not a generic coding-site clone.

# 6. STITCH PROMPTS

Every prompt below repeats the design direction because Stitch does not reliably remember prior prompts. Generate the Style Seed first and attach its screenshot as a visual reference when possible. Use the same 8 page IDs and names throughout.

## STITCH PROMPT 0 — STYLE SEED

```text
Design one responsive style-guide / component-sheet screen for Apogee, “Mission control for your placement journey,” a placement-training web app for college students, trainers and placement admins.

STYLE: “ANALOG MISSION CONTROL.” Retro-futuristic space-agency flight-ops room, printed mission paper, stamped labels, analog gauges, phosphor displays, orbit diagrams and registration marks. Do NOT use neon purple galaxies, generic glassmorphism, stock astronauts or stock planet illustrations. Palette must be exact: ink #0E1116 (main dark), panel #161B22 (raised dark), paper #F2EBDD (warm paper cards), signal #FF5A1F (primary action only), phosphor #3DFFA2 (live/OK only), amber #FFB547 (warning), steel #8B98A9 (muted text/borders), ice #BFE3FF (rare information accent). Fonts: Space Grotesk headings, Inter body, JetBrains Mono uppercase data labels with wide letter spacing. Sharp 2–4px corners, 1px borders, hard offset shadows. Use faint grain/scanlines on dark surfaces, thin concentric orbit lines, 1px crosshair/registration marks in card corners, slightly rotated status stamps, and a top telemetry bar with UTC clock, status dot and “APOGEE”. One primary orange CTA per screen.

Show a polished component sheet, not a marketing landing page:
1. Top telemetry bar: “APOGEE”, “UTC // 14:32:08”, green dot “SYSTEMS NOMINAL”, workspace “STUDENT FLIGHT DECK”.
2. Palette swatches with exact names and hex values.
3. Typography samples: display heading, h1, body copy, mono label “MISSION ID // 0042”, metric “54 / 100”.
4. Buttons: primary “Analyze resume”, secondary “View debrief”, disabled “Submit test”.
5. Warm BriefingCard with corner registration marks and a Launch Readiness Score of 54/100.
6. Dark PanelCard with status stamp “PRE-LAUNCH”.
7. StatusStamp examples “NOMINAL”, “ATTENTION”, “BASIC MODE”.
8. Instrument GaugeRadial showing 54, tick marks and label “LAUNCH READINESS”.
9. SegmentedBar at 6 of 10.
10. Form field with label “Email address”, helper text and visible focus treatment.
11. DataTable sample row “Aarav Sharma | CSE-A 2027 | 54”.
12. OrbitLoader and EmptyState examples.
Keep text legible and spacing disciplined. The screen must communicate a reusable design system with real Apogee terminology. No lorem ipsum.
```

## STITCH PROMPT — S1 Launch Gate

```text
Design a responsive web screen for Apogee, a placement-preparation platform where students improve a Launch Readiness Score and trainers monitor progress.

STYLE: “ANALOG MISSION CONTROL.” Retro-futuristic flight-ops room; printed mission paper, analog gauges, phosphor displays, orbit lines and registration marks. No neon purple galaxy, glassmorphism, stock astronauts or stock planet illustrations. Exact palette: ink #0E1116, panel #161B22, paper #F2EBDD, signal #FF5A1F, phosphor #3DFFA2, amber #FFB547, steel #8B98A9, ice #BFE3FF. Space Grotesk headings, Inter body, JetBrains Mono uppercase micro-labels with wide tracking. Sharp 2–4px corners, 1px borders, hard offset shadows, faint dark scanline grain, crosshair card corners, thin concentric orbit arcs, slightly rotated status stamps, top telemetry bar with UTC clock, status dot and project name. Orange is only the primary CTA; green means live/OK.

Layout:
- Telemetry bar: apogee orbit-ring wordmark, “UTC // 14:32:08”, green dot “SYSTEMS NOMINAL”, “PUBLIC ACCESS”.
- Desktop two columns; left warm paper briefing panel, right dark access panel. Mobile stacks compact brand then access form.
- Left panel headline: “Your next placement starts with a systems check.” Body: “Prepare with a clearer picture of your skills. Analyze your resume, practice interviews and tests, then track your Launch Readiness Score.” Small stamp “PLACEMENT TRAINING // ONLINE”.
- Right panel tabs “LOG IN” and “SIGN UP”. Log in fields “Email address” and “Password”; primary button “Log in to Apogee”. Sign-up state adds “Full name”, “Email address”, “Password”, “Role” selector with Student and Trainer. Do not offer Admin self-registration.
- Micro-label: “SESSION TOKEN ISSUED AFTER AUTHENTICATION”.
- Show visible invalid-password state with message “Access not cleared. Check your email and password, then try again.” Also show a subtle loading state “Verifying credentials…”.
- Footer: “APOGEE // PLACEMENT OPERATIONS” and “DEMO ENVIRONMENT”.
Use believable, concise content, strong contrast and accessible field labels. Do not invent extra pages. Keep consistent with the previous screens: same top telemetry bar, same navigation, same colour tokens, same fonts.
```

## STITCH PROMPT — S2 Mission Control

```text
Design a responsive web screen for Apogee, “Mission control for your placement journey,” showing the student dashboard and Launch Readiness Score.

STYLE: “ANALOG MISSION CONTROL.” Retro-futuristic flight-ops room with printed mission paper, analog gauges, phosphor displays, orbit diagrams and registration marks. No neon purple galaxy, glassmorphism, stock astronauts or stock planet illustrations. Exact palette: ink #0E1116, panel #161B22, paper #F2EBDD, signal #FF5A1F, phosphor #3DFFA2, amber #FFB547, steel #8B98A9, ice #BFE3FF. Space Grotesk headings, Inter body, JetBrains Mono uppercase micro-labels. Sharp 2–4px corners, 1px borders, hard offset shadows, faint scanline texture, corner crosshairs, orbit-line dividers, angled status stamps and top telemetry bar with UTC clock, status dot and “APOGEE”. Orange only for the main CTA; green only for live/OK.

Layout:
- Top telemetry: “APOGEE”, “UTC // 14:32:08”, green dot “SYSTEMS NOMINAL”, workspace “STUDENT FLIGHT DECK”.
- Left desktop nav: Mission Control, Test Arena, Interview Room, Resume Lab, Code Lab. Mobile uses compact menu and bottom shortcuts.
- Page header “MISSION CONTROL”; brief “Mission brief: close the largest skill gap before your next placement drive.”
- Main row: warm paper launch gauge card “LAUNCH READINESS SCORE” with large “54 / 100”, stamp “PRE-LAUNCH”, note “Based on 2 of 4 areas”. Next to it dark panel “RECOMMENDED NEXT ACTION” with copy “Compare your resume with the Backend Intern role at NovaPay.” and primary CTA “Open Resume Lab”.
- Assigned tests list: “SQL Fundamentals Check” / SQL / 20 min / “DUE”; “Data Structures Sprint” / DSA / 15 min / “COMPLETED”.
- Streak panel: “3 DAYS IN ORBIT”, “240 POINTS”, level “CADET”.
- Recent activity: “Resume analysis not yet recorded”; “Last test: Data Structures Sprint · 72%”.
- Leaderboard preview: “CSE-A 2027”, “Your rank: 8 / 12”.
- Lower tabs/sections “STUDY PLAN” and “STUDY LIBRARY” should appear only as clearly labelled future sections or populated sections when built, never as fake working controls.
Show loading skeletons and an empty assigned-tests state in a small state sample. Keep the gauge instrument-like with tick marks and a precise pointer, not a generic donut. Keep consistent with the previous screens: same top telemetry bar, same navigation, same colour tokens, same fonts.
```

## STITCH PROMPT — S8 Command Center

```text
Design a responsive web screen for Apogee, a placement-training command center used by trainers and placement admins to create tests and monitor students.

STYLE: “ANALOG MISSION CONTROL.” Retro-futuristic space-agency flight-ops room, printed mission paper, stamped labels, analog gauges, phosphor displays, orbit diagrams and registration marks. No neon purple galaxy, glassmorphism, stock astronauts or stock planet illustrations. Exact palette: ink #0E1116, panel #161B22, paper #F2EBDD, signal #FF5A1F, phosphor #3DFFA2, amber #FFB547, steel #8B98A9, ice #BFE3FF. Space Grotesk headings, Inter body, JetBrains Mono uppercase micro-labels. Sharp 2–4px corners, 1px borders, hard offset shadows, faint scanlines, registration marks, thin orbit dividers, angled status stamps, top telemetry bar with UTC clock, status dot and project name. One primary orange CTA per screen; green only for live/OK.

Layout:
- Telemetry bar: “APOGEE”, “UTC // 14:32:08”, green dot “SYSTEMS NOMINAL”, workspace “COMMAND CENTER”.
- Desktop left rail; mobile compact navigation. Header “COMMAND CENTER”, subtitle “Crew status, assessment readiness and batch-level gaps.” User label “MS. PRIYA NAIR // TRAINER CONSOLE”.
- Tabs “TESTS”, “BATCHES”, “STUDENTS”.
- Metrics: “12 STUDENTS”, “58 AVG READINESS”, “3 BELOW THRESHOLD”, “4 TESTS ASSIGNED”.
- Main split: large “CREW ROSTER” table and “BATCH WEAK TOPICS” bars. Row: “Aarav Sharma | CSE-A 2027 | 61 | Docker / Containers, SQL Joins | Today”. Topic counts: “Docker / Containers — 7 students”, “SQL Joins — 6 students”, “REST API Design — 4 students”.
- Tests tab form sample: “Backend Readiness Check”, topic “Backend”, duration “25 minutes”; CSV upload result “22 questions added · 2 rows rejected. Review the rejected rows before assigning.” Batch selector “CSE-A 2027”, action “Assign test”.
- Batches tab shows batch name/year/trainer and Admin-only “Create batch”. Students tab includes Admin-only “Add user”.
- Header action “Export readiness CSV”. Show a compact error state “Roster could not sync. Retry loading the crew roster.”
Do not cram every tab into one screen; show a clear active Tests tab with enough roster context to show the purpose. Dense data must remain readable. Keep consistent with the previous screens: same top telemetry bar, same navigation, same colour tokens, same fonts.
```

## STITCH PROMPT — S3 Test Arena

```text
Design a responsive web screen for Apogee, where college students take timed multiple-choice placement tests and submit their answers.

STYLE: “ANALOG MISSION CONTROL.” Retro-futuristic flight-ops console with printed mission paper, analog gauges, phosphor displays, orbit diagrams and registration marks. No neon purple galaxy, glassmorphism, stock astronauts or stock planet illustrations. Exact palette: ink #0E1116, panel #161B22, paper #F2EBDD, signal #FF5A1F, phosphor #3DFFA2, amber #FFB547, steel #8B98A9, ice #BFE3FF. Space Grotesk headings, Inter body, JetBrains Mono uppercase labels. Sharp 2–4px corners, 1px borders, hard offset shadows, faint scanlines, crosshair corners, orbit dividers, angled stamps and telemetry bar with UTC clock, status dot and “APOGEE”. Signal orange only for the primary action; green only for live/OK.

Show the active test state:
- Telemetry bar and student navigation; page header “TEST ARENA”.
- Test header “SQL Fundamentals Check”, “20 MINUTES”, “12 QUESTIONS”, topic “SQL”.
- Launch-countdown header with large mono “18:42” and label “TIME REMAINING”, segmented progress “QUESTION 01 / 12”, stamp “IN PROGRESS”.
- Warm paper question card: “Which SQL clause filters grouped rows after aggregation?”
- Four rectangular answer rows: “A. WHERE”, “B. ORDER BY”, “C. HAVING”, “D. DISTINCT”. Show option C selected in the visual sample, with clear outline and accessible selected state.
- Desktop right panel “QUESTION PALETTE” with numbered squares and answered/unanswered/current states; mobile use a compact collapsible strip.
- Bottom actions “Previous”, “Next”, and primary “Submit test”. Include a confirmation modal state: “3 questions are unanswered. Submit anyway?”.
- Small notice: “Answers are saved as you progress.” Include a subtle Focus Guard warning example: “Tab switch detected. Stay on this test to avoid recording more interruptions.”
Keep the countdown like an instrument, not a generic progress bar. Keep consistent with the previous screens: same top telemetry bar, same navigation, same colour tokens, same fonts.
```

## STITCH PROMPT — S4 Debrief

```text
Design a responsive web screen for Apogee, showing the result and topic analysis after a student submits a timed placement test.

STYLE: “ANALOG MISSION CONTROL.” Retro-futuristic flight-ops room, printed mission paper, analog gauges, phosphor displays, orbit diagrams and registration marks. No neon purple galaxy, glassmorphism, stock astronauts or stock planet illustrations. Exact palette: ink #0E1116, panel #161B22, paper #F2EBDD, signal #FF5A1F, phosphor #3DFFA2, amber #FFB547, steel #8B98A9, ice #BFE3FF. Space Grotesk headings, Inter body, JetBrains Mono uppercase labels. Sharp 2–4px corners, 1px borders, hard offset shadows, faint dark scanlines, crosshair corners, orbit-line dividers, angled status stamps and telemetry bar with UTC clock, status dot and “APOGEE”. Orange is reserved for the main CTA; amber marks caution.

Layout:
- Telemetry bar and student nav; page header “DEBRIEF // TEST ATTEMPT”, test “SQL Fundamentals Check”, stamp “DEBRIEF COMPLETE”.
- Top paper result card: “72 / 100”, “9 / 12 correct”, accuracy gauge.
- Comparison card “YOUR ORBIT / BATCH ORBIT”: “Your score 72” and “Batch average 68”, clearly labelled.
- Topic bars: “SQL Basics — 83%”, “Joins — 50%”, “Aggregation — 67%”. Highlight Joins with an amber marker and text “WEAK AREA”.
- Timing panel: “Question 04 took 01:42 — slower than your median of 00:38.”
- Paper recommendation card: “Review SQL joins, then retry a short practice set.”
- Below, question review rows with chosen answer and correct answer visible only after submission.
- Main CTA “Return to Mission Control”.
Show loading state “Calculating topic accuracy and batch comparison…” and an error state “Your score loaded, but the batch comparison is unavailable.” Keep charts instrument-like and label all values. Keep consistent with the previous screens: same top telemetry bar, same navigation, same colour tokens, same fonts.
```

## STITCH PROMPT — S5 Interview Room (WOW PAGE)

```text
Design a responsive web screen for Apogee, an adaptive text-based mock interviewer that asks follow-up questions based on a student's own answers and resume gaps.

STYLE: “ANALOG MISSION CONTROL.” Retro-futuristic flight-ops room with printed mission paper, stamped labels, analog gauges, phosphor displays, orbit diagrams and registration marks. No neon purple galaxy, glassmorphism, stock astronauts or stock planet illustrations. Exact palette: ink #0E1116, panel #161B22, paper #F2EBDD, signal #FF5A1F, phosphor #3DFFA2, amber #FFB547, steel #8B98A9, ice #BFE3FF. Space Grotesk headings, Inter body, JetBrains Mono uppercase micro-labels. Sharp 2–4px corners, 1px borders, hard offset shadows, faint scanlines, crosshair corners, thin orbit dividers, angled status stamps and top telemetry bar with UTC clock, status dot and “APOGEE”. One primary orange CTA; green only for live/OK.

Design the active Technical interview state, with a small setup strip:
- Telemetry bar; student nav; header “INTERVIEW ROOM”; subtitle “Technical round // adaptive follow-ups enabled”.
- Setup summary: selected round “TECHNICAL”; focus keywords stamped “Docker”, “REST API”, “SQL JOINS”.
- Desktop main chat panel about two-thirds width and right “SESSION TELEMETRY” panel; on mobile put chat first and keep answer input anchored safely at the bottom.
- Chat messages are sharp rectangular blocks with speaker labels, not rounded chat bubbles. First interviewer message: “Tell me about a project where you used Docker. What problem did it solve?” Student response: “I used Docker once.” Follow-up from interviewer, visually emphasized with a signal-orange left rule: “What was the container running, and how did you start it?” Add micro-label “FOLLOW-UP GENERATED FROM YOUR ANSWER”.
- Session telemetry: “ROUND // TECHNICAL”, “QUESTION 02 / 05”, “FOCUS // DOCKER”, “STATUS: WAITING FOR RESPONSE”.
- Answer textarea placeholder “Write your answer…”. Secondary “End interview” action opens confirmation modal. Primary “Send answer”.
- Include a visible typing state “Reviewing your answer for a useful follow-up…” and a fallback badge “BASIC MODE — using the practice question bank”.
- Also show a compact Interview Report preview state below or as an adjacent alternate state: “Communication 6/10”, “Technical Depth 4/10”, “Problem Solving 5/10”, “Structure of Answers 5/10”; strengths “You stayed on the question” and “You identified a relevant tool”; weaknesses “Explain what the container ran” and “Describe the outcome with a concrete example”.
The aha moment is the follow-up clearly reacting to “I used Docker once.” Prioritize legibility and real chat content over decoration. Keep consistent with the previous screens: same top telemetry bar, same navigation, same colour tokens, same fonts.
```

## STITCH PROMPT — S6 Resume Lab

```text
Design a responsive web screen for Apogee, where students upload a resume PDF and receive ATS-style scoring, missing keywords, section feedback and line-level rewrites for a target role.

STYLE: “ANALOG MISSION CONTROL.” Retro-futuristic flight-ops room, printed mission paper, analog gauges, phosphor displays, orbit diagrams and registration marks. No neon purple galaxy, glassmorphism, stock astronauts or stock planet illustrations. Exact palette: ink #0E1116, panel #161B22, paper #F2EBDD, signal #FF5A1F, phosphor #3DFFA2, amber #FFB547, steel #8B98A9, ice #BFE3FF. Space Grotesk headings, Inter body, JetBrains Mono uppercase labels. Sharp 2–4px corners, 1px borders, hard offset shadows, faint scanlines, crosshair corners, thin orbit-line dividers, angled stamps and telemetry bar with UTC clock, status dot and “APOGEE”. Signal orange for primary CTA; green only for healthy states.

Layout:
- Telemetry bar and student nav; header “RESUME LAB”, subtitle “A precise review of your resume against the role you want.”
- Intake card: PDF dropzone labelled “Upload resume PDF”; helper “PDF only · text-based PDFs · add a job description for keyword matching”. Job description textarea labelled “Optional job description”, sample target “Backend Intern at NovaPay”. Primary CTA “Analyze resume”.
- Results area: paper gauge card “ATS SCORE 61 / 100”; stamp “BASIC MODE” if rules-only fallback is active.
- Keyword panels: missing “REST API”, “Docker”, “SQL joins”; matched “Python”, “Git”, “Data Structures”.
- Section feedback rows: “Education — clear degree and graduation date”; “Skills — add role-specific backend tools”; “Projects — describe the result, not just the task”; “Experience — add measurable outcomes where accurate”.
- Resume line comparison: original “Worked on backend APIs for college project.” Suggested rewrite “Built and tested backend API endpoints for a college project; add the actual framework, scope and measured outcome if available.” Label the original and suggestion distinctly; never imply invented outcomes are facts.
- Primary action after results “Interview me on these gaps”, sending focus keywords to Interview Room.
- If the optional Resume Builder is implemented, show “ANALYZE” and “BUILDER” tabs; otherwise do not show a dead Builder tab.
Show loading “Reading your PDF and checking role keywords…”, invalid-file error “Upload a text-based PDF to continue.” and fallback note “Basic mode: rules-based checks are available; AI rewrite suggestions may be limited.” Keep consistent with the previous screens: same top telemetry bar, same navigation, same colour tokens, same fonts.
```

## STITCH PROMPT — S7 Code Lab

```text
Design a responsive web screen for Apogee, a placement-preparation Code Lab where students solve seeded problems in Python, Java, C++ or JavaScript.

STYLE: “ANALOG MISSION CONTROL.” Retro-futuristic flight-ops console, printed mission paper, analog gauges, phosphor displays, orbit diagrams and registration marks. No neon purple galaxy, glassmorphism, stock astronauts or stock planet illustrations. Exact palette: ink #0E1116, panel #161B22, paper #F2EBDD, signal #FF5A1F, phosphor #3DFFA2, amber #FFB547, steel #8B98A9, ice #BFE3FF. Space Grotesk headings, Inter body, JetBrains Mono uppercase labels. Sharp 2–4px corners, 1px borders, hard offset shadows, faint scanlines, corner crosshairs, thin orbit dividers, angled stamps and telemetry bar with UTC clock, status dot and “APOGEE”. One primary orange CTA; green only for successful/live status.

Layout:
- Telemetry bar and student navigation; header “CODE LAB”, subtitle “Write, run and verify a solution in a controlled environment.”
- Desktop three-panel workbench: problem list on left; code editor center; custom input/output and test results on right. Mobile uses tabs “PROBLEM”, “EDITOR”, “OUTPUT” with no horizontal scrolling.
- Selected problem: “Two Sum”, difficulty “EASY”. Statement: “Given an array of integers and a target, return the indices of two numbers that add up to the target.” Sample input “nums = [2, 7, 11, 15], target = 9”; sample output “[0, 1]”.
- Editor language selector “Python”; code text should look like a compact editor with line numbers, not a full IDE clone.
- Input panel with editable custom input; output panel with “Run output appears here”.
- Buttons “Run code” and primary “Submit solution”.
- Result state: “4 / 5 tests passed · 18 ms”, test rows “TEST 01 PASS”, “TEST 02 PASS”, “TEST 03 PASS”, “TEST 04 PASS”, “TEST 05 FAIL”.
- Runner outage state: “The code runner is unavailable. You can inspect the seeded demo result, or try again shortly.”
Show a loading label “Starting the code runner…” and clear runtime/compiler errors. Keep consistent with the previous screens: same top telemetry bar, same navigation, same colour tokens, same fonts.
```

## Mobile variant prompt — S2 Mission Control

```text
Design a mobile-first 375px-wide screen for Apogee Mission Control, the student dashboard. STYLE: ANALOG MISSION CONTROL: ink #0E1116, panel #161B22, paper #F2EBDD, signal #FF5A1F, phosphor #3DFFA2, amber #FFB547, steel #8B98A9, ice #BFE3FF; Space Grotesk headings, Inter body, JetBrains Mono uppercase labels. Sharp 2–4px corners, 1px borders, hard shadows, faint scanlines, corner registration marks, thin orbit arcs, angled status stamps and a top telemetry bar with UTC clock, status dot and “APOGEE”. No purple galaxy, glassmorphism or stock space art. Stack all cards, no horizontal overflow. Show a compact menu and bottom shortcuts. First: “LAUNCH READINESS SCORE 54 / 100” in a paper instrument card with tick-mark radial gauge and “PRE-LAUNCH” stamp. Second: “RECOMMENDED NEXT ACTION” with “Compare your resume with the Backend Intern role at NovaPay” and primary “Open Resume Lab”. Then “SQL Fundamentals Check · SQL · 20 min · DUE”, “3 DAYS IN ORBIT”, “240 POINTS”, and “CSE-A 2027 · Your rank 8 / 12”. Use readable 16px body text and 44px touch targets. Keep consistent with the previous screens: same top telemetry bar, same navigation, same colour tokens, same fonts.
```

## Mobile variant prompt — S5 Interview Room

```text
Design a mobile-first 375px-wide screen for Apogee Interview Room, an adaptive text-based mock interview. STYLE: ANALOG MISSION CONTROL: ink #0E1116, panel #161B22, paper #F2EBDD, signal #FF5A1F, phosphor #3DFFA2, amber #FFB547, steel #8B98A9, ice #BFE3FF; Space Grotesk headings, Inter body, JetBrains Mono uppercase labels. Sharp 2–4px corners, 1px borders, hard offset shadows, faint scanlines, crosshair marks, thin orbit lines, angled status stamps, and top telemetry bar with UTC clock, status dot and “APOGEE”. No purple galaxy, glassmorphism or stock astronauts/planets. Show header “INTERVIEW ROOM”, round “TECHNICAL”, focus tags “Docker”, “REST API”, “SQL JOINS”. Stack sharp rectangular chat messages with speaker labels. Show student message “I used Docker once.” and the emphasized adaptive follow-up “What was the container running, and how did you start it?” with label “FOLLOW-UP GENERATED FROM YOUR ANSWER”. Session status “QUESTION 02 / 05”. Keep the answer textarea and “Send answer” action visible at the bottom without covering chat; “End interview” is secondary. Include a compact fallback stamp “BASIC MODE” and an alternate report summary with four skill scores. Prioritize legibility, safe-area spacing, and 44px controls. Keep consistent with the previous screens: same top telemetry bar, same navigation, same colour tokens, same fonts.
```

## Recommended generation order

1. **Style Seed** — lock the token look and component language.
2. **S5 Interview Room** — the wow page and clearest demonstration of Apogee’s innovation.
3. **S6 Resume Lab** — it feeds the interview and establishes the paper-document result style.
4. **S2 Mission Control** — establishes the student shell and readiness gauge.
5. **S8 Command Center** — proves the student-to-trainer insight loop.
6. **S1 Launch Gate** — authentication and public entry.
7. **S3 Test Arena**, then **S4 Debrief** — the test flow and report.
8. **S7 Code Lab** — only after MUST features work.

**If Stitch drifts:** attach the Style Seed screenshot as a visual reference. If a prompt is too long, shorten secondary content but never remove the style block, exact palette, typography or layout structure. Regenerate rather than trying to repair a fundamentally off-style screen by hand. Time-box Stitch to about **3 hours** so the team has enough time to build and connect the app.

# 7. Frontend Build Phases

The PRD has four build groups. F0 is a frontend foundation phase before those groups; it does not add a page or route.

## F0 — Foundation

**Pages included:** Shared shell and route scaffolding for S1–S8; no new page beyond the PRD inventory.

**New components:** Design tokens, font loading, TelemetryBar, Navbar, Button, BriefingCard, PanelCard, StatusStamp, PageHeader, FormField, OrbitLoader, EmptyState, ErrorState, Toast, Modal, route guards and shared API client.

**Mock data needed:** Seed User records for Aarav Sharma (`student`), Ms. Priya Nair (`trainer`) and Dr. Rohan Kulkarni (`admin`); Batch `CSE-A 2027`; representative Test and Question records.

**Backend connection:** Initially use mocks. Establish the `src/api` layer and agree response shapes with the backend API_CONTRACT before integration.

**Done when**
- [ ] Tailwind v4 tokens and fonts are applied globally.
- [ ] All eight routes render inside the same shell.
- [ ] Role guard sends Student to S2 and Trainer/Admin to S8.
- [ ] Mobile menu, keyboard focus and shared error/loading states work.
- [ ] No console errors and no random colour values outside the tokens.

**What the user sees:** A consistent Apogee shell and navigable placeholder content, not a finished feature set.

## Group 1 — Foundation features: S1, S2 basic, S8

**Pages included:** S1 Launch Gate, basic S2 Mission Control, S8 Command Center.

**New components:** LaunchReadinessSummary, GaugeRadial, DataTable, BatchWeakTopics, CSV upload summary, role-aware dashboard sections.

**Mock data needed:** Aarav’s readiness score `54`, assigned tests, 12 students in `CSE-A 2027`, three weak topics and a sample test builder CSV response `22 added / 2 rejected`.

**Backend connection:** Login/session and roles, batches, test and question creation, CSV import, assignment, dashboard summary and roster. Follow Group 1 in API_CONTRACT.

**Done when**
- [ ] Student, Trainer and Admin can authenticate and land on the correct dashboard.
- [ ] Student sees saved assigned tests and readiness score.
- [ ] Trainer can create a test, import a CSV, inspect rejected rows and assign to a batch.
- [ ] Students outside the assigned batch do not see the test.
- [ ] Command Center shows a readable roster and can export CSV.
- [ ] Logout clears the session.

**What the user sees:** A working login, student home and trainer console backed by saved data.

## Group 2 — Tests: S3, S4

**Pages included:** S3 Test Arena, S4 Debrief.

**New components:** QuestionPalette, QuestionOption, countdown display, topic accuracy panel and answer review list.

**Mock data needed:** `SQL Fundamentals Check`, 12 MCQs, varied topics and difficulties, one completed `TestAttempt`, per-question timing and a batch average of `68`.

**Backend connection:** Test delivery with shuffled questions, answer submission, auto-submit-compatible attempt handling, scoring, topic analysis, batch average and Launch Readiness Score v1.

**Done when**
- [ ] Timer counts down and auto-submits at zero.
- [ ] Question order is randomized and correct answers are not exposed before submit.
- [ ] Answers and time-per-question are submitted.
- [ ] Debrief shows score, topic accuracy, question timing, weak areas and batch comparison.
- [ ] Submission recalculates readiness score and S2 reflects the server value.
- [ ] The active test works at 375px without horizontal overflow.

**What the user sees:** A timed test followed by a useful, specific performance report.

## Group 3 — AI: S5, S6

**Pages included:** S5 Interview Room, S6 Resume Lab.

**New components:** InterviewRoundSelector, ChatMessage, ResumeDropzone, KeywordTag, ResumeLineDiff and report skill-score display.

**Mock data needed:** Sample text-based resume PDF, NovaPay Backend Intern job description, ATS score `61`, missing keywords `REST API`, `Docker`, `SQL joins`, and a 4–5 question Technical interview with an adaptive Docker follow-up and report.

**Backend connection:** PDF parsing, rules-based resume scoring, AI-enhanced section feedback and rewrites, InterviewSession create/message/end/report, ResumeReport persistence and Launch Readiness Score v2. Keep the AI provider key server-side.

**Done when**
- [ ] PDF upload returns feedback for Education, Skills, Projects and Experience.
- [ ] Missing/matched keywords and at least one actual resume line with a suggested rewrite appear.
- [ ] `Interview me on these gaps` starts a Technical interview with those focus keywords.
- [ ] At least one follow-up refers to the student's real answer.
- [ ] Interview report has four skill scores, two strengths, two weaknesses and per-answer comments.
- [ ] AI outage triggers the PRD fallback and shows `BASIC MODE`.
- [ ] Readiness updates on S2 after resume analysis and interview completion.

**What the user sees:** The main wow moment: resume gaps become interview questions, then a report and updated readiness score.

## Group 4 — Extras: S7, plus S2 additions

**Pages included:** S7 Code Lab and additions to S2 for F7 Streaks & Leaderboard, F9 Study Library & Company Tracks and F10 Smart Study Plan. F11 Focus Guard appears within S3 if implemented; it is not a new page.

**New components:** CodeEditorPanel, StreakPatch, StudyModuleRow, leaderboard and study-plan panels.

**Mock data needed:** Five CodingProblem records with Easy/Medium tags, one sample CodeSubmission, top 10 students in a batch, three mission patches, six study modules and a 7-day study plan.

**Backend connection:** Hosted code-runner, CodeSubmission results, points/streaks, seeded study content, completion tracking, company-track filters and smart study plan. If code execution is not reliable, follow the PRD and cut to editor-only or a clearly labelled seeded demo result.

**Done when**
- [ ] Student can choose a problem/language, run custom input and see output/errors.
- [ ] Submitting a seeded problem shows hidden-test pass/fail and runtime, or a clearly labelled fallback.
- [ ] Test/interview completion awards points and updates streak.
- [ ] Leaderboard is limited to the top 10 in the student's batch.
- [ ] Six study modules and a seven-day plan appear only when implemented.
- [ ] Extras do not block or destabilize the F1–F5 demo.

**What the user sees:** A broader practice toolkit after the main resume-to-interview workflow already works.

# 8. From Stitch to Working Code (handoff plan)

## Beginner-friendly steps

1. **Generate screens in Stitch.** Start with Style Seed, then S5, S6, S2, S8, S1, S3, S4 and S7. Follow Stitch's current export options; save available HTML/CSS exports or screenshots into `/frontend/stitch-export/` using names such as `S1_launch-gate.html`, `S2_mission-control.html`, `S5_interview-room.html`. If Stitch only gives you a screenshot, treat it as a visual reference—not working application code.
2. **Keep exports separate from the app.** Do not paste all generated files into one React component. The exported design is a reference for spacing, colour and hierarchy; the coding agent should rebuild it in the actual project.
3. **Have the coding agent read these files first:** `/frontend/FRONTEND_DESIGN.md`, `/docs/PRD.md`, `/docs/API_CONTRACT.md`, `/frontend/package.json`, `/frontend/src/styles/*` (or the existing stylesheet), `/frontend/src/api/*`, and any existing `/frontend/src/mocks/*`. If the API contract lives at another path, use the team's actual path rather than inventing a replacement.
4. **Use this copy-paste instruction block for the coding agent:**

```text
Rebuild each exported screen as a React page using Tailwind CSS v4 and the tokens in src/styles. Extract repeated UI into the components in FRONTEND_DESIGN.md Section 4. Use src/mocks data identical to the API_CONTRACT example responses. Keep the API calls in src/api only. Do not add libraries beyond react-router-dom and framer-motion (and recharts only if the PRD needs charts). Work only in /frontend.

Read FRONTEND_DESIGN.md and PRD.md before coding. Preserve the exact page IDs and canonical names S1 Launch Gate, S2 Mission Control, S3 Test Arena, S4 Debrief, S5 Interview Room, S6 Resume Lab, S7 Code Lab, and S8 Command Center. Do not create additional routes. Use the Analog Mission Control palette exactly. Implement loading, empty, error and success states for every page. Never put the AI provider key in frontend code. Never execute student code in the browser or app server. Keep all network calls inside src/api and make mock/API switching controlled by VITE_USE_MOCKS. Do not work in /backend, /docs or /scripts.
```

## Suggested route table

| Path | Page ID | React component | Access |
|---|---|---|---|
| `/login` | S1 | `LaunchGate` | Public |
| `/mission-control` | S2 | `MissionControl` | Student |
| `/command-center` | S8 | `CommandCenter` | Trainer, Admin |
| `/test-arena` | S3 | `TestArena` | Student |
| `/debrief/:attemptId` | S4 | `Debrief` | Student |
| `/interview-room` | S5 | `InterviewRoom` | Student |
| `/resume-lab` | S6 | `ResumeLab` | Student |
| `/code-lab` | S7 | `CodeLab` | Student |

These paths are frontend suggestions because the PRD defines page IDs, not literal URL paths. Confirm them with the team before the backend integration.

## Switching from mocks to the real API

- Create or use `src/api` as the only place that knows backend URLs and HTTP details. Page components should call named functions such as `getDashboardSummary()` or `analyzeResume()` rather than using `fetch()` directly.
- Keep `src/mocks` response objects aligned with the examples in `/docs/API_CONTRACT.md`. Mock responses should use the same camelCase entity fields as the backend contract.
- Use `VITE_USE_MOCKS=true` for local UI work and the seeded demo. Use `VITE_USE_MOCKS=false` when connecting to the live FastAPI backend. If the project skeleton already defines this flag, preserve its exact behaviour.
- Put the Render backend URL in a Vite environment variable such as `VITE_API_BASE_URL`; never put AI provider keys or code-runner secrets in Vite variables because frontend variables are visible to users.
- Test one flow at a time: login → dashboard, then create/assign test, then take test → debrief, then resume analysis → interview → report. Verify the returned Launch Readiness Score comes from the backend, not from a hard-coded frontend animation.

## “Waking up the server” UX

Render's free backend may sleep and take up to a minute on the first request. During a slow first response, keep the page shell visible and show an OrbitLoader with:

**Heading:** `Waking up the training server…`  
**Detail:** `The first connection can take up to a minute. Your work is safe—please keep this tab open.`

After a reasonable timeout, show a retry action and a note that the service may still be starting. Do not show a fake success state or clear a user's form while waiting.

# 9. Quality Checklist

- [ ] Responsive and usable at 375px, 768px and 1280px.
- [ ] No horizontal page scrolling at 375px; dense tables can scroll inside their own panel.
- [ ] All text and controls meet readable contrast against ink, panel and paper.
- [ ] Every interactive element has keyboard focus styling and a logical tab order.
- [ ] Touch targets are at least 44px high/wide where practical.
- [ ] Every page handles loading, empty, error and success states.
- [ ] Every error explains what happened and what the user can do next.
- [ ] AI failure uses the documented fallback; it does not strand the user.
- [ ] No correct answer is exposed before a TestAttempt is submitted.
- [ ] Resume text, passwords and tokens are not written to console logs.
- [ ] AI keys and code-runner secrets stay on the backend.
- [ ] No student code runs directly on the app server.
- [ ] Colour use comes from the defined tokens; no random colours or unapproved gradients.
- [ ] Signal orange is used sparingly, with one primary CTA per screen.
- [ ] Phosphor green means live/OK only; amber warnings have text labels.
- [ ] Motion is limited to the readiness count-up, restrained status blink, optional typewriter reveal and slow orbit; respect reduced-motion settings.
- [ ] No console errors, broken routes or dead tabs.
- [ ] Role guards stop students from opening trainer/admin pages.
- [ ] API calls are contained in `src/api`; mock data is contract-compatible.
- [ ] Student, Trainer and Admin flows are tested with seeded accounts.
- [ ] Test timer, auto-submit, PDF upload, AI fallback and mobile Interview Room are manually tested.
- [ ] Deploy frontend to Vercel and backend to Render; verify the production API URL and CORS settings.
- [ ] Warm the Render server before the demo and keep the backup recording ready.

# 10. Fallback Theme

## SOLAR FLARE BRUTALIST

Use this only if the team explicitly switches themes. Keep the same page structure, content, data fields and navigation.

| Token | Hex | Usage |
|---|---|---|
| Black | `#0A0A0A` | Main canvas and dark panels |
| Solar yellow | `#FFD400` | Main CTA, key metrics and emphasis |
| White | `#FFFFFF` | Main text and paper-like panels |
| Concrete grey | `#A7A7A7` | Secondary labels and dividers |
| Signal red | `#F04438` | Error or critical warning only |

**Five-line rule set**
1. Use a black canvas, solar-yellow primary action and high-contrast white text.
2. Use 3px borders, oversized grotesque headings and hard, obvious offset shadows.
3. Use cut-out collage shapes and abstract planet fragments—not stock space illustrations.
4. Keep cards square and layouts editorial; avoid gradients, glass effects and soft shadows.
5. Preserve clear data labels, accessible focus states and one primary CTA per screen.

**How to adjust Stitch prompts:** Replace the Analog Mission Control style paragraph in every prompt with the fallback palette and five-line rule set. Remove phosphor/amber status semantics, orbit-gauge styling and paper-card emphasis; use cut-out collage shapes and brutalist frames instead. Keep the exact Apogee page names, sample data, layouts, responsive requirements and final consistency line unchanged.
