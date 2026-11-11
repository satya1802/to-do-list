<!-- sdlc:auto:start adr -->
# ADR-0001: Use Angular 22 for Frontend

Status: Accepted  
Date: 2026-11-11

## Context and Problem Statement

Which Frontend technology does the project use? Decided in architecture v1.

## Considered Options

- Angular 22
- React
- Vue

## Decision Outcome

Chosen option: Angular 22, because Approved stack. Delivers the responsive single-user UI; Angular CDK provides accessible drag-and-drop for reordering and the built SPA is served statically from CloudFront on a separate origin from the API.

## Consequences

Full-featured framework is heavier than needed for one user, but it is the approved choice and its tooling covers forms validation, routing guards, and responsive layout out of the box.
<!-- sdlc:auto:end adr -->