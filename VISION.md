# SkyFlow-Core — Product Vision

## Problem
Airline disruptions (weather, technical failures, crew shortages) cost
European carriers billions every year. When fog closes Warsaw Chopin (WAW)
at 06:00, network planners have minutes to re-route aircraft, reassign
crews and remain compliant with EU261 and EASA flight-time limitations.
Much of this work is still manual.

## Solution
SkyFlow-Core is a cloud-native, polyglot platform that:
1. Models the flight network as a dynamic directed graph.
2. Recalculates affected routes in real time when disruption events arrive.
3. Offers an AI Disruption Copilot that proposes recovery plans,
   grounded on live network state and EU regulations.

## Users (personas)
- **Network Planner — Anna (Warsaw OCC):** needs fast, ranked alternatives.
- **Crew Controller — Piotr:** needs legal crew reassignments.
- **Platform Engineer / SRE:** needs observability and reliability.

## Goals
- p99 route recalculation latency < 200 ms.
- Sustain ≥ 1,000 disruption events per second.
- Every AI recommendation is explainable and cites its sources.
- Each workload runs on the runtime best suited for it (Java or Node).

## Non-goals
- Ticket booking, payments or passenger-facing features.
- Certified, production-grade aviation software.
- Real air traffic control (ATC) integration.

## Data sources
- OurAirports — airports and runways (public domain).
- OpenSky Network — live aircraft positions.
- Open-Meteo and aviationweather.gov METAR — weather.

## Success criteria (24-week challenge)
- Public repository with CI, tests, ADRs and a live demo.