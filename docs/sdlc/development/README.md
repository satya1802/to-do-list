# Development

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
### DEV-SPRINT-1 · draft · source: plan:Sprint 1

Sprint 1 plan targets secure sign-in, private sessions, and confirming the app is free, with capacity of 20 points.

Goal: Secure sign-in, private sessions, and confirmation the app has no paywall. Capacity: 20 points. Covers US-001 (Sign in with email and password, 8 pts), US-002 (Keep my list private across sessions, 5 pts), US-003 (Use the app free of charge, 1 pt). Plan status: generated, version 1 (not yet marked approved).

**Related:** US-001, US-002, US-003

### DEV-SPRINT-2 · draft · source: plan:Sprint 2

Sprint 2 plan targets core task management: adding, due dates, editing, completing, and deleting tasks, with capacity of 20 points.

Goal: Core task management: add, set due date, edit, complete, delete. Capacity: 20 points. Covers US-004 (Add a task to the list, 8 pts), US-005 (Set a due date and time on a task, 3 pts), US-006 (Edit a task, 3 pts), US-007 (Mark a task complete, 3 pts), US-008 (Delete a task, 2 pts). Plan status: generated, version 1 (not yet marked approved).

**Related:** US-004, US-005, US-006, US-007, US-008

### DEV-SPRINT-3 · draft · source: plan:Sprint 3

Sprint 3 plan targets task reordering, outstanding/completed views, and responsive layout, with capacity of 20 points.

Goal: Reordering, outstanding/completed views, and responsive layout. Capacity: 20 points. Covers US-009 (Reorder tasks in the list, 5 pts), US-010 (View outstanding versus completed tasks, 3 pts), US-011 (Use the app on phone and desktop, 5 pts). Plan status: generated, version 1 (not yet marked approved).

**Related:** US-009, US-010, US-011

### EPIC-001 · draft · source: plan:EPIC-001

Epic grouping for secure single-user access.

Epic EPIC-001: Secure single-user access. No points or role assigned at epic level. Contains stories US-001, US-002, US-003.

**Related:** US-001, US-002, US-003

### EPIC-002 · draft · source: plan:EPIC-002

Epic grouping for managing tasks in the list.

Epic EPIC-002: Managing tasks in the list. No points or role assigned at epic level. Contains stories US-004, US-005, US-006, US-007, US-008, US-009.

**Related:** US-004, US-005, US-006, US-007, US-008, US-009

### EPIC-003 · draft · source: plan:EPIC-003

Epic grouping for viewing and tracking task progress.

Epic EPIC-003: Viewing and tracking task progress. No points or role assigned at epic level. Contains stories US-010, US-011.

**Related:** US-010, US-011

### US-001 · draft · source: plan:US-001

Story to let a user sign in with email and password, broken into four implementation tasks (8 points, backend-agent).

Story US-001: Sign in with email and password (8 pts, assigned role: backend-agent). Planned tasks: T1 - Add users and sessions schema migration (backend-agent); T2 - Implement POST /auth/login and GET /auth/me endpoints (backend-agent); T3 - Build Angular sign-in page and auth state service (frontend-agent); T4 - Write auth flow test suite (qa-agent).

**Related:** EPIC-001

### US-002 · draft · source: plan:US-002

Story to keep a user's task list private across sessions (5 points, backend-agent).

Story US-002: Keep my list private across sessions (5 pts, assigned role: backend-agent). No sub-tasks listed in the plan.

**Related:** EPIC-001, US-001

### US-003 · draft · source: plan:US-003

Story confirming the app is usable free of charge (1 point, qa-agent).

Story US-003: Use the app free of charge (1 pt, assigned role: qa-agent). No sub-tasks listed in the plan.

**Related:** EPIC-001

### US-004 · draft · source: plan:US-004

Story to add a task to the list, broken into four implementation tasks (8 points, backend-agent).

Story US-004: Add a task to the list (8 pts, assigned role: backend-agent). Planned tasks: T1 - Add tasks table migration (backend-agent); T2 - Implement POST /tasks and GET /tasks endpoints (backend-agent); T3 - Build Angular task list view and add-task form (frontend-agent); T4 - Write test suite for add-task validation and listing (qa-agent).

**Related:** EPIC-002

### US-005 · draft · source: plan:US-005

Story to set a due date and time on a task (3 points, frontend-agent).

Story US-005: Set a due date and time on a task (3 pts, assigned role: frontend-agent). No sub-tasks listed in the plan.

**Related:** EPIC-002, US-004

### US-006 · draft · source: plan:US-006

Story to edit a task (3 points, backend-agent).

Story US-006: Edit a task (3 pts, assigned role: backend-agent). No sub-tasks listed in the plan.

**Related:** EPIC-002, US-004

### US-007 · draft · source: plan:US-007

Story to mark a task complete (3 points, backend-agent).

Story US-007: Mark a task complete (3 pts, assigned role: backend-agent). No sub-tasks listed in the plan.

**Related:** EPIC-002, US-004

### US-008 · draft · source: plan:US-008

Story to delete a task (2 points, backend-agent).

Story US-008: Delete a task (2 pts, assigned role: backend-agent). No sub-tasks listed in the plan.

**Related:** EPIC-002, US-004

### US-009 · draft · source: plan:US-009

Story to reorder tasks in the list (5 points, frontend-agent).

Story US-009: Reorder tasks in the list (5 pts, assigned role: frontend-agent). No sub-tasks listed in the plan.

**Related:** EPIC-002

### US-010 · draft · source: plan:US-010

Story to view outstanding versus completed tasks (3 points, frontend-agent).

Story US-010: View outstanding versus completed tasks (3 pts, assigned role: frontend-agent). No sub-tasks listed in the plan.

**Related:** EPIC-003

### US-011 · draft · source: plan:US-011

Story to use the app on phone and desktop (5 points, frontend-agent).

Story US-011: Use the app on phone and desktop (5 pts, assigned role: frontend-agent). No sub-tasks listed in the plan.

**Related:** EPIC-003
<!-- sdlc:auto:end narrative -->
