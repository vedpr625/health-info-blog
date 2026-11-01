---
title: "Projects"
date: 2026-11-01
---

A selection of the national digital health platforms, open-source infrastructure, and commercial products I've architected and built.

## National & Government Platforms

**Digital Health Platform — Ministry of Health and Mass Media, Sri Lanka** *(UNOPS)*
Solutions Architect on a UNOPS-contracted national digital health programme, spanning three workstreams:

- **Digital Health Information Warehouse** — secondary-use data warehouse for population health analytics
- **Platform Support Services** — generic, reusable FOSS components shared across the national platform
- **Document and Imaging Repository** — a HAPI FHIR JPA document repository (ITI-65 Provide Document Bundle, ITI-67 Find Document References, ITI-68 Retrieve Document, ITI-105) paired with an Orthanc DICOMweb server (STOW-RS, WADO-RS, QIDO-RS) and a Record Locator service resolving cross-facility document and imaging pointers at national scale — with PDPA-compliant consent enforcement, SHA-256 document integrity verification, and IHE ATNA/BALP-compliant audit logging, aligned to Sri Lanka's national NEHR/NHDX systems

This work sits on an open-source stack throughout — HAPI FHIR, Orthanc, and SeaweedFS object storage — chosen deliberately so the Ministry owns and can run the infrastructure without vendor lock-in.

**Mongolian Hospital Information System**
Architected and delivered a full-scale, greenfield Hospital Information System for a leading Mongolian healthcare institution, replacing a decade-old legacy platform. Built on HL7 FHIR R4 and openEHR (EHRbase CDR), with IHE integration profiles (PIX, PDQ, XDS, XCA) and multi-terminology support (SNOMED CT, LOINC, ICD-10/11). Twelve clinical modules — EMR, OPD, IPD, Nursing, Finance, Pharmacy, CDSS, LIMS, HRMS, RIS, and PACS — with full Mongolian (Cyrillic) localisation.

**HCX — Health Claims Data Exchange**
Lead Architect on an open-source national initiative, inspired by the Joint Working Group of NHA and IRDAI, defining interoperable protocol specifications for secure, multi-party health insurance claims exchange between payors, providers, beneficiaries, and regulators across India.

**HIP/HIU — Health Information Provider / User Platform**
Architected a standards-compliant EMR platform enabling hospitals, diagnostic centres, and telemedicine providers to digitally exchange patient health information under a structured, FHIR Consent-based framework.

**UHI — Unified Health Interface Reference Application**
Co-led the open-source reference implementation of India's Unified Health Interface, an open network protocol for interoperable health services — teleconsultation, appointment booking, and prescription exchange — using the Beckn Protocol mapped to FHIR resources.

## Open-Source Infrastructure

**AJ FHIR Platform** — [ajfhir.org](https://ajfhir.org)
A suite of open-source, Apache 2.0-licensed FHIR components stewarded by the Dr. Akriti Jamwal Foundation, including a SMART App Launch v2.2 authorization server, SMART client, a drop-in HAPI FHIR plugin for SMART discovery and scope enforcement, a FHIR Consent Manager, an Immunisation App with WHO schedule forecasting, and a cross-facility Referral Module built on IHE MHD. Designed as reference implementations for modern health informatics standards adoption, and pursuing Digital Public Goods recognition.

**Open-Source EMR & Patient Management System**
Released two open-source FHIR-native health applications — among the first of their kind in India — a Patient Management System and a fully standards-compliant EMR, built on EHRbase (openEHR Clinical Data Repository) and HAPI FHIR Server, using a dual-model architecture that preserves clinical semantics while enabling interoperable exchange.

## Commercial Products

**Jam Health Platform** — built by Akhester Technologies for hospital networks and national health information exchanges
A full HIE stack including a HL7v2-to-FHIR integration engine, a probabilistic-matching Master Patient Index, a Facility Registry, a Shared Health Record, a patient-facing Health Record portal, and a FHIR bulk-export population health data warehouse — serving hospital markets in the US and Middle East.

**JamEMR**
A full FHIR-native Electronic Medical Record built on the Jam platform, with consent, referral, immunisation, and shared health record support built in from day one.

---

I'm always interested in conversations about health interoperability, FHIR implementation, and standards-based digital health architecture. Reach out through the links in the footer.
