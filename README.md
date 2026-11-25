# Hospital operations dashboard (Power BI)

A Power BI report on hospital demand, capacity and workforce attendance, built from patient, weekly service and staff-schedule data.

**Status:** in progress — the data model and DAX measures are built; report pages are being finished.

**Tools:** Power BI · Power Query · DAX

## The question

How are services managing demand against capacity? Where do admissions, refusals, length of stay, patient experience and staff attendance point to pressure that stakeholders should act on?

## Data used

| Dataset | Main fields | Purpose |
| --- | --- | --- |
| Patients | Patient ID, name, age, arrival date, departure date, service, satisfaction | Patient volume, demographics, length of stay, service use and experience |
| Services Weekly | Week, month, service, available beds, patient requests, patients admitted, patients refused, satisfaction, staff morale, event | Weekly demand, capacity, admissions, refusals and operational change |
| Staff Schedule | Week, staff ID, staff name, role, service, present | Scheduled staffing and attendance by week, service and role |

## Approach

1. Define the operational questions the report has to answer.
2. Review and prepare each dataset in Power Query.
3. Build a connected model, checking relationship direction, key uniqueness and filter behaviour — deliberately avoiding joins that would multiply values and inflate totals.
4. Create a calendar table with a numeric month-sort column, and a week key matching the service and staff-schedule tables.
5. Write DAX measures for the core operational indicators.
6. Present the results as interactive report pages for stakeholders.

## Core measures

```dax
Total Requests   = SUM('Services Weekly'[patients_request])
Total Admissions = SUM('Services Weekly'[patients_admitted])
Total Refused    = SUM('Services Weekly'[patients_refused])
Admission Rate   = DIVIDE([Total Admissions], [Total Requests], 0)
Refusal Rate     = DIVIDE([Total Refused], [Total Requests], 0)
Average Patient Satisfaction = AVERAGE('Patients'[satisfaction])
Staff Attendance Rate = DIVIDE(SUM('Staff Schedule'[present]), COUNTROWS('Staff Schedule'), 0)
```

Average length of stay is calculated with AVERAGEX over patients that have both an arrival and a departure date.

## Skills demonstrated

Power Query preparation · star-schema modelling and relationship design in Power BI · DAX measures and KPIs · time intelligence with a calendar table · report design for operational stakeholders.

---

By [Chantelle Quarshie](https://chantelle-quarshie.github.io/) — Data Analyst & Data Visualisation Professional, London.
