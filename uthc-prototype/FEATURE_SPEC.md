# Ulluriaq Scheduling App — Feature Specification

**Prepared for:** Ulluriaq Adolescent Center (UTHC)
**Purpose:** This document, together with the included HTML prototype files, defines the complete scope for a developer or agency to quote and build the production scheduling application.

---

## 1. Overview

A web (and ideally mobile-friendly) application that replaces manual/paper scheduling for Ulluriaq's two units — **Boys** and **Girls** — each staffed by **Educators** and **Intervention Agents (IAs)** across day, evening, and overnight shifts, tracked in two-week **Pay Periods**.

There are two user roles:
- **Management & Scheduler** — full edit access to schedules, staff, approvals, and restricted information.
- **Employee** — access to their own schedule, requests, and limited information only.

There is no "Admin" role label anywhere in the product — use "Scheduling Admin," "Unit Manager," "Management & Scheduler" instead.

---

## 2. Authentication & Access

| Requirement | Detail |
|---|---|
| Separate login flows | Management/Scheduler and Employee sign in through visually distinct flows, but can link to one another. |
| Password-based login | Standard email/employee-number + password. |
| Email + OTP verification | Required **only** on first sign-in, and again automatically once every **12 months** thereafter. Not required on every login. |
| Session persistence | Sessions persist between the OTP checkpoints described above. |
| Landing page after login | **Management/Scheduler:** lands directly on the Management Dashboard (see §4). **Employee:** lands directly on their own schedule (the one they've pinned as "home" — see §5). |
| Suspend / Terminate / Reinstate | Management can change any employee's account status to Active, Suspended, or Terminated from the Staff & Access screen. Suspended/Terminated employees are immediately blocked from logging in. Reinstating restores access instantly. Each status change supports an optional internal note and effective date. Historical schedule data for the employee is retained regardless of status. |

---

## 3. Schedules (core feature)

### 3.1 Structure
Four distinct schedules, organized by unit and role:
1. Boys — Educators
2. Boys — Intervention Agents (Day/Evening)
3. Boys — Intervention Agents (Overnight)
4. Girls — Educators
5. Girls — Intervention Agents (Day/Evening)
6. Girls — Intervention Agents (Overnight)

*(Note: the employee-facing "4 schedules to switch between" referenced in conversation maps to the 4 primary grids — Boys Educators, Girls Educators, Boys IA, Girls IA — with Day/Evening and Overnight as sub-views within the IA schedules.)*

### 3.2 Time range & layout
- Each schedule displays a **full 4-week view**: the current Pay Period (Weeks 1–2) and the following Pay Period (Weeks 3–4), stacked vertically.
- Weeks 1–2 appear at the top; scrolling down reveals Weeks 3–4.
- All employees on the relevant roster appear as rows; dates as columns.
- The staff-name column should be **compact** (just enough room for name + status tag) to maximize horizontal space for the actual schedule grid.
- Sticky headers: date row and staff-name column remain visible while scrolling.

### 3.3 Shift codes
J1, J2, J/T, S1, S2, S/T, N, N/T, N/E, T, R, V, DNR, SW, OT, CNR, TRAN, ESC — each color-coded. Full list and meanings to be provided by UTHC (see source documents).

### 3.4 Cell-level functionality (Management only — editable)
Clicking any shift cell opens an edit panel allowing management to:
- Set/change the shift code
- Mark a switch (sw) or vacation (v) tag
- Mark the shift as overtime (highlights the employee's name)
- **Assign a "cover" / "fill-in" name** — the person who picked up or is covering that specific shift. This name displays directly beneath the shift code on the grid for all viewers. Options should include all UTHC staff plus an "agency staff" option (agency names marked with `*`).
- Clear the cell entirely

### 3.5 Employee names / rows (Management only — editable)
Management can edit a staff member's displayed name/sub-label on a schedule, or remove them from a given schedule, or add a new staff row to a schedule.

### 3.6 Transportation & Escort shifts
- Shown directly on the schedule grid using the `TRAN` and `ESC` codes.
- Clicking a `TRAN` or `ESC` cell opens a detail panel (linked to a "memo," see §8) showing: number of youth, destination/community, start time, end time, and any notes.
- **Visibility rule:** the detail behind a `TRAN`/`ESC` cell is visible only to (a) the employee assigned to that shift and (b) Management. Other employees see the code on the shared schedule (so they know the slot is filled) but cannot open the detail — clicking it as a non-involved employee shows an access-restricted message.

### 3.7 Loan of Service (LOS)
- **LOS does NOT appear on the shared schedule grid that all employees see.** It is not a shift code visible to the general staff.
- LOS is tracked as a **duration of stay**, not shift-by-shift: originating unit, receiving unit, departure date, expected return date, and an auto-calculated duration (days / weeks / months).
- Visible only to: (a) the employee who is on loan (who sees their own LOS info as part of their personal view) and (b) Management, via a dedicated Management-only tab/screen. It is never shown to other employees.

---

## 4. Management & Scheduler Dashboard

The dashboard is the landing page immediately after Management/Scheduler login. It is **tabbed**, all within one area:

| Tab | Contents |
|---|---|
| **Overview** | Key stats (active staff, pending book-offs, unfilled shifts, OT assigned this period), recent activity feed, quick-action shortcuts, department/unit coverage %. |
| **Schedules** | All 4 (6) schedules, switchable, fully editable per §3. |
| **Overtime** | OT distribution queue (see §6). |
| **Book-offs** | Pending/approved book-off requests with approve/deny actions. |
| **Staff & Access** | Full staff directory with search/filter, and Suspend / Terminate / Reinstate controls (see §2). |
| **Staff on leave** | Locked/marked as Management-only. See §9. |

---

## 5. Employee Experience

- After login, employees land on a schedule — **their pinned "home" schedule**.
- Employees can switch between viewing all relevant schedules via tabs, but only one is their default landing view.
- Each schedule tab has a "pin" control letting the employee designate which one loads automatically at next login.
- Employees see schedules **read-only** — they cannot edit shift codes, cover names, or other employees' rows. Clicking a cell shows shift detail and, where relevant, prompts them toward a request flow (switch, book-off) rather than direct editing.
- Employees never see: the Management Dashboard, Staff & Access controls, other staff's Loan of Service or restricted leave details, or anyone's `TRAN`/`ESC` detail except their own.

---

## 6. Overtime (OT) Distribution

- Triggered after the weekly shift-request window closes (Wed–Fri 9:00 AM cycle, per UTHC's existing process).
- Priority order, strictly enforced:
  1. Full-time employees, by seniority (most senior offered first); OT must be distributed fairly — no junior employee should accumulate more OT than a senior one.
  2. Part-time employees, by rotation/seniority (may take up to 10 shifts/period or go into overtime).
  3. Recall workers.
  4. Outsourced agency (if all above decline).
- Each offer supports two outcomes:
  - **T (Taken):** confirmation email sent to employee + management; cover name appears on schedule.
  - **R (Refused):** email sent to employee with manager copy, logged with date/time; system automatically advances to the next person in rotation.
- Management must always be able to see who was last offered/given a shift, to verify fair rotation.

---

## 7. Requests & Approvals

### 7.1 Book-off / Vacation requests (employee-submitted)
- Employee selects date(s) and a **mandatory** leave-type tag before they can submit: Sick, Vacation, Stat, Psychosocial, LIB, Maternity leave, or similar — submission is blocked until one is selected.
- **Requests submitted less than 24 hours before the shift are automatically denied** — employee sees an in-app message directing them to contact management directly; management receives a notification of the attempted late request.
- 3+ consecutive days off is automatically flagged as a vacation request requiring management approval.
- 3 consecutive weekend (Fri/Sat/Sun) book-offs in a row triggers an automatic alert to management.
- Management approves/denies from the Book-offs tab; both outcomes notify the employee via app + email.

### 7.2 Shift Switches (between two employees)
This is a **three-step approval chain**, never a two-way agreement alone:

1. **Proposal:** Employee A messages Employee B directly (see §10) and/or sends a formal switch proposal specifying: the shift Employee A gives up, the shift Employee A would take from Employee B, and the unit (same-unit or cross-unit, e.g., Boys↔Girls / "SWB"/"SWG").
2. **Counterparty agreement:** Employee B must explicitly agree (or decline) within the app. If declined, the process ends and Employee A is notified — it never reaches management.
3. **Management approval:** Once both employees have agreed, the request appears in Management's approval queue (requests pending one party's agreement are NOT visible to management yet). Management gives final approval or denial.
- **Three-way switches are never permitted** — only direct 1-to-1 swaps.
- Switches restricted to same role type: Educator↔Educator, IA↔IA.
- Every stage (proposal sent, agreement, decline, management approval/denial) triggers a notification via **both** in-app notification and email, to all relevant parties.
- Approved switches update the schedule automatically.

### 7.3 Confidentiality
Employees may never view a schedule template before it has been officially published/sent by management.

---

## 8. Memos (Transportation & Northern Escorts)

A dedicated area for Management/Scheduler to log details tied to transportation or escort shifts:

| Field | Notes |
|---|---|
| Memo type | "Transportation shift" or "Northern escort" |
| Staff assigned | |
| Date | |
| Number of youth | |
| Destination / community | |
| Start time / End time | |
| Notes (free text) | e.g., agency arrival requirements, overnight stay details |

- Memos can be created, viewed, and removed by Management.
- Each memo is linked to its corresponding `TRAN`/`ESC` cell on the schedule (see §3.6) and inherits the same visibility restriction (only the assigned employee + management can open the full memo from the schedule).
- Transportation shifts must first be offered to UTHC staff with a set deadline; if unfilled, sent to the outsourced agency. Agency staff must arrive 1 hour before the appointment.

---

## 9. Staff on Leave (Management-only)

A tracker, visible only within the Management Dashboard's "Staff on leave" tab — never to employees in general:

| Field | Notes |
|---|---|
| Employee name | |
| Leave type | Sick, Maternity, Paternity, CNESST, Vacation, Other |
| Date started | |
| Expected return date | |
| Progressive return? | Yes/No |
| Progressive return detail | Free text, e.g., "2 shifts/week for 2 weeks, then full schedule" — only shown if Progressive return = Yes |

**Exception — the employee themselves:** the specific employee who is on leave *does* see their own progressive-return schedule and regular schedule as part of their personal view once logged in (so they know their own ramp-up plan). This is scoped strictly to that one employee's own account — no other employee sees this information about anyone, including themselves if not applicable.

Management can add, edit, and remove leave records freely.

---

## 10. Coworker Messaging

- A direct messaging area where any two employees can message each other (primarily intended for negotiating shift/unit switches before formalizing a request).
- Includes a "Propose switch" action inside a conversation, which launches the structured switch-proposal form described in §7.2 and posts a live-updating status card into the conversation thread showing each stage of the approval chain (employee A agreed → employee B agreed/pending → management approved/pending).
- Conversation list shows unread indicators.

---

## 11. Mass Communications

- Management/Scheduler can broadcast a message to: All staff, a specific unit, a specific role, or Management only.
- A persisted log of all sent broadcasts, visible to Management, so they can refer back to what was previously communicated.

---

## 12. On-Call Manager

- A visible indicator (to all staff) of who the on-call manager is for the current week/weekend, with contact info.
- Automatically notifies all staff if the on-call assignment changes.
- Management can edit/reassign the on-call manager.
- The on-call manager's own view includes full schedule access, seniority lists, and staff contact information for that period.

---

## 13. Seniority Lists

- Separate seniority lists for Educators and Intervention Agents, each showing: employee number, name, employment status (FT/PT/TFT/Recall), start date, seniority in years and days.
- **Reorderable by Management:** staff can be moved up or down the list via drag-and-drop or up/down arrow controls. The saved order directly drives OT distribution and rotation order (§6).

---

## 14. Staff Directory / Contact List

- Full staff list: name, role, employment status, unit, phone, email.
- Searchable/filterable by unit, role, employment status.
- Editable by Management (add/edit/remove staff, change unit/role/status).

---

## 15. Notifications

Every action listed below must trigger a notification via **both** in-app notification and email, to all relevant parties:
- Book-off submitted / approved / denied / attempted-late
- Switch proposed / agreed / declined / approved / denied
- OT offered / taken / refused
- Schedule updated
- Account status changed (suspended/terminated/reinstated)
- Mass communication sent
- On-call assignment changed
- Availability change submitted (effective 10 days later)

---

## 16. Schedule Updates — Timing & Routing

- Updates occur Monday, Wednesday, and Friday, with the effective date clearly shown at the top of the schedule.
- Updates received Monday–Friday between 9:00–17:00 route to the **Scheduling Admin**.
- Updates received after 17:00 or on weekends route to the **On-call manager**.

---

## 17. Availability Sheets

- Recall workers must submit every pay period; part-time block workers only need to if requesting shifts beyond their fixed block.
- Deadline: every second-to-last Wednesday of the month at 9:00 AM. Late submissions are flagged and placed at the bottom of the shift-rotation list, with an automatic notice to the employee and to management.
- Minimum requirements: recall workers need 4 shifts including 2 weekend shifts and 1 weekend evening shift; part-time block workers already meet this via their block.
- Format: `X` = desired shift, `W` = scheduled block shift (part-time only).
- Availability can be submitted up to 10 days before a new schedule period begins. Changes to availability take effect 10 days after the change request, with immediate notification to the employee, management, and scheduler.

---

## 18. Visual / Color Reference

| Code/Color | Meaning |
|---|---|
| Baby blue (on staff name) | Overtime shift |
| SW (Red) | Permanent switch |
| SW (Black) | Temporary switch |
| V | Vacation |
| LIB | Liberation day |
| Stat | Statutory holiday |
| `*` (after a name) | Outsourced agency worker (not UTHC) |
| SH | Shadow shift (new employee) |
| PXT | Training week |
| ESC | Escort shift |
| L.O.S. | Loan of Service |
| SWG / SWB | Switch to Girls unit / Switch to Boys unit |
| Tran | Transportation shift |
| CNR | Cannot Replace — shift sent to both UTHC and agency, remains unfilled; management notified |
| DNR | Do Not Replace — staff not needed on the floor |

---

## 19. Non-Functional Requirements

- **Privacy/role-based visibility** is a first-class requirement throughout — not an afterthought. Multiple features above (Staff on Leave, LOS, TRAN/ESC detail, progressive return) depend on strict per-user visibility rules, not just role-level rules. The data model must support "visible to: this specific employee + management" as a pattern, not just "visible to: management only."
- Mobile-friendly responsive design (staff are shift workers, likely checking schedules from a phone).
- This is a Quebec health/social-services-adjacent organization (CSSS/CIUSSS network) — confirm whether any provincial health-data privacy requirements (e.g., Loi 25 / Law 25) apply to staff personal and leave data, and build accordingly.
- All historical schedule/staff data should be retained for record-keeping even after an employee's access is suspended or terminated.

---

## 20. Suggested Phasing (for quoting purposes)

**Phase 1 — Core (minimum viable launch)**
- Authentication (incl. 12-month OTP cycle, suspend/terminate)
- The 6 schedule grids (4-week view, full roster, editable by management, read-only for employees)
- Book-off requests + approval
- Staff directory + seniority lists (reorderable)
- Notifications (app + email) for the above

**Phase 2 — Operational depth**
- OT distribution queue & rotation logic
- Shift switch request chain (employee↔employee↔management)
- Schedule update timing/routing logic
- Staff on Leave tracker (incl. progressive return, restricted visibility)

**Phase 3 — Extended features**
- Coworker direct messaging
- Memos (transport/escort) with linked schedule detail
- Loan of Service tracking
- Mass communications log
- On-call manager assignment & visibility

---

## Appendix: Source Materials Provided

- Real schedule documents: Boys/Girls × Educators/IA Day-Eve/Overnight, Pay Periods 07–08
- Educators Seniority List, PP 18
- Intervention Agents Seniority List, PP 18
- Staff contact directory (all roles, with emails and phone numbers)
- Availability sheet samples (Educators & Intervention Agents), handwritten and digital
- Book-off request log, PP 07–08
- Internal scheduling procedures and guidelines document (full text)
- Working interactive HTML/CSS/JS prototype covering all features above (see accompanying files)
