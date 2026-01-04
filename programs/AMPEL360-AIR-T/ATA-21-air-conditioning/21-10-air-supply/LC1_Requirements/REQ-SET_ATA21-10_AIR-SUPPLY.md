# Requirement Set — ATA 21-10 Air Supply
**Program:** AMPEL360-AIR-T  
**ATA:** 21-10  
**Parent System:** ECS-21  
**Lifecycle Phase:** LC-1 Requirements

## 1. Scope
ATA 21-10 defines the requirements for aircraft air supply to the ECS, including bleed air extraction, 
regulation, conditioning, and delivery to downstream air conditioning and pressurization subsystems.

## 2. Governing Standards & Guidance
- ARP4754A (requirements and allocation discipline)
- ARP4761 (safety assessment process)
- CS-25 / FAR-25 (airworthiness requirements)
- SAE AS8018 (bleed air performance)
- S1000D (technical publications)

## 3. Assumptions / Operating Context
See: `ENV_REFS_ATA21-10.yaml`

## 4. Requirements Register (Master)

| Req ID | Title | Type | Allocated To | Safety Class | DAL | Verification |
|---|---|---|---|---|---|---|
| REQ-ATA21-10-0001 | Bleed air mass flow capacity | Performance | ATA21-10-BleedSystem | Minor | N/A | Test |
| REQ-ATA21-10-0002 | Bleed air pressure regulation | Functional | ATA21-10-PressureReg | Major | DAL-C | Test+Analysis |
| REQ-ATA21-10-0003 | Bleed air temperature limits | Safety | ATA21-10-TempControl | Hazardous | DAL-B | Test+Analysis |
| REQ-ATA21-10-0004 | Contamination protection | Safety | ATA21-10-Filtration | Major | DAL-C | Test+Inspection |
| REQ-ATA21-10-0005 | Bleed air isolation capability | Safety | ATA21-10-Isolation | Hazardous | DAL-B | Test+Demonstration |
| REQ-ATA21-10-0006 | Engine interface compatibility | Interface | ATA21-10-EngineIF | Minor | N/A | Analysis+Inspection |
| REQ-ATA21-10-0007 | APU bleed compatibility | Interface | ATA21-10-APUIF | Minor | N/A | Analysis |
| REQ-ATA21-10-0008 | Material compatibility (high temp) | Environmental | ATA21-10-Materials | Minor | N/A | Test+Inspection |
| REQ-ATA21-10-0009 | Duct integrity under pressure | Performance | ATA21-10-Ducting | Major | DAL-C | Test+Analysis |
| REQ-ATA21-10-0010 | Maintainability access provisions | Functional | ATA21-10-Access | No_Safety_Effect | N/A | Inspection |

## 5. Global Constraints

### 5.1 Materials
- All pressure-bearing components shall be rated for maximum bleed air temperature plus margin.
- Duct materials shall comply with flammability requirements per CS-25.853.
- No restricted substances per program environmental policy (REACH/RoHS where applicable).

### 5.2 Environmental Envelope
- Operating altitude: 0 to 45,000 ft
- Bleed air temperature range: -40°C to +650°C (engine source)
- Bleed air pressure: up to 45 psig at source

### 5.3 Safety & Operational Risk
- Bleed air overheat conditions shall trigger automatic isolation.
- Loss of bleed air shall not result in loss of aircraft control.
- Contaminated bleed air detection shall initiate crew alert.

### 5.4 Interfaces
- ATA 36 (Pneumatic) — bleed air source
- ATA 71/72 (Power Plant) — engine bleed ports
- ATA 49 (APU) — auxiliary bleed source
- ATA 21-20 (Air Conditioning) — conditioned air delivery
- ATA 21-30 (Pressurization) — cabin pressure supply

## 6. Verification Planning Summary

| Req ID | Method | Acceptance Criteria | Evidence Placeholder |
|---|---|---|---|
| REQ-ATA21-10-0001 | Test | Mass flow ≥ specified value at all flight phases | TR-ATA21-10-FLOW-001 |
| REQ-ATA21-10-0002 | Test+Analysis | Pressure within ±X% of setpoint | TR-ATA21-10-PRESS-001; AN-ATA21-10-PRESS-001 |
| REQ-ATA21-10-0003 | Test+Analysis | Temperature never exceeds limit; overheat shutdown verified | TR-ATA21-10-TEMP-001; AN-ATA21-10-TEMP-001 |
| REQ-ATA21-10-0004 | Test+Inspection | Filtration efficacy demonstrated; no contamination pass-through | TR-ATA21-10-FILT-001; INSP-ATA21-10-FILT-001 |
| REQ-ATA21-10-0005 | Test+Demonstration | Isolation valve closes within X seconds on command | TR-ATA21-10-ISO-001; DEMO-ATA21-10-ISO-001 |
| REQ-ATA21-10-0006 | Analysis+Inspection | Engine bleed port compatibility confirmed | AN-ATA21-10-ENGIF-001; INSP-ATA21-10-ENGIF-001 |
| REQ-ATA21-10-0007 | Analysis | APU bleed characteristics within acceptable range | AN-ATA21-10-APUIF-001 |
| REQ-ATA21-10-0008 | Test+Inspection | Materials certified for temperature range | TR-ATA21-10-MAT-001; INSP-ATA21-10-MAT-001 |
| REQ-ATA21-10-0009 | Test+Analysis | Duct integrity at max pressure with safety factor | TR-ATA21-10-DUCT-001; AN-ATA21-10-DUCT-001 |
| REQ-ATA21-10-0010 | Inspection | Access panels and maintenance provisions verified | INSP-ATA21-10-ACCESS-001 |

## 7. Change Control
- Issue/Rev: I01-R01
- Owner: STK_SE (or your governance AoR)
- Parent Baseline: ECS-21 System Requirements
