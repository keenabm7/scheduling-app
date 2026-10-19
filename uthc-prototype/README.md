# Ulluriaq Scheduling App — Developer Handoff Package

This package contains everything needed to quote and build the Ulluriaq Adolescent Center (UTHC) scheduling application.

## How to use this package

1. **Read `FEATURE_SPEC.md` first.** It documents every rule, workflow, and permission in the app — including the ones not shown in a clickable file (see "Specced but not prototyped" below). This is the source of truth; the HTML files are illustrations of it, not a replacement for it.
2. **Open the files in `screens/` in any web browser** — just double-click, no install or server needed. Every button, tab, and modal in them is functional so you can see the intended look and interaction, not just read about it.
3. **Quote in phases.** Section 20 of the feature spec suggests a 3-phase build order (core schedules → operational logic → extended features). Please quote each phase separately so the client can decide how much to build at once.

---

## ✅ What IS in this package

### Written specification
- `FEATURE_SPEC.md` — complete behavior spec for all 20 sections: auth, schedules, dashboard, employee experience, overtime, requests/approvals, memos, staff-on-leave, messaging, mass comms, on-call, seniority, staff directory, notifications, update timing, availability sheets, visual/color reference, non-functional requirements, and suggested phasing.

### Clickable HTML prototypes (`screens/` folder)

| File | What it shows |
|---|---|
| `01-login-and-dashboard.html` | Management login, employee login, the tabbed Management Dashboard (Overview / Schedules / Staff & Access / Staff on Leave) |
| `02-employee-home-and-full-grid.html` | Employee home screen with 4 pinnable schedule tabs; full 4-week scrollable schedule grid with the entire roster, shown from both employee and management perspective (including TRAN/ESC click-to-detail and the access-denied state for non-involved employees) |
| `03-overtime-and-bookoff.html` | OT distribution queue (seniority-ordered, T/R actions), management's book-off approval queue, and the employee-facing book-off request form (24-hour cutoff, mandatory leave-type selector) |
| `04-messaging-and-switch-approval.html` | The full 3-step shift-switch flow: Employee A proposes → Employee B agrees/declines → Management approval queue → final confirmation to both parties |
| `05-memos-leave-and-access.html` | Transportation/escort memo cards, the Staff on Leave tracker (leave type, dates, progressive return), and the Staff & Access screen (suspend/terminate/reinstate) |
| `06-seniority-reorder.html` | Drag-and-drop (and arrow-button) reorderable seniority list |

That's **8 of the 8 core screen groups** described in the feature spec, each as a real, openable file.

---

## ⚠️ What is NOT fully built out — read this before quoting

These items are described in the feature spec (so the *rules* are documented) but are **not separately prototyped as their own file**, or are only partially shown:

| Item | Status |
|---|---|
| **Real 6-schedule set** | Only **Boys IA Day/Evening** is built out with the full 4-week grid + entire roster (file 02). The other 5 schedules (Boys Educators, Boys IA Overnight, Girls Educators, Girls IA Day/Evening, Girls IA Overnight) follow the *same pattern* but were not individually re-built at full roster/4-week depth in these files. Developer should treat file 02 as the template and apply it to all 6. |
| **Mass communications screen** | Described in spec §11; referenced from the dashboard quick actions in file 01, but not built as its own screen. |
| **On-call manager assignment screen** | Described in spec §12; not prototyped as a standalone screen. |
| **Availability sheet submission UI** (the employee-facing form for submitting/editing their own availability) | Described in spec §17; not prototyped. Original paper-based availability sheets are referenced in the spec appendix but the *digital submission form* itself was not mocked up. |
| **Staff directory / contact list screen** | Described in spec §14; data exists in the source documents but no standalone browsable directory screen was built (distinct from the Staff & Access screen in file 05, which focuses on status, not contact info). |
| **"Add memo" / "Add leave record" / "Add staff" forms** | These are referenced via `alert()` placeholders in the HTML files (e.g., clicking "+ New memo" shows what fields the form needs, rather than a fully laid-out form UI). The fields themselves are fully specified in the feature spec. |

### Always out of scope for an HTML mockup (genuine development work, not a prototyping gap)
- Real backend, database, and API — nothing in `screens/` is connected to data; refreshing any page resets it
- Real authentication: password hashing, session/token security, real OTP delivery via email/SMS
- Real email sending — every "email sent" message in the prototypes is a placeholder alert
- Hosting and infrastructure setup
- Data migration of real staff/schedule records into whatever database is built
- Confirming whether Quebec's Law 25 (private-sector data privacy law) applies to how staff personal and leave data is stored/handled — flag this to the client before building the Staff on Leave / personal-data features, don't assume an answer

---

## Real source data referenced in the spec

The client (Ulluriaq / UTHC) has real staff lists, seniority lists, contact directories, availability sheets, and historical schedules that were used to build these mockups. These are not included in this package but are available from the client upon request, and will be needed for actual data migration once development begins.

## Questions during quoting?

Direct technical or business-logic questions back to the client — the feature spec and prototypes together answer "how should this work" for nearly everything, but anything ambiguous (especially in the "not fully built out" list above) should be clarified with the client before a quote is finalized, not assumed.
