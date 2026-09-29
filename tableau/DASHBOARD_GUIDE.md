# Tableau Dashboard: HR Attrition Command Center

**Data source:** `hr_attrition_tableau.csv` (1,470 rows, one per employee, produced by the Python notebook). It includes the model's `RiskScore` / `RiskTier`, plus `AgeBand`, `IncomeBand`, `TenureBand` and `AnnualReplacementCost`.

## Calculated fields
```text
Attrition Rate          = SUM([Left]) / COUNT([EmployeeNumber])
Employees               = COUNTD([EmployeeNumber])
Leavers                 = SUM([Left])
Replacement Cost        = SUM([AnnualReplacementCost])
High-Risk Active Staff  = SUM(IF [Left] = 0 AND [RiskTier] = "High" THEN 1 ELSE 0 END)
Avg Monthly Income      = AVG([MonthlyIncome])
```

## Layout (1200 × 800)
| Zone | Visual | Fields |
|---|---|---|
| Top | 5 KPI tiles | Employees · Leavers · Attrition Rate · Replacement Cost · High-Risk Active Staff |
| Left middle | Horizontal bar | JobRole × Attrition Rate (sorted, coloured by rate) |
| Right middle | Highlight table | OverTime × IncomeBand → Attrition Rate |
| Left bottom | Stacked bar | TenureBand × Leavers, colour = RiskTier |
| Right bottom | Scatter | MonthlyIncome vs YearsAtCompany, colour = Attrition, size = RiskScore |
| Filters | — | Department, Gender, AgeBand, BusinessTravel (applied to all sheets) |

Use the **RiskTier = High & Left = 0** filter action to list the active employees HR should talk to first.
