# Traceability Matrix

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start legend -->
Built from recorded links, not written by a model: requirement key → plan item (`source_stable_key`) → development ticket (`stable_key`) → the ticket's test steps → the last live deployment that started after the work finished. **AC tests** counts the story's acceptance criteria that have a test case, and those whose test cases all passed in the latest finished E2E run.
<!-- sdlc:auto:end legend -->

<!-- sdlc:auto:start matrix -->
| Requirement | Epic | Title | Plan items | Sprint | Design | Code | Commits | Ticket | Tests | AC tests | Deployed |
|---|---|---|---|---|---|---|---|---|---|---|---|
| US-001 | EPIC-001 | Sign in with email and password | US-001, US-001-T1, US-001-T2, US-001-T3, US-001-T4 | 1 | GET /auth/me, POST /auth/login, api, db, sessions, users, web | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-002 | EPIC-001 | Keep my list private across sessions | US-002 | 1 | GET /auth/me, POST /auth/logout, api, sessions, web | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-003 | EPIC-001 | Use the app free of charge | US-003 | 1 | — | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-004 | EPIC-002 | Add a task to the list | US-004, US-004-T1, US-004-T2, US-004-T3, US-004-T4 | 2 | GET /tasks, POST /tasks, api, db, tasks, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-005 | EPIC-002 | Set a due date and time on a task | US-005 | 2 | PATCH /tasks/:id, POST /tasks, api, tasks, web | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-006 | EPIC-002 | Edit a task | US-006 | 2 | PATCH /tasks/:id, api, tasks, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-007 | EPIC-002 | Mark a task complete | US-007 | 2 | PATCH /tasks/:id/completion, api, tasks, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-008 | EPIC-002 | Delete a task | US-008 | 2 | DELETE /tasks/:id, api, tasks | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-009 | EPIC-002 | Reorder tasks in the list | US-009 | 3 | PATCH /tasks/reorder, api, tasks, web | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-010 | EPIC-003 | View outstanding versus completed tasks | US-010 | 3 | GET /tasks, tasks, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-011 | EPIC-003 | Use the app on phone and desktop | US-011 | 3 | web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
<!-- sdlc:auto:end matrix -->
