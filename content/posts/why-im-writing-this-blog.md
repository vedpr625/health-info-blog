---
title: "Why I'm Writing This Blog"
date: 2026-11-01
tags: ["interoperability", "health informatics", "FHIR", "introduction"]
categories: ["reflections"]
description: "An introduction to this blog and what it will cover."
---

## The gap I kept noticing

Interoperability projects generate an enormous amount of knowledge — lessons learned the hard way, trade-offs debated in meeting rooms, workarounds that eventually became best practice. Almost none of it is written down in a form anyone outside the project ever reads. What does get documented is usually formal, sanitized, and locked inside project reports that exist to satisfy a funder, not to teach.

The same is true one layer down, at the code. A FHIR Implementation Guide tells you what a resource profile should look like. It rarely tells you what actually breaks when you wire a Spring Boot microservice to a HAPI FHIR server under real load, or why a dual openEHR-plus-FHIR architecture sounds elegant on a whiteboard and gets messy the moment two systems disagree about which one owns the truth.

I wanted a place to write the version that doesn't make it into those reports — the standards debates *and* the engineering decisions behind them.

## What I've seen across three countries

I've worked on health interoperability in three very different settings: India, Mongolia, and now Sri Lanka, where I'm a Solutions Architect on a UNOPS national digital health platform. Each context has its own constraints — infrastructure, governance maturity, political will, workforce capacity — and yet the underlying challenges rhyme more than you'd expect. Standards adoption, stakeholder alignment, and the gap between a well-designed architecture and a system that actually gets used: these show up everywhere, just wearing different clothes.

What's changed less across those eighteen-plus years than I expected is the engineering itself. Whether it's a national Hospital Information System in Mongolia, a health claims exchange in India, or a document and imaging repository in Sri Lanka, the same questions keep returning: how do you design FHIR resource profiles that are both standards-compliant and usable by the people who have to populate them? How do you build a Spring Boot microservice layer that survives contact with a government data centre's network? When does a message queue save you, and when does it just move the failure somewhere harder to debug?

## What this blog will cover

I plan to write about:

- **Standards** — HL7 FHIR, openEHR, IHE profiles, and the practical reality of implementing them in resource-constrained settings
- **Engineering decisions** — the Spring Boot, Kafka, and Kubernetes choices behind the architecture diagrams, and what they cost in practice
- **Governance and policy** — the non-technical hurdles that often decide whether an architecture succeeds
- **Stakeholder management** — getting ministries, implementers, and vendors to agree on anything
- **The human side** — what large-scale health IT projects are actually like to work on, for the engineers building them as much as the architects designing them

## Who this is for

Informatics professionals, fellow architects and engineers, policymakers, and anyone trying to make sense of health interoperability from the inside — from the FHIR resource profile down to the code that implements it — rather than from a glossy final report.

## An invitation

If you've worked on similar projects — in Sri Lanka, India, Mongolia, or anywhere else — I'd like to hear how your experience compares. Disagree with something I write here? Good. That's worth a conversation too.
