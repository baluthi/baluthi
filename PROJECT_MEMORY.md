# Baluthi Project Memory

**Status:** Active  
**Last updated:** 2026-08-03  
**Current phase:** Closed Beta preparation and isolated Android test validation

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

The web beta remains active. Android builds are generated for controlled testing through a native project and Android Studio, initially as APK outside the Play Store.

The mobile app contains only user-facing functions. The administrative panel remains exclusively web, with administrative permissions enforced server-side.

### D-008 — Android environment is fully isolated from the beta

The Android test environment must maintain separate:

- application URL;
- database;
- authentication;
- backend functions and RPCs;
- attachment storage;
- credentials and secrets;
- users and sessions;
- financial data and test records;
- transactional e-mail configuration;
- redirect URLs.

The approved mobile POC URL is `https://baluthi-mobile-poc.lovable.app`, unless formally replaced and documented.

The Android app must never point to the beta database or use beta users, sessions or real data. Android tests use fictional data only.

### D-009 — Baluthi 2.0 is the functional source; Android is synchronized in controlled batches

Corrections are first implemented and validated in Baluthi 2.0. After validation, each correction or small batch is replicated to the Android copy with traceability to the source commit.

Database migrations, RPCs and backend changes are then applied separately to the Android environment and validated there.

The projects must not be maintained as two independent manual implementations, and the Android copy should not be replaced wholesale only after a large backlog of changes.

### D-010 — Documentation must be proactive

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
- Full isolation between the beta environment and the Android test environment formally documented.
- Controlled code-correction synchronization workflow formally documented.
- Proactive documentation governance rule added to `AI_CONTEXT.md`.

---

## 4. In Progress

- Validating Android build and installation on physical device.
- Reconciling the exact mobile scripts and dependencies present in the current application repository/copy.
- Recording the identifiers of the isolated Android backend, authentication, storage and redirects without exposing secrets.
- Defining the exact technical mechanism used to transfer each approved commit or change set from Baluthi 2.0 to the Android copy.
- Completing critical-journey tests on web and Android.
- Preparing evidence for controlled Android APK distribution.

---

## 5. Pending Verification

### Android environment isolation

- exact mobile project/branch and commit used by the first approved APK;
- confirmed URL `https://baluthi-mobile-poc.lovable.app` in the current Android build;
- separate Android database identifier;
- separate authentication configuration;
- separate storage configuration;
- separate RPC/backend deployment;
- separate redirect and transactional e-mail configuration;
- evidence that beta users, sessions and data are absent;
- evidence that Android requests do not call beta services.

### Android build and behavior

- mobile build script currently present in the active Android copy;
- Capacitor configuration and Android project location;
- JDK, Gradle, Android Studio and SDK versions;
- permissions for camera, gallery and PDF;
- button-back, keyboard, offline and resume behavior;
- first complete test report;
- version, build number, filename and hash of the approved APK.

### Synchronization and release

- formal identification of the Baluthi 2.0 commit corresponding to each Android change set;
- separate application of migrations/RPCs in the Android environment;
- regression evidence after each synchronized batch;
- documented process for Android APK distribution and replacement.

### Security and isolation between users

- cross-user isolation using two separate test accounts in each environment;
- ordinary user denial on administrative routes and RPCs;
- server-side resistance to manual record-ID tampering;
- storage and attachment isolation;
- ownership and role validation for authenticated RPCs;
- recovery token expiration, invalidation and non-reuse.

---

## 6. Current Blockers

1. The active Android copy and its mobile scripts must be reconciled with the documented build process.
2. The isolated Android environment identifiers are not yet fully recorded in the release document.
3. The technical sync mechanism between Baluthi 2.0 and the Android copy is not yet formally evidenced.
4. Manual security and cross-user validation remain incomplete.
5. The first Android release record is not yet filled with commits, version, environment and test evidence.

---

## 7. Risks

- Android configuration may accidentally point to beta services.
- Copying the whole project may transport beta URLs or credentials.
- Maintaining corrections manually in two projects may create divergent financial rules.
- Delaying synchronization until the end of a large backlog may create merge conflicts and hidden regressions.
- Migrations may be applied to the wrong database if environment ownership is not explicit.
- APK distribution outside the Play Store lacks automatic update control.
- Camera, file and storage permissions may expose platform-specific defects.
- Direct database-permission changes can break financial flows if not regression-tested separately in each environment.
- Undocumented steps can become de facto process and create operational dependency on individual memory.

---

## 8. Technical Debt

- Recharts 2 and an unmaintained transitive dependency generate non-blocking build warnings.
- Some production chunks exceed 500 kB and need controlled code splitting after critical release blockers.
- Authentication e-mail branding remains pending.
- Security validation is still partly manual and lacks automated negative authorization tests.
- Android scripts, dependencies and project configuration need repository-level reconciliation and explicit version pinning.
- The commit-transfer/synchronization mechanism between Baluthi 2.0 and Android still needs final technical definition.
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

Before implementing the next improvement batch:

1. identify the active Baluthi 2.0 project and the active Android copy;
2. record the branch/project and commits of both;
3. confirm the Android URL and all isolated service identifiers;
4. choose and document the exact controlled synchronization mechanism;
5. implement and validate the first small correction batch in Baluthi 2.0;
6. replicate that batch to Android without copying beta environment configuration;
7. apply any migration/RPC only to the Android backend separately;
8. execute the Android isolation and regression tests;
9. update the Android release record.

Any mismatch between the documented process, code and environment must be corrected before the APK is treated as reproducible or safe.

---

## 11. Change Log

| Date | Change |
|---|---|
| 2026-07-28 | Initial Project Memory created from verified prior project decisions and repository audit |
| 2026-07-29 | Updated with current architecture, rebranding, e-mail validation, authentication recovery and security backlog |
| 2026-08-03 | Added Android test architecture, build/QA/release documentation and proactive documentation governance |
| 2026-08-03 | Formalized full isolation of Android database/backend from beta and controlled synchronization of corrections from Baluthi 2.0 |
