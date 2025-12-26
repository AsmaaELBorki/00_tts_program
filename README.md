# Tracking the Sun — Analytical Program

This repository serves as the **program-level overview and governance layer** for a modular analytical program built on the NREL *Tracking the Sun* dataset.

The program is structured as a sequence of independent but related repositories, each answering a specific class of analytical questions about solar system design, scaling behavior, temporal evolution, and risk patterns.

This repository contains **no analysis code**.  
Its purpose is to explain structure, dependencies, and analytical contracts
across the program.

---

## Program Motivation

The *Tracking the Sun* dataset captures detailed information about distributed solar installations across the United States over multiple decades.

Rather than treating the dataset as a single exploratory exercise, this program approaches it as a **systems-level analytical object**, decomposed into focused, traceable analytical modules.

Each module:
- answers a specific question class
- produces explicit outputs
- feeds downstream reasoning without duplication

---

## Repository Map

The program is organized into the following repositories:

### Repo 1 — System Size Determinants  
**Purpose:**  
Understand what contextual, technical, and temporal factors contribute to observed system size.

**Outputs:**  
System-size features and contextual baselines used downstream.

---

### Repo 2 — System Configuration & Inverter Architecture  
**Purpose:**  
Analyze how systems of a given size are configured, with emphasis on inverter count, capacity per inverter, and installer behavior.

**Outputs:**  
Configuration-level features describing inverter architecture and scaling.

---

### Repo 3 — Scaling, Regimes, and Deviation  
**Purpose:**  
Examine expected scaling behavior, regime formation, and deviations across time and geography.

**Outputs:**  
Baseline scaling models and deviation surfaces.

---

### Repo 4 — Predictive Signals, Risk, and Oversizing  
**Purpose:**  
Use features derived from earlier repositories to estimate the likelihood and direction of configuration deviation and potential oversizing.

**Outputs:**  
Predictive features and baseline models.

---

## Role of Time Across the Program

Time is treated differently across repositories:

- **Repo 1 & Repo 2:**  
  Time is a conditioning context (e.g., cohorting, comparison across periods).

- **Repo 3:**  
  Time is an evolutionary signal used to identify regime shifts and structural change.

- **Repo 4:**  
  Time is a predictive feature used in risk and deviation modeling.

This separation prevents conflating descriptive, evolutionary, and predictive claims.

---

## Analytical Substrate

All downstream repositories assume a **single trusted analytical substrate**:
- validated schema
- consistent column semantics
- documented assumptions

These contracts are defined in the `docs/` directory of this repository.

Downstream repositories do not re-validate raw data unless explicitly stated.

---

## How to Navigate This Program

1. Start with this repository to understand scope and structure.
2. Review `docs/data-contract.md` to understand shared assumptions.
3. Explore individual repositories based on analytical interest.
4. Follow outputs forward; repositories are not nested or duplicated.

---

## Scope Boundaries

This program is:
- observational, not causal
- focused on analytical reasoning, not policy prescription
- modular by design to support extension and reuse

---

## Status

The program is actively under development.  
Repository structures are stable; analytical content evolves iteratively.
