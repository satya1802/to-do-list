# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-STACK · approved · source: requirements:technology-stack

Product owner approved an exact technology stack for this build; no substitutions allowed.

Approved stack: Backend NestJS 11; Cloud AWS (smallest/low-cost tier, room to scale); Database PostgreSQL 16 (relational fit for tasks with due dates/done flag/single user, supports efficient 'due soon' queries); Frontend Angular 22.

### REQ-SERVICES · approved · source: requirements:services

One runtime service approved: a Redis queue, intended to hold reminders until due time.

Queue: Redis (as a queue), container redis:7-alpine. Rationale given: a reminder must fire at a specific time ahead of a task's due time; a delayed-job queue holds the reminder and triggers it, which a plain web request cannot do alone. Required API key/env var: REDIS_URL. Note: despite this rationale, actual reminder delivery (email/push/SMS) is explicitly out of scope in this version per EPIC-002 assumptions -- due date/time is recorded and displayed only, no reminder message is sent.

**Related:** US-005

### REQ-OUT-OF-SCOPE · approved · source: requirements:out-of-scope

Explicit exclusions for this delivery.

Out of scope: native mobile app (iOS/Android); mobile push notifications and SMS reminders; email (SendGrid was removed from the stack). Delivery scope flagged as 'lightweight'; requirements version 1.

### EPIC-001 · draft · source: requirements:EPIC-001

Secure single-user access: the to-do list is private to one individual, protected by email + password sign-in, with no public sign-up.

Single account is provisioned for the owner only; no multi-user onboarding. Sessions are protected and can be ended by signing out. Assumptions: single-user login protects the list with no public self-service sign-up flow in this version; app is free with no payment, billing, or subscription features.

**Related:** US-001, US-002, US-003

### US-001 · draft · source: requirements:US-001

Critical story: owner signs in with email and password to reach their private task list.

AC-001: correct email+password on sign-in page -> signed in, taken to task list. AC-002: email/password that doesn't match account -> not signed in, invalid-credentials error shown. AC-003: stored credentials are persisted only as a hash, never in plain text.

**Related:** EPIC-001, AC-001, AC-002, AC-003, NFR-001, NFR-004

### US-002 · draft · source: requirements:US-002

High-priority story: session stays protected and owner can sign out, so an unattended device doesn't expose tasks.

AC-004: not signed in and trying to open task list -> redirected to sign-in page, no tasks visible. AC-005: signing out ends session, must sign in again to view tasks. AC-006: session inactive beyond expiry -> session expires, sign-in required again.

**Related:** EPIC-001, AC-004, AC-005, AC-006, NFR-002, NFR-003, NFR-004

### US-003 · draft · source: requirements:US-003

Low-priority story: the whole app is usable free of charge with no paywall.

AC-007: while signed in, using any feature never prompts payment, billing details, or subscription, and no feature is locked behind a paywall.

**Related:** EPIC-001, AC-007, NFR-007

### EPIC-002 · draft · source: requirements:EPIC-002

Managing tasks: owner maintains a single flat list -- add, edit, complete, delete, reorder, and optionally set a due date/time.

No categories, priorities, notes, or subtasks in this version. Assumptions: single flat list with no categories/priority/subtasks; due dates interpreted in owner's own time zone; time-based reminders before due time are NOT delivered in this version (email/push/SMS all out of scope) -- due date/time is recorded and displayed only, no reminder is sent.

**Related:** US-004, US-005, US-006, US-007, US-008, US-009

### US-004 · draft · source: requirements:US-004

Critical story: owner adds a new task to capture something to do.

AC-008: entering a description and saving -> task appears in list as outstanding. AC-009: trying to save with empty description -> not saved, owner told description is required.

**Related:** EPIC-002, AC-008, AC-009

### US-005 · draft · source: requirements:US-005

High-priority story: owner can set a due date and time on a task so they know when it needs to be done.

AC-010: setting due date/time on add or edit and saving -> task shows that due date/time. AC-011: due date/time is shown in the owner's own time zone. AC-012: saving without a due date/time -> task saved with no due date and still appears in the list.

**Related:** EPIC-002, AC-010, AC-011, AC-012, NFR-006

### US-006 · draft · source: requirements:US-006

High-priority story: owner edits a task's description or due date to keep the list accurate.

AC-013: editing description or due date/time and saving -> task shows updated details. AC-014: clearing description and trying to save -> change rejected, description-required message shown.

**Related:** EPIC-002, AC-013, AC-014

### US-007 · draft · source: requirements:US-007

Critical story: owner marks a task complete (and can reopen it) to track what's finished.

AC-015: marking an outstanding task complete -> shown as completed, removed from outstanding view. AC-016: marking a completed task not-complete -> returns to outstanding tasks.

**Related:** EPIC-002, AC-015, AC-016

### US-008 · draft · source: requirements:US-008

Medium-priority story: owner deletes a task to keep the list free of unneeded items.

AC-017: deleting a task removes it so it no longer appears in outstanding or completed views.

**Related:** EPIC-002, AC-017

### US-009 · draft · source: requirements:US-009

Medium-priority story: owner reorders tasks in the list to work through them in a preferred order.

AC-018: moving a task to a new position among several outstanding tasks keeps it there, and the new order persists on return to the list.

**Related:** EPIC-002, AC-018

### EPIC-003 · draft · source: requirements:EPIC-003

Viewing and tracking task progress: see outstanding vs. completed tasks, usable comfortably on phone or desktop.

Assumptions: delivered as a mobile-friendly responsive web app, not a native mobile app; all dates/times shown in owner's own time zone.

**Related:** US-010, US-011

### US-010 · draft · source: requirements:US-010

High-priority story: owner sees outstanding tasks separately from completed ones.

AC-019: viewing outstanding tasks shows only tasks not yet complete. AC-020: viewing completed tasks shows only tasks marked complete.

**Related:** EPIC-003, AC-019, AC-020, NFR-006

### US-011 · draft · source: requirements:US-011

Medium-priority story: app adapts to screen size for comfortable use on phone or computer.

AC-021: on a small mobile screen, layout fits and add/edit/complete/delete/reorder all work without horizontal scrolling. AC-022: on a large desktop screen, layout adapts to the wider screen with all the same actions available.

**Related:** EPIC-003, AC-021, AC-022, NFR-005

### NFR-001 · draft · source: requirements:NFR-001

Security: account password must be stored only as a hash, never plain text.

Applies to US-001. Ensures stored credentials cannot be read back.

**Related:** US-001

### NFR-002 · draft · source: requirements:NFR-002

Security: sessions must end on sign-out and expire after inactivity.

Applies to US-002. After expiry or sign-out, owner must sign in again before seeing any tasks.

**Related:** US-002

### NFR-003 · draft · source: requirements:NFR-003

Security: unauthenticated access to the task list must be blocked.

Applies to US-002. Anyone not signed in trying to open the task list is sent to the sign-in page and sees no tasks.

**Related:** US-002

### NFR-004 · draft · source: requirements:NFR-004

Privacy: the task list is private to the single owner.

Applies to US-001, US-002. Only the signed-in owner can view or manage their tasks.

**Related:** US-001, US-002

### NFR-005 · draft · source: requirements:NFR-005

Usability: app must adapt layout to screen size for phone and desktop use.

Applies to US-011. Add, edit, complete, delete, and reorder must work on small mobile screens without horizontal scrolling, and the same actions must be available on wide desktop screens.

**Related:** US-011

### NFR-006 · draft · source: requirements:NFR-006

Usability: all due dates and times must be shown in the owner's own time zone.

Applies to US-005, US-010.

**Related:** US-005, US-010

### NFR-007 · draft · source: requirements:NFR-007

Compliance: every feature must be usable free of charge, with no paywall.

Applies to US-003. Owner is never asked to pay, enter billing details, or subscribe; no feature is locked behind a paywall.

**Related:** US-003
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v1  
**Delivery scope:** lightweight  
**Approved:** 2026-11-11

**Capabilities in scope:** Single-user email and password sign-in, Add a task to the list, Set a due date and time on a task, Mark a task complete, Edit a task, Delete a task, Reorder tasks in the list, View outstanding versus completed tasks, Single flat task list (no categories or subtasks), Due dates shown in the individual's own time zone, Free to use, with no payment or subscription

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | NestJS | — |
| cloud | AWS | AWS is the available host and comfortably runs a small web app, its database, and a scheduled reminder job on modest, low-cost resources. Since the app is free and serves one person, you can run it on the smallest tier and keep the bill minimal while keeping room to scale if you ever open it up. |
| database | PostgreSQL | Your data is a list of tasks with a due date, a done flag, and one user account, exactly the structured, date-driven data a relational database is built for. PostgreSQL stores it reliably and lets the app ask 'which tasks are due soon' efficiently so reminders go out on time. It is the available option and more than enough for one user's task list. |
| frontend | Angular | — |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-001: Secure single-user access

The to-do list is private to one individual and is protected behind an email + password sign-in. There is no public sign-up or multi-user onboarding; the single account is provisioned for the owner. Sessions are protected and can be ended by signing out. ASSUMPTION: a single-user login protects the list and no public self-service sign-up flow exists in this version. ASSUMPTION: the app is free of charge with no payment, billing or subscription features.

### US-001: Sign in with email and password

**Priority:** critical

> As a the task list owner, I want to sign in with my email address and password, so that only I can view and manage my private task list.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | I am on the sign-in page and an account exists for my email | I enter my correct email and password and submit | I am signed in and taken to my task list |
| AC-002 | I am on the sign-in page | I enter an email or password that does not match the account | I am not signed in and I see an error that the credentials are not valid |
| AC-003 | the system stores my account credentials | my password is persisted | it is stored only as a hash and never in plain text |

### US-002: Keep my list private across sessions

**Priority:** high

> As a the task list owner, I want my session to be protected and to be able to sign out, so that no one else can reach my tasks on a shared or unattended device.

| ID | Given | When | Then |
|---|---|---|---|
| AC-004 | I am not signed in | I try to open the task list directly | I am redirected to the sign-in page and cannot see any tasks |
| AC-005 | I am signed in | I choose to sign out | my session ends and I must sign in again to view my tasks |
| AC-006 | I am signed in | my session has been inactive beyond its expiry period | the session expires and I am required to sign in again |

### US-003: Use the app free of charge

**Priority:** low

> As a the task list owner, I want to use the whole app without paying, so that I can manage my tasks with no cost or subscription.

| ID | Given | When | Then |
|---|---|---|---|
| AC-007 | I am signed in | I use any feature of the app | I am never asked to pay, enter billing details, or subscribe, and no feature is locked behind a paywall |

## EPIC-002: Managing tasks in the list

The owner maintains a single flat list of tasks: adding, editing, completing, deleting and reordering them, and optionally giving a task a due date and time. There are no categories, priorities, notes or subtasks in this version. ASSUMPTION: tasks live in one flat list with no categories, priority flags/sorting, or subtasks. ASSUMPTION: due dates are interpreted in the owner's own time zone. ASSUMPTION: time-based reminders before the due time are NOT delivered in this version because email, push and SMS channels are all out of scope; a due date/time is recorded and displayed but no reminder message is sent.

### US-004: Add a task to the list

**Priority:** critical

> As a the task list owner, I want to add a new task to my list, so that I can capture something I need to do.

| ID | Given | When | Then |
|---|---|---|---|
| AC-008 | I am signed in and viewing my list | I enter a task description and save it | the task appears in my list as outstanding |
| AC-009 | I am adding a task | I try to save it with an empty description | the task is not saved and I am told a description is required |

### US-005: Set a due date and time on a task

**Priority:** high

> As a the task list owner, I want to give a task a due date and time, so that I know when it needs to be done.

| ID | Given | When | Then |
|---|---|---|---|
| AC-010 | I am adding or editing a task | I set a due date and time and save | the task shows that due date and time |
| AC-011 | a task has a due date and time | I view it | the due date and time are shown in my own time zone |
| AC-012 | I am adding or editing a task | I save it without setting a due date and time | the task is saved with no due date and appears in the list |

### US-006: Edit a task

**Priority:** high

> As a the task list owner, I want to change a task's description or due date, so that my list stays accurate as things change.

| ID | Given | When | Then |
|---|---|---|---|
| AC-013 | a task exists in my list | I edit its description or due date and time and save | the task shows the updated details |
| AC-014 | I am editing a task | I clear the description and try to save | the change is rejected and I am told a description is required |

### US-007: Mark a task complete

**Priority:** critical

> As a the task list owner, I want to mark a task as complete (and reopen it if needed), so that I can track what I have finished.

| ID | Given | When | Then |
|---|---|---|---|
| AC-015 | an outstanding task exists | I mark it complete | the task is shown as completed and removed from the outstanding tasks |
| AC-016 | a completed task exists | I mark it as not complete | the task returns to the outstanding tasks |

### US-008: Delete a task

**Priority:** medium

> As a the task list owner, I want to delete a task, so that my list is free of things I no longer need.

| ID | Given | When | Then |
|---|---|---|---|
| AC-017 | a task exists in my list | I delete it | the task is removed and no longer appears in outstanding or completed views |

### US-009: Reorder tasks in the list

**Priority:** medium

> As a the task list owner, I want to change the order of tasks in my list, so that I can arrange them the way I want to work through them.

| ID | Given | When | Then |
|---|---|---|---|
| AC-018 | my list has several outstanding tasks | I move a task to a new position | the task stays in that position and the new order is kept when I return to the list |

## EPIC-003: Viewing and tracking task progress

The owner can see outstanding versus completed tasks and use the app comfortably on a phone or desktop. ASSUMPTION: delivered as a mobile-friendly responsive web app, not a native mobile app. ASSUMPTION: all dates and times are shown in the owner's own time zone.

### US-010: View outstanding versus completed tasks

**Priority:** high

> As a the task list owner, I want to see my outstanding tasks separately from completed ones, so that I can focus on what still needs doing while keeping a record of what is done.

| ID | Given | When | Then |
|---|---|---|---|
| AC-019 | my list has both outstanding and completed tasks | I view my outstanding tasks | I see only tasks that are not yet complete |
| AC-020 | my list has completed tasks | I view my completed tasks | I see only tasks that have been marked complete |

### US-011: Use the app on phone and desktop

**Priority:** medium

> As a the task list owner, I want the app to adapt to my screen size, so that I can manage tasks comfortably on my phone or my computer.

| ID | Given | When | Then |
|---|---|---|---|
| AC-021 | I open the app on a small mobile-sized screen | I view and interact with my task list | the layout fits the screen and I can add, edit, complete, delete and reorder tasks without horizontal scrolling |
| AC-022 | I open the app on a large desktop screen | I view my task list | the layout adapts to the wider screen and all the same actions are available |
<!-- sdlc:auto:end epics -->
