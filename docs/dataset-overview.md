# Dataset Overview

This program is built on the NREL *Tracking the Sun* dataset.

The dataset captures detailed information about distributed solar photovoltaic installations across the United States over multiple decades.

---

## Coverage

The dataset includes:
- residential, commercial, and other customer segments
- installations spanning from the late 1990s to 2024
- technical, financial, geographic, and configuration-related attributes

Coverage varies by year, provider, and system type.  
This variability is structural, not incidental.

---

## Structure

The dataset is wide rather than tall.

It includes:
- multiple identifier fields
- mixed temporal representations
- repeated component families (e.g. modules, inverters)
- indicator flags encoded as integers
- measurements expressed in physical and monetary units

Several columns encode multiplicity through positional suffixes (`_1`, `_2`, `_3`) rather than normalization. This reflects how systems are reported, not how they should be interpreted analytically.

---

## Known Characteristics

The dataset exhibits:
- uneven reporting precision across time
- provider-specific gaps
- evolving technology representations
- mixed use of nulls, zeros, and structural absences

These characteristics are not treated as errors by default.  
They are constraints that shape what questions can be asked.

---

## Analytical Implications

Because of its temporal depth and structural heterogeneity, the dataset does not support unconstrained exploration.

Meaningful analysis requires:
- explicit cohorting
- careful handling of time
- disciplined treatment of missingness
- separation of description, pattern detection, and prediction

These requirements motivate the architectural decisions defined in this repository.

---

## Relationship to the Architecture

This document describes what the dataset contains.  
It does not define how it is cleaned, transformed, or analyzed.

Those decisions are governed by:
- column roles
- data contracts
- violation definitions
- canonical schema

All analytical work downstream is expected to respect these constraints.

---

## Status

The dataset is treated as fixed input.

Understanding of its structure evolves as analysis proceeds.  
Interpretation is constrained by architecture, not convenience.
