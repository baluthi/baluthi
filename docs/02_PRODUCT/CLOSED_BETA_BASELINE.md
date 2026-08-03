# Closed Beta Functional Baseline

**Product:** Baluthi  
**Origin:** FINAN Closed Beta baseline  
**Status:** Scope frozen  
**Effective date:** 2026-08-03

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

## 3. Supported Test Surfaces

The same frozen functional baseline may be validated through:

1. the Baluthi web application deployed through the approved web release flow;
2. the Baluthi Android application generated for controlled Closed Beta testing.

The Android application is a delivery surface for the approved baseline, not a new product module. Platform-specific adjustments are permitted only when necessary for compatibility, security, privacy, data integrity, accessibility or critical mobile usability.

Initial Android distribution occurs as a controlled APK outside the Play Store. Publication through Play Store, commercial distribution, billing or platform-specific new functionality requires separate approval and documentation.

---

## 4. Current Product Rule

The FINAN Closed Beta is the functional baseline for Baluthi.

The current work must preserve this baseline while applying only:

- product renaming;
- branding alignment;
- documentation reconciliation;
- verified defect corrections;
- security, privacy and data-integrity corrections;
- tests and operational safeguards required to make the existing beta solid;
- mobile packaging and compatibility work required to test the same approved scope on Android.

No new features are approved before validation of the frozen baseline.

Artificial intelligence functionality is not part of the current implementation scope unless separately approved in the official sources after Closed Beta validation.

---

## 5. Android Closed Beta Rules

Before an APK is distributed, the release must identify:

- version and build number;
- source commit;
- environment used by the application;
- database, authentication, storage and backend configuration;
- devices and Android versions tested;
- known limitations;
- test evidence;
- rollback or replacement procedure.

The APK must not be described as isolated from production unless that isolation has been technically verified.

The test group must be informed that the package is a Closed Beta build and is not an official Play Store publication.

---

## 6. Validation Requirement

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
- release readiness;
- mobile permissions and lifecycle behavior;
- keyboard, navigation and button-back behavior;
- offline or unstable-network handling;
- attachment access through camera, gallery and files.

---

## 7. Out of Scope

Until the frozen baseline is validated, the following are out of scope:

- new product modules;
- broad UX redesigns unrelated to critical usability;
- speculative integrations;
- artificial intelligence features;
- post-beta roadmap items;
- architectural rewrites without a verified Closed Beta blocker;
- Play Store publication without separate release approval;
- Android-only financial functionality not present in the approved baseline.

---

## 8. Traceability

This baseline must be read together with:

- `AI_CONTEXT.md`;
- `PROJECT_MEMORY.md`;
- `docs/README.md`;
- `docs/04_TECHNICAL/ADR-ANDROID-APP-AND-SEPARATE-ENVIRONMENT.md`;
- `docs/04_TECHNICAL/ANDROID_BUILD_GUIDE.md`;
- `docs/05_QA/ANDROID_CLOSED_BETA_TEST_PLAN.md`;
- `docs/06_RELEASES/ANDROID_CLOSED_BETA_RELEASE.md`;
- `docs/06_RELEASES/CLOSED_BETA_REPOSITORY_AUDIT.md`.

Implementation traceability must always reference the actual application commit used for each web or Android release.
