# Application Repository Audit

**Application repository:** `baluthi/baluthi-com`  
**Audit date:** 2026-07-28  
**Current phase:** Closed Beta stabilization

---

## 1. Repository Located

The actual application source was located in the private repository `baluthi/baluthi-com`.

The commit history contains an explicit FINAN Beta homologation commit and subsequent product work. This confirms that the application repository is the continuation point for the Closed Beta rather than a new implementation.

---

## 2. Verified Technology Stack

The application uses:

- React 19;
- TypeScript;
- TanStack Start;
- TanStack Router;
- TanStack Query;
- Vite;
- Supabase JavaScript client;
- Tailwind CSS;
- Radix UI components;
- React Hook Form and Zod;
- Vitest;
- Python-based end-to-end test entrypoint;
- jsPDF and jsPDF AutoTable for PDF export.

Available scripts include development, build, lint, format, unit tests, coverage, type checking, E2E, and a check intended to prevent Supabase service-role usage in client code.

---

## 3. Verified Functional Evidence

Repository history and route metadata provide evidence of the following application areas:

- authentication and authenticated routes;
- user dashboard;
- administration dashboard;
- calendar;
- cards and invoices;
- categories;
- settings;
- bank accounts;
- financial entries;
- recurring entries;
- reports and PDF generation;
- plans and subscription screens;
- security center;
- About and Support page;
- system status presentation.

These areas still require behavior and data-isolation validation before they can be classified as Closed Beta ready.

---

## 4. Current Branding State

The current application source still identifies the product as `FINAN` in root metadata and multiple authenticated routes.

The application repository README identifies the project as `Baluthi V2.0`, but also contains legacy wording such as the provisional name `Meu Fluxo` and the prior MVP prompt.

This creates a verified inconsistency between:

- the official product identity: Baluthi;
- the implemented application identity: FINAN;
- legacy repository wording: Meu Fluxo.

---

## 5. Initial Closed Beta Blocker

### CB-BLOCKER-001 — Product identity inconsistency

**Severity:** High  
**Category:** Release consistency / user trust

A Closed Beta release must not expose three different product identities across repository documentation, browser metadata, application navigation, reports, and support information.

The correction is within the frozen Closed Beta scope because it is a product renaming and branding-alignment task, not a new feature.

### Acceptance criteria

- all user-facing `FINAN` and `Meu Fluxo` references are inventoried;
- approved product name is consistently `Baluthi`;
- document titles, metadata, navigation, generated reports, support pages, and visible version labels use the approved identity;
- technical identifiers are changed only when safe and necessary;
- no financial behavior is altered by the branding correction;
- build, typecheck, lint, and tests remain passing after the correction.

---

## 6. Additional Audit Priorities

After branding consistency, validate in this order:

1. authentication and protected-route enforcement;
2. Supabase client/server separation and secret handling;
3. row-level data isolation and authorization;
4. core financial calculations and card invoice rules;
5. duplicate-expense prevention on invoice payment;
6. recurring and installment generation;
7. PDF report accuracy;
8. critical journey E2E reliability;
9. build and deployment reproducibility;
10. error handling, logging, and beta support diagnostics.

This order does not create new product scope. It prioritizes risk within the approved Closed Beta baseline.

---

## 7. Audit Decision

The application is no longer classified as missing. It is now available for technical audit and incremental Closed Beta stabilization.

The first verified correction target is the product identity inconsistency. Security and data-isolation validation remain mandatory before release approval.
