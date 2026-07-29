# Baluthi Product Bible

**Version:** 1.0.1

**Status:** Active

**Owner:** Franciel Salvático

**Created:** 2026-07-28

**Last updated:** 2026-07-28

---

# Purpose

The Product Bible is an official source of truth for the Baluthi project.

Every architectural decision, business rule, product definition, technical specification and roadmap must be documented here.

When documentation and implementation diverge, the documentation must be updated as part of the same work.

---

# Official Source Hierarchy

The project must be interpreted using the following official sources together:

1. `AI_CONTEXT.md`
2. `PROJECT_MEMORY.md`
3. Product Bible (`docs/`)

No source may be replaced by assumptions.

When an official source is absent, inaccessible or conflicts with another official source, the gap must be documented before implementation decisions are made.

For Closed Beta work, only changes supported by the official sources or required to correct verified defects, security risks, data integrity risks, release blockers or critical usability failures are allowed.

---

# Documentation Structure

## 00_PROJECT

Project governance, vision and strategy.

- DOC-000 — Index
- DOC-001 — Constitution
- DOC-002 — Product Vision
- DOC-003 — Product Principles
- DOC-004 — Scope
- DOC-005 — Roadmap

---

## 01_BRAND

Brand identity.

- Mission
- Vision
- Values
- Logo
- Colors
- Typography
- Voice

---

## 02_PRODUCT

Functional documentation.

- Modules
- Features
- Business Rules
- User Stories
- Personas

---

## 03_UX

Experience documentation.

- Wireframes
- User Flows
- Navigation
- Design Decisions

---

## 04_TECHNICAL

Engineering documentation.

- Architecture
- Backend
- Frontend
- Database
- Infrastructure
- APIs
- Security

---

## 05_FINAN_MIGRATION

Migration documentation.

- Inventory
- Mapping
- Legacy Decisions
- Compatibility

---

## 06_RELEASES

Version history and release readiness evidence.

- Changelog
- Release Notes
- Milestones
- [Closed Beta Repository Audit](06_RELEASES/CLOSED_BETA_REPOSITORY_AUDIT.md)

---

## 07_ADR

Architecture Decision Records.

---

## 08_FUTURE

Ideas not yet approved.

---

# Documentation Rules

Every important decision must be documented.

Documentation evolves together with the code.

Every feature must have an owner.

Business rules always prevail over implementation.

The official sources collectively form the project's source of truth.

Closed Beta documentation must distinguish verified facts, evidence gaps, risks and approved decisions.

---

# Version History

| Version | Date | Description |
|----------|------|-------------|
| 1.0.1 | 2026-07-28 | Added official source hierarchy, Closed Beta constraints and audit reference |
| 1.0.0 | 2026-07-28 | Initial Product Bible |
