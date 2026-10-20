---
document_id: awp-knowledge-management-standard/methodology/personal/kb-method-personal-finance
language: en
publication: public
title: "Personal Finance Domain Methodology"
---

# Personal Finance Domain Methodology

> Manage one thing: how to write files in personal finance domain (investing, insurance, major decisions, asset archive).
> Inherits personal domain constraints (privacy classification, decision/record/reference three-output skeletons), this file only declares finance-specific additions.

## Responsibility

Finance domain records "wealth" — investment strategy, insurance planning, major decisions, asset archives. It answers background Agent needs when making financial advice, consumption decisions, tax planning.

**Not daily accounting** — that's accounting apps' job. Moving transactions into knowledge base neither maintains them nor adds decision value.

## Four Design Principles

- **Strategy not transactions** — store decisions and long-lived info only, not high-frequency flows.
- **Numbers masked as much as possible** — use ranges, don't write exact amounts.
- **Privacy defaults to read-on-demand** — content with amounts or accounts doesn't enter default context.
- **Major spending must post-mortem** — what matters isn't the spend, but why spend and is it worth.

## Required Files

| File | Type | Required Content |
|------|------|---------|
| `investment-strategy.md` | Decision | Asset allocation principles + risk tolerance + cycle + review records |
| `insurance-list.md` | Reference | Insurance types + coverage scope + renewal dates (no policy numbers) |

## Recommended Files

| File | Type | Recommended Content |
|------|------|---------|
| `decision-{topic}.md` | Decision | Major spending or investment "why + tradeoffs + post-mortem" |
| `net-worth-snapshot-{year}.md` | Record | Quarterly or annual asset structure (category + ratio, no absolute numbers) |
| `tax-memo.md` | Reference | Tax filing rhythm + deductions + historical issues |

## Add Per Lifestyle

| Situation | Additional File | Privacy Level |
|------|---------|---------|
| Own real estate | `property-archive.md` (address summary, purchase, loan timeline, no complete address) | Sensitive or Restricted |
| Hold business equity | `equity-list.md` | Sensitive or Restricted |
| Cross-border assets | `cross-border-{country or currency}.md` | Sensitive |
| Have debt | `debt-list.md` (type, interest rate, term, no principal) | Sensitive |
| Support dependents | `family-spending-strategy.md` | Sensitive |

## Privacy Defaults

| File | Default Level | Notes |
|------|---------|------|
| Investment Strategy | Internal; specific config drops to Sensitive | — |
| Insurance List | **Sensitive** | Contains insurer & types |
| Net Worth Snapshot | **Sensitive** | Contains asset structure |
| Real Estate / Equity / Cross-border | **Sensitive or Restricted** | Depends on specifics |
| Bank/Broker account password | **Restricted** | Not into KB; use password manager |
| Full policy number, card number | **Restricted** | Not into KB |

## Number Masking

| Good | Bad | Reason |
|----|-----|------|
| "Stock allocation 40%" | "Stocks 123k" | Ratios support decisions; absolutes unnecessary |
| "Cash covers 6 months expenses" | "Cash 85k" | Multipliers are reference; absolutes sensitive |
| "Mid-range spending" | "Spent 5980" | Ranges sufficient |
| "Purchased 1 critical illness policy" | "Coverage 500k, annual 8200" | Quantity sufficient; details sensitive |

When absolute values necessary, force entire file sensitivity level to Sensitive or Restricted.

## Deduplication with Other Domains

| Content | Belongs To | Does Not Belong To |
|------|------|------|
| Daily transaction flow | External accounting app | Finance domain |
| Bank/broker account passwords | Credential directory or encrypted notes | Finance domain |
| Own brand revenue data | Brand strategy domain | Finance domain |
| Financial tool API keys | Credential directory | Finance domain |
| Tax software operation steps | Best practices | Finance domain |

## Checklist

- [ ] Metadata contains type, privacy level, update date
- [ ] Numbers masked as much as possible (use ratios, ranges, multiples instead of absolutes)
- [ ] Investment strategy contains review date
- [ ] Policy numbers, card numbers, account passwords not in knowledge base
- [ ] Sensitive-level files marked for read-on-demand access
- [ ] Daily flow not in knowledge base

## Change Log

> Rolling window, keep last 3 entries, ≤20 characters each.

| Date | Change |
|------|---------|
| 2026-08-07 | Generalized from finance specification |
