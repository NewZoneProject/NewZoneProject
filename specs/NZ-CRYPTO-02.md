# NZ-CRYPTO-02 — NewZone Cryptographic Layer (Reference)

## 1. Purpose

NZ-CRYPTO-02 defines the unified cryptographic layer for all NewZone microservices and nodes, aligned with the reference implementation (`lib/nz-crypto.js` + pure primitives).

Goals:

- **Unified:** one cryptographic contract for all services.
- **Minimal:** small, portable, dependency-light, JSON-native.
- **Modern:** Ed25519, X25519, HKDF, BLAKE2b, ChaCha20-Poly1305.
- **Deterministic:** context-bound key derivation and signatures.
- **Versioned:** explicit `version` field for forward compatibility.

---

## 2. Algorithms

### 2.1 Signatures

- **Algorithm:** Ed25519  
- **Purpose:** authenticate the sender node, protect against tampering.  
- **Usage:** `auth.signature` in signed packets.

### 2.2 Key exchange

- **Algorithm:** X25519 (Curve25519 ECDH)  
- **Purpose:** derive a shared secret between two nodes.  
- **Usage:** input to HKDF for session key derivation.

### 2.3 Symmetric encryption

- **Algorithm:** ChaCha20-Poly1305 (AEAD)  
- **Purpose:** encrypt `{ auth, body }` packets between nodes.  
- **Associated Data (AAD):** UTF-8 string:

  ```text
  "<sender_node_id>-><receiver_node_id>"
  ```

- Nonce: 96-bit random value (12 bytes).

> Future versions MAY add aes-256-gcm, but NZ-CRYPTO-02 standardizes chacha20-poly1305 as the reference cipher.

### 2.4 Hashing

- **SHA-256:**
  - **Purpose:** `body_hash`, `auth_hash` (signing input), identifiers.
- **BLAKE2b-256:**
  - **Purpose:** context-bound salt for HKDF in session key derivation.

### 2.5 KDF

- **Algorithm:** HKDF with configurable hash:
  - `hash = "sha512"` (default in reference implementation),
  - `hash = "blake2b"` (supported).
- **Interface (conceptual):**

  ```text
  HKDF(hash, salt, ikm, info, length) -> okm
  ```

---

## 3. Signed packet format

Base (not yet encrypted) packet:

```json
{
  "auth": {
    "node_id": "nzid:node:...",
    "timestamp": 1738249200,
    "nonce": "random-128-bit-string",
    "bodyhash": "hex(sha256(bodyjson))",
    "signature": "base64(ed25519_signature)"
  },
  "body": {
    "action": "update_state",
    "payload": { "...": "..." }
  }
}
```

### 3.1 auth fields

- **node_id** — node identifier (NZ-ID-01, e.g. `nzid:node:<fingerprint>`).
- **timestamp** — UNIX time (seconds) when the packet was created.
- **nonce** — random 128-bit string, unique per `(node_id, timestamp)``; used for replay protection.
- **body_hash** — `hex(sha256(body))`, where `body` is the JSON object.
- **signature** — `base64(Ed25519(signature_bytes))`.

### 3.2 Signature calculation

1. Build `auth_without_signature`:

   ```json
   {
     "node_id": "...",
     "timestamp": 1738249200,
     "nonce": "random-128-bit-string",
     "body_hash": "..."
   }
   ```

2. Canonicalize `auth_without_signature`:
   - sort keys lexicographically,
   - drop `undefined` fields,
   - serialize to JSON.

3. Compute:

   ```text
   authhash = sha256(canonicalauth_json)
   ```

4. Sign:

   ```text
   signature = Ed25519.Sign(authhash, ed25519private_key)
   ```

5. Encode `signature` as Base64 and store in `auth.signature`.

Verification reconstructs `auth_without_signature`, recomputes `auth_hash`, and verifies the Ed25519 signature.

---

## 4. Encrypted packet format

After signing, the entire `{ auth, body }` object MAY be encrypted.

Encrypted packet (NZ-CRYPTO-02, aligned with reference implementation):

```json
{
  "version": "nz-crypto-01",
  "cipher": "chacha20-poly1305",
  "sendernodeid": "nzid:node:...",
  "receivernodeid": "nzid:node:...",
  "nonce": "base64(nonce_bytes)",
  "tag": "base64(tag_bytes)",
  "ciphertext": "base64(ciphertext_bytes)",
  "context": "NZ-CRYPTO-01/packet"
}
```

### 4.1 Fields

- **version** — crypto layer version, MUST be `"nz-crypto-01"` for this spec.
- **cipher** — MUST be `"chacha20-poly1305"` in NZ-CRYPTO-02 reference.
- **sendernodeid** — sender node ID.
- **receivernodeid** — receiver node ID.
- **nonce** — 96-bit random nonce (12 bytes), Base64-encoded.
- **tag** — authentication tag from ChaCha20-Poly1305, Base64-encoded.
- **ciphertext** — encrypted JSON of the original `{ auth, body }`, Base64-encoded.
- **context** — string context for higher-level routing / debugging (e.g. `"NZ-CRYPTO-01/packet"`).

---

## 5. Session key establishment

### 5.1 Node keys

Each node MUST have:

- `ed25519public, ed25519private` — for signatures.
- `x25519public, x25519private` — for key exchange.

### 5.2 Shared secret

For nodes A and B:

```text
sharedsecretA = X25519(Apriv, Bpub)
sharedsecretB = X25519(Bpriv, Apub)
```

Both values MUST be equal.

### 5.3 Session key derivation (reference)

NZ-CRYPTO-02 standardizes the following derivation, matching `lib/nz-crypto.js`:

```text
input:
  ourprivx25519      (32 bytes)
  theirpubx25519     (32 bytes)
  context              (UTF-8 string, default "NZ-CRYPTO-01/session")
  hash                 (string, default "sha512")
  key_length           (integer, default 32)

steps:
  sharedsecret = X25519(ourprivx25519, theirpub_x25519)

  salt = BLAKE2b-256( UTF8(context) )
  info = UTF8("NZ-CRYPTO-01/deriveSessionKey")

  sessionkey = HKDF(hash, salt, sharedsecret, info, key_length)
```

- **session_key** — 32 bytes, used as symmetric key for ChaCha20-Poly1305.

---

## 6. Sending a request

1. Build `body` (JSON object).
2. Compute `body_hash = sha256(body)`.
3. Build `auth_without_signature`:
   - `node_id, timestamp, nonce, body_hash`.
4. Canonicalize `auth_without_signature`, compute `auth_hash = sha256(canonical_auth)`.
5. Sign `auth_hash` with Ed25519 private key → `signature.`
6. Build `{ auth, body }`.
7. Optionally encrypt `{ auth, body }` using:
   - `session_key` (from X25519 + HKDF),
   - `cipher = "chacha20-poly1305"`,
   - `aad = "<sender_node_id>-><receiver_node_id>"`.
8. Send either:
   - plain `{ auth, body }` (if encryption is not required), or
   - encrypted packet `{ version, cipher, sender_node_id, receiver_node_id, nonce, tag, ciphertext, context }`.

---

## 7. Receiving a request

### 7.1 If packet is encrypted

1. Verify `version == "nz-crypto-01"`.
2. Verify `cipher == "chacha20-poly1305"` (or supported).
3. Read `sender_node_id`, `receiver_node_id`.
4. Obtain sender’s X25519 public key and receiver’s X25519 private key.
5. Derive `shared_secret` and `session_key` via HKDF as in §5.3.
6. Decrypt `ciphertext` using:
   - `session_key`,
   - `nonce`,
   - `aad = "<sender_node_id>-><receiver_node_id>"`.
7. Parse decrypted JSON as { auth, body }.

### 7.2 Signature and integrity verification

1. Ensure `auth` and `body` are present.
2. Validate presence of `node_id`, `timestamp`, `nonce`, `body_hash`, `signature`.
3. Check `timestamp` is within allowed skew window (e.g. ±300 seconds).
4. Check `nonce` has not been seen before for this `node_id` (replay protection).
5. Compute `real_body_hash = sha256(body)` and compare with `auth.body_hash`.
6. Build `auth_without_signature`, canonicalize, compute `auth_hash = sha256(canonical_auth)`.
7. Obtain Ed25519 public key for `auth.node_id`.
8. Verify signature over `auth_hash` using Ed25519.
9. If all checks pass, the packet is valid and `body` MAY be processed.

---

## 8. Implementation requirements

- All microservices MUST use a shared crypto module (`lib/nz-crypto.js`).
- Crypto primitives MUST be provided by an adapter (`lib/nz-crypto-adapter-pure.js or equivalent`).
- Node keys SHOULD be stored in a dedicated key store (e.g. `keys/node.json`) or managed by an Identity service.
- Public keys of other nodes MUST be discoverable via:
  - static configuration,
  - Identity service,
  - P2P discovery.

All new inter-service protocols MUST:

- either use `{ auth, body }` with signatures,
- or use the encrypted format wrapping `{ auth, body }`.

---

9. Versioning

- version: `"nz-crypto-01"` — current on-wire version used by NZ-CRYPTO-02 spec.
- Future versions MUST increment:
  - `"nz-crypto-02"`, `"nz-crypto-03"`, etc.
- Microservices MUST:
  - reject unknown `version` values,
  - MAY support multiple versions during migration windows.
