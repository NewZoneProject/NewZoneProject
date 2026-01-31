# NZ-CRYPTO-SEED v0.1 — Seed Phrase, Password, and Deterministic Key Tree for NewZone

## 0. Metadata

- **Standard:** NZ-CRYPTO-SEED  
- **Version:** v0.1  
- **Status:** Proposed Standard  
- **Author:** NewZoneProject  
- **Dependencies:**  
  - NZ-CRYPTO (Ed25519, X25519, ChaCha20, AES-GCM)  
  - NZ-ID (identifier formats `nz://id/...`)  

---

## 1. Purpose

This standard defines the deterministic cryptographic identity root for the NewZone ecosystem:

- **24-word seed phrase + password (≥ 12 characters) → master_secret → hierarchical key tree**

The standard ensures:

- deterministic identity recovery without storing key files;
- a unified root for:
  - users,
  - nodes,
  - microservices,
  - objects,
  - sessions.

Identity in NewZone is derived from **knowledge**, not from stored artifacts.  
Key files are optional caches and must never be the source of truth.

---

## 2. Seed Phrase

### 2.1 Requirements

- **Exactly 24 words.**  
- **12-word phrases are not allowed.**  
- Dictionary size: **2048 words.**  
- Minimum entropy: **256 bits.**  
- Normalization:
  - lowercase,
  - trim leading/trailing whitespace,
  - collapse multiple spaces.

### 2.2 Format

A single string of 24 space-separated words.  
Dictionary and checksum rules are defined in `NZ-CRYPTO-MNEMONIC`.

---

## 3. Password

### 3.1 Requirements

- **Mandatory.**  
- **Minimum length: 12 characters.**  
- Any Unicode characters allowed.  
- The password:
  - is never stored,
  - is never transmitted,
  - is used exclusively as input to the KDF.

### 3.2 Normalization

Recommended:

- normalize to NFC,
- preserve case and whitespace (password is exact).

---

## 4. Master Secret Derivation

### 4.1 Seed Extraction

```
seed = SeedFromMnemonic(mnemonic)
```

`SeedFromMnemonic` must:

- validate word count (24),
- validate dictionary membership,
- validate checksum (if defined),
- return a binary seed of at least 256 bits.

### 4.2 KDF

```
master_secret = KDF(
    input  = seed || password,
    salt   = "NZ-CRYPTO-SEED-v0.1",
    params = { time, memory, parallelism }
)
```

Requirements:

- Recommended KDF: **Argon2id**.  
- Concatenation `seed || password` must be unambiguous.  
- Salt is fixed for this version.

---

## 5. Deterministic Key Tree

All keys are derived using HKDF:

```
key_material = HKDF(
    master_secret,
    info = "nz:" + path
)
```

- HKDF-SHA256 is recommended.
- Output length: 32 bytes (sufficient for Ed25519, X25519, ChaCha20, AES-GCM).

`path` defines the purpose of the key and must be deterministic.

---

## 6. Identifier and Path Mapping

Identifiers follow `nz://id/...` formats defined in NZ-ID.  
Each identifier maps to a deterministic HKDF path.

### 6.1 User Identity

**Identifier**

```
nz://id/user/<user_id>
```

**Paths**

```
id:user:<user_id>:sign
id:user:<user_id>:enc
```

**Keys**

```
kusersign = HKDF(mastersecret, "nz:id:user:<userid>:sign")
kuserenc  = HKDF(mastersecret, "nz:id:user:<userid>:enc")
```

Used to generate Ed25519 and X25519 private keys.

---

### 6.2 Node Identity

**Identifier**

```
nz://id/node/<node_id>
```

**Paths**

```
id:node:<node_id>:sign
id:node:<node_id>:enc
```

**Keys**

```
knodesign = HKDF(mastersecret, "nz:id:node:<nodeid>:sign")
knodeenc  = HKDF(mastersecret, "nz:id:node:<nodeid>:enc")
```

---

### 6.3 Microservice Identity

**Identifier**

```
nz://id/service/<service_name>/v<version>
```

**Paths**

```
id:service:<service_name>:v<version>:sign
id:service:<service_name>:v<version>:enc
```

**Keys**

```
kservicesign = HKDF(mastersecret, "nz:id:service:<servicename>:v<version>:sign")
kserviceenc  = HKDF(mastersecret, "nz:id:service:<servicename>:v<version>:enc")
```

---

### 6.4 Objects

**Identifier**

```
nz://id/obj/<type>/<object_id>
```

**Path**

```
id:obj:<type>:<object_id>
```

**Key**

```
kobj = HKDF(mastersecret, "nz:id:obj:<type>:<object_id>")
```

Used for symmetric encryption or as material for derived key pairs.

---

### 6.5 Sessions

**Identifier**

```
nz://id/session/<timestamp>/<nonce>
```

**Path**

```
session:<timestamp>:<nonce>
```

**Key**

```
ksession = HKDF(mastersecret, "nz:session:<timestamp>:<nonce>")
```

---

## 7. Key File (Optional Cache)

### 7.1 Purpose

Key files are optional caches for performance.  
They must never be the source of truth.

### 7.2 Requirements

- Every key in the file must be reproducible from:
  - `master_secret`,
  - the corresponding `path`.
- Losing the file must not cause identity loss.

### 7.3 Recommended Contents

- `path`
- key type (Ed25519/X25519/symmetric)
- public key (if applicable)
- metadata (labels, timestamps)

Format defined in `NZ-CRYPTO-FILE`.

---

## 8. Rotation and Forward Secrecy

### 8.1 Rotation

Rotation is performed by modifying the path:

```
id:user:<user_id>:sign:v2
id:service:<name>:v3:enc
```

Or by introducing epochs:

```
longterm:<epoch>
```

### 8.2 Forward Secrecy

Session keys must not be derived directly from `master_secret`.

Recommended:

```
klongterm = HKDF(mastersecret, "nz:longterm:<epoch>")
ksession  = HKDF(klongterm, "nz:session:<timestamp>:<nonce>")
```

Optionally combined with X25519 ECDH.

---

## 9. Compatibility with NZ-CRYPTO

NZ-CRYPTO-SEED adds deterministic key derivation on top of NZ-CRYPTO.

### 9.1 Required Functions

- `deriveMasterSecret(mnemonic, password)``
- `deriveKey(master_secret, path)``

### 9.2 Existing Functions

All NZ-CRYPTO primitives remain unchanged.

---

## 10. Summary

NZ-CRYPTO-SEED v0.1 defines:

- **24-word seed phrase + mandatory password ≥ 12 chars**
- deterministic master secret derivation,
- hierarchical key tree for all NewZone identities,
- strict mapping between `nz://id/...`` and HKDF paths,
- optional key file as a cache,
- rotation and forward secrecy mechanisms.

This standard establishes the cryptographic foundation for identity across the entire NewZone ecosystem.
