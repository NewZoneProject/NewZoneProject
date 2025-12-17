# NZ-0010: Payload Schema Definition
Version: draft v0  
Status: Active  
Category: Core  

## 1. Purpose

This specification defines the deterministic payload schema used in the NewZone standard.  
The payload represents the content of a message and must be structured in a minimalistic, durable, and platform‑agnostic way.  
The schema ensures that payloads remain interpretable, verifiable, and stable across decades.

---

## 2. Scope

This specification covers:

- the conceptual structure of payloads  
- required and optional fields  
- deterministic schema rules  
- constraints ensuring durability and formal verifiability  
- terminology used across payload‑related specifications  

This specification does **not** define serialization formats or encoding algorithms.

---

## 3. Terminology

**Payload** — the content of a message.  
**Schema** — a deterministic structure describing allowed fields and types.  
**Field** — a named component of the payload.  
**Type** — a deterministic, platform‑agnostic representation of data.  
**Variant** — a schema‑defined alternative structure.  
**Envelope** — metadata defined in NZ‑0009.

---

## 4. Principles

### 4.1 Minimalism
Payloads must contain only essential information.

### 4.2 Determinism
The same payload must always produce the same representation.

### 4.3 Explicit Structure
All fields must be explicitly defined in the schema.

### 4.4 Portability
Payloads must be representable in plain text or binary formats.

### 4.5 Durability
Payload schemas must remain stable for decades.

### 4.6 Formal Verifiability
All schema rules must be expressible in formal logic.

---

## 5. Design Constraints

1. No timestamps or environment‑dependent fields.  
2. No probabilistic or random values.  
3. No implicit defaults — all fields must be explicit.  
4. No platform‑specific types.  
5. No reliance on synchronized clocks.  
6. All fields must be deterministic and stable.  
7. Payloads must be self‑contained and not depend on external context.

---

## 6. Payload Structure

A payload consists of:

1. **schema_id**  
   - required  
   - identifies the schema variant  
   - deterministic and stable  

2. **fields**  
   - required  
   - a deterministic mapping of field_name → value  
   - field order must follow schema definition  

3. **integrity_tag**  
   - optional  
   - deterministic integrity check for the payload  
   - algorithm‑agnostic and quantum‑resilient  
   - defined in future specifications  

---

## 7. Schema Definition Rules

### 7.1 Field Types
Allowed types:

- integer  
- fixed‑precision number  
- boolean  
- string  
- binary  
- list (deterministic ordering)  
- map (deterministic ordering)  
- variant (explicitly defined alternatives)

### 7.2 Field Ordering
Fields must appear in the exact order defined by the schema.

### 7.3 Explicit Nulls
If a field is empty, it must be explicitly set to null.

### 7.4 Deterministic Lists
Lists must:

- preserve order  
- contain only deterministic types  
- not contain duplicates unless explicitly allowed  

### 7.5 Deterministic Maps
Maps must:

- use deterministic key ordering  
- contain only deterministic types  

### 7.6 Variants
Variants must:

- be explicitly declared  
- contain only fields defined for that variant  
- not allow implicit inheritance  

---

## 8. Security Considerations

- Payloads must not expose sensitive information unless explicitly allowed.  
- Integrity tags must be resistant to quantum attacks.  
- Schema IDs must not leak internal state.  
- Payloads must be validated before processing.  
- Payload structure must be formally verifiable.  
- Payloads must not rely on external references.

---

## 9. Future Work

- NZ‑0033 Deterministic Serialization Rules  
- NZ‑0034 Payload Integrity Format  
- NZ‑0035 Schema Versioning Model  
- NZ‑0036 Variant Compression Rules  

---

## 10. References

None.