# Closed Beta Functional Baseline

**Product:** Baluthi  
**Origin:** FINAN Closed Beta baseline  
**Status:** Scope frozen  
**Effective date:** 2026-07-28

---

## 1. Purpose

This document records the approved functional baseline that must be preserved while FINAN is transitioned to the Baluthi identity.

It is not a new roadmap. It does not authorize new functionality.

---

## 2. Approved Closed Beta Baseline

The Closed Beta baseline includes the following existing core capabilities:

- authentication;
- administrative panel;
- financial accounts;
- cards;
- categories;
- income entries;
- expense entries;
- transfers;
- recurring entries;
- installment entries;
- reports;
- PDF export;
- audit capability;
- modular application architecture.

---

## 3. Current Product Rule

The FINAN Closed Beta is the functional baseline for Baluthi.

The current work must preserve this baseline while applying only:

- product renaming;
- branding alignment;
- documentation reconciliation;
- verified defect corrections;
- security, privacy, and data-integrity corrections;
- tests and operational safeguards required to make the existing beta solid.

No new features are approved before validation of the frozen baseline.

Artificial intelligence functionality is not part of the current implementation scope unless separately approved in the official sources after Closed Beta validation.

---

## 4. Validation Requirement

Each baseline capability must be classified against the actual application source as one of:

- implemented and validated;
- implemented with defects;
- partially implemented;
- documented but not found;
- not auditable due to missing evidence.

Validation must include, where applicable:

- access control;
- expected business rules;
- data persistence;
- error handling;
- critical-path tests;
- auditability;
- release readiness.

---

## 5. Out of Scope

Until the frozen baseline is validated, the following are out of scope:

- new product modules;
- broad UX redesigns unrelated to critical usability;
- speculative integrations;
- artificial intelligence features;
- post-beta roadmap items;
- architectural rewrites without a verified Closed Beta blocker.

---

## 6. Traceability

This baseline must be read together with:

- `AI_CONTEXT.md`;
- `PROJECT_MEMORY.md`;
- `docs/README.md`;
- `docs/06_RELEASES/CLOSED_BETA_REPOSITORY_AUDIT.md`.

Implementation traceability will be added once the application source is available for audit.
