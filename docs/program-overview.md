# Program Overview

This document explains the **design rationale** behind the *Tracking the Sun* program.

It does not define scope, repository roles, or analytical authority.  
Those are fixed in the canonical README.

The purpose of this document is to explain **why the program is structured the way it is**, and what problems that structure is designed to prevent.

---

## Why Modularization Matters

The *Tracking the Sun* dataset is large, heterogeneous, and structurally uneven across time, geography, and reporting programs.

Attempting to exhaust such a dataset in a single analytical pass encourages:
- uncontrolled scope expansion
- implicit assumptions
- silent reuse of intermediate results
- loss of interpretability as analysis grows

Modularization forces each analytical step to:
- answer a narrow class of questions
- expose its assumptions explicitly
- produce outputs that can be inspected independently

This makes reasoning **composable** rather than accumulative, and allows the program to grow without collapsing into a single opaque analysis.

---

## Why Separation Prevents Semantic Drift

As analytical work progresses, there is a natural tendency for:
- variables to shift meaning
- baselines to be reinterpreted
- exceptions to become informal rules
- early assumptions to be forgotten

This phenomenon—semantic drift—is one of the primary sources of analytical error in long-lived projects.

The program is explicitly separated into repositories so that:
- meanings are fixed before they are reused
- later work cannot silently redefine earlier constructs
- changes to assumptions must propagate deliberately

Separation ensures that concepts retain **stable meaning over time**, even as new questions are introduced.

---

## Why Upstream / Downstream Discipline Exists

Not all analytical questions are logically independent.

Some questions require others to be settled first:
- size must be defined before structure can be compared
- structure must be understood before scaling can be characterized
- scaling behavior must be established before deviation can be evaluated

Upstream/downstream discipline enforces this ordering.

Repositories are not arranged by convenience or tooling, but by **inferential dependency**.  
A downstream repository may only reason using objects that have already been defined upstream.

This prevents post-hoc justification and ensures that conclusions are conditional on clearly established preconditions.

---

## Why Canonical Artifacts Are Used

As cross-repository dependencies increased, passing files manually between repositories became a source of ambiguity and semantic drift.

The canonical artifacts repository exists to:
- freeze agreed-upon analytical results
- enforce continuity across analytical stages
- prevent silent modification of upstream outputs
- make dependencies explicit rather than implicit

Artifacts do not introduce new logic or analytical authority.  
They serve as a shared analytical memory, allowing downstream reasoning to proceed without re-derivation or reinterpretation.

---

## Why Outputs Are Passed Unchanged

Each repository produces outputs that are consumed downstream **without reinterpretation**.

This rule exists to prevent:
- retroactive adjustment of results to fit later findings
- silent correction of inconvenient structure
- blending of analytical stages

By passing outputs unchanged:
- errors are easier to locate
- uncertainty remains visible
- responsibility for interpretation is localized

As the program matured, this principle was formalized through the introduction of a canonical artifacts repository.

Not all outputs are passed downstream.  
Only outputs that have been explicitly promoted to artifacts—because their grain, semantics, and ownership are stable—are treated as fixed inputs by downstream repositories.

Exploratory or intermediate outputs remain local to their producing repository and are not relied upon elsewhere.

If an output is insufficient, the correct response is to revise the upstream repository—not to patch the downstream one.

---

## Why the Program Evolved This Way

The program did not begin with this level of structure.

It evolved as the scope of inquiry expanded and the limitations of monolithic analysis became clear:
- early exploratory questions revealed the need for stable baselines
- attempts to compare installations surfaced reporting constraints
- scaling analysis exposed the need for regime-aware reasoning
- evaluative questions required prior structure to be explicit

The architecture is therefore not theoretical—it is **reactive to analytical pressure**.

Each layer exists because proceeding without it led to ambiguity, fragility, or misinterpretation.

---

## What This Document Is (and Is Not)

This document:
- explains design choices
- records architectural intent
- provides context for future modifications

It does not:
- define analytical rules
- describe data properties
- authorize inference
- replace the canonical README

Those functions live elsewhere by design.

---

## Status

The architecture is active and stabilized.

Changes to structure are introduced deliberately, documented explicitly, and propagated through the program rather than applied locally.

Propagation occurs through regeneration of upstream repositories and updates to canonical artifacts, not through local downstream modification.


