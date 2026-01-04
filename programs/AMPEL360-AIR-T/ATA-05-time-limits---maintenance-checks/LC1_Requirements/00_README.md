# LC1_Requirements — ATA 05 Time Limits / Maintenance Checks (AMPEL360-AIR-T)

## Purpose
Define the complete LC-1 requirements baseline for ATA 05 (Time Limits / Maintenance Checks).
This dataset is the authoritative source for downstream traceability into LC-2..LC-7.

## Scope (Object-of-Control)
- Object Type: System (program-level ATA chapter)
- ATA Chapter: 05
- Program: AMPEL360-AIR-T

## Mandatory Outputs
- REQ-SET (human-readable master)
- REQ-REGISTER (machine-readable register)
- ENV_REFS (operational environment and assumptions)
- Glossary (terms used in requirements)

## Rules (Institutional)
1. No requirement may exist without:
   - verification method(s)
   - allocation target (system/subsystem/LRU/part/software/document)
2. Requirements of type Safety MUST link to:
   - hazard ids (or explicit "No_Safety_Effect")
   - derived DAL when applicable
3. Every requirement must be traceable forward:
   LC2 design item(s) → LC3 verification items → LC4 validation tests → LC5 MoC → LC6 maintenance docs → LC7 disposal/closure.
