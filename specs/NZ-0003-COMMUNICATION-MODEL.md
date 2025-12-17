# NZ-0003: Communication Model
Version: draft v0  
Status: Active  
Category: Core  

## 1. Purpose

This specification defines the conceptual communication model used in the NewZone standard.  
It describes how nodes exchange messages, how communication flows are structured, and how interactions remain deterministic, minimalistic, and platform‑agnostic.  
This document does not define specific protocols or message formats; those are defined in later specifications.

---

## 2. Scope

This specification covers:

- the conceptual model of communication between nodes  
- message flow principles  
- interaction patterns  
- constraints ensuring autonomy and durability  
- terminology used across communication‑related specifications  

This specification does **not** define routing, addressing, or transport mechanisms.  
Those are defined in NZ‑0004 and subsequent documents.

---

## 3. Terminology

**Node** — any entity capable of sending or receiving messages.  
**Message** — a structured unit of communication between nodes.  
**Channel** — a logical pathway for message exchange.  
**Session** — a temporary logical context for multi‑step communication.  
**Envelope** — metadata required for message interpretation.  
**Payload** — the content of the message.  
**Flow** — a sequence of messages forming a logical interaction.

---

## 4. Principles

### 4.1 Minimalism
Communication must use the smallest viable structure.  
No unnecessary metadata or fields are allowed.

### 4.2 Determinism
Message interpretation must be identical across all implementations.

### 4.3 Autonomy
Nodes must be able to communicate without centralized services or authorities.

### 4.4 Durability
The communication model must remain stable for decades, independent of transport technologies.

### 4.5 Layer Separation
Communication must be independent from routing, identity, and storage layers.

### 4.6 Symmetry
All nodes are equal; no privileged roles or hierarchical communication patterns are allowed.

---

## 5. Design Constraints

1. Messages must be self‑contained and interpretable without external context.  
2. Message structure must be stable and platform‑agnostic.  
3. Communication must not rely on centralized servers or authorities.  
4. Message ordering must be deterministic when required by the flow.  
5. Nodes must not assume synchronized clocks or shared state.  
6. Communication must support offline, intermittent, and degraded environments.  
7. The model must support both synchronous and asynchronous flows.

---

## 6. Communication Model

The NewZone communication model consists of three conceptual layers:

### 6.1 Message Layer
Defines the structure of a message:

- Envelope  
- Payload  

The envelope contains minimal metadata required for interpretation.  
The payload contains the actual content.

### 6.2 Channel Layer
Defines logical pathways between nodes:

- direct channels  
- broadcast channels  
- ephemeral channels  
- persistent channels  

Channels are logical constructs and do not imply specific transport mechanisms.

### 6.3 Flow Layer
Defines interaction patterns:

- request → response  
- publish → subscribe  
- broadcast → receive  
- multi‑step sessions  

Flows must be deterministic and must not rely on hidden state.

---

## 7. Message Structure

A message consists of:

1. **Envelope**  
   - sender identity  
   - optional receiver identity  
   - message type  
   - optional flow identifier  

2. **Payload**  
   - structured content defined by higher‑level specifications  

The envelope must be minimal and deterministic.  
The payload must be self‑describing or follow a predefined schema.

---

## 8. Interaction Patterns

### 8.1 Direct Communication
One node sends a message to another node.

### 8.2 Broadcast Communication
One node sends a message to multiple nodes without expecting direct responses.

### 8.3 Session‑Based Communication
Nodes exchange multiple messages forming a logical session.  
Sessions must not rely on synchronized clocks or external state.

### 8.4 Stateless Communication
Nodes exchange messages without maintaining long‑term state.

---

## 9. Security Considerations

- Messages must not expose sensitive information in the envelope.  
- Nodes must validate message structure before processing.  
- Communication must assume adversarial environments.  
- Message tampering must be detectable by higher‑level specifications.  
- Replay attacks must be mitigated without relying on synchronized clocks.

---

## 10. Future Work

- NZ‑0004 Routing Protocol  
- NZ‑0005 Storage Model  
- NZ‑0006 Trust Graph  
- NZ‑0009 Message Envelope Format  
- NZ‑0010 Payload Schema Definition  

---

## 11. References

None.