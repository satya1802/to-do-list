<!-- sdlc:auto:start adr -->
# ADR-0002: Use NestJS 11 for Backend

Status: Accepted  
Date: 2026-11-11

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v1.

## Considered Options

- NestJS 11
- Express
- Fastify

## Decision Outcome

Chosen option: NestJS 11, because Approved stack. Structured modules host the auth (opaque session), task, and ordering logic; guards enforce the Bearer-token session on every protected route and keep the owner's list private.

## Consequences

More structure than a minimal API needs for one user, but gives clean validation, DI, and testability with little overhead.
<!-- sdlc:auto:end adr -->