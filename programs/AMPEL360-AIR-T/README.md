# AMPEL360-AIR-T Aircraft Program

This folder contains the canonical lifecycle management structure for the **AMPEL360-AIR-T** aircraft program, organized according to the **7-LC Canonical Lifecycle Model** and **ATA 100** chapter structure.

---

## Program Structure

```
AMPEL360-AIR-T/
├── README.md                           # This file
├── ATA-XX-<system-name>/               # ATA chapter folders
│   ├── LC1_Requirements/               # Requirements definition
│   ├── LC2_Design/                     # Design artifacts
│   ├── LC3_Analysis/                   # Analysis & Verification
│   ├── LC4_Integration/                # Integration & Validation
│   ├── LC5_Certification/              # Certification & Approval
│   ├── LC6_Operation/                  # Operation & Maintenance
│   ├── LC7_Decommissioning/            # Decommissioning
│   └── XX-YY-<subsystem-name>/         # Subsystem folders (where applicable)
│       ├── LC1_Requirements/
│       ├── LC2_Design/
│       ├── LC3_Analysis/
│       ├── LC4_Integration/
│       ├── LC5_Certification/
│       ├── LC6_Operation/
│       └── LC7_Decommissioning/
```

---

## ATA Chapters Included

### Aircraft General (ATA 05-12)

| ATA | System | Description |
|-----|--------|-------------|
| 05 | Time Limits / Maintenance Checks | Scheduled maintenance intervals |
| 06 | Dimensions and Areas | Aircraft physical specifications |
| 07 | Lifting and Shoring | Jacking and shoring procedures |
| 08 | Leveling and Weighing | Weight and balance |
| 09 | Towing and Taxiing | Ground movement |
| 10 | Parking, Mooring, Storage | Aircraft ground handling |
| 11 | Placards and Markings | Required markings |
| 12 | Servicing | Routine servicing |

### Airframe Systems (ATA 20-46)

| ATA | System | Description |
|-----|--------|-------------|
| 20 | Standard Practices - Airframe | General airframe practices |
| 21 | Air Conditioning | Environmental control system (ECS) |
| 22 | Auto Flight | Autopilot and flight management |
| 23 | Communications | Radio and data communications |
| 24 | Electrical Power | Electrical generation and distribution |
| 25 | Equipment / Furnishings | Cabin and cargo equipment |
| 26 | Fire Protection | Fire detection and suppression |
| 27 | Flight Controls | Primary and secondary flight controls |
| 28 | Fuel | Fuel storage and distribution |
| 29 | Hydraulic Power | Hydraulic systems |
| 30 | Ice and Rain Protection | Anti-icing and de-icing |
| 31 | Indicating / Recording Systems | Instruments and recorders |
| 32 | Landing Gear | Main and nose gear systems |
| 33 | Lights | Interior and exterior lighting |
| 34 | Navigation | Navigation systems |
| 35 | Oxygen | Crew and passenger oxygen |
| 36 | Pneumatic | Bleed air systems |
| 37 | Vacuum | Vacuum systems |
| 38 | Water / Waste | Potable water and waste |
| 42 | Integrated Modular Avionics | IMA systems |
| 44 | Cabin Systems | Cabin management |
| 45 | Central Maintenance System | Onboard maintenance |
| 46 | Information Systems | Data networks |

### Structures (ATA 51-57)

| ATA | System | Description |
|-----|--------|-------------|
| 51 | Standard Practices - Structures | General structural practices |
| 52 | Doors | Access and emergency doors |
| 53 | Fuselage | Fuselage structure |
| 54 | Nacelles / Pylons | Engine mounting structures |
| 55 | Stabilizers | Horizontal and vertical stabilizers |
| 56 | Windows | Windshields and windows |
| 57 | Wings | Wing structure |

### Power Plant (ATA 70-80)

| ATA | System | Description |
|-----|--------|-------------|
| 49 | Airborne Auxiliary Power | APU system |
| 70 | Standard Practices - Engine | General engine practices |
| 71 | Power Plant | Engine installation |
| 72 | Engine | Engine core |
| 73 | Engine Fuel and Control | Engine fuel system |
| 74 | Ignition | Engine ignition |
| 75 | Air | Engine air system |
| 76 | Engine Controls | Engine control system |
| 77 | Engine Indicating | Engine instruments |
| 78 | Exhaust | Engine exhaust |
| 79 | Oil | Engine lubrication |
| 80 | Starting | Engine starting system |

---

## Subsystems with Full Decomposition

The following ATA chapters include subsystem-level folders:

### ATA 21 - Air Conditioning (ECS)
- 21-10 Air Supply
- 21-20 Air Conditioning & Temperature Control
- 21-30 Pressurization Control
- 21-40 Ventilation
- 21-50 Equipment Cooling

### ATA 24 - Electrical Power
- 24-10 Generator Drive
- 24-20 AC Generation
- 24-30 DC Generation
- 24-40 External Power
- 24-50 AC Distribution
- 24-60 DC Distribution

### ATA 27 - Flight Controls
- 27-10 Aileron
- 27-20 Rudder
- 27-30 Elevator
- 27-40 Horizontal Stabilizer
- 27-50 Flaps
- 27-60 Spoiler
- 27-70 Gust Lock
- 27-80 Lift Augmentation

### ATA 28 - Fuel
- 28-10 Storage
- 28-20 Distribution
- 28-30 Dump
- 28-40 Indicating

### ATA 29 - Hydraulic Power
- 29-10 Main System
- 29-20 Auxiliary System
- 29-30 Indicating

### ATA 32 - Landing Gear
- 32-10 Main Gear Doors
- 32-20 Nose Gear Doors
- 32-30 Extension / Retraction
- 32-40 Wheels / Brakes
- 32-50 Steering
- 32-60 Position / Warning

### ATA 36 - Pneumatic
- 36-10 Distribution
- 36-20 Indicating

### ATA 71 - Power Plant
- 71-10 Cowling
- 71-20 Mounts
- 71-30 Fireseals
- 71-40 Attach Fittings
- 71-50 Electrical Harness
- 71-60 Air Intakes
- 71-70 Engine Drains

### ATA 72 - Engine
- 72-10 Turbine Section
- 72-20 Compressor Section
- 72-30 Combustion Section
- 72-40 Governor
- 72-50 Air Bleed

---

## 7-LC Lifecycle Phases

Each folder contains subfolders for the seven canonical lifecycle phases:

| Phase | Folder | Purpose |
|-------|--------|---------|
| LC-1 | `LC1_Requirements/` | Requirements definition — Why does this object exist? |
| LC-2 | `LC2_Design/` | Design definition — How is it implemented? |
| LC-3 | `LC3_Analysis/` | Analysis & Verification — Does it work as expected? |
| LC-4 | `LC4_Integration/` | Integration & Validation — Does it work in the system? |
| LC-5 | `LC5_Certification/` | Certification & Approval — Is it legally authorized? |
| LC-6 | `LC6_Operation/` | Operation & Maintenance — How is it kept safe in service? |
| LC-7 | `LC7_Decommissioning/` | Decommissioning — How is it retired without risk? |

---

## Governance

This program structure is governed by the [Lifecycle & Governance Authority Agent](../../agents/lifecycle-governance-agent.md) and validated against the [7-LC Canonical Lifecycle Schema](../../schemas/lifecycle-7lc.schema.json).

### Core Principle

> **If an object cannot demonstrate its complete lifecycle, it does not officially exist within the system.**

---

## Adding Objects

To add a managed object (System, Subsystem, LRU, Part, Software, Dataset, Document):

1. Create the object JSON file following the schema
2. Place it in the appropriate ATA chapter folder
3. Populate the relevant LC phase subfolders with evidence artifacts
4. Validate against the governance agent

See [examples/ata21/](../../examples/ata21/) for reference object instances.

---

## Related Standards

- ARP4754A — Guidelines for Development of Civil Aircraft and Systems
- ARP4761 — Guidelines and Methods for Conducting the Safety Assessment Process
- DO-178C — Software Considerations in Airborne Systems
- DO-254 — Design Assurance Guidance for Airborne Electronic Hardware
- CS-25 — Certification Specifications for Large Aeroplanes
- S1000D — International Specification for Technical Publications
- ATA-iSpec-2200 — Information Standards for Aviation Maintenance
