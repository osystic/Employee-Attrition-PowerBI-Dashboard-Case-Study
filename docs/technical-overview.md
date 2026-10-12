# Technical Overview

## Analytical grain
One row per employee.

The three source datasets shared a common EmployeeID population, so they were merged in Power Query rather than preserved as three one-to-one tables.

## Power Query responsibilities
- source ingestion
- explicit typing
- NA/blank to null handling
- EmployeeID validation
- left joins
- removal of constant fields
- readable category labels
- ordered age, tenure, history and satisfaction bands

## DAX responsibilities
- total employees
- attrition employees
- retained employees
- attrition rate
- company benchmark
- attrition risk index
- tooltip helpers
- small-sample warning logic

## Report architecture
Page 1: Attrition Overview
Page 2: Drivers & Employee Experience

Power Query handles reusable row-level shaping. DAX handles calculations that must recompute under report filter context.
