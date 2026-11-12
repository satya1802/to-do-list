# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-TECHSTACK · approved · source: requirements:v2

Technology stack approved by the product owner: NestJS 11 backend, Angular 22 frontend, PostgreSQL 16 database, hosted on AWS.

Backend: NestJS 11. Frontend: Angular 22. Database: PostgreSQL 16 -- chosen because the app's data (tasks with due date, done flag, one user account) is structured, date-driven data suited to a relational database, and it lets the app efficiently query 'which tasks are due soon' for timely reminders; more than sufficient for a single user. Cloud: AWS -- comfortably runs the small web app, its database, and a scheduled reminder job on modest, low-cost resources; app is free and single-user so smallest tier is used, with room to scale later. Product owner directive: design against exactly this stack, do not substitute.

### REQ-SERVICES · approved · source: requirements:v2

One runtime service approved: a Redis-backed delayed job queue to fire due-date reminders at the right time.

Queue: Redis (as a queue), container redis:7-alpine. Rationale: a reminder must fire at a specific time ahead of each task's due time; a delayed-job queue holds each reminder until the moment it should send and triggers it, which a plain web request cannot do on its own. Required API key/env var: REDIS_URL.

### REQ-SCOPE · approved · source: requirements:v2

Scope is a lightweight, single-user web to-do list with due-date reminders; native mobile apps, push/SMS reminders, and email are explicitly excluded.

Delivery scope: lightweight. Out of scope -- do not design or build: (1) Native mobile app (iOS/Android); (2) Mobile push notifications and SMS reminders; (3) Email (the previously suggested SendGrid was removed from the stack). Note: email delivery is out of scope even though the Redis queue exists to time reminders -- the input does not state what channel reminders ultimately use, so this is flagged rather than assumed.

### REQ-FEAT-AUTH · approved · source: requirements:v2

Single-user sign-in using email and password.

Capability: Single-user email and password sign-in. Supports exactly one user account per the database rationale (one user account is part of the app's structured data).

### REQ-FEAT-TASKMGMT · approved · source: requirements:v2

Core task CRUD: create, edit, and delete tasks on the list.

Capabilities: Add a task to the list; Edit a task; Delete a task.

### REQ-FEAT-DUEDATE · approved · source: requirements:v2

Tasks carry a due date and time, displayed in the individual's own time zone.

Capabilities: Set a due date and time on a task; Due dates shown in the individual's own time zone. Due date/time is the field the Redis-backed reminder queue schedules against.

### REQ-FEAT-STATUS · approved · source: requirements:v2

Tasks can be marked complete, and the list can be viewed split by outstanding versus completed status.

Capabilities: Mark a task complete; View outstanding versus completed tasks.

### REQ-FEAT-ORDER · approved · source: requirements:v2

Tasks can be manually reordered within the list.

Capability: Reorder tasks in the list.

### REQ-FEAT-STRUCTURE · approved · source: requirements:v2

The task list is a single flat list with no categories or subtasks.

Capability: Single flat task list (no categories or subtasks) -- explicitly constrains the data model and UI to avoid hierarchical or grouped task structures.

### REQ-NFR-FREE · approved · source: requirements:v2

The application is free to use with no payment or subscription model.

Non-functional/business constraint: Free to use, with no payment or subscription. Reinforced by the AWS stack rationale noting the app serves one person for free and should run on minimal-cost resources.
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v2  
**Delivery scope:** lightweight  
**Approved:** 2026-11-12

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
