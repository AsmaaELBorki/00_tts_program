# Program Overview

This document explains the **design rationale** behind the *Tracking the Sun* program.

It does not define scope, repository roles, or analytical authority.  
Those are fixed in the canonical README.

The purpose of this document is to explain **why the program is structured the way it is**, and what problems that structure is designed to prevent.

---

## Modularization: 

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

## Separation & Semantic Drift Prevention 

As analytical work progresses, there is a natural tendency for:
- variables to shift meaning
- baselines to be reinterpreted
- exceptions to become informal rules
- early assumptions to be forgotten

This phenomenon—semantic drift, is one of the primary sources of analytical error in long-lived projects.

The program is explicitly separated into repositories so that:
- meanings are fixed before they are reused
- later work cannot silently redefine earlier constructs
- changes to assumptions must propagate deliberately

Separation ensures that concepts retain **stable meaning over time**, even as new questions are introduced.

---

## Upstream / Downstream Discipline

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

## Canonical Artifacts

The canonical artifacts repository exists to record and preserve promoted analytical results that are treated as stable reference points within the program.

While artifacts are not currently enforced as executable dependencies, their versioning and centralization serve to freeze analytical meaning at specific stages, making changes explicit rather than implicit and ensuring that downstream interpretation remains traceable.


---

## Outputs 

Each repository produces outputs that are consumed downstream **without reinterpretation**.

This rule exists to prevent:
- retroactive adjustment of results to fit later findings
- silent correction of inconvenient structure
- blending of analytical stages

By passing outputs unchanged:
- errors are easier to locate
- uncertainty remains visible
- responsibility for interpretation is localized

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

## Status

The architecture is active and stabilized.

Changes to structure are introduced deliberately, documented explicitly, and propagated through the program rather than applied locally.

Propagation occurs through regeneration of upstream repositories and updates to canonical artifacts, not through local downstream modification.


