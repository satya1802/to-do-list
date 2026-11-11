# Sprint Plan

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start sprints -->
## Sprint 1: Sprint 1

Secure sign-in, private sessions, and confirmation the app has no paywall

Capacity: 20 points · Committed: 14

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-001 | Story | Sign in with email and password | 8 | backend-agent | — |
| ↳ US-001-T1 | Task | Add users and sessions schema migration | — | backend-agent | — |
| ↳ US-001-T2 | Task | Implement POST /auth/login and GET /auth/me endpoints | — | backend-agent | — |
| ↳ US-001-T3 | Task | Build Angular sign-in page and auth state service | — | frontend-agent | — |
| ↳ US-001-T4 | Task | Write auth flow test suite | — | qa-agent | — |
| US-002 | Story | Keep my list private across sessions | 5 | backend-agent | US-001 |
| US-003 | Story | Use the app free of charge | 1 | qa-agent | — |

## Sprint 2: Sprint 2

Core task management: add, set due date, edit, complete, delete

Capacity: 20 points · Committed: 19

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-004 | Story | Add a task to the list | 8 | backend-agent | — |
| ↳ US-004-T1 | Task | Add tasks table migration | — | backend-agent | — |
| ↳ US-004-T2 | Task | Implement POST /tasks and GET /tasks endpoints | — | backend-agent | — |
| ↳ US-004-T3 | Task | Build Angular task list view and add-task form | — | frontend-agent | — |
| ↳ US-004-T4 | Task | Write test suite for add-task validation and listing | — | qa-agent | — |
| US-005 | Story | Set a due date and time on a task | 3 | frontend-agent | US-004 |
| US-006 | Story | Edit a task | 3 | backend-agent | US-004 |
| US-007 | Story | Mark a task complete | 3 | backend-agent | US-004 |
| US-008 | Story | Delete a task | 2 | backend-agent | US-004 |

## Sprint 3: Sprint 3

Reordering, outstanding/completed views, and responsive layout

Capacity: 20 points · Committed: 13

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-009 | Story | Reorder tasks in the list | 5 | frontend-agent | US-004 |
| US-010 | Story | View outstanding versus completed tasks | 3 | frontend-agent | US-004, US-007 |
| US-011 | Story | Use the app on phone and desktop | 5 | frontend-agent | US-004, US-009, US-010 |

## Unscheduled

_Nothing unscheduled._
<!-- sdlc:auto:end sprints -->
