# ATA 21 Reference Schema (ECS) — Institutional Decomposition

This document provides the canonical decomposition, object ID conventions, and example instances for **ATA 21 (Environmental Control System)** aligned to the 7-LC Canonical Lifecycle Schema.

---

## 1. Scope

**ATA 21 = Environmental Control System (ECS)** covering:

* Air supply / conditioning (packs)
* Temperature control & distribution
* Pressurization control
* Ventilation
* Equipment cooling (often boundary with ATA 24/42/46 depending on architecture)

---

## 2. Canonical Hierarchy

**System → Subsystem → LRU → Part / Software / Dataset / Document**

### Level 0 — System

| Object ID | Type | Name |
|-----------|------|------|
| `ECS-21` | System | Environmental Control System |

### Level 1 — Subsystems (Canonical Set)

| Object ID | ATA Chapter | Name |
|-----------|-------------|------|
| `ECS-21-10` | 21-10 | Air Supply |
| `ECS-21-20` | 21-20 | Air Conditioning & Temperature Control |
| `ECS-21-30` | 21-30 | Pressurization Control |
| `ECS-21-40` | 21-40 | Ventilation |
| `ECS-21-50` | 21-50 | Equipment Cooling |

### Level 2 — Functional Groupings (Example)

#### 21-20 Air Conditioning & Temperature Control

* Pack / ACM group (Air Cycle Machine)
* Primary Heat Exchanger (PHX)
* Secondary Heat Exchanger (SHX)
* Water separator / condenser
* Temperature control valves (mixing / bypass)
* Sensors (temp/pressure/flow)
* Pack controller (SW/HW)
* Ducting & distribution manifold interfaces

#### 21-30 Pressurization Control

* Outflow valve(s)
* Safety valve(s)
* Cabin pressure controller (SW/HW)
* Cabin pressure sensors
* Pressure schedule logic / modes

---

## 3. Object ID Rules

The schema enforces:
* `object_id` pattern: `^[A-Z]{2,4}-\d{2}-\d{2,3}(-\d{3})?$`
* `ata_chapter` pattern: `^\d{2}(-\d{2})?(-\d{2})?$`

### Naming Convention (Institutional Standard)

| Level | Pattern | Example |
|-------|---------|---------|
| System | `ECS-21` | `ECS-21` |
| Subsystem | `ECS-21-xx` | `ECS-21-20`, `ECS-21-30` |
| LRU | `<TAG>-21-xx-###` | `PCC-21-30-001`, `ACM-21-20-001` |
| Part | `<TAG>-21-xx-###-###` | (Optional deeper suffix) |

### Common TAGs for ATA 21

| TAG | Component |
|-----|-----------|
| `ACM` | Air Cycle Machine |
| `PHX` | Primary Heat Exchanger |
| `SHX` | Secondary Heat Exchanger |
| `TCV` | Temperature Control Valve |
| `OFV` | Outflow Valve |
| `PCC` | Pressure Cabin Controller |
| `PCS` | Pressure Sensor (Cabin) |
| `ECS` | ECS System Controller |

---

## 4. Agent Enforcement Hooks

These are **institutional checks** specific to ATA 21 (they do not change the 7-LC Canon; they are reference constraints):

### 4.1 Hierarchy Integrity

Any object with `ata_chapter` starting `21-` **MUST** have `parent_object_id` resolving upward to `ECS-21`.

```
Violation: Object PCC-21-30-001 has ata_chapter "21-30" but parent_object_id
           does not trace to ECS-21.
Action:    Correct parent_object_id to establish valid hierarchy.
```

### 4.2 Safety Relevance Defaults

The following objects **SHOULD** default `safety_relevant=true` unless justified:

* `ECS-21` (System)
* `ECS-21-30` (Pressurization Control Subsystem)
* `OFV-*` (Outflow Valves)
* `PCC-*` (Pressure Cabin Controllers)

### 4.3 Interface Expectations

ATA 21 **MUST** declare interfaces to at least one of:

| ATA Chapter | Interface Type | Description |
|-------------|----------------|-------------|
| ATA 24 | Electrical | Electrical power, controllers |
| ATA 36 | Pneumatic | Pneumatic supply / bleed (if applicable) |
| ATA 46 | Data | Information systems (if ECS ties to avionics networks) |

These should appear in LC-2 as `interfaces[]` entries.

---

## 5. Example Object Instances

See the [`examples/ata21/`](../../examples/ata21/) directory for complete, schema-compliant JSON instances:

* [`ecs-21-system.json`](../../examples/ata21/ecs-21-system.json) — ECS System
* [`ecs-21-30-subsystem.json`](../../examples/ata21/ecs-21-30-subsystem.json) — Pressurization Control Subsystem
* [`ofv-21-30-001-lru.json`](../../examples/ata21/ofv-21-30-001-lru.json) — Outflow Valve LRU

---

## 6. Related Standards

* ARP4754A — Guidelines for Development of Civil Aircraft and Systems
* ARP4761 — Guidelines and Methods for Conducting the Safety Assessment Process
* CS-25 — Certification Specifications for Large Aeroplanes
* S1000D — International Specification for Technical Publications
* ATA-iSpec-2200 — Information Standards for Aviation Maintenance
