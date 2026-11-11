# Data Model

<!-- sdlc:auto:start entities -->
### users

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| email | varchar(320) | False | — | False |
| password_hash | varchar(255) | False | — | False |
| timezone | varchar(64) | False | — | False |
| created_at | timestamptz | False | — | False |

### sessions

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| user_id | uuid | False | users.id | False |
| token_hash | varchar(255) | False | — | False |
| expires_at | timestamptz | False | — | False |
| last_active_at | timestamptz | False | — | False |
| created_at | timestamptz | False | — | False |

### tasks

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| user_id | uuid | False | users.id | False |
| description | text | False | — | False |
| due_at | timestamptz | False | — | True |
| is_complete | boolean | False | — | False |
| position | integer | False | — | False |
| created_at | timestamptz | False | — | False |
| updated_at | timestamptz | False | — | False |
<!-- sdlc:auto:end entities -->

<!-- sdlc:auto:start relationships -->
| Source | Target | Type |
|---|---|---|
| users | tasks | one-to-many |
| users | sessions | one-to-many |
<!-- sdlc:auto:end relationships -->

<!-- sdlc:auto:start er-diagram -->
```mermaid
erDiagram
  users {
    uuid id PK
    varchar_320_ email
    varchar_255_ password_hash
    varchar_64_ timezone
    timestamptz created_at
  }
  sessions {
    uuid id PK
    uuid user_id FK
    varchar_255_ token_hash
    timestamptz expires_at
    timestamptz last_active_at
    timestamptz created_at
  }
  tasks {
    uuid id PK
    uuid user_id FK
    text description
    timestamptz due_at
    boolean is_complete
    integer position
    timestamptz created_at
    timestamptz updated_at
  }
  users ||--o{ tasks : "one-to-many"
  users ||--o{ sessions : "one-to-many"
```
<!-- sdlc:auto:end er-diagram -->
