# UTHC Ulluriaq — Scheduling App — Developer Package

## Live Interactive Prototype
Click to open and click through the full prototype (works on phone or computer, no download needed):

**https://claude.ai/artifact/NaCK1Mj3exjsN87CGXeDd8**

## Files in this package

| File | What it is |
|---|---|
| FEATURE_SPEC.md | Complete written specification — 20 sections covering all features, rules, workflows, and permissions |
| uthc-prototype-full.html | Single-file interactive HTML prototype — open in any browser |

## For developers

1. Open the live prototype link above and click through all screens
2. Read FEATURE_SPEC.md fully — it covers every business rule and workflow
3. Provide a phased quote as described in Section 20 of the spec (Phase 1, Phase 2, Phase 3 separately)

## What the prototype covers
- Management login → tabbed dashboard (Overview, Schedules, Overtime, Book-offs, Messaging, Memos, Staff on Leave, Staff & Access, Seniority)
- Employee login → pinned schedule tabs, book-off request form, switch request, messaging, on-call manager
- Full 4-week schedule grid with TRAN/ESC access control
- OT queue with T/R actions
- Shift switch 3-step approval chain
- Seniority list drag-and-drop reorder
- Staff on leave tracker
- Staff access controls (suspend/terminate/reinstate)

## What is NOT in the prototype (but is fully specced in FEATURE_SPEC.md)
- Real backend, database, or authentication
- Real email delivery
- Mass communications screen (specced §11)
- Availability sheet digital submission form (specced §15)
- Last-minute cover logic under 2 hours (specced §3.7)
- On-call package auto-generation (specced §12)

## Technology recommendation
Build as a **Progressive Web App (PWA)** — web app accessible via browser URL, installable to phone home screen, no App Store required.
Suggested stack: Node.js backend, React frontend, PostgreSQL database.

## Privacy note
Confirm Quebec Law 25 (Loi 25) requirements with CIUSSS IT/privacy contact before building Staff on Leave and personal data features.
