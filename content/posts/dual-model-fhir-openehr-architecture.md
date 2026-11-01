---
title: "Why We Run a Dual FHIR + openEHR Architecture (And What It Actually Costs)"
date: 2026-11-01
tags: ["FHIR", "openEHR", "architecture", "EHRbase", "interoperability"]
categories: ["engineering"]
description: "A look at dual-model clinical data architecture — openEHR for structured clinical documentation, FHIR for interoperable exchange — and the real engineering trade-offs behind it."
---

On paper, the pitch for a dual-model clinical data architecture is clean: use **openEHR** archetypes for structured, meaning-preserving clinical documentation, and **HL7 FHIR** resources for interoperable exchange. Two models, each doing what it's best at. I've built this pattern more than once now — across an open-source Patient Management System and EMR, a health information exchange platform, and a national Hospital Information System — and it's worth being honest about what it buys you and what it costs.

## Why not just pick one?

FHIR is excellent at exchange. It's REST-native, has a huge ecosystem, and every health information exchange, national registry, and EHR vendor increasingly speaks it. But FHIR resources are deliberately general-purpose — a `Observation` resource can represent almost anything, which means it doesn't enforce the clinical precision a structured record actually needs.

openEHR goes the other way. Archetypes model clinical concepts with real semantic depth — a blood pressure reading isn't just a number with a code, it's a structured concept with position, cuff size, method, and a dozen other clinically meaningful qualifiers, versioned and governed by clinical domain experts rather than engineers. That precision is exactly what you want for the system of record. It's also exactly why openEHR alone doesn't solve interoperability — the archetype ecosystem outside your own deployment is thinner, and most external systems you need to talk to expect FHIR at the door.

So: openEHR as the clinical data repository, FHIR as the exchange layer. On an architecture diagram, one arrow connects them. In practice, that arrow is the hardest part of the system.

## What the dual model actually requires

**A mapping layer that never stops moving.** Every openEHR archetype needs a corresponding FHIR profile, and the mapping between them isn't static — it changes every time a clinical team wants a new field, every time a FHIR Implementation Guide gets a new constraint, every time a national terminology server updates its value sets. The mapping layer isn't a one-time ETL job; it's a piece of software with its own lifecycle, its own tests, and its own on-call rotation.

**A decision about where truth lives.** The moment you have two models, you have to decide which one is authoritative when they disagree — and they will disagree, usually at 2am during a data migration. We've settled on openEHR as the system of record for clinical documentation (EHRbase as the Clinical Data Repository) and FHIR as a derived, synchronized view for exchange. That's a defensible choice, but it's a choice, and it has consequences: every write path has to go through the openEHR layer first, which adds latency and complexity that a FHIR-only system wouldn't have.

**Two sets of conformance tests.** You're not just testing FHIR profile conformance anymore — you're testing that the openEHR-to-FHIR mapping holds under every archetype variant your clinical teams actually use, not just the ones in your test fixtures. This is where most of the "it worked in the demo" failures come from.

**Operational cost that's easy to underestimate.** Running EHRbase and a HAPI FHIR server side by side, kept in sync, with Spring Boot microservices orchestrating the mapping between them, is meaningfully more infrastructure than running either one alone. On a national-scale deployment — the kind with Kafka event streams pushing updates across a dozen hospital modules and a Kubernetes cluster that has to stay up — that cost compounds.

## Is it worth it?

For a system that genuinely needs both deep clinical semantics *and* broad interoperability — which, in my experience, describes most national-scale health platforms — yes. A FHIR-only system tends to drift toward using extensions and loosely-typed Observations to capture clinical nuance, which just relocates the semantic precision problem into undocumented local conventions. An openEHR-only system tends to under-invest in the exchange layer until an external integration forces the issue, at which point you're retrofitting FHIR under deadline pressure.

The dual model front-loads the cost instead of deferring it. Whether that trade is right depends on how much of your system's life will be spent exchanging data with systems you don't control — which, for anything touching a national health information exchange, is usually "most of it."

What I'd tell a team considering this architecture for the first time: budget real engineering time for the mapping layer as its own component, not as glue code. It's the part of the system that will need the most ongoing care, and it's the part most often left out of the initial estimate.
