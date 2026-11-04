# ADR-0002: Polyglot backend — Java/Spring for the core, Node/NestJS for the edge

- Status: Accepted
- Date: 2026-11-03

## Context
The system has two very different workloads: CPU-bound graph computation
with strong transactional consistency, and I/O-bound integration,
real-time delivery and AI agent orchestration.

## Decision
- Java 25 + Spring Boot 4: flight-scheduling, route-optimizer.
- Node.js LTS + NestJS 11 (TypeScript strict): ingestion-service,
  api-gateway, disruption-copilot.
- Inter-service contracts defined language-neutrally (Avro/Protobuf,
  OpenAPI, AsyncAPI) in `/contracts`.

## Consequences
- (+) Each workload runs on the runtime best suited for it.
- (+) Demonstrates cross-language contracts, tracing and testing.
- (−) Two toolchains (Gradle + pnpm) and two dependency ecosystems.
- (−) Contract drift risk — mitigated by schema registry and Pact.