# Contributing Guidelines

Thank you for your interest in contributing to the NewZone standard.  
This document defines the rules and expectations for all contributions to ensure clarity, consistency, and long-term stability.

---

## 1. Philosophy

NewZone is a minimalistic, durable, and dependency-free standard.  
All contributions must follow these principles:

- minimalism over complexity  
- autonomy over centralization  
- durability over trends  
- clarity over cleverness  
- predictability over ambiguity  

Every change must strengthen the long-term stability of the standard.

---

## 2. Contribution Types

You may contribute by:

- adding new specifications  
- improving existing specifications  
- updating documentation  
- refining templates and structure  
- fixing errors or inconsistencies  
- improving clarity without adding complexity  

All contributions must align with the core principles defined in `NZ-0001`.

---

## 3. Workflow

1. Create or update files in your branch.  
2. Ensure the structure follows `NZ_STANDARD_STRUCTURE.md`.  
3. Follow the commit message rules in `COMMIT_STYLE.md`.  
4. Update the following when applicable:
   - `NZ_SPEC_INDEX.md`
   - `CHANGELOG.md`
   - `VERSION`
5. Submit a pull request with a clear description of the change.

---

## 4. Specification Rules

All specifications must:

- follow the template in `.github/SPEC_TEMPLATE.md`  
- use English only  
- avoid implementation details  
- remain platform-agnostic  
- avoid external dependencies  
- use deterministic terminology  
- avoid ambiguous or subjective language  

Each specification must define its purpose, scope, terminology, and constraints.

---

## 5. Versioning

- The global version is stored in `VERSION`.  
- Every change that affects the standard must increment the version.  
- All changes must be documented in `CHANGELOG.md`.  
- Specifications do not have individual version numbers; they inherit the global version.

---

## 6. Communication

All discussions must remain technical, minimalistic, and focused on improving the standard.  
Avoid philosophical debates unless they directly influence the structure or clarity of the standard.

---

## 7. Licensing

All contributions are made under the repository’s license.  
By contributing, you agree that your work becomes part of the NewZone standard.

---

## 8. Final Notes

NewZone is designed to outlast platforms, tools, and trends.  
Contributions must reflect this long-term vision.