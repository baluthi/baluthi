# Baluthi Project Memory

**Status:** Active  
**Last updated:** 2026-08-03  
**Current phase:** Closed Beta preparation and Android test validation

---

## 1. Purpose

This document preserves verified project continuity between development sessions.

It records approved decisions, current state, completed work, active blockers, risks, technical debt, and the exact next step. It must not contain invented implementation details.

---

## 2. Approved Decisions

### D-001 — FINAN becomes Baluthi

The FINAN Closed Beta is the functional origin of Baluthi and is being consolidated under the Baluthi identity.

### D-002 — Closed Beta is the current priority

The immediate objective is to deliver a stable Closed Beta for an initial group of approximately 10–20 users.

### D-003 — Closed Beta scope is frozen

No speculative features, broad redesigns, or post-beta modules should be introduced unless formally approved in the official sources.

### D-004 — Official sources are complementary

`AI_CONTEXT.md`, `PROJECT_MEMORY.md`, and the Product Bible under `docs/` must be read together. Missing or conflicting information must be documented rather than inferred.

### D-005 — Hosting and service topology

Current verified topology:

- Lovable: development/editor and managed cloud backend;
- GitHub `baluthi/baluthi-com`: application source code;
- GitHub `baluthi/baluthi`: official documentation and Product Bible;
- Vercel: application deployment;
- Lovable Cloud/Supabase: database and authentication;
- Resend: application transactional e-mails sent by the Vercel server.

### D-006 — Security validation is a release gate

Automatic security scans are not sufficient. Manual cross-user, authorization, storage, authentication, and RPC validation is mandatory before the Closed Beta group is invited.

### D-007 — Android is a separate test delivery track

The Android application is an additional test and delivery track for the same approved Closed Beta scope. It does not authorize a second implementation of financial rules or new product functionality.

The web production deployment remains active. Android builds are generated for controlled testing through a native project and Android Studio, initially as APK outside the Play Store.

### D-008 — Environment separation must be explicit

Every Android release must state whether separation applies only to the build artifact or also to URL, database, authentication, storage, backend functions, credentials, e-mail and redirect URLs.

No claim of data isolation may be made without technical evidence.

### D-009 — Documentation must be proactive

When a requested step is outside or absent from the official documentation, the Documentation Lead must identify the gap and propose or execute the corresponding update in the same work session when authorized.

---

## 3. Completed

- Official AI context and Project Memory created.
- Product Bible governance and frozen Closed Beta baseline documented.
- Application repository `baluthi/baluthi-com` located and audited.
- Brand changed from FINAN/Meu Fluxo to Baluthi.
- Official tagline, colors, logo assets, favicon, metadata, reports, PDFs, and contact addresses applied.
- Vercel deployment validated in an anonymous browser session.
- Supabase/Lovable Cloud environment variables configured in Vercel.
- Resend domain and API configured.
- Transactional e-mail successfully delivered from `noreply@baluthi.com` with replies directed to `support@baluthi.com`.
- Password recovery flow corrected to use Lovable Cloud/Supabase Auth.
- Mandatory manual security checklist created.
- Unified financial launch flow, transfer integrity, recurring entries, cards, invoices, reports and account/card deletion defects received verified corrections during Closed Beta preparation.
- Android architecture decision documented.
- Android build guide created.
- Android Closed Beta test plan created.
- Android release record template created.
- Proactive documentation governance rule added to `AI_CONTEXT.md`.

---

## 4. In Progress

- Validating Android build and installation on physical device.
- Reconciling the exact mobile scripts and dependencies present in the current application repository.
- Identifying the backend, authentication, storage and redirect configuration used by the APK.
- Completing critical-journey tests on web and Android.
- Preparing evidence for controlled Closed Beta distribution.

---

## 5. Pending Verification

### Android

- exact branch and commit used by the first approved APK;
- mobile build script currently present in `package.json`;
- Capacitor configuration and Android project committed in the application repository;
- JDK, Gradle, Android Studio and SDK versions;
- backend and database used by the APK;
- authentication and storage isolation;
- permissions for camera, gallery and PDF;
- button-back, keyboard, offline and resume behavior;
- first complete test report;
- version, build number, filename and hash of the approved APK.

### Security and isolation

- cross-user isolation using two separate test accounts;
- ordinary user denial on administrative routes and RPCs;
- server-side resistance to manual record-ID tampering;
- storage and attachment isolation;
- ownership and role validation for authenticated RPCs;
- recovery token expiration, invalidation and non-reuse.

### Release and operations

- final CI success after recent changes;
- full critical-journey regression test;
- monitoring, logging, support, rollback and defect-triage evidence;
- documented process for Android APK distribution and replacement.

---

## 6. Current Blockers

1. The current application repository evidence must be reconciled with the mobile build process used in testing.
2. The APK environment is not yet fully identified in the Android release record.
3. Manual security and cross-user validation remain incomplete.
4. The first Android Closed Beta release record is not yet filled with commit, version, environment and test evidence.

---

## 7. Risks

- Android tests may unintentionally use production services.
- Native configuration can diverge from the web source.
- APK distribution outside the Play Store lacks automatic update control.
- Camera, file and storage permissions may expose platform-specific defects.
- Direct database-permission changes can break financial flows if not regression-tested.
- Future changes made directly in GitHub or Lovable can reintroduce permission, build or CI regressions.
- Undocumented steps can become de facto process and create operational dependency on individual memory.

---

## 8. Technical Debt

- Recharts 2 and an unmaintained transitive dependency generate non-blocking build warnings.
- Some production chunks exceed 500 kB and need controlled code splitting after critical release blockers.
- Authentication e-mail branding remains pending.
- Security validation is still partly manual and lacks automated negative authorization tests.
- Android scripts, dependencies and project configuration need repository-level reconciliation and explicit version pinning.
- Formal Play Store signing, AAB, Play Console and update strategy remain future work.

---

## 9. Required Reading Order for the Next Session

1. `AI_CONTEXT.md`
2. `PROJECT_MEMORY.md`
3. `docs/README.md`
4. `docs/02_PRODUCT/CLOSED_BETA_BASELINE.md`
5. `docs/04_TECHNICAL/ADR-ANDROID-APP-AND-SEPARATE-ENVIRONMENT.md`
6. `docs/04_TECHNICAL/ANDROID_BUILD_GUIDE.md`
7. `docs/05_QA/ANDROID_CLOSED_BETA_TEST_PLAN.md`
8. `docs/06_RELEASES/ANDROID_CLOSED_BETA_RELEASE.md`
9. `docs/04_TECHNICAL/CLOSED_BETA_SECURITY_VALIDATION.md`

---

## 10. Exact Next Step

Reconcile the Android build configuration against the current `baluthi/baluthi-com` repository, then fill the Android release record with:

1. branch and commit;
2. scripts and dependencies used;
3. Android Studio/JDK/Gradle versions;
4. backend, authentication and storage environment;
5. APK version, build number, filename and hash;
6. device and Android version;
7. results of the mandatory Android test plan.

Any mismatch between the documented process and the repository must be corrected before the APK is treated as reproducible.

---

## 11. Change Log

| Date | Change |
|---|---|
| 2026-07-28 | Initial Project Memory created from verified prior project decisions and repository audit |
| 2026-07-29 | Updated with current architecture, rebranding, e-mail validation, authentication recovery and security backlog |
| 2026-08-03 | Added Android test architecture, environment-separation rules, build/QA/release documentation and proactive documentation governance |
