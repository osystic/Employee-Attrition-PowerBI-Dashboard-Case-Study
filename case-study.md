# Employee Attrition Power BI Dashboard - Full Case Study

## Problem

The source case study contained many candidate variables that could plausibly relate to employee attrition. The challenge was to avoid a dashboard that simply visualized everything.

The report needed to narrow the variable set, avoid duplicate correlated stories, balance Power Query and DAX, remain interactive and presentation-ready, document the process, and avoid causal claims from descriptive data.

## Source model

Three employee-level datasets shared the same 4,410 unique EmployeeIDs:

1. general employee demographics, role, tenure and pay attributes;
2. employee survey attributes;
3. manager survey attributes.

Because all sources represented the same employee grain, Power Query was used to merge them into one consolidated analytical table.

## Data-quality decisions

The source audit found no duplicate or missing EmployeeIDs. Small amounts of missing data were retained as null rather than imputed because the work was descriptive and guessed values could create artificial patterns.

## Power Query architecture

1. Import each CSV as a staging query.
2. Promote headers and assign explicit data types.
3. Convert NA/blank survey values to null before numeric conversion.
4. Validate EmployeeID uniqueness.
5. Use the general employee table as the base Employees query.
6. Left-join employee survey attributes.
7. Left-join manager survey attributes.
8. Create analytical bands and readable labels.
9. Validate 4,410 rows and 4,410 distinct EmployeeIDs.
10. Load the consolidated Employees table.

## DAX measure layer

Representative measures:

Total Employees = DISTINCTCOUNT(Employees[EmployeeID])

Attrition Employees = SUM(Employees[AttritionFlag])

Attrition Rate = DIVIDE([Attrition Employees], [Total Employees], 0)

Company Attrition Rate = CALCULATE([Attrition Rate], REMOVEFILTERS(Employees))

Attrition Risk Index = DIVIDE([Attrition Rate], [Company Attrition Rate], 0)

## Driver selection

| Variable | Approx. grouped association | Treatment |
|---|---:|---|
| Total Working Years | 0.244 | Supporting lifecycle evidence |
| Years at Company | 0.227 | Headline lifecycle driver |
| Age | 0.210 | Headline lifecycle driver |
| Years with Current Manager | 0.188 | Supporting/actionable driver |
| Marital Status | 0.177 | Contextual driver |
| Environment Satisfaction | 0.122 | Employee experience driver |
| Job Satisfaction | 0.110 | Employee experience driver |
| Number of Companies Worked | 0.107 | Mobility/history driver |
| Work-Life Balance | 0.106 | Employee experience driver |
| Distance from Home | 0.043 | Deprioritized |
| Monthly Income | 0.032 | Deprioritized |
| Percent Salary Hike | 0.031 | Deprioritized |

These values were used as a visual-prioritization aid, not as proof of causality.

## Dashboard story

Page 1 answers: Where is attrition concentrated?

It includes KPIs, slicers, age, company tenure, marital status and work-life balance.

Page 2 adds employee-experience and lifecycle context through an age x tenure heatmap, environment satisfaction, job satisfaction, manager tenure, companies worked and total working years.

## Key findings

- Overall attrition: 16.12%
- Age 18-24: 39.18%
- Company tenure 0-1 years: 34.88%
- Age 18-24 and tenure 0-1 years: 60.47%
- Key intersection: 78 leavers of 129 employees
- Single employees: 25.53%
- Bad work-life balance: 31.38%
- Low environment satisfaction: 25.21%
- Low job satisfaction: 22.91%
- 0-1 years with current manager: 28.32%

## Correlation and interpretation

Age, company tenure and total working years can all reflect employee lifecycle stage. The report therefore uses age and company tenure as the main lifecycle story, total working years as corroborating context, and experience variables as a separate descriptive layer.

## Interactivity

The report uses compact multi-select dropdown slicers, synchronized filters, chart cross-filtering, tooltips and a conditionally formatted age-tenure matrix.

## Validation

The full-population baseline was checked at 4,410 employees, 711 leavers and 16.12% attrition. Final QA also covered report opening state, sort order, slicers, cross-filtering, heatmap values, sample-size context and consistency between the report and replication documentation.

## Outcome

The engagement produced a presentation-ready Power BI dashboard and a process guide designed to make the data preparation, model, DAX layer and visual story reproducible.

The strongest insight was an employee-lifecycle pattern in which attrition was heavily concentrated among younger employees and those early in company tenure, with additional descriptive differences across work-life balance, satisfaction and manager-tenure measures.

This is a diagnostic analytics artifact, not a causal model or individual employee prediction system.
