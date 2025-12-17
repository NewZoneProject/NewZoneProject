# NZ-0005: Storage Model
Version: draft v0  
Status: Active  
Category: Core  

## 1. Purpose

This specification defines the conceptual storage model of the NewZone standard.  
It describes how data is represented, persisted, and retrieved in a deterministic, minimalistic, and platform‑agnostic manner.  
The goal is to ensure long‑term durability and interoperability across all implementations.

---

## 2. Scope

This specification covers:

- the conceptual structure of stored data  
- rules for deterministic representation  
- storage constraints  
- terminology used across storage‑related specifications  

This specification does **not** define physical storage formats, file systems, databases, or serialization algorithms.  
Those are implementation details outside the scope of the standard.

---

## 3. Terminology

**Record** — a structured unit of stored data.  
**Block** — a minimal container for one or more records.  
**Snapshot** — a consistent representation of a storage state.  
**Index** — a deterministic mapping for locating records.  
**Persistence** — the ability to retain data across sessions.  
**Representation** — the deterministic encoding of data.

---

## 4. Principles

### 4.1 Minimalism
Stored data must contain only essential information.  
No redundant metadata or environment‑specific fields are allowed.

### 4.2 Determinism
The same input must always produce the same stored representation.

### 4.3 Portability
Stored data must be representable in plain text or binary formats without platform dependencies.

### 4.4 Durability
Stored data must remain valid and interpretable for decades.

### 4.5 Independence
Storage must not rely on centralized services, proprietary formats, or external authorities.

### 4.6 Transparency
Storage structures must be clear, predictable, and self‑describing.

---

## 5. Design Constraints

1. Storage must not depend on specific file systems or databases.  
2. Storage must not include timestamps or environment‑dependent metadata.  
3. Storage must be deterministic across all platforms.  
4. Storage must support offline and degraded environments.  
5. Storage must not rely on mutable global state.  
6. Storage must support incremental updates without requiring full rewrites.  
7. Storage must be verifiable without external dependencies.

---

## 6. Storage Model

The NewZone storage model consists of three conceptual layers:

### 6.1 Representation Layer
Defines how data is encoded:

- deterministic structure  
- stable field ordering  
- explicit types  
- no implicit defaults  

Representations must be self‑contained and platform‑agnostic.

### 6.2 Block Layer
Defines how data is grouped:

- blocks contain one or more records  
- blocks are immutable once finalized  
- blocks may reference other blocks deterministically  

Blocks must support incremental growth without rewriting existing data.

### 6.3 Index Layer
Defines how data is located:

- deterministic mapping from identity → block → record  
- no probabilistic indexing  
- no external dependencies  
- no centralized registries  

Indexes must be reproducible across implementations.

---

## 7. Storage Behavior

### 7.1 Immutable Records
Once written, records must not be modified.  
Updates must create new records.

### 7.2 Append‑Only Blocks
Blocks must support append‑only behavior to ensure durability.

### 7.3 Deterministic Snapshots
Snapshots must be reproducible from the same sequence of blocks.

### 7.4 Stateless Retrieval
Retrieval must not depend on hidden state or external context.

### 7.5 Offline Operation
Storage must function without network connectivity.

---

## 8. Security Considerations

- Stored data must be validated before use.  
- Blocks must include integrity checks defined in future specifications.  
- Storage must assume adversarial environments.  
- Corrupted or tampered data must be detectable.  
- Sensitive data must not be stored in plain text unless explicitly allowed.

---

## 9. Future Work

- NZ‑0014 Block Integrity Format  
- NZ‑0015 Deterministic Serialization Rules  
- NZ‑0016 Snapshot Compression Model  
- NZ‑0017 Distributed Storage Synchronization  

---

## 10. References

None.