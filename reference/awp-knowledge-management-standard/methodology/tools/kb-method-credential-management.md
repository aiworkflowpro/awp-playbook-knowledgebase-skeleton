---
document_id: awp-knowledge-management-standard/methodology/tools/kb-method-credential-management
language: en
publication: public
title: "Credential Management Methodology"
---

# Credential Management Methodology

> Manage one thing: how Markdown files storing authentication info look like, how machines parse them, how they're layered loaded, how to handle expiration.
> Not managing specific service fields (those are decided by the service), nor key rotation tutorials (that's best practices).

## Responsibility

| Dimension | Description |
|-----------|-------------|
| **Output** | `.md` files holding API keys, authorization tokens, service accounts, usernames and passwords |
| **Responsibility** | Define unified format contract, dual-zone structure, ownership type model, parsing protocol, layered loading strategy |
| **Granularity** | Default one service one file; multi-brand or multi-account within same service uses level-three headings for aggregation |
| **Not managing** | Specific service field lists, service samples, actual credential values |

## Credential files hold only what

Credential files **only save information directly related to "using this key"**:

| Allowed content | Forbidden content (goes where) |
|-----------------|-------------------------------|
| The key itself | Other services' complete keys (→ separate credential file) |
| How to obtain (steps, web login, authorization flow) | Platform resource lists (channel tables, buckets, DNS records) (→ best practices or tool docs) |
| Where to manage (console links) | Standards explanation (field descriptions, loading order) (→ this methodology) |
| How to call (call samples, endpoints, models) | Deployment scripts, ops steps, troubleshooting logs (→ best practices) |
| When it expires (deadline, rotation) | Business data (→ business files) |
| Quotas, billing, call rules | Historical change ledger (→ one-line description, or delete) |
| Who uses it (associated tool paths) | Tool start/stop commands, debug flow (→ best practices or tool entry files) |

## Dual-zone structure

Each credential file splits into two strictly isolated zones:

| Zone | Sections | Readers | Constraints |
|------|----------|---------|------------|
| **Interface zone** | `## Authentication Info` (exactly one) | Tool reading functions | Strict contract: five immutable constraints + parsing protocol |
| **Human zone** | All other sections | Human maintainers | Section whitelist + order + no narrative |

**Interface zone holds only "field → value"**, no narrative, timestamps, status, notes.
**Human zone holds only credential-related content**; section names must come from the whitelist.

## Nine Iron Laws

| # | Law | Explanation |
|---|-----|------------|
| 1 | **Dual-zone separation** | Interface zone for machines only, human zone for people, roles don't cross |
| 2 | **Format contract not data list** | Constrain parsing protocol and section whitelist, don't constrain specific field names |
| 3 | **Minimum required + whitelist extension** | One mandatory interface section + optional standard human sections, no invented names |
| 4 | **Machine and human readable** | Same Markdown table readable by people, parseable by regex |
| 5 | **Layered isolation** | Placeholder layer and real-value layer separate; security emerges naturally |
| 6 | **Tools forbid self-parsing** | Tools must fetch via shared reading function, not each write own regex |
| 7 | **Credentials store uniquely** | Sensitive values only in credential directory `.md` files. Best practices, workflows, memory—forbid plaintext keys, only write `<see credentials/{file}.md §{section}[  -  {field}]>` |
| 8 | **Ownership type first** | Judge ownership type before deciding login subject and resource subject; don't blanket force all credentials to a brand |
| 9 | **Explicit resource boundary** | Resource-type credentials must clarify login subject, resource subject, impact scope; forbid relying on filename, domain, or human memory |

## Ownership Model

Credential storage location, ownership type, and brand boundary are three different things:

| Dimension | Solves what problem |
|-----------|-------------------|
| Storage location | Which layer in the fallback chain |
| Ownership type | Does this credential need to enter brand, project, or shared-base routing |
| Brand ownership | For resource-type credentials, which brand or shared infrastructure |
| Resource subject | What account, organization, project, workspace, bucket the interface actually operates on |
| Login subject | Whose token or authorization is executing the operation |

### Six Ownership Types

| Type | Rule | Typical examples |
|------|------|------------------|
| `generic_tool` | General-ability keys not bound to brand assets; default don't mark brand ownership | Search interface, scrape interface, general model interface |
| `personal_operator` | Individual or operator login account; not a brand subject, but may authorize multiple services | Email login, device account, personal auth shell account |
| `brand_dedicated` | Single mature brand's exclusive resource; must mark brand scope | Certain brand's CMS |
| `project_dedicated` | Single product or project resource; must mark project subject and brand scope | Certain project's database, auth app |
| `shared_infra` | One account carries multiple brand resources; must list routing matrix and impact scope | Cloud service account, payment account, mail service account |
| `incubator_shared` | Incubation shared account or org hosting new brand; must mark exit conditions | New product temporarily under main-brand org |

### Judgment Sequence

| Question | Judgment |
|----------|----------|
| Only provides general compute, search, model call ability, not directly binding public brand resources? | `generic_tool` |
| Represents person's login identity, can authorize multiple services, but isn't business resource subject? | `personal_operator` |
| Only operates one brand's site, channel, send domain, repo, or payment target? | `brand_dedicated` |
| Only operates one product or project's database, auth app, content repo, or monitoring project? | `project_dedicated` |
| Same account, project, or workspace can impact multiple brands? | `shared_infra` |
| New brand temporarily under main-brand account or org, future independence possible? | `incubator_shared` |

### Must-enter-brand-routing Signals

Any of these signals mean it can't default to generic tool:

| Signal | Examples |
|--------|----------|
| Public identity | Code hosting account or org, social platform app, video channel |
| Public entry | Domain, send domain, object storage bucket, deployment project |
| User data | Auth app, database, error monitoring project, analytics property |
| Payment and business | Payment account and product, ad account |
| Cloud resource subject | Cloud project, cloud account, workspace, org |

### No-brand-routing Signals

| Signal | Examples |
|--------|----------|
| No public resource subject | Search interface, scrape interface, query interface |
| No brand data isolation need | General model interface, image generation interface, CAPTCHA platform, general proxy pool |
| Result archived elsewhere by caller | Harvest, generate, query tool temporary keys |

Generic tool keys can serve multiple brands; brand isolation happens in call product, storage path, publish target, or business directory, **not in the credential itself**.

### Three Fields Must Split

| Field | Meaning |
|-------|---------|
| `auth_user` | Current token or authorization login account |
| `resource_owner` | Interface default operation target, can be org, project, workspace, bucket, or account |
| `scope_type` | Ownership type, take one of six |
| `brand_scope` | Business brand scope, use `brand:<id>` / `shared:<name>` / `personal` / `generic` |

When tools read credentials, **forbid auto-equating login subject with resource subject**. Personal token can operate org repo, but commit author should still use personal account identity.

Generic tool credentials without resource subject—don't invent one. When brand context needed, workflow explicitly passes it.

## Why Markdown table

| Approach | Tradeoff |
|----------|----------|
| Markdown table | Human readable, machine parseable, version-control friendly, one regex covers all consumer ends |
| JSON / YAML / env files | Lose human readability or add parsing dependency |

> **Env files forbidden for self-use only.** This constraint applies to machine and knowledge-base internal self-use credentials. **Packages distributed to external consumers are exceptions**—consumers follow their ecosystem conventions; env files and placeholder templates allowed.

## Why not list fields

| Cost of listing | Benefit of rulemaking |
|-----------------|----------------------|
| Add a service, change spec | Spec stays one year unchanged |
| Specs bloat into data | Spec stays constraint-only |
| New tooling, same-meaning different-write | "Same concept, consistent across base" rule + audit tool fallback |

## Section Whitelist

Every credential file's level-two headers must come from whitelist:

| # | Section | Zone | Required | Responsibility |
|---|---------|:----:|:--------:|----------------|
| 1 | `## Authentication Info` | Interface | Required | Machine-parseable field→value table |
| 2 | `## How to obtain` | Human  -  Tier 1 | Optional | How to get this key |
| 3 | `## Web login` | Human  -  Tier 1 | Optional | Browser account login info |
| 4 | `## Resource ID` | Human  -  Tier 1 | Optional | Platform resource identifiers directly related to auth (small count) |
| 5 | `## Brand ownership` | Human  -  Tier 1 | Optional | Ownership type, login subject, resource subject, brand scope |
| 6 | `## Call examples` | Human  -  Tier 2 | Optional | Minimal runnable call sample |
| 7 | `## Common config` | Human  -  Tier 2 | Optional | Call-required tech parameters (endpoint, port, timeout) |
| 8 | `## Common models` | Human  -  Tier 2 | Optional | Model service's available models list |
| 9 | `## Integration config` | Human  -  Tier 2 | Optional | Third-party tool integration code |
| 10 | `## Management entry` | Human  -  Tier 3 | Optional | Console, docs, key management links |
| 11 | `## Quota and billing` | Human  -  Tier 3 | Optional | Quota, rate limit, billing |
| 12 | `## Validity period` | Human  -  Tier 3 | Optional | Expiration, rotation pace |
| 13 | `## Usage rules` | Human  -  Tier 3 | Optional | Call rate-limit, concurrency, forbidden |
| 14 | `## Associated tools` | Human  -  Tier 4 | Optional | Tool paths using this credential |
| 15 | `## Consumers` | Human  -  Tier 4 | Optional | Who's using this quota. Check before revoke key |
| 16 | `## Trigger words` | Human  -  Tier 4 | Optional | Routing words: say what should send here |
| 17 | `## Purpose` | Human  -  Tier 4 | Optional | Use case paragraph |

### Normalize homonyms

One thing, one section name across base:

| See these | Write as |
|-----------|----------|
| `Associated` / `Associated resources` / `Landing` | `## Associated tools` |
| `Ownership` | `## Brand ownership` |
| `Account info` / `Account` / `Credentials` / `Interface config` / `Login info` | `## Authentication Info` |
| `Call sample` | `## Call examples` |
| `Quota` / `Quota and limit` / `Quota` | `## Quota and billing` |
| `Deploy info` / `Common commands` | `## Common config` or `## Integration config` |
| `Use case` / `Special features` | `## Purpose` |
| `Consumer list` | `## Consumers` |

### Tier order

```text
# {Service} Credential          ← Required
{One sentence}
---

## Authentication Info         ← Interface zone  -  only required

## How to obtain               ← Tier 1 follow auth info
## Resource ID
## Brand ownership

## Call examples               ← Tier 2 call guide
## Common config
## Integration config

## Management entry            ← Tier 3 lifecycle
## Quota and billing
## Validity period
## Usage rules

## Associated tools            ← Tier 4 index (end)
## Consumers
## Trigger words
## Purpose
```

| Rule | Level |
|------|:-----:|
| Level-two headers must come from whitelist | Required |
| Optional sections use as-needed, omit if unused | Required |
| Arrange by tier | Required |
| Order within tier | Optional |
| New-invented section names | Forbidden |
| `## Authentication Info` must be first level-two | Required |

## Five Immutable Contracts for Authentication Info

This section is the tool's only anchor to read credentials.

```markdown
## Authentication Info

| Field | Value |
|-------|-------|
| {field_name 1} | `{value 1}` |
| {field_name 2} | `{value 2}` |
```

| # | Contract | Explanation |
|---|----------|------------|
| 1 | Section title fixed as `## Authentication Info` | Changing it breaks all base tools |
| 2 | Headers fixed as "Field, Value" two columns | Extra columns misdirect regex |
| 3 | Values must start with backtick` | No backtick = parse fail |
| 4 | Field names unique within subsection | Duplication within subsection causes read ambiguity; same name across subsections is normal for multi-account files |
| 5 | No metadata fields in this table | Creation time, version, status, origin go in "Usage rules" or "Validity period" |

> **Contract 3 judges the start, not the whole cell.** Reading function takes only first backtick-quoted segment after field name, so `` | expiration | `2026-10-16`(~90 days) | `` fully legal—value first, short note after, parse gets date. Illegal is whole cell no backtick: `| storage | Base stores hash, plaintext only here |`. That's not a value, it's narrative; move to text block below table or move to "Usage rules".

### Field naming

| Rule | Level |
|------|:-----:|
| Semantic, same concept consistent across base | Required |
| Protocol-level fields use English standard names, follow service official docs | Required |
| Business-level fields can use descriptive names | Optional |
| Reuse existing names over creating new (audit before adding) | Required |
| Same concept use multiple writes | Forbidden |
| Unclear abbreviations | Forbidden |
| Field names themselves quoted with backtick | Forbidden |

### Multi-account and large credentials

Single service multi-auth domain or multi-account—use level-three subheadings, keep "field, value" two-column within each subsection.

> **Subsection: callers must name subsection.** Subsections share field names (each account has own key field), parsing regex doesn't recognize subsection boundary; no subsection param only matches **first** in file. Change subsection order, fetched value silently swaps—no error, just wrong.

Large credentials can't fit table (structured config, cert, private key)—put in code block under subheading, **and** keep a field in the field→value table pointing to that code block.

Consumers pick one reading capability:

| Consumer capability | Use what |
|-------------------|----------|
| Can eat string directly | Read-code-block-raw function |
| Only knows disk file path | Extract-code-block-to-disk-and-return-path function, permission fixed to owner-only read-write |

Disk landing **must be outside knowledge base** (user cache dir convention)—it's runtime cache only, auto-rebuild when source changes. Don't write landing products back to credential directory, that's rebuilding the env-file directory you already revoked.

### Placeholders in distribution

| Rule | Level |
|------|:-----:|
| Distribution template layer use placeholders for values | Required |
| Placeholders all-caps, underscore-separated | Required |
| Placeholder prefix: `YOUR_` / `REPLACE_` / `CHANGEME` | Required |
| Placeholder value outside template layer is unconfigured | Required |
| Leave blank or no backtick | Forbidden |

## Parsing Contract

Tool reading credentials' hard handshake—any implementation must follow.

### Read protocol

Given service name and field name, parsing flow fixed:

1. Locate file path (see layered fallback chain)
2. Read file content (UTF-8, support BOM)
3. Lock section: match `^##\s*Authentication Info\s*$` to next level-two header
4. In section apply field extraction regex
5. Apply placeholder detection
6. Return real value, or trigger unconfigured error

### Field extraction regex

```python
re.search(rf"\|\s*{re.escape(key)}\s*\|\s*`([^`]+)`", content)
```

### Placeholder detection regex

```python
re.match(r"^(YOUR_|REPLACE_|CHANGEME)", value, re.IGNORECASE)
```

### Default field boundary

| Scenario | Handle |
|----------|--------|
| Single-key service | Read default field directly |
| Official term isn't default field name | Tool must explicitly pass field name |
| Multi-account or plan subsection | Each subsection keep bare default name, tool locate via subsection |
| Multi-auth method (no default field) | Tool must explicitly pass field name |

### Four immutable anchors

| Anchor | Constraint |
|--------|-----------|
| `## Authentication Info` section name | Unchangeable |
| "Field, Value" two-column headers | Unchangeable |
| Backtick-quote values | No exception |
| Field names no backtick | Regex depends |

**Don't version this contract**: modifying it = base-level rework, not regular change flow.

## Layered fallback chain

Four-layer chain is base credentials' only true source. Diff in any scenario only allowed increasing form referencing this chain, never paralleling or changing tier semantics.

| Layer | Location | Who has | Purpose | In version control |
|-------|----------|---------|---------|:------------------:|
| **L0** | Environment variable | Everyone | Temp override, CI, container | — |
| **L1a** | Tool-package credential template dir | Everyone | Distribution placeholder template | Yes |
| **L1b** | User home credential dir | User | User real value | No |
| **L2** | Knowledge base credential dir | KB author | Built-in real value | No |

> **L1a follows code, not in KB.** Tool code is separate repo, placeholder template in code version control. KB has only L2.
>
> **L2 is single-zone, no subdirs.** All credential files flat, `.md` only. Large credentials no-table (use code block method) don't open dir for env or config files.
>
> **L2 syncs to all machines with KB**—all credential dir `.md` files sync, **no "don't-sync sensitive zone"** exists. Keys needing stronger isolation go L1b only (outside KB, no sync).
>
> **L2 position declared by base itself**: base root declaration file marks credential dir, only true source. Code doesn't guess base location from own file path—it ships in system package dir, can't guess; same install serves multiple bases.

### Runtime lookup order

```text
L0 → L1b → L2
```

L1a only template, **never participates runtime lookup**. After tool install, users can init-command copy L1a template to L1b.

### File locating unified parser

"Service name → file" location—one shared parser only, reading function, credential subcommand, health check use same conclusion, **forbid each tool self-locating**. Fallback:

1. **Exact name**: credential dir same-name file.
2. **Service segment index**: four-segment naming, service segment exact-match hits.
3. **Variant**: dash variant and suffix variant.
4. **Ambiguity tie-break**: hit multiple candidates, exactly one generic scope use it; else **refuse and list candidates**, require caller rename to full filename. Multi-brand same-service never guess brand.
5. **Miss**: report auth error, attach full chain and candidate suggestions.

Caller stability agreement: tool declaration and code service-name param **prefer full filename** (hit exact name, no parsing); short name convenience entry only. Env-var layer temp override only, not regular chain—restart loses it, stable main-chain is KB file layer.

### Layer value-type requirement

| Layer | Requirement |
|-------|------------|
| L1a | Must be placeholder |
| L0 / L1b / L2 | Must be real value (placeholder = unconfigured) |

### "Configured" judgment

| Layer | Judgment |
|-------|----------|
| L0 | Env var exists, non-empty non-placeholder |
| L1b / L2 | File exists, **and** auth info section has ≥1 non-placeholder value |
| L1a | File exists (template anyway) |

### Environment variable naming

```text
{service_uppercase_no_extension_no_dash}_{field_uppercase_space_to_underscore}
```

## Tool Integration Contract

### Command-line tools

| Rule | Level |
|------|:-----:|
| Must fetch via shared reading function | Required |
| Service param no extension | Required |
| Must implement credential subcommand (init, list, set, read) | Required |
| Self-write credential parsing regex | Forbidden |
| Hardcode key | Forbidden |
| Stdout or stderr print key value | Forbidden |
| Error message expose full path | Forbidden |

### Custom server endpoints

| Rule | Level |
|------|:-----:|
| Must wrap equivalent reading function | Required |
| Must reference same parsing regex and same tier order | Required |
| Must support env var fallback | Required |
| Return raw key in protocol response | Forbidden |
| Transport unmasked key | Forbidden |

Third-party server keys don't flow through base reading function—wrapper script injects from separate key file to env var, landing L0 tier.

### Exception declaration

Single service crossing multiple credential files (e.g., comprehensive server-info file)—allowed relax mandatory-section constraint, **but** must explicitly declare top description after:

```markdown
> Exception: this file is comprehensive credential set, no single "Authentication Info" section.
> Reason: aggregates multiple services' credentials, each service independent in subsection.
> Tools: read via separate service files, don't apply parsing contract to this file.
```

## File naming

Format: `{domain}-{service}-{ownership}-{purpose}.md`

| Segment | Answers what | Value range |
|---------|------------|------------|
| **domain** | What type | Controlled vocab, see below |
| **service** | Which platform | Service official name, segment concatenated no symbol |
| **ownership** | Whose | `shared` (generic) / brand ID / `personal` / project name |
| **purpose** | What for | Controlled vocab, extensible |

**Iron rules**:

| Rule | Level |
|------|:-----:|
| Exactly three dashes separate four segments | Required |
| Lowercase letters + dash-between-segments + `.md` | Required |
| Concatenate within segment, no dash | Required |
| File name maps to tool-call service param | Required |
| Four segments all required; use `shared` for generic, default purpose `api` | Required |
| Space, non-ASCII, uppercase, underscore | Forbidden |
| Same-name collision (four segments identical) | Forbidden |

**Domain controlled vocab** (extensible, new values register in table):

| Domain | Coverage |
|--------|----------|
| `model` | Model service |
| `search` | Search and scrape |
| `cms` | Content management and publish |
| `social` | Social platform |
| `cloud` | Cloud service and deploy |
| `dev` | Dev tool |
| `infra` | Infrastructure (server, network) |
| `account` | Personal account |
| `payment` | Payment and ad |
| `media` | Media asset |
| `proxy` | Proxy and network |
| `storage` | Cloud storage |
| `verify` | Verify and detect |

**Purpose controlled vocab** (extensible):

`api` (default)  -  `bot`  -  `server`  -  `oauth`  -  `config`  -  `index`  -  `curl`  -  `auth`  -  `prod`  -  `dev`  -  `accounts`  -  `console`  -  `cloud`  -  `local`  -  `proxy`  -  `cookie`  -  `history`  -  `registry`  -  `signing`  -  `userbot`

**Registered exceptions**: host ledger-type files allow underscore in service segment, because host ID is composite encoding with underscore as internal delimiter. These files called by full filename, renaming risks outweigh benefits. **All other credential files still forbid underscore.**

## Security red line

| Red line | Level | Explanation |
|----------|:-----:|------------|
| Real keys don't version-control | Forbidden | Ignore-rule exclude real-value layer |
| Script don't output key | Forbidden | Stdout and stderr both don't print |
| Error don't expose full path | Forbidden | Only say "credential unconfigured: {service}" |
| Don't hardcode | Forbidden | Must fetch via reading function |
| Audit don't desensitize | Warning | Audit to spec don't modify user-configured real keys |
| Rotate regularly | Optional | Suggest periodically update key |

## Expired credential handling

Service stopped, account closed, key revoked—that credential file can't stay credential-dir root—service-segment index still scans it, tool gets unpingable value.

| Handle | Method | Level |
|--------|--------|:-----:|
| Revoke first | To service console revoke key or close account, confirm online dead | Required |
| Then move out root | Whole file to archive-zone month dir, remove from credential index | Required |
| No subdirs ever | Expired go to archive zone. Credential zone flat, no subdirs | Forbidden |
| Filename mark dead date | `{original}-{YYYY-MM-DD}-expired-archive.md`, date is revoke-day not archive-day | Required |
| Top write one dead note | When, why dead, replacement credential which (or "none") | Required |
| Audit callers | Pre-move search whole base filename and service-segment, change still-calling declaration, call, workflow | Required |
| Leave in root only change content | Only delete values, file still root | Forbidden |
| Directly delete file | Dead record itself has traceability value (when used, why stopped) | Forbidden |

Pre-archive ensure online key really revoked—**archive zone doesn't follow credential-zone security red lines, leaving unrevoked live value moved outside fence.**

## Ledger-type files

Credential zone has second legal form: **ledger**. Not "one service one credential", it's "resource-list with passwords"—host ledger, domain ledger, analytics-resource ledger all fit.

Forcing credential skeleton gets fake violations: they lack single "this key", resource-list sections impossible whitelist. This methodology recognizes form, demands clear boundary.

**Judge** (both must be true):

| Condition | Explanation |
|-----------|------------|
| Subject is resource list not single credential | Machine, domain, property, node list; passwords just one column |
| No single auth-info section writable | Forcing it just relabels the list |

**Skeleton**: must declare form post-description, then own section set, exempt whitelist:

```markdown
> Ledger-type: this file is {machine/domain/property} resource list, not single-service credential.
> No single "Authentication Info" section; each resource's password in own subsection.
> Tools: don't use credential-reading function on this file, read by resource name direct.
```

| Rule | Level |
|------|:-----:|
| Top declare ledger form | Required |
| **New** ledger filename end `-config` / `-registry` / `-index` / `-history` | Required |
| Password values still backtick-quoted | Required |
| Still follow security red lines and expired handling | Required |
| Credential reading function read direct | Forbidden |
| Use ledger as excuse stuff deploy script, ops step, troubleshoot log | Forbidden |

**Existing files don't force re-name.** Credential filename is service-segment index key; rename needs update all callers, risk outweighs benefit. Mark it ledger in declaration block enough.

> Ledger-type is **acknowledge status**, not new best practice. When building new credentials prioritize split into single-service files; only when resource-list itself is subject and splitting loses relationship do you use ledger-type.

## Checklist

**New credential file  -  Interface zone**

- [ ] Filename lowercase four-segment, purpose from controlled vocab; new purpose registered
- [ ] Level-one title `# {service} Credential`
- [ ] One sentence + separator line
- [ ] `## Authentication Info` exists, is first level-two
- [ ] Headers exactly "Field, Value" two columns
- [ ] All values backtick-quoted
- [ ] Field names unique within subsection
- [ ] No metadata fields mixed in
- [ ] No other services' keys

**New credential file  -  Human zone**

- [ ] All level-two headers from whitelist
- [ ] Sections arranged tier 1→tier 4
- [ ] Ownership type judged
- [ ] Generic tool not brand-forced
- [ ] Resource credential has brand ownership
- [ ] Split ownership type, login subject, resource subject, brand scope
- [ ] Shared infra marked default use, routing matrix, impact scope
- [ ] Incubator shared marked exit condition
- [ ] No platform resource list, no spec explanation, no deploy script, no history ledger
- [ ] Code blocks tagged language

**Multi-subsection file**

- [ ] Multi-account callers all pass subsection param
- [ ] Cross-subsection same-name only subsection-unique, no same-subsection duplicate

**Expired handling**

- [ ] Stopped-service credentials revoked online, moved archive, removed from index
- [ ] Large credentials in code block, table has field pointing, landing cache outside KB
- [ ] Credential dir only `.md`, no subdirs
- [ ] Pre-move searched whole base filename and service-segment, changed all callers

**Ledger-type**

- [ ] Top declared ledger form, says why no auth-info
- [ ] Filename `-config` / `-registry` / `-history` end
- [ ] No tool using credential reading on it

**When modifying this methodology**

- [ ] No specific service field list or sample code
- [ ] All rules verifiable (no "try", "best" soft words)
- [ ] Parsing contract untouched (changes need base-level rework)

## Changelog

> Rolling window, keep last 3 entries, ≤20 chars each.

| Date | Change |
|------|--------|
| 2026-08-07 | Generalized from credential spec |
