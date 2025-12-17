# NZ-0013: Deterministic Neighbor Table Format
Version: draft v0  
Status: Active  
Category: Core  

## 1. Purpose

This specification defines the deterministic neighbor table format used in the NewZone standard.  
Its purpose is to ensure that all nodes maintain a predictable, minimalistic, and formally verifiable representation of their immediate network environment.  
The table must remain stable, portable, and durable for decades.

---

## 2. Scope

This specification covers:

- the structure of the neighbor table  
- deterministic ordering rules  
- constraints ensuring predictability and formal verifiability  
- terminology used across routing‑related specifications  

This specification does **not** define neighbor discovery or transport mechanisms.

---

## 3. Terminology

**Neighbor** — a directly reachable node.  
**Neighbor Table** — a deterministic list of neighbors with associated metadata.  
**Identity** — deterministic node identifier (NZ‑0002).  
**Link Properties** — deterministic metadata describing the connection.  
**Deterministic Ordering** — lexicographic ordering of identities.

---

## 4. Principles

### 4.1 Determinism  
Given identical inputs, all nodes must derive identical neighbor tables.

### 4.2 Minimalism  
The table must contain only essential information.

### 4.3 Predictability  
Ordering and structure must be transparent and reproducible.

### 4.4 Formal Verifiability  
All fields must be explicitly defined and verifiable.

### 4.5 Quantum Resilience  
No metadata may rely on cryptographic shortcuts vulnerable to quantum attacks.

### 4.6 Independence  
The table must not depend on time, randomness, or external state.

---

## 5. Design Constraints

1. No timestamps or time‑based fields.  
2. No probabilistic or random values.  
3. No implicit defaults — all fields must be explicit.  
4. No platform‑specific metadata.  
5. No reliance on synchronized clocks.  
6. All fields must be deterministic and stable.  
7. Table ordering must be deterministic and reproducible.

---

## 6. Table Structure

Each neighbor table entry consists of:

1. **identity**  
   - required  
   - deterministic node identity (NZ‑0002)

2. **link_quality**  
   - required  
   - deterministic, algorithm‑agnostic metric  
   - must not rely on time or randomness  
   - must be comparable using deterministic ordering rules

3. **capabilities**  
   - optional  
   - deterministic list of supported features  
   - list must be lexicographically ordered

4. **integrity_tag**  
   - optional  
   - deterministic integrity check  
   - algorithm‑agnostic and quantum‑resilient  
   - defined in future specifications

---

## 7. Ordering Rules

Neighbor table entries must be ordered lexicographically by:

1. **identity**  
2. **link_quality** (if identities match)  
3. **capabilities** (if both above match)

Ordering must be:

- deterministic  
- stable  
- platform‑agnostic  
- formally verifiable  

---

## 8. Deterministic Link Quality Model

Link quality must:

- be deterministic  
- be derived from stable, environment‑independent metrics  
- not rely on time, randomness, or probabilistic sampling  
- be comparable lexicographically  

Examples of allowed metrics:

- fixed integer cost  
- deterministic hop weight  
- static capability flags  

Examples of forbidden metrics:

- latency  
- jitter  
- packet loss  
- bandwidth  
- dynamic measurements  

---

## 9. Formal Verification Requirements

The neighbor table must define:

- preconditions (valid identities, valid metrics)  
- postconditions (deterministic ordering)  
- invariants (no randomness, no ambiguity)  
- proof obligations (uniqueness of ordering)  

All rules must be compatible with NZ‑0008.

---

## 10. Security Considerations

- Malicious nodes must not influence ordering through nondeterministic metadata.  
- Identity spoofing must be detectable by higher‑level specifications.  
- Link quality must not leak sensitive information.  
- Deterministic ordering must prevent routing manipulation.  
- Table structure must be formally verifiable.

---

## 11. Future Work

- NZ‑0045 Deterministic Link Quality Derivation  
- NZ‑0046 Neighbor Table Integrity Format  
- NZ‑0047 Multi‑Layer Neighbor Representation  
- NZ‑0048 Formal Neighbor Table Proofs  

---

## 12. References

None.