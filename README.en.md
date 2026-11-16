# OEE and Line Downtime Dashboard – Packaging

[Español](README.md) | English

A **Power BI** dashboard that measures OEE at a bottling plant through its three components (availability, performance and quality), identifies the highest-impact downtime down to sub-cause and equipment level, and quantifies the effect of improvement actions.

![Operational performance]

## Business problem

Line stoppages were recorded in detail but never linked to production. There was no quick way to answer how much OEE is lost and why, which causes and equipment explain the downtime, which lines and shifts perform worst, and whether improvements are working.

**Key question:** how can production and downtime records be turned into indicators that prioritize maintenance and continuous improvement actions?

## Key results

| Indicator | Value |
|---|---|
| Annual OEE | **78.6%** (85% target, −6.4 pp gap) |
| Availability / Performance / Quality | 89.8% / 88.8% / 98.5% |
| Downtime hours | 2,673 h (≈ 1.56 M cases not produced) |
| OEE before vs. after improvements | 74.1% → **82.9% (+8.8 pp)** |
| Downtime hours before vs. after | **−37%** |
| Changeover time (SMED) | 29.4 → **19.2 min (−35%)** |

## Main findings

- **Availability and performance explain 94% of the OEE loss**; quality has a minor impact.
- **Maintenance (31.7%) and Machine setup (26.2%)** account for 58% of downtime and have the longest stops (~25 min).
- **11 of 18 causes explain 80%** of downtime; mechanical maintenance is the top cause (15%).
- All three lines have similar OEE, but **L1 accounts for 57% of lost cases** due to its higher speed.
- **Shift C** has the lowest OEE (77.1%) because of lower performance, not more downtime.

## Recommendations

1. Preventive maintenance plan for sensors, filler bearings, transmission and electrical panel, with monthly MTTR and MTBF tracking.
2. Extend SMED to calibrations, start-ups and product changes, replicating the changeover results.
3. Prioritize L1: each hour recovered is worth more than twice as much as on L2.
4. Review shift C speed and practices, standardizing shift A practices.

## Dashboard

| Downtime analysis | Improvement impact |
|---|---|
|**[Proyecto_OEE_page-0001)](img/Proyecto_OEE_page-0001.jpg)** **[Proyecto_OEE_page-0002](img/Proyecto_OEE_page-0002.jpg)** |**[Proyecto_OEE_page-0003](img/Proyecto_OEE_page-0003.jpg)**|


## Technical solution

- **Star schema:** 2 fact tables (production and downtime) and dimensions for calendar, line, shift and stoppage (category → cause → sub-cause → equipment).
- **55 DAX measures** organized in folders: OEE and components, MTTR, MTBF, Pareto with RANKX and cumulative %, loss waterfall, lost cases and Before/After comparison.
- **Power Query** to type the data and split the date and time of each stoppage.
- **Data:** 3,285 production records and 7,821 stoppages across 3 lines and 3 shifts (year 2025).

![Data model]

```DAX
OEE = [Disponibilidad] * [Rendimiento] * [Calidad]
MTTR = DIVIDE([Tiempo Parada], [Número de Paradas], 0)
OEE Antes = CALCULATE([OEE], CalendarioDAX[Periodo] = "Antes")
```

## Tools

Power BI · Power Query · DAX · Dimensional modeling · Data visualization

## Repository structure

```
├── README.md            Spanish version
├── README.en.md         This document
├── docs/Informe_OEE.pdf Full analysis report (Spanish)
├── img/                 Dashboard and model screenshots
└── (.pbix file and data, if published)
```

**[View full report (PDF, Spanish)]**

## Notes

Fictitious company (Embotelladora SAC) and synthetic data built for this project; they do not represent results from any real company.

## Author

**Sergio Aguilar Dinis** – Data Analyst | Business Intelligence
[LinkedIn](https://www.linkedin.com/in/sergio-aguilar-dinis-4766b858) · [Portfolio](https://fancy-coyote-67e.notion.site/PORTFOLIO-ES-b44f7f51a593839abe7b0196b748def2)
