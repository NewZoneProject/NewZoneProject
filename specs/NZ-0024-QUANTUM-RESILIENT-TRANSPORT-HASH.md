NZ-0024: Quantum-Resilient Transport Hash
Version: draft v0  
Status: Active  
Category: Transport  

1. Purpose

This specification defines the quantum‑resilient transport hash used in the NewZone standard.  
Its purpose is to provide a collision‑resistant, timeless, and formally verifiable hashing mechanism for transport identifiers, ensuring resilience against quantum computing attacks.

---

2. Scope

This specification covers:

- deterministic hash function definition  
- usage in sessionid (NZ‑0022) and flowid (NZ‑0023)  
- compatibility with transport envelope (NZ‑0021)  
- constraints ensuring predictability and formal verifiability  

This specification does not define encoding (NZ‑0025) or integrity proofs (NZ‑0026).

---

3. Terminology

Transport Hash — deterministic mapping from identity pairs and payload types to fixed identifiers.  
Collision Resistance — impossibility of two distinct inputs producing the same output.  
Quantum Resilience — resistance against quantum algorithms (e.g., Grover’s search).  
Fixed Width — deterministic output length.

---

4. Principles

4.1 Determinism
Hash outputs must be identical across all implementations.

4.2 Minimalism
Only essential inputs may be included.

4.3 Predictability
Hashing must be transparent and reproducible.

4.4 Formal Verifiability
All rules must be expressible in formal logic.

4.5 Quantum Resilience
Hashing must resist quantum search and collision attacks.

4.6 Independence
Hashing must not depend on time, randomness, or external state.

---

5. Design Constraints

1. No probabilistic hashing.  
2. No time‑based salts.  
3. No adaptive or environment‑dependent inputs.  
4. No dynamic negotiation.  
5. All hash rules must be deterministic and stable.  
6. Hash must be forward‑compatible for decades.

---

6. Hash Function Definition

The transport hash is defined as:

```
transporthash(input) = fixedwidth_output
```

Where:

- input = (identitypair, payloadtype)  
- fixedwidthoutput = 256‑bit deterministic value  
- must be collision‑resistant  
- must be quantum‑resilient  

Forbidden:

- random salts  
- time‑based seeds  
- environment‑dependent entropy  

---

7. Usage

7.1 Session ID (NZ‑0022)
```
sessionid = transporthash(identity_pair)
```

7.2 Flow ID (NZ‑0023)
```
flowid = transporthash(identitypair, payloadtype)
```

7.3 Transport Envelope (NZ‑0021)
```
flowid embedded in transportenvelope
```

---

8. Formal Verification Requirements

Hashing must define:

- preconditions (valid identities, valid payload type)  
- postconditions (deterministic hash output)  
- invariants (no randomness, no ambiguity)  
- proof obligations (collision resistance, uniqueness)  

Compatible with NZ‑0008.

---

9. Security Considerations

- Malicious nodes must not influence hash outputs.  
- Hash must resist Grover’s algorithm.  
- Deterministic rules must prevent manipulation.  
- Hash must be formally verifiable.

---

10. Future Work

- NZ‑0025 Fixed‑Width Transport Encoding  
- NZ‑0026 Deterministic Session Integrity Proofs  
- NZ‑0027 Stateless Flow Verification Model  
- NZ‑0028 Quantum‑Resilient Identity Hash  

---

11. References

None.
