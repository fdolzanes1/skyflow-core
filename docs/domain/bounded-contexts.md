# Bounded Contexts

## 1. Scheduling — `flight-scheduling` (Java / Spring Boot)

Flights, rotations, crew pairings and the operational plan.
Receives commands: create, delay, cancel, swap aircraft.
**Why Java:** rich transactional domain, strong consistency, JPA + PostGIS.

## 2. Network — `route-optimizer` (Java / Spring Boot)  ← core domain

Airports, routes and graph topology. Owns pathfinding
(Dijkstra, A*, k-shortest paths).
**Why Java:** CPU-bound work, massive concurrency with virtual threads,
precise benchmarking with JMH.

## 3. Ingestion — `ingestion-service` (Node / NestJS)  ← supporting

Adapters for OpenSky, METAR and OurAirports. Normalizes data and publishes events.
**Why Node:** I/O-bound, many concurrent HTTP calls, event loop shines.

## 4. Recovery Copilot — `disruption-copilot` (Node / NestJS)

AI agent that builds context (network sub-graph + regulations) and proposes Recovery Plans. Never changes the plan without human approval.
**Why Node:** most mature AI agent / MCP ecosystem, structured output with Zod.

## 5. Experience — `api-gateway` (Node / NestJS)  ← generic

Backend-for-frontend: GraphQL for the web app, WebSocket for the live map.
**Why Node:** real-time delivery, same language as the frontend.

## Context map (main events)

- Ingestion → `WeatherObserved`, `AircraftPositionReported` → Network, Copilot
- Scheduling → `FlightDelayed`, `FlightCancelled`, `AircraftSwapped` → Network
- Network → `RoutesRecalculated` → Copilot, Gateway
- Copilot → `RecoveryPlanProposed` → Gateway (human approval)