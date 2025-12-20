# Metadata Microservice

Stateless microservice for generating and verifying metadata integrity proofs.

## Principles
- Based on NewZone specs: NZ-0037 (Metadata Integrity Proofs), NZ-0057 (Metadata Forward Proofs).
- Stateless, deterministic, portable.
- No external dependencies (Vanilla JS + built-in crypto).

## Usage

```bash
node services/metadata/index.js
```

## Output

```
Generated Proof: <64-char hash>
Verification: true
```

API (planned)
- POST /generate → returns proof_id
- POST /verify → returns boolean
