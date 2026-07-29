# Closed Beta Security Validation

**Product:** Baluthi  
**Status:** Mandatory before inviting 10–20 Closed Beta users  
**Last updated:** 2026-07-29

---

## 1. Verified Security Change

The Lovable security agent revoked direct execution of internal database functions, triggers, and helpers for anonymous visitors and authenticated users where direct execution was not required.

Verified database state after the correction:

- sensitive business RPCs are not executable by the anonymous role;
- authenticated RPCs remain available where they form part of the application API;
- administrative and financial RPCs are expected to enforce ownership or role validation internally;
- internal trigger/helper functions that remain executable are documented as accepted by design where they do not expose user data or privileged business actions.

The automatic scan reported:

- fixed issues: 1;
- remaining automatic findings: 0;
- accepted by design: 1 documented item.

This result does not replace manual security validation or penetration testing.

---

## 2. Accepted-by-Design Functions

Some functions may remain executable because they are:

- PostgreSQL extension functions such as similarity or unaccent helpers;
- trigger functions invoked internally by the database;
- deterministic helpers that calculate values without reading or modifying user data.

These functions must be reviewed again if their definitions or grants change.

---

## 3. Special Follow-up: First Superadmin Bootstrap

The function `promover_primeiro_superadmin()` is authenticated-only and prevents promotion when a superadmin already exists.

Before Closed Beta release, verify one of the following:

- execution has been revoked for ordinary authenticated users after the first superadmin was created; or
- the function is removed/disabled; or
- a documented and tested control proves that it cannot be abused after bootstrap.

Status: **Pending validation**.

---

## 4. Mandatory Manual Validation Checklist

### 4.1 Cross-user data isolation

Using two separate test accounts, confirm that User A cannot view, query, edit, archive, delete, or export data belonging to User B for:

- accounts;
- cards;
- invoices;
- income and expenses;
- transfers;
- recurring entries;
- installments;
- categories and user-specific catalog data;
- reports and exports;
- attachments and receipts.

### 4.2 Administrative authorization

Confirm that an ordinary authenticated user cannot:

- access administrative routes;
- list users;
- change plans or benefits;
- suspend, reactivate, or purge users;
- view administrative KPIs;
- invoke administrative RPCs directly.

### 4.3 Identifier tampering

For critical mutations, alter record IDs manually in browser/network requests and confirm that the server rejects operations on records not owned by the active user.

Validate at minimum:

- edit/delete/archive account;
- edit/delete/archive card;
- mark/unmark financial entry as paid;
- pay/reopen/reverse invoice;
- create/edit/cancel/reverse transfer;
- edit/delete recurring series;
- remove attachments.

### 4.4 File and storage isolation

Confirm that:

- users cannot list another user's files;
- a copied storage URL does not expose private files without authorization;
- upload paths are scoped to the authenticated user;
- deletion of files validates ownership;
- signed URLs expire where applicable.

### 4.5 Authentication and password recovery

Confirm that:

- password recovery does not reveal whether an address is registered;
- recovery tokens expire and cannot be reused;
- an invalid or altered token is rejected;
- a recovery link cannot change another account's password;
- redirect URLs only allow approved Baluthi/Lovable/Vercel domains;
- session handling after password reset is correct.

### 4.6 RPC authorization review

For each authenticated RPC used by the application, confirm:

- ownership checks use the authenticated user identity, not a user ID supplied by the client;
- administrative functions validate role server-side;
- `SECURITY DEFINER` functions have a fixed `search_path`;
- anonymous execution is revoked unless explicitly required and documented;
- error messages do not expose sensitive database details.

---

## 5. Release Rule

The Closed Beta security gate is not complete until:

1. all checklist items have evidence;
2. high or critical findings are fixed;
3. medium findings have an approved mitigation or release decision;
4. accepted risks are documented;
5. the validation is repeated after material changes to authentication, database grants, RLS, RPCs, storage policies, or administrative permissions.

---

## 6. Evidence Record

For each test, record:

- date;
- environment and deployment URL;
- tester;
- accounts/roles used;
- exact action attempted;
- expected result;
- actual result;
- screenshots or logs;
- issue/commit reference when a correction is required.
