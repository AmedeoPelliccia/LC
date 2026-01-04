# Requirement Set — ATA 05 Time Limits / Maintenance Checks
**Program:** AMPEL360-AIR-T  
**ATA:** 05  
**Lifecycle Phase:** LC-1 Requirements

## 1. Scope
ATA 05 defines time-controlled maintenance requirements and scheduled checks to ensure continued airworthiness,
including intervals, thresholds, limits, and associated maintenance planning constraints.

## 2. Governing Standards & Guidance
- ARP4754A (requirements and allocation discipline)
- MSG-3 (maintenance planning logic)
- ATA-iSpec-2200 / S1000D (publication of maintenance tasks)
- CS-25 / FAR-25 (continued airworthiness obligations, as applicable)

## 3. Assumptions / Operating Context
See: `ENV_REFS_ATA05.yaml`

## 4. Requirements Register (Master)
| Req ID | Title | Type | Allocated To | Safety Class | DAL | Verification |
|---|---|---|---|---|---|---|
| REQ-ATA05-0001 | Scheduled task program baseline | Functional | ATA05-Program | No_Safety_Effect | N/A | Inspection |
| REQ-ATA05-0002 | Interval definition structure | Interface | ATA05-DataModel | Minor | N/A | Analysis |
| REQ-ATA05-0003 | Escalation rules (overdue tasks) | Safety | ATA05-OpsRules | Major | DAL-D | Analysis+Inspection |
| REQ-ATA05-0004 | MSG-3 traceability | Compliance | ATA05-Planning | Minor | N/A | Inspection |
| REQ-ATA05-0005 | Publication compatibility | Interface | ATA05-Docs | No_Safety_Effect | N/A | Demonstration |

## 5. Global Constraints
### 5.1 Materials (where physical tags/placards/markings apply)
- Any physical marking/label related to time limits shall meet flammability/ink/adhesive constraints (refer to program FST rules).
- Restricted substances must comply with program environmental policy (REACH/RoHS where applicable).

### 5.2 Safety & Operational Risk
- Overdue maintenance checks must never create a latent unsafe state without explicit mitigation and authority acceptance.
- Any waiver mechanism must be auditable with approval reference and expiry.

## 6. Verification Planning Summary
| Req ID | Method | Acceptance Criteria | Evidence Placeholder |
|---|---|---|---|
| REQ-ATA05-0001 | Inspection | Approved baseline exists; task list complete | EVID-ATA05-BASELINE-001 |
| REQ-ATA05-0002 | Analysis | Interval model supports hours/cycles/calendar; edge cases defined | AN-ATA05-DATAMODEL-001 |
| REQ-ATA05-0003 | Analysis+Inspection | Escalation rules implemented and auditable | AN-ATA05-ESC-001; EVID-ATA05-ESC-LOGIC-001 |
| REQ-ATA05-0004 | Inspection | Each task links to MSG-3 decision logic | EVID-ATA05-MSG3-TRACE-001 |
| REQ-ATA05-0005 | Demonstration | Export to S1000D/ATA-iSpec format is valid | DEMO-ATA05-PUB-001 |

## 7. Change Control
- Issue/Rev: I01-R01
- Owner: STK_SE (or your governance AoR)
