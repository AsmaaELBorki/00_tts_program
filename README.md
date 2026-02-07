# Tracking the Sun (TTS) Program Canon and Analytical Architecture

## The Program Answers The following Question: 

**Given a residential solar installation in California, is this system sized appropriately for its context — or does it deviate in a way that plausibly indicates oversizing, undersizing, or elevated design risk?**

Answering this question reliably is not trivial.  
Raw system size alone is not informative without context: installation time, location, typical scalability as well as normal design variation threshholds at a given size - all matter.


This program is built to answer that question **systematically**, by decomposing it into ordered analytical steps that make deviation interpretable rather than arbitrary.

---

## Real World Applications: 

The outputs of this program are applicable wherever **residential solar sizing decisions need to be evaluated, compared, or flagged without assuming intent or causality**, including:

- **Homeowners and advisors** assessing whether a system appears unusually large or small relative to comparable installations  
- **Installers and designers** benchmarking system sizing practices against observed norms  
- **Financiers, insurers, and analysts** identifying installations with elevated uncertainty or atypical design profiles  
- **Researchers and market analysts** studying how residential solar systems scale in practice across time and geography  

The program does not render judgments or prescribe actions.  
It produces **context-aware signals** that help distinguish normal design variation from atypical sizing patterns.

---

## This Repository's Purpose: 

This repository defines the **canonical analytical questions, scope, ordering, and logical constraints** of the *Tracking the Sun* program.

It does **not** contain analysis or data products.

Its role is to make explicit:
- Questions and their order. 
- The analytical preconditions that govern downstream work  

This repository exists so that all subsequent work can be understood as part of a **single, coherent analytical system**, rather than a collection of disconnected analyses.

---

## Program-Level Repositories

The *Tracking the Sun* program is governed by **two program-level repositories**, each with distinct and non-overlapping authority.

### Repo 0 — Program Canon (this repository)

Defines the **analytical logic of the program**:
- core questions
- scope and boundaries
- analytical ordering
- prohibitions and invariants

Repo 0 governs **how analysis is allowed to proceed**, but does not own data or analytical outputs.

---

### Canonical Artifacts Repository

Serves as the **canonical archival layer** for cross-repository analytical outputs.

It:
- stores frozen artifacts produced by upstream analytical repositories  
- preserves agreed-upon analytical states for downstream reference  
- enables continuity across analytical stages through explicit schemas, invariants, and documented handoffs  

#### Current operational role

In the present implementation, the Artifacts Repository functions as an **authoritative archival store**, not as an executable dependency layer.

- Analytical repositories do not programmatically ingest artifacts from this repository  
- Inputs are staged locally within each repository  
- Continuity across stages is enforced through schema discipline, invariant definitions, and explicit human-mediated handoffs  

This design reflects a **research-stage workflow**, prioritizing analytical stability, inspection, and epistemic control over pipeline automation.

#### Intended role

In a productionized or extended version of *Tracking the Sun*, the Artifacts Repository would function as an executable dependency layer, replacing manual inputs with versioned data contracts and enforcing downstream continuity programmatically.

This capability is intentionally deferred until analytical structures and invariants are fully stabilized.

---

## Program Value

This program is designed to produce a **reliable analytical substrate** for understanding residential solar system sizing behavior in California.

Its value lies in:

- Establishing **defensible reference frames** for what constitutes “typical” system size  
- Separating **measurement, structure, scaling behavior, and evaluation** so conclusions are interpretable  
- Enabling **abnormality and sizing-risk assessment** (both over-sizing and under-sizing) without inventing structure downstream  
- Making analytical decisions **transparent, auditable, and reusable**

---

## Program Scope

- **Dataset:** NREL *Tracking the Sun* (publicly released)
- **Geographic focus:** **California only**
- **Population:** Residential solar systems only  
  (`customer_segment == "RES"`)

All findings, baselines, structures, and evaluations produced by this program apply **only** to residential solar installations in California.

---

## Canonical Entity, Identity, and Analytical Grain

This program operates on a **single canonical analytical entity**.

**Entity:**  
A *physical residential photovoltaic system*.

**Canonical identifier:**  
`tts_link_id`.

**Entity definition:**  
All records sharing the same `tts_link_id` are treated as referring to the same physical system.

**Canonical analytical grain:**  
One row per `tts_link_id`.

**Identity rules:**
- `tts_link_id` is the only identifier permitted to represent a system  
- Provider-specific identifiers (e.g. `system_id_1`, `system_id_2`) are non-canonical and may not be used as system keys  
- Row-level uniqueness does not imply system-level uniqueness  

**Invariant:**  
No system-level artifact may be materialized unless `tts_link_id` is unique in the output.

This invariant applies to **all repositories that claim to produce system-keyed outputs**, including baseline artifacts, residuals, regime mappings, and abnormality scores.

---

## Analytical Posture and Boundaries

- Analyses are **descriptive and structural by design**
- Evaluation of sizing abnormality considers **both undersizing and oversizing**
- Predictive and evaluative work is permitted **only within upstream constraints**
- Measurement limits are respected as declared by the dataset owners

### Non-Goals

- No causal attribution  
- No policy evaluation  
- No counterfactual claims  
- No inference beyond declared measurement limits  

---

## Data Ownership and Provenance

This program does **not** own or generate the underlying data.

All statements about data collection, reporting, and measurement are derived **exclusively from declarations made by the dataset owners (NREL)** and accompanying public documentation.

The data-generation, recording, and reporting process — including known limitations, incentives, omissions, and comparability constraints — is documented in **Repo 1**.

No repository in this program is permitted to reinterpret or extend those declarations.

---

## Analytical Architecture and Logical Ordering

The program is organized as a **strictly ordered analytical stack**.

- **Repo 0** defines analytical logic and constraints  
- **The Artifacts Repository** defines canonical analytical outputs and data continuity  

All analytical repositories depend on **both**.

Each analytical repository answers a **real-world applied question** and a corresponding **analytical question**, and establishes **preconditions** for downstream work.

---

## Repository Stack (Canonical)

### [Repo 1 — Data Generation & Measurement](https://github.com/AsmaaELBorki/01_tts_data.git)

**Applied question:**  
What do these data actually represent, and what limits do their recording and reporting processes place on interpretation?

**Analytical question:**  
How were the data recorded, reported, and structured as declared by the dataset owners?

**Responsibilities:**
- Document declared data-generation processes  
- Record known biases, omissions, and comparability limits  
- Establish measurement validity constraints  

**Produces:**  
- Measurement admissibility rules  
- Explicit inference prohibitions  

**Prohibited:**  
- Speculation beyond declared documentation  
- Analytical transformation or modeling  

---

### [Repo 2 — Canonical System Size Baseline](https://github.com/AsmaaELBorki/02_tts_baselines.git)

**Applied question:**  
What system size is typical for residential solar installations in California, given when and where they were installed?

**Analytical question:**  
What is the expected residential system size in a given context?

**Responsibilities:**
- Establish defensible size baselines  
- Quantify uncertainty and temporal drift  
- Materialize canonical baseline artifacts  

**Produces:**  
- Expected size distributions  
- **System-keyed (one row per `tts_link_id`) baseline artifacts**

**Prohibited:**  
- Structural interpretation  
- Configuration analysis  
- Prediction  

---

### [Repo 3 — Within-Size Structural Configuration](https://github.com/AsmaaELBorki/03_tts_configuration.git)

**Applied question:**  
When two residential systems are similar in size, in what meaningful ways can their designs still differ?

**Analytical question:**  
When system size is held constant, what system characteristics vary in structured, non-trivial ways?

**Responsibilities:**
- Consume canonical baseline artifacts  
- Identify structural degrees of freedom at fixed size  
- Define configuration equivalence classes  

**Produces:**  
- Structural constraints  
- Admissible variation space  

**Prohibited:**  
- Re-derivation of upstream baselines  
- Scaling analysis  
- Regime formation  
- Risk evaluation  

---

### [Repo 4 — Scaling Regimes & Deviation Geometry](https://github.com/AsmaaELBorki/04_tts_scaling.git)

**Applied question:**  
How does residential solar system size scale in practice, and what forms of deviation are typical versus unusual?

**Analytical question:**  
Given size and structure, how does system behavior scale, and where do stable regimes and deviation surfaces emerge?

**Responsibilities:**
- Formalize scaling behavior  
- Identify regime boundaries  
- Define deviation geometry  

**Produces:**  
- Scaling regimes  
- Deviation surfaces  
- Regime membership mappings  

**Prohibited:**  
- Risk scoring  
- Abnormality evaluation  
- Prediction  

---

### [Repo 5 — Evaluation & Risk Surfaces](https://github.com/AsmaaELBorki/05_tts_abnormality_directionality_risk.git)

**Applied question:**  
Is a given residential solar system unusually sized for its context, and does that deviation plausibly indicate oversizing, undersizing, or benign variation?

**Analytical question:**  
Given regime-aware scaling behavior, how unusual is a system and in which direction does the deviation occur?

**Responsibilities:**
- Evaluate deviation likelihood  
- Assess directional abnormality (over- and under-sizing)  
- Assign sizing-risk indicators  

**Produces:**  
- Abnormality scores  
- Directional sizing-risk flags  

**Prohibited:**  
- Introduction of new structure  
- Reinterpretation of upstream definitions  

---

## Governing Invariant

> **No repository is permitted to answer a question whose analytical preconditions — including required upstream artifacts, canonical entity definitions, and analytical grain — have not already been settled upstream.**


