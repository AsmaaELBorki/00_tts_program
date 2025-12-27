# Repository Dependencies

This document defines how repositories within the Tracking the Sun analytical architecture relate to one another.

Dependencies are explicit.  
They are directional.  
They are not inferred.

Repositories do not duplicate logic, re-derive shared concepts, or silently reinterpret upstream decisions.

---

## Architectural Principle

Each repository operates at a distinct analytical layer.

Dependencies describe:
- what a repository is allowed to assume
- what it is required to inherit
- what it is not permitted to redefine

A repository may depend on outputs from an upstream repository, but it does not depend on its internal implementation.

Only declared outputs are trusted.

---

## Repo 0 — Analytical Architecture

**Role:** governance and constraint definition

Repo 0 defines:
- column roles
- schema boundaries
- canonical representations
- violation classifications
- allowed assumptions

Repo 0 produces no analytical outputs.  
It establishes the conditions under which analysis elsewhere is valid.

All downstream repositories depend on Repo 0.

---

## Repo 1 — System Size Determinants

**Depends on:**
- Repo 0 schemas
- Repo 0 data contracts
- Repo 0 violation definitions

Repo 1 is the first execution layer.

It:
- loads raw data
- applies validation rules
- derives canonically approved fields
- establishes descriptive baselines related to system size

Repo 1 does not:
- make predictive claims
- reinterpret schema semantics
- introduce new canonical fields without updating Repo 0

Outputs from Repo 1 are consumed downstream.

---

## Repo 2 — System Configuration & Inverter Architecture

**Depends on:**
- Repo 0 governance
- Repo 1 outputs

Repo 2 assumes that:
- system size baselines are stable
- canonical fields derived in Repo 1 are valid

It examines configuration behavior conditional on those baselines.

Repo 2 does not:
- re-clean raw data
- redefine size-related assumptions
- bypass violations identified upstream

---

## Repo 3 — Scaling, Regimes, and Deviation

**Depends on:**
- Repo 0 governance
- Repo 1 baselines
- Repo 2 configuration features

Repo 3 formalizes expected structure:
- scaling behavior
- regime formation
- deviation patterns

It treats time and size strictly according to definitions established upstream.

Repo 3 does not:
- introduce new interpretations of time
- reinterpret configuration semantics
- bypass cohort constraints

---

## Repo 4 — Predictive Signals, Risk, and Oversizing

**Depends on:**
- Repo 0 governance
- Repos 1–3 outputs

Repo 4 operates within the tightest constraints.

It uses only:
- canonically defined fields
- upstream-approved features
- declared assumptions

Repo 4 does not:
- redefine violations
- reinterpret uncertainty
- expand scope beyond what upstream layers support

---

## Dependency Rules

- Dependencies are **additive**, not circular
- Outputs flow forward only
- Assumptions are inherited, not reintroduced
- Any change to Repo 0 may require downstream review

If a repository requires a new shared concept, it must be defined upstream before use.

---

## Versioning Implications

Breaking changes in Repo 0:
- invalidate downstream assumptions
- require explicit review
- may force downstream updates

Downstream repositories do not pin internal implementation details, only declared outputs and contracts.

---

This document defines structure, not sequence.

Execution order may vary.  
Dependency relationships do not.
