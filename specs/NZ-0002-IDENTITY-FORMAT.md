# NZ-0002: Identity Format
Version: draft v0  
Status: Active  
Category: Core  

## 1. Purpose

This specification defines the deterministic identity format used across the NewZone standard.  
Identity is the foundational element that enables communication, routing, trust, and verification between nodes.  
The goal is to establish a minimalistic, portable, and long‑term stable representation of identity that does not depend on external systems or centralized authorities.

---

## 2. Scope

This specification covers:

- the structure of a NewZone identity  
- the rules for generating and validating identities  
- constraints ensuring determinism and durability  
- terminology related to identity  

This specification does **not** define authentication, authorization, or trust models.  
Those are defined in later specifications.

---

## 3. Terminology

**Identity** — a deterministic, unique, and portable representation of a node.  
**Seed** — the minimal input required to generate an identity.  
**Fingerprint** — a compact representation derived from the identity.  
**Node** — any entity participating in the NewZone ecosystem.  
**Deterministic** — producing the same output for the same input across all platforms and implementations.

---

## 4. Principles

### 4.1 Determinism
Identity generation must produce identical results across all platforms, architectures, and implementations.

### 4.2 Minimalism
The identity format must contain only essential information.  
No metadata, timestamps, or environment‑dependent fields are allowed.

### 4.3 Portability
Identities must be representable in plain text and usable across any system.

### 4.4 Durability
The identity format must remain stable for decades without requiring migration.

### 4.5 Independence
Identity generation must not rely on centralized services, external authorities, or third‑party infrastructure.

---

## 5. Design Constraints

1. Identity must be derived from a minimal seed.  
2. The seed must be user‑controlled and platform‑agnostic.  
3. Identity must be representable as a fixed‑length text string.  
4. Identity must not include timestamps or environment‑specific data.  
5. Identity must not depend on cryptographic algorithms that are expected to degrade within decades.  
6. Identity must be verifiable without external dependencies.  
7. Identity must be stable across all implementations.

---

## 6. Identity Structure

A NewZone identity consists of three components:

1. **Seed** — minimal input chosen by the node.  
2. **Core Hash** — deterministic transformation of the seed.  
3. **Fingerprint** — shortened representation for indexing and routing.

### 6.1 Seed Requirements

- Must be user‑defined or system‑defined.  
- Must be stable and reproducible.  
- Must not contain environment‑specific data.  
- Must be treated as opaque input by the standard.

### 6.2 Core Hash Requirements

- Must be deterministic.  
- Must be platform‑agnostic.  
- Must not rely on hardware‑specific features.  
- Must be resistant to collisions within the expected lifespan of the standard.  
- Must be representable as plain text.

### 6.3 Fingerprint Requirements

- Must be derived from the Core Hash.  
- Must be short enough for efficient routing.  
- Must be long enough to avoid collisions in large networks.  
- Must be stable and deterministic.

---

## 7. Security Considerations

Identity must not expose sensitive information.  
Seed values must not be inferable from the identity or fingerprint.  
Implementations must avoid weak or deprecated hashing algorithms.  
Identity collisions must be extremely unlikely.

---

## 8. Future Work

- Formal definition of the hashing mechanism.  
- Quantum‑resistant identity derivation (NZ‑0007).  
- Identity lifecycle and rotation rules.  
- Identity‑based addressing for routing (NZ‑0004).  

---

## 9. References

None.