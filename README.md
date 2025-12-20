# NewZone Standard

NewZone is a minimalistic, durable, and dependency-free standard for building autonomous digital systems.  
It defines a unified set of specifications covering identity, communication, routing, storage, trust, security, and long-term survivability.

This repository contains:

- core specifications (`/specs/`)
- documentation and templates (`/docs/`, `.github/`)
- standard structure and style guides
- versioning and changelog
- the complete index of all NewZone specifications

All documents follow strict minimalism, portability, and long-term stability principles.

## Goals

- Provide a civilization-scale digital standard
- Ensure autonomy and decentralization
- Maintain platform-agnostic design
- Guarantee deterministic and predictable behavior
- Preserve clarity and structural consistency across decades

## Structure

See `NZ_STANDARD_STRUCTURE.md` for the full repository layout.  
See `NZ_SPEC_INDEX.md` for the list of all specifications.

## Status

Draft v0 — active development phase.  
All specifications are subject to refinement until v1 stabilization.

---

## Reference Implementation (Microservices)

To demonstrate how NewZone principles can be applied in practice, this repository also includes a minimalistic set of stateless, dependency-free microservices:

- Identity Microservice  
- Metadata Microservice  
- Consensus Microservice  

Each service follows the same principles as the standard:

- deterministic behavior  
- strict minimalism  
- no external dependencies  
- long-term portability  
- unified REST API pattern  

These services are located under: `/services/`

They are not part of the standard itself, but serve as a practical reference for implementers.

## Running the Reference Cluster

A minimal multi-service setup is provided via docker-compose.yml.

Start all services:

```bash
docker-compose up --build
```

Stop:

```bash
docker-compose down
```

Services run on:

- Identity → http://localhost:3000
- Metadata → http://localhost:3001
- Consensus → http://localhost:3002

This cluster is optional and exists solely as a demonstration of how NewZone specifications can be implemented in real systems.