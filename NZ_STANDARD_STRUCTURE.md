# NewZone Standard Repository Structure

This document defines the official structure of the NewZoneProject repository.  
All files, directories, and specifications must follow this layout to ensure clarity, predictability, and long-term stability.

---

## 1. Root Files

```
README.md               — project overview  
VERSION                 — global version of the standard  
CHANGELOG.md            — history of all changes  
NZSPECINDEX.md        — index of all specifications  
COMMIT_STYLE.md         — unified commit message rules  
CONTRIBUTING.md         — contribution guidelines  
NZSTANDARDSTRUCTURE.md — this structure definition  
```

These files form the foundation of the standard and must always remain in the root directory.

---

## 2. Specifications Directory

```
/specs/
    NZ-0001-*.md
    NZ-0002-*.md
    NZ-0003-*.md
    ...
```

Rules:

- Each specification has a unique numeric ID.  
- IDs are sequential and never reused.  
- Filenames follow the format:  
  NZ-XXXX-NAME.md  
- All specifications must follow the template in .github/SPEC_TEMPLATE.md.  
- Only English is allowed inside specification files.

---

## 3. Documentation Directory

```
/docs/
    (optional future documentation)
```

This directory is reserved for extended documentation, diagrams, or explanatory materials.  
It must not contain specifications.

---

## 4. GitHub Templates

```
/.github/
    SPEC_TEMPLATE.md     — template for all specifications
```

Additional GitHub-related files (workflows, issue templates, etc.) may be added later, but must not interfere with the minimalistic nature of the repository.

---

## 5. Naming Rules

- Use uppercase for all specification filenames.  
- Use hyphens (-) as separators.  
- Avoid spaces, underscores, or camelCase.  
- Keep names short, descriptive, and stable.

---

## 6. Versioning Rules

- The global version is stored in VERSION.  
- All changes must be reflected in CHANGELOG.md.  
- Specifications do not have individual version numbers; they inherit the global version.  
- Structural changes require a version bump.

---

## 7. Philosophy

The structure must remain stable for decades.  
It must be:

- minimalistic  
- predictable  
- platform‑agnostic  
- easy to navigate  
- resistant to technological change  

This structure is part of the NewZone standard itself and must not be altered without strong justification.
