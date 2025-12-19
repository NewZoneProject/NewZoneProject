# Identity Microservice

Stateless microservice for generating and verifying identity IDs.

## Principles
- Based on NewZone specs: NZ-0002 (Identity Format), NZ-0032 (Identity Graph Verification), NZ-0056 (Identity Forward Proofs).
- Stateless, deterministic, portable.
- No external dependencies (Vanilla JS + built-in crypto).

## Usage

```bash
node services/identity/index.js
```

## Output:

```
Generated ID: <32-char identity>
Verification: true
```

## API (planned)

```
- POST /generate → returns identity_id
- POST /verify → returns boolean
```