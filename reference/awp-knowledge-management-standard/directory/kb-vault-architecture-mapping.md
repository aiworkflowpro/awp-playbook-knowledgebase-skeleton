---
document_id: awp-knowledge-management-standard/directory/kb-vault-architecture-mapping
language: en
publication: public
title: "Knowledge Base Architecture and Directory Mapping"
---

# Knowledge Base Architecture and Directory Mapping

> Scope: How the knowledge base is structured at the top level; what each area contains; how CLI recognizes the library.
> Out of scope: Which directory organization pattern an area uses (→ Directory Organization Pattern Registry); what a single file is called (→ Naming Dimension).
> Actual paths, usernames, hostnames, and sync devices are declared by each deployment environment; not hardcoded in this spec.

---

## One-Sentence Summary

The knowledge base is a single, self-contained library identified by a root identity file. Eleven top-level areas divide content by responsibility. CLI resolves all paths from this identity file.

---

## Top-Level Area Map

| Area Key | Default Directory | Responsibility |
|----------|-------------------|----------------|
| `{owner_root}` | `owner/` | Owner experience, expertise, and decisions |
| `{brand_root}` | `brand/` | Brand package |
| `{commerce_root}` | `commerce/` | Strategy and business model |
| `{business_root}` | `business/` | Product delivery and operations data |
| `{workflows_root}` | `workflows/` | Automation pipelines |
| `{tools_root}` | `tools/` | CLIs, services, MCP servers, and credentials |
| `{specs_root}` | `specs/` | Authoring and development standards |
| `{research_root}` | `research/` | Research library |
| `{dashboard_root}` | `dashboard/` | Operations control |
| `{inbox_root}` | `inbox/` | Transit and archive |
| `{personal_root}` | `personal/` | Credentials, health, investment, and personal life |

> Each area owns its content independently. Only `specs/` requires per-document identity tracking across files. Each area's internal organization is defined by its own skeleton spec.

---

## How CLI Identifies the Library

One library CLI serves the knowledge base. It must not guess library identity by current working directory or code install location. The library root must have an identity file (`.awp-vault.toml`); declare at least `name`, `credentials_dir`, `output_dir`, and `archive_dir`.

CLI first reads the identity file, then parses the path. If the file is missing, fields are incomplete, or the request path overflows the root, CLI refuses to execute. Code install location only shows program location, not library location.

---

## File Synchronization

The library can use file-sync tools to sync among multiple devices. Each deployment uses independent ignore rules and conflict handling. Device sync only copies files; it does not change library identity.

---

## Edit Rules

- **Default: edit within the library only.** A task only modifies files within this library. Cross-boundary operations require explicit request.
- **Product code repos are separate from the library.** The library stores content, config, and controlled credentials only — not tool or product code repos. Code repo paths are declared by the install environment alone.
