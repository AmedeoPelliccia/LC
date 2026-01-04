# LC — 7-LC Canonical Lifecycle Governance Framework

This repository implements the **7-LC Canonical Lifecycle Model** for aerospace lifecycle management, providing schema definitions and governance agent specifications.

## Overview

The 7-LC framework enforces structured lifecycle governance for all managed objects within aerospace programs, including:

- **System**
- **Subsystem**
- **LRU** (Line Replaceable Unit)
- **Part**
- **Software**
- **Dataset**
- **Document**

## The 7-LC Canonical Lifecycle Model

Every object **MUST** have an explicit state in each of the following lifecycle phases:

| Phase | Name | Description |
|-------|------|-------------|
| LC-1 | Requirements | Why does this object exist? |
| LC-2 | Design | How is it implemented? |
| LC-3 | Analysis & Verification | Does it work as expected? |
| LC-4 | Integration & Validation | Does it work within the system? |
| LC-5 | Certification & Approval | Is it legally authorized? |
| LC-6 | Operation & Maintenance | How is it kept safe in service? |
| LC-7 | Decommissioning | How is it retired without risk or debt? |

If a lifecycle phase does not apply to an object, it **MUST** be declared as **N/A with approved justification**.

## Repository Structure

```
├── README.md                           # This file
├── schemas/
│   └── lifecycle-7lc.schema.json       # JSON Schema for 7-LC model
├── agents/
│   └── lifecycle-governance-agent.md   # Agent specification
├── references/
│   └── ata21/
│       └── ata21-reference-schema.md   # ATA 21 decomposition & conventions
└── examples/
    └── ata21/
        ├── ecs-21-system.json          # ECS System object
        ├── ecs-21-30-subsystem.json    # Pressurization Control Subsystem
        └── ofv-21-30-001-lru.json      # Outflow Valve LRU
```

## Schema

The JSON Schema for the 7-LC model is located at [`schemas/lifecycle-7lc.schema.json`](schemas/lifecycle-7lc.schema.json).

### Applicable Standards

The schema supports compliance with:
- ARP4754A, ARP4761
- DO-178C, DO-254, DO-326A
- CS-25, FAR-25
- S1000D, ATA-iSpec-2200
- MSG-3
- ISO-9001, AS9100

## Governance Agent

The [Lifecycle & Governance Authority Agent](agents/lifecycle-governance-agent.md) enforces:

1. **Structure Governance** — Valid classification and hierarchy
2. **Lifecycle Control** — Complete 7-LC states with evidence
3. **Mandatory Traceability** — All artifacts trace to requirements
4. **N/A Management** — Justified and approved exemptions only
5. **Domain Separation** — Verification ≠ Validation, Certification is a legal state

## ATA Reference Schemas

The framework includes reference decompositions for ATA chapters with canonical hierarchies, object ID conventions, and example instances:

| ATA Chapter | System | Reference |
|-------------|--------|-----------|
| ATA 21 | Environmental Control System (ECS) | [Reference Schema](references/ata21/ata21-reference-schema.md) |

*Additional ATA chapters will be added as the framework expands.*

See [`examples/`](examples/) for schema-compliant JSON object instances.

## Compliance Outputs

When evaluating an object, the agent produces one of:

| Status | Meaning |
|--------|---------|
| **COMPLIANT** | Object meets 7-LC Canon, baseline-ready |
| **CONDITIONALLY COMPLIANT** | Partial compliance, conditions listed |
| **NON-COMPLIANT** | Missing LC, traceability, or invalid evidence |

## Fundamental Principle

> **If an object cannot demonstrate its complete lifecycle, it does not officially exist within the system.**

This principle is non-negotiable.

## License

This framework is provided for aerospace lifecycle governance purposes.
