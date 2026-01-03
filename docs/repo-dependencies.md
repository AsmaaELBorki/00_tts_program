# Repository Dependencies

This document defines the **dependency structure** of the *Tracking the Sun* analytical program.

Dependencies are:
- explicit
- directional
- inferential (not merely data flow)

Repositories do not duplicate logic, re-derive shared concepts, or reinterpret upstream decisions.

This document exists to make **analytical ordering enforceable**, not negotiable.

---

## Architectural Principle

Each repository operates at a distinct analytical layer.

Dependencies define:
- what a repository is allowed to assume
- what it must inherit unchanged
- what it is not permitted to redefine

A repository may depend on **declared outputs** from an upstream repository, but never on its internal implementation or intermediate reasoning.

Only declared outputs that have been **promoted to canonical artifacts** are trusted for cross-repository use.

---

## Program-Level Dependencies

The *Tracking the Sun* program includes a **canonical artifacts repository** that mediates all cross-repository data dependencies.

The artifacts repository:
- stores canonical analytical outputs produced upstream
- replaces manual passing of files between repositories
- enforces continuity by freezing agreed-upon results

Analytical repositories depend on upstream repositories **via artifacts**, not via repo-local outputs.

---

## Repo 0 — Program Canon & Analytical Contracts

**Applied question:**  
What rules must hold so that conclusions about residential solar system sizing are interpretable and internally consistent?

**Analytical question:**  
What analytical structure, scope, and invariants govern all downstream work?

**Depends on:**  
None.

**Defines:**
- program scope (California, residential only)
- analytical posture and non-goals
- repository ordering and invariants
- governance documents and authority boundaries

Repo 0 produces no analytical outputs.  
All downstream repositories depend on Repo 0.

---

## Repo 1 — Data Generation & Measurement Process

**Applied question:**  
What do the Tracking the Sun data actually represent, and what limits do reporting processes impose on interpretation?

**Analytical question:**  
Which comparisons, aggregations, and inferences are admissible given the declared data-generation process?

**Depends on:**
- Repo 0 program constraints

**Defines:**
- declared data provenance and reporting context
- unit of observation
- structural absences and known limitations
- binding analytical constraints derived from dataset-owner documentation

Repo 1 does not transform or model data.  
It defines what downstream analysis is **allowed** to do.

All downstream repositories inherit Repo 1 constraints unchanged.

---

## Repo 2 — Canonical System Size Baselines

**Applied question:**  
What residential solar system size is typical in California, given time and context?

**Analytical question:**  
How can expected system size be defined descriptively and defensibly, including uncertainty?

**Depends on:**
- Repo 0 analytical contracts
- Repo 1 measurement constraints

**Defines:**
- expected system size distributions
- temporal and contextual baselines
- uncertainty bounds around size

Repo 2 does not:
- interpret structure
- analyze configuration
- evaluate abnormality
- make predictive claims

Declared outputs from Repo 2 are **promoted to canonical artifacts** and form the size reference frame for all downstream work.

---

## Repo 3 — Within-Size Structural Configuration

**Applied question:**  
When system size is held constant, how do residential solar systems differ in their configuration?

**Analytical question:**  
What structural degrees of freedom exist at fixed size, and which variations are non-trivial?

**Depends on:**
- Repo 0 governance
- Repo 1 measurement constraints
- Repo 2 size baselines (via canonical artifacts)

**Defines:**
- configuration equivalence classes
- admissible structural variation at fixed size

Repo 3 does not:
- redefine size
- analyze scaling
- evaluate risk or abnormality
- re-derive upstream baselines

Its outputs describe **structure conditional on size**, not outcomes.

---

## Repo 4 — Scaling Behavior, Regimes, and Deviation Structure

**Applied question:**  
How do residential solar systems scale in practice, and where do stable regimes and deviation patterns emerge?

**Analytical question:**  
How does size interact with structure across time and geography to produce regime-like behavior?

**Depends on:**
- Repo 0 governance
- Repo 1 constraints
- Repo 2 baselines (via artifacts)
- Repo 3 structural definitions

**Defines:**
- scaling behavior
- regime boundaries
- deviation surfaces and geometry

Repo 4 characterizes pattern structure.  
It does not assign risk, abnormality, or likelihood.

---

## Repo 5 — Abnormality, Directionality, and Sizing Risk

**Applied question:**  
Given established scaling regimes, is a system unusually sized for its context—and in which direction?

**Analytical question:**  
How likely is observed deviation, and when does it plausibly indicate sizing risk?

**Depends on:**
- Repo 0 governance
- Repo 1 measurement constraints
- Repo 2–4 declared outputs (via canonical artifacts)

**Defines:**
- abnormality measures
- deviation likelihood
- over- and under-sizing risk indicators

Repo 5 does not:
- introduce new structure
- reinterpret upstream definitions
- expand scope beyond established constraints

---

## Dependency Rules (Binding)

- Dependencies are **additive**, not circular
- Analytical logic flows forward only
- Assumptions are inherited, not recreated
- Cross-repository data dependencies are mediated through canonical artifacts
- If a new shared concept is required, it must be defined upstream and promoted explicitly

Changes to Repo 0, Repo 1, or canonical artifacts may invalidate downstream assumptions and require review.

---

## Note on Execution

This document defines **inferential dependency**, not execution order.

Repositories may be executed independently for development or testing,  
but analytical conclusions are valid only when dependency relationships and artifact contracts are respected.
