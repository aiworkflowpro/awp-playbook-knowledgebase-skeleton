---
document_id: awp-knowledge-management-standard/methodology/business/kb-method-business-metrics
language: en
publication: public
title: "Business Methodology  -  Operational Metrics"
---

# Business Methodology  -  Operational Metrics

> Manage periodic business data output: cycle types, metric comparison, data sources, data masking.
> Inherits all constraints from `kb-method-business-general.md`; this file only adds metric-specific sections.

## One. What to Manage

Daily reports, weekly reports, monthly reports, quarterly reports, annual reports, metric dashboards, advertising data, traffic data, sales data. Answer one question: how is the business performing across different time granularities.

## Two. Five Principles

- **Store aggregated cycles, not real-time transactions**: Real-time data belongs to external reporting tools or accounting software.
- **Comparability is the baseline**: The same metric across different cycles must use identical definitions and statistical methods.
- **Data sources are traceable**: Every metric can be traced back to its source — which tool, which script, or manual entry.
- **Masking first**: Replace absolute numbers with ratios, ranges, or period-over-period comparisons whenever possible.
- **Data is not decision**: This section stores data only; analysis and decisions belong to strategy decisions or project archives.

## Three. Required Sections

| Section | Content |
|---------|---------|
| Metadata | Nine fields plus cycle type plus cycle identifier |
| Key Metrics | Table for this cycle: metric / current period / previous period / period-over-period |
| Data Sources | Each metric's source: tool, script, or manual export, plus date |
| Anomalies | Anomalous values in this cycle and explanations |
| Action Items | Next steps derived from data; write briefly |

## Four. Cycle Type Glossary

| Cycle | Frequency | Typical Use |
|-------|-----------|-------------|
| Daily | Every day | High-frequency trading, live streaming, customer service, public sentiment |
| Weekly | Every week | Advertising, content publishing, event monitoring |
| Monthly | Every month | Operational monthly reports, metric benchmarking |
| Quarterly | Every quarter | Strategy review, target benchmarking |
| Annual | Every year | Annual summary, planning basis |
| Special | As needed | Campaign post-mortems, project settlement |

## Five. Comparison Rules

Each periodic report must include at least one of the following comparisons:

| Comparison | Meaning |
|-----------|---------|
| Period-over-period | Compared to the previous cycle |
| Year-over-year | Compared to the same cycle last year; common for quarterly and annual reports |
| Trend | Direction over the last N cycles |
| Target comparison | Compared to target value |

## Six. Data Masking Rules

| Recommended | Not Recommended | Reason |
|-------------|-----------------|--------|
| Month-over-month revenue +15% | Monthly revenue 123k | Period-over-period supports decision-making; absolute values are sensitive |
| Gross margin 35% to 40% | Gross margin 37.6% | Ranges are sufficient |
| Users in 1000s magnitude | 1247 users | Order of magnitude replaces exact counts |
| Ad ROI greater than 3x | Ad spend 8500, conversion 26000 | Use ratios instead of details |

When absolute values are necessary, upgrade the file's sensitivity level to restricted and open it only when needed; more sensitive data should not enter the knowledge base.

## Seven. Recommended Sections

| Section | Description |
|---------|-------------|
| Benchmark Analysis | Comparison with competitors or industry averages |
| Historical Trend Chart | Trend visualization or placeholder chart |
| Alert Thresholds | Thresholds that trigger action |
| Next Period Forecast | Forecast based on trends |

## Eight. Industry Optional Metrics

| Business Model | Recommended Additional Metrics |
|---|---|
| Content Creation | Views, engagement, followers, completion rate, viral rate |
| E-commerce | GMV, advertising-to-sales ratio, category rank, return rate, inventory turnover |
| Online Services | MAU, DAU, retention, churn rate, monthly recurring revenue, revenue per user |
| Consulting Services | Deals in progress, signed deals, deliveries, customer satisfaction |
| Education | Enrollment, course starts, completion rate, renewal rate |
| Brick-and-mortar Retail | Foot traffic, average order value, table turns, sales per square foot |
| Manufacturing | Capacity, yield rate, delivery time, failure rate |
| Nonprofit | Donations, volunteers, beneficiaries, number of projects |

Industry optional metrics are only added as rows to the "Key Metrics" table, not as new top-level sections.

## Nine. Naming

| Cycle | Naming Pattern | Notes |
|-------|---|---|
| Daily Report | `daily-report-YYYYMMDD.md` | Or consolidated by month as `daily-report-YYYY-MM.md` |
| Weekly Report | `weekly-report-YYYY-W{ww}.md` | |
| Monthly Report | `monthly-report-YYYY-MM.md` | |
| Quarterly Report | `quarterly-report-YYYY-Q{q}.md` | |
| Annual Report | `annual-report-YYYY.md` | |
| Special | `{topic}-{year-month}.md` | |

## Ten. Archiving

- Cross-year reports are automatically archived to `archive/{year}/`.
- Monthly, quarterly, and annual reports can have an index file `{type}-index.md` listing all historical reports for easy trend comparison.

## Eleven. Deduplication Boundaries

| Content | Belongs To | Does Not Belong To |
|---------|-----------|-------------------|
| Real-time transactions, individual transactions | External reports or accounting software | Operational metrics |
| Decisions behind data | Strategy decisions | Operational metrics |
| Projects triggered by data | Project archives | Operational metrics |
| Latest snapshot of single asset | Operational assets | Operational metrics (store aggregates only) |
| Long-term business model summary | Brand operations domain | Reference relationship |
| Personal financial data | Personal area finances | Business operational data |

## Twelve. Checklist

- [ ] Metadata contains nine fields plus cycle type plus cycle identifier
- [ ] Key metrics table includes at least one type of comparison
- [ ] Data sources are traceable
- [ ] Anomalies are explained
- [ ] Action items are clear, not just numbers
- [ ] Absolute values follow masking rules
- [ ] Restricted-level data marked for read-on-demand access
- [ ] Naming follows cycle pattern
- [ ] Cross-year reports archived

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|--------|
| 2026-08-07 | Migrated from operational metrics specification and generalized |
