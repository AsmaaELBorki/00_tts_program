# Column Role Taxonomy

This architecture classifies every column by role.

Roles are authoritative. They define how a column is allowed to behave analytically.
Ad-hoc rules are not introduced downstream.

Every column must declare exactly one role.

---

## identifier

Identifiers represent entities. They are not measurements and do not summarize.

Identifiers exist to distinguish records, not to be analyzed.

Required:
- nullability semantics
- uniqueness expectation
- stability over time

Identifiers are never:
- aggregated
- imputed
- coerced into meaning

Any transformation beyond validation invalidates the identifier.

---

## temporal

Temporal fields anchor observations in time.

They are structural. They determine how cohorts are formed, how evolution is measured,
and what claims about change are allowed.

Required:
- canonical representation
- reporting window
- allowed aggregation levels
- violation classification

Temporal aggregation refers to loss of precision, not arithmetic combination.

Allowed:
- coarsening (e.g. date → year)

Disallowed:
- reinterpretation of temporal meaning
- inference beyond stated resolution

---

## measurement

Measurements represent quantitative values tied to physical or economic units.

They describe magnitude, not identity.

Required:
- explicit unit
- valid numeric bounds
- zero vs null semantics
- physical or economic plausibility constraints

Measurements may be aggregated only where units and scope permit.
Aggregation changes meaning and must be explicit.

---

## categorical

Categorical fields describe qualitative attributes.

They are labels, not quantities.

Required:
- value domain (open or closed)
- null semantics
- grouping intent

Categorical values have no ordinal meaning unless explicitly stated.

---

## indicator

Indicators encode state or presence.

They are flags, not measurements.

Required:
- encoding definition (e.g. 0/1)
- null vs false semantics
- interpretation of absence

Magnitude is not meaningful. Semantics are.

---

## repeated_component

Repeated components represent structured multiplicity
(e.g. `*_1`, `*_2`, `*_3`).

They encode composition, not variation.

Required:
- cardinality rules
- absence vs non-applicability semantics
- aggregation constraints

Presence and absence are analytically meaningful and must be interpreted consistently.

---

## derived

Derived fields do not exist in raw data.

They are created downstream under defined constraints.

Required:
- source fields
- derivation intent (high-level)
- downstream scope

Derived fields exist only in canonical representations.
