<!-- sdlc:auto:start adr -->
# ADR-0004: Use AWS for Cloud

Status: Accepted  
Date: 2026-11-11

## Context and Problem Statement

Which Cloud technology does the project use? Decided in architecture v1.

## Considered Options

- AWS
- Fly.io
- Render

## Decision Outcome

Chosen option: AWS, because Approved stack. Runs the static SPA (S3/CloudFront), the API (App Runner/Fargate), PostgreSQL (RDS), and the Redis container comfortably on smallest tiers.

## Consequences

Managed services cost a little even at idle, but smallest tiers keep the bill minimal for a free single-user app.
<!-- sdlc:auto:end adr -->