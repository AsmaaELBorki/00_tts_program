# Data Contract

This document defines how data is allowed to be interpreted within the architecture.

It does not describe how data is cleaned.
It defines what “valid,” “usable,” and “out of scope” mean.

All downstream repositories inherit these constraints.

---

## installation_date

**Role:** temporal

### Raw State

- source type: string
- format: inconsistent
- precision: mixed (year-only, partial, full date)
- nullability: allowed

In raw form, `installation_date` is valid but not analytically usable.

---

### Canonical Representation

All time-based analysis relies on a derived field:

- `installation_year` (integer)

This defines the minimum temporal resolution required for inclusion in analytical workflows.

No analysis relies directly on raw date strings.

---

### Reporting Window

- earliest valid year: 1998
- latest valid year: current reporting year

Values outside this window are excluded from time-based analysis.

---

### Validity and Violations

**Hard violations**
- unparseable values
- future dates
- values outside the reporting window

Hard violations exclude records from all time-based analysis.

**Soft violations**
- missing month or day
- provider-specific reporting gaps

Soft violations restrict usage but do not require exclusion.

**Structural absences**
- missing values in early cohorts with known reporting limitations

Structural absences are not treated as data quality failures.

---

### Allowed Assumptions

- installation year reflects commissioning year
- year-level aggregation is acceptable where finer precision is unavailable
- reporting gaps are cohort- and provider-specific rather than random

These assumptions are explicit and may not be silently altered downstream.
