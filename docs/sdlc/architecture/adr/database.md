<!-- sdlc:auto:start adr -->
# ADR-0003: Use PostgreSQL 16 for Database

Status: Accepted  
Date: 2026-11-11

## Context and Problem Statement

Which Database technology does the project use? Decided in architecture v1.

## Considered Options

- PostgreSQL 16
- MySQL
- SQLite

## Decision Outcome

Chosen option: PostgreSQL 16, because Approved stack. Relational store fits the structured, date-driven task data and answers 'which tasks are due soon' efficiently via indexed timestamptz columns.

## Consequences

A relational engine is more than one user strictly needs, but it is reliable, free-tier friendly, and leaves room to scale.
<!-- sdlc:auto:end adr -->