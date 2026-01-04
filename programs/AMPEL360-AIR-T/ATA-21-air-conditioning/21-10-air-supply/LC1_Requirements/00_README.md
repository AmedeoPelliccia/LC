# LC1_Requirements — ATA 21-10 Air Supply (AMPEL360-AIR-T)

## Purpose
Define the authoritative LC-1 requirements baseline for ATA 21-10 (Air Supply).
This dataset is the single source of truth for downstream lifecycle phases LC-2 to LC-7.

## Scope (Object-of-Control)
- Object Type: Subsystem
- ATA Chapter: 21-10
- Parent System: ATA 21 Environmental Control System (ECS)
- Program: AMPEL360-AIR-T

## Functional Intent
Provide conditioned air mass flow with defined pressure, temperature, purity,
and reliability to downstream ECS consumers under all approved operating conditions.

## Mandatory Outputs
- REQ-SET (human-readable master)
- REQ-REGISTER (machine-readable register)
- ENV_REFS (operational environment and assumptions)
- Glossary (terms used in requirements)

## Institutional Rules
1. No design, analysis, test, or document may exist without traceability to a requirement herein.
2. Safety-relevant requirements MUST include hazard linkage and derived DAL where applicable.
3. Material requirements apply to all pressure-bearing and ducted components.
4. Environmental envelopes are mandatory inputs for LC-2 design sizing.
5. Every requirement must be traceable forward:
   LC2 design item(s) → LC3 verification items → LC4 validation tests → LC5 MoC → LC6 maintenance docs → LC7 disposal/closure.
