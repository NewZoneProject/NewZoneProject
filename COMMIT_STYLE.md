# Commit Style Guide

This document defines the unified commit message format for the NewZone standard.  
All commits across the repository must follow this structure to ensure clarity, consistency, and long-term maintainability.

---

## 1. Format

Each commit message must follow the format:

<type>(<scope>): <message>

Examples:
- feat(spec): add NZ-0001 NewZone Core specification
- docs(index): update NZ_SPEC_INDEX with new entries
- chore(core): bump version to 0.0.2
- fix(structure): correct directory layout

---

## 2. Types

- **feat** — new specification, feature, or structural addition  
- **fix** — bug fix, correction, or structural repair  
- **docs** — documentation updates (README, INDEX, templates, etc.)  
- **chore** — maintenance tasks (version bump, cleanup, metadata)  
- **refactor** — internal restructuring without functional changes  
- **style** — formatting or stylistic adjustments  
- **test** — adding or updating tests (if applicable)

---

## 3. Scopes

- **spec** — specification files in `/specs/`  
- **core** — foundational files (README, VERSION, CHANGELOG, INDEX)  
- **structure** — repository layout and directories  
- **template** — `.github/SPEC_TEMPLATE.md` or other templates  
- **docs** — general documentation  
- **workflow** — automation or scripts (if added later)

---

## 4. Message Rules

- Use English only.  
- Keep the message short and descriptive.  
- Do not include trailing periods.  
- Do not use capital letters after the colon.  
- Do not include emojis.  
- Do not include multiple sentences.

---

## 5. Examples

```
feat(spec): add NZ-0002 identity format specification
docs(core): update README with structure reference
chore(core): update version to 0.0.3
fix(spec): correct terminology in NZ-0001
```

---

## 6. Philosophy

Commit messages must remain readable and meaningful decades later.  
They are part of the long-term durability of the NewZone standard.