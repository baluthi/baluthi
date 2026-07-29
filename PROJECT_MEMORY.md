# Baluthi Project Memory

**Status:** Active  
**Last updated:** 2026-07-29  
**Current phase:** Closed Beta preparation

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
- Password recovery e-mail successfully received using the default Lovable Cloud auth sender/template.
- Lovable security correction revoked unnecessary direct execution of internal database functions for anonymous and authenticated roles.
- Automatic security scan reported one issue fixed, zero remaining automatic findings, and one item accepted by design.
- Mandatory manual security checklist created at `docs/04_TECHNICAL/CLOSED_BETA_SECURITY_VALIDATION.md`.

---

## 4. In Progress

- Validating the complete password-reset journey after clicking the recovery link.
- Configuring branded authentication e-mails if the Lovable Cloud plan and Custom Auth Emails feature allow it.
- Stabilizing GitHub CI after recent e-mail and authentication changes.
- Preparing the security evidence required before inviting 10–20 users.

---

## 5. Pending Verification

### Security and isolation

- Cross-user isolation using two separate test accounts.
- Ordinary user denial on administrative routes and RPCs.
- Server-side resistance to manual record-ID tampering.
- Storage and attachment isolation.
- Ownership and role validation for all authenticated RPCs.
- Recovery token expiration, invalidation, and non-reuse.
- Approved redirect URL enforcement.
- Review of `promover_primeiro_superadmin()` after initial bootstrap.

### Release and operations

- Final CI success after recent commits.
- Full critical-journey regression test.
- Closed Beta access/invitation process.
- Monitoring, logging, support, rollback, and defect triage evidence.
- Removal of temporary administrative e-mail test card after e-mail validation is fully recorded.

---

## 6. Current Blockers

1. Manual security validation has not yet been completed.
2. Branded authentication e-mails are not yet configured; current recovery messages use the Lovable Cloud sender and English default template.
3. CI has recently failed and requires confirmation of a green run after the latest corrections.
4. Closed Beta acceptance evidence is not yet complete.

---

## 7. Risks

- Automatic security scanning may miss authorization, RLS, storage, or business-logic vulnerabilities.
- Authenticated RPCs may still expose cross-user operations if internal ownership checks are incomplete.
- The bootstrap function `promover_primeiro_superadmin()` may remain callable by ordinary authenticated users, although it rejects execution once a superadmin exists.
- Direct database-permission changes can break financial flows if not regression-tested.
- Lovable Cloud authentication e-mails currently use a generic sender/template, which may reduce user trust during beta.
- Future changes made directly in GitHub or Lovable can reintroduce permission or CI regressions.

---

## 8. Technical Debt

- Recharts 2 and an unmaintained transitive dependency generate non-blocking build warnings.
- Some production chunks exceed 500 kB and need controlled code splitting after critical release blockers.
- Authentication e-mail branding remains pending.
- Temporary e-mail test code/card remains in the administrator panel until final validation.
- Security validation is still partly manual and lacks automated negative authorization tests.

---

## 9. Required Reading Order for the Next Session

1. `AI_CONTEXT.md`
2. `PROJECT_MEMORY.md`
3. `docs/README.md`
4. `docs/02_PRODUCT/CLOSED_BETA_BASELINE.md`
5. `docs/04_TECHNICAL/APPLICATION_REPOSITORY_AUDIT.md`
6. `docs/04_TECHNICAL/CLOSED_BETA_SECURITY_VALIDATION.md`
7. `docs/06_RELEASES/VERCEL_DEPLOYMENT_VALIDATION.md`

---

## 10. Exact Next Step

Complete and record the password-reset link test, then execute the mandatory two-user security validation starting with:

1. create two ordinary test accounts;
2. create distinct accounts, cards, entries, transfers, and attachments for each;
3. attempt cross-user reads and mutations by altering IDs and requests;
4. verify ordinary users cannot invoke administrative routes or RPCs;
5. record evidence in `docs/04_TECHNICAL/CLOSED_BETA_SECURITY_VALIDATION.md` or a linked test report;
6. fix any high/critical finding before inviting beta users.

No new roadmap should be created.

---

## 11. Change Log

| Date | Change |
|---|---|
| 2026-07-28 | Initial Project Memory created from verified prior project decisions and repository audit |
| 2026-07-29 | Updated with current architecture, rebranding, e-mail validation, authentication recovery, security correction, and mandatory security test backlog |
