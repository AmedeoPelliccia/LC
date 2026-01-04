# LC
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://aerospace-governance.org/schemas/lifecycle-7lc/v1.0.0/schema.json",
  "title": "7-LC Canonical Lifecycle Schema",
  "description": "Minimum mandatory dataset schema for aerospace lifecycle management.  Applicable to System, Subsystem, LRU, Part, Software, Data, Document.",
  "type":  "object",
  "required": ["metadata", "object_definition", "lifecycle_states"],
  "additionalProperties": false,

  "properties": {
    "metadata": {
      "$ref": "#/$defs/Metadata"
    },
    "object_definition": {
      "$ref": "#/$defs/ObjectDefinition"
    },
    "lifecycle_states": {
      "$ref": "#/$defs/LifecycleStates"
    }
  },

  "$defs": {
    "Metadata": {
      "type": "object",
      "description": "Schema and governance metadata",
      "required": ["schema_version", "created_date", "authority"],
      "properties": {
        "schema_version": {
          "type":  "string",
          "pattern": "^\\d+\\.\\d+\\.\\d+$",
          "description": "Semantic version of this schema",
          "examples": ["1.0.0"]
        },
        "created_date":  {
          "type": "string",
          "format": "date",
          "description":  "ISO 8601 date of record creation"
        },
        "last_modified_date": {
          "type": "string",
          "format": "date",
          "description": "ISO 8601 date of last modification"
        },
        "authority": {
          "type": "string",
          "description": "Governing body or organization",
          "examples": ["Engineering Governance Board"]
        },
        "applicable_standards": {
          "type": "array",
          "items":  {
            "type": "string",
            "enum":  [
              "ARP4754A",
              "ARP4761",
              "DO-178C",
              "DO-254",
              "DO-326A",
              "CS-25",
              "FAR-25",
              "S1000D",
              "ATA-iSpec-2200",
              "MSG-3",
              "ISO-9001",
              "AS9100"
            ]
          },
          "uniqueItems": true
        }
      }
    },

    "ObjectDefinition":  {
      "type": "object",
      "description": "Identity and classification of the managed object",
      "required": ["object_id", "object_type", "name", "ata_chapter"],
      "properties": {
        "object_id": {
          "type":  "string",
          "pattern": "^[A-Z]{2,4}-\\d{2}-\\d{2,3}(-\\d{3})?$",
          "description": "Unique identifier following ATA structure",
          "examples":  ["ECS-21-21-001", "ACM-21-21"]
        },
        "object_type":  {
          "type": "string",
          "enum": [
            "System",
            "Subsystem",
            "LRU",
            "Part",
            "Software",
            "Dataset",
            "Document"
          ],
          "description": "Hierarchical classification of the object"
        },
        "name": {
          "type": "string",
          "minLength": 1,
          "maxLength": 200,
          "description": "Human-readable name"
        },
        "ata_chapter": {
          "type": "string",
          "pattern":  "^\\d{2}(-\\d{2})?(-\\d{2})?$",
          "description": "ATA chapter reference (2, 4, or 6 digits)",
          "examples":  ["21", "21-20", "21-21"]
        },
        "part_number": {
          "type": "string",
          "description": "Manufacturer part number if applicable"
        },
        "serial_number": {
          "type": "string",
          "description": "Serial number if applicable"
        },
        "parent_object_id":  {
          "type": "string",
          "description": "Reference to parent object for hierarchy"
        },
        "safety_relevant": {
          "type": "boolean",
          "default": false,
          "description": "Indicates if object has safety implications"
        },
        "design_assurance_level": {
          "type": "string",
          "enum": ["DAL-A", "DAL-B", "DAL-C", "DAL-D", "DAL-E", "N/A"],
          "description": "Development Assurance Level per ARP4754A"
        }
      }
    },

    "LifecycleStates": {
      "type": "object",
      "description": "State and evidence for each of the 7 lifecycle phases",
      "required": [
        "LC1_Requirements",
        "LC2_Design",
        "LC3_Analysis",
        "LC4_Integration",
        "LC5_Certification",
        "LC6_Operation",
        "LC7_Decommissioning"
      ],
      "properties": {
        "LC1_Requirements":  {
          "$ref": "#/$defs/LC1_Requirements"
        },
        "LC2_Design":  {
          "$ref": "#/$defs/LC2_Design"
        },
        "LC3_Analysis": {
          "$ref": "#/$defs/LC3_Analysis"
        },
        "LC4_Integration": {
          "$ref":  "#/$defs/LC4_Integration"
        },
        "LC5_Certification": {
          "$ref": "#/$defs/LC5_Certification"
        },
        "LC6_Operation":  {
          "$ref": "#/$defs/LC6_Operation"
        },
        "LC7_Decommissioning": {
          "$ref": "#/$defs/LC7_Decommissioning"
        }
      }
    },

    "PhaseStatus": {
      "type": "string",
      "enum": [
        "Not_Started",
        "In_Progress",
        "Complete",
        "Approved",
        "N/A"
      ],
      "description": "Status of lifecycle phase"
    },

    "NAJustification": {
      "type": "object",
      "description": "Required justification when phase is marked N/A",
      "required": ["reason", "approved_by", "approval_date"],
      "properties": {
        "reason": {
          "type":  "string",
          "minLength": 10,
          "description": "Detailed justification for N/A status"
        },
        "approved_by": {
          "type": "string",
          "description":  "Name or ID of approving authority"
        },
        "approval_date":  {
          "type": "string",
          "format": "date"
        },
        "approval_reference": {
          "type": "string",
          "description":  "Document or ticket reference for approval"
        }
      }
    },

    "ArtifactReference": {
      "type":  "object",
      "description": "Reference to an evidence artifact",
      "required": ["artifact_id", "artifact_type", "location"],
      "properties": {
        "artifact_id": {
          "type":  "string",
          "description": "Unique identifier for the artifact"
        },
        "artifact_type": {
          "type":  "string",
          "description": "Type classification of artifact"
        },
        "name": {
          "type": "string",
          "description":  "Human-readable name"
        },
        "version": {
          "type": "string",
          "description":  "Version or revision of artifact"
        },
        "location": {
          "type":  "string",
          "format": "uri",
          "description":  "URI or path to artifact"
        },
        "format": {
          "type": "string",
          "enum":  [
            "PDF",
            "Markdown",
            "XML",
            "JSON",
            "Excel",
            "DOORS",
            "ReqIF",
            "CAD",
            "SysML",
            "Code",
            "S1000D",
            "Database"
          ]
        },
        "hash": {
          "type": "string",
          "pattern": "^sha256:[a-f0-9]{64}$",
          "description": "SHA-256 hash for integrity verification"
        }
      }
    },

    "ApprovalGate": {
      "type": "object",
      "description": "Formal approval gate record",
      "required": ["gate_name", "status"],
      "properties":  {
        "gate_name": {
          "type": "string",
          "description": "Name of the approval gate"
        },
        "status": {
          "type": "string",
          "enum":  ["Pending", "Passed", "Failed", "Waived"],
          "description": "Gate passage status"
        },
        "date": {
          "type": "string",
          "format":  "date"
        },
        "approved_by": {
          "type": "string"
        },
        "minutes_reference": {
          "type": "string",
          "description":  "Reference to meeting minutes or approval record"
        },
        "conditions": {
          "type": "array",
          "items":  {
            "type": "string"
          },
          "description":  "Conditions or actions required post-gate"
        }
      }
    },

    "LC1_Requirements": {
      "type":  "object",
      "description": "LC-1: Requirements Definition - ¿Por qué existe este objeto?",
      "required": ["status"],
      "properties":  {
        "status": {
          "$ref": "#/$defs/PhaseStatus"
        },
        "na_justification": {
          "$ref":  "#/$defs/NAJustification"
        },
        "requirements":  {
          "type": "array",
          "items": {
            "$ref": "#/$defs/Requirement"
          },
          "minItems": 1
        },
        "safety_objectives": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/SafetyObjective"
          },
          "description": "Required if object is safety-relevant"
        },
        "artifacts": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/ArtifactReference"
          }
        },
        "approval_gate": {
          "$ref": "#/$defs/ApprovalGate"
        }
      },
      "if": {
        "properties": {
          "status": { "const": "N/A" }
        }
      },
      "then":  {
        "required": ["status", "na_justification"]
      },
      "else":  {
        "if": {
          "properties": {
            "status": { "enum": ["Complete", "Approved"] }
          }
        },
        "then": {
          "required": ["status", "requirements"]
        }
      }
    },

    "Requirement": {
      "type": "object",
      "required": ["requirement_id", "text", "type", "verification_method"],
      "properties": {
        "requirement_id": {
          "type":  "string",
          "pattern": "^REQ-[A-Z0-9]+-\\d{3,}$",
          "examples": ["REQ-ECS-001", "REQ-ACM-042"]
        },
        "text": {
          "type":  "string",
          "minLength": 10,
          "description": "Requirement statement"
        },
        "type": {
          "type":  "string",
          "enum": ["Functional", "Safety", "Environmental", "Interface", "Performance"]
        },
        "source": {
          "type": "string",
          "description": "Upstream traceability reference"
        },
        "verification_method": {
          "type":  "array",
          "items": {
            "type": "string",
            "enum":  ["Analysis", "Test", "Inspection", "Demonstration"]
          },
          "minItems":  1
        },
        "allocated_to": {
          "type": "array",
          "items": {
            "type": "string"
          },
          "description": "Downstream allocation references"
        },
        "rationale": {
          "type": "string"
        }
      }
    },

    "SafetyObjective": {
      "type": "object",
      "required": ["objective_id", "description", "failure_condition", "classification"],
      "properties": {
        "objective_id": {
          "type":  "string",
          "pattern": "^SO-[A-Z0-9]+-\\d{3}$"
        },
        "description": {
          "type": "string"
        },
        "failure_condition":  {
          "type": "string"
        },
        "classification": {
          "type": "string",
          "enum": [
            "Catastrophic",
            "Hazardous",
            "Major",
            "Minor",
            "No_Safety_Effect"
          ]
        },
        "probability_objective": {
          "type": "string",
          "description":  "e.g., <1E-9 per flight hour"
        },
        "derived_dal":  {
          "type": "string",
          "enum": ["DAL-A", "DAL-B", "DAL-C", "DAL-D", "DAL-E"]
        }
      }
    },

    "LC2_Design": {
      "type":  "object",
      "description": "LC-2: Design Definition - ¿Cómo está implementado? ",
      "required": ["status"],
      "properties": {
        "status":  {
          "$ref": "#/$defs/PhaseStatus"
        },
        "na_justification": {
          "$ref": "#/$defs/NAJustification"
        },
        "design_definition": {
          "$ref": "#/$defs/DesignDefinition"
        },
        "interfaces": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/InterfaceDefinition"
          }
        },
        "artifacts": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/ArtifactReference"
          }
        },
        "approval_gate":  {
          "$ref": "#/$defs/ApprovalGate"
        }
      },
      "if": {
        "properties": {
          "status":  { "const": "N/A" }
        }
      },
      "then": {
        "required": ["status", "na_justification"]
      }
    },

    "DesignDefinition": {
      "type": "object",
      "required": ["design_id", "version", "description", "traces_to_requirements"],
      "properties":  {
        "design_id": {
          "type": "string"
        },
        "version": {
          "type": "string"
        },
        "description":  {
          "type": "string"
        },
        "architecture_type": {
          "type": "string",
          "enum":  ["Physical", "Logical", "Software", "Hybrid"]
        },
        "materials": {
          "type": "array",
          "items":  {
            "type": "string"
          }
        },
        "traces_to_requirements":  {
          "type": "array",
          "items": {
            "type": "string"
          },
          "minItems": 1,
          "description":  "Requirement IDs this design implements"
        }
      }
    },

    "InterfaceDefinition":  {
      "type": "object",
      "required": ["interface_id", "type", "connected_to"],
      "properties":  {
        "interface_id": {
          "type": "string"
        },
        "type":  {
          "type": "string",
          "enum": ["Mechanical", "Electrical", "Pneumatic", "Hydraulic", "Data", "Thermal"]
        },
        "connected_to":  {
          "type": "string",
          "description": "Object ID of connected component"
        },
        "icd_reference": {
          "type": "string",
          "description":  "Interface Control Document reference"
        }
      }
    },

    "LC3_Analysis": {
      "type":  "object",
      "description": "LC-3: Analysis & Verification - ¿Funciona según lo esperado?",
      "required": ["status"],
      "properties": {
        "status": {
          "$ref": "#/$defs/PhaseStatus"
        },
        "na_justification": {
          "$ref": "#/$defs/NAJustification"
        },
        "verification_matrix": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/VerificationItem"
          }
        },
        "safety_analyses": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/SafetyAnalysis"
          }
        },
        "technical_analyses": {
          "type": "array",
          "items": {
            "$ref": "#/$defs/TechnicalAnalysis"
          }
        },
        "artifacts":  {
          "type": "array",
          "items": {
            "$ref":  "#/$defs/ArtifactReference"
          }
        },
        "approval_gate": {
          "$ref":  "#/$defs/ApprovalGate"
        }
      },
      "if": {
        "properties": {
          "status": { "const": "N/A" }
        }
      },
      "then":  {
        "required": ["status", "na_justification"]
      }
    },

    "VerificationItem": {
      "type":  "object",
      "required": ["requirement_id", "verification_method", "status"],
      "properties": {
        "requirement_id": {
          "type":  "string"
        },
        "verification_method":  {
          "type": "string",
          "enum": ["Analysis", "Test", "Inspection", "Demonstration"]
        },
        "status": {
          "type": "string",
          "enum":  ["Open", "Passed", "Failed", "Waived"]
        },
        "evidence_reference": {
          "type": "string"
        },
        "waiver_reference": {
          "type": "string",
          "description":  "Required if status is Waived"
        }
      }
    },

    "SafetyAnalysis": {
      "type":  "object",
      "required": ["analysis_id", "type", "status"],
      "properties":  {
        "analysis_id": {
          "type": "string"
        },
        "type":  {
          "type": "string",
          "enum": ["FHA", "PSSA", "SSA", "FTA", "FMEA", "FMES", "CMA", "ZSA"]
        },
        "status":  {
          "type": "string",
          "enum": ["Draft", "Under_Review", "Approved"]
        },
        "document_reference": {
          "type": "string"
        },
        "findings": {
          "type": "array",
          "items":  {
            "type": "string"
          }
        }
      }
    },

    "TechnicalAnalysis":  {
      "type": "object",
      "required": ["analysis_id", "type", "status", "compliance_statement"],
      "properties": {
        "analysis_id": {
          "type":  "string"
        },
        "type": {
          "type": "string",
          "enum":  [
            "Thermal",
            "Structural",
            "Fatigue",
            "Damage_Tolerance",
            "EMC",
            "EMI",
            "HIRF",
            "Lightning",
            "Software",
            "Reliability"
          ]
        },
        "status": {
          "type": "string",
          "enum":  ["Draft", "Under_Review", "Approved"]
        },
        "assumptions": {
          "type": "array",
          "items":  {
            "type": "string"
          }
        },
        "results_summary": {
          "type": "string"
        },
        "compliance_statement":  {
          "type": "string"
        },
        "document_reference": {
          "type": "string"
        }
      }
    },

    "LC4_Integration": {
      "type":  "object",
      "description": "LC-4: Integration & Validation - ¿Funciona dentro del sistema?",
      "required": ["status"],
      "properties":  {
        "status": {
          "$ref": "#/$defs/PhaseStatus"
        },
        "na_justification": {
          "$ref": "#/$defs/NAJustification"
        },
        "integration_tests": {
          "type": "array",
          "items": {
            "$ref": "#/$defs/IntegrationTest"
          }
        },
        "non_conformances": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/NonConformance"
          }
        },
        "artifacts": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/ArtifactReference"
          }
        },
        "approval_gate":  {
          "$ref": "#/$defs/ApprovalGate"
        }
      },
      "if": {
        "properties": {
          "status":  { "const": "N/A" }
        }
      },
      "then": {
        "required": ["status", "na_justification"]
      }
    },

    "IntegrationTest":  {
      "type": "object",
      "required": ["test_id", "test_procedure_ref", "status"],
      "properties": {
        "test_id": {
          "type": "string"
        },
        "test_procedure_ref": {
          "type": "string"
        },
        "description": {
          "type": "string"
        },
        "status": {
          "type": "string",
          "enum": ["Not_Run", "Passed", "Failed", "Blocked"]
        },
        "execution_date": {
          "type": "string",
          "format":  "date"
        },
        "report_reference": {
          "type": "string"
        }
      }
    },

    "NonConformance": {
      "type":  "object",
      "required": ["ncr_id", "description", "disposition", "status"],
      "properties": {
        "ncr_id":  {
          "type": "string",
          "pattern":  "^NCR-\\d{4,}$"
        },
        "description": {
          "type": "string"
        },
        "disposition": {
          "type":  "string",
          "enum": ["Use_As_Is", "Rework", "Repair", "Scrap", "Return_to_Vendor"]
        },
        "status":  {
          "type": "string",
          "enum": ["Open", "Closed", "Deferred"]
        },
        "approval_authority": {
          "type": "string"
        },
        "closure_date": {
          "type": "string",
          "format":  "date"
        }
      }
    },

    "LC5_Certification": {
      "type": "object",
      "description":  "LC-5: Certification & Approval - ¿Está legalmente autorizado?",
      "required":  ["status"],
      "properties": {
        "status": {
          "$ref":  "#/$defs/PhaseStatus"
        },
        "na_justification":  {
          "$ref": "#/$defs/NAJustification"
        },
        "certification_basis": {
          "$ref": "#/$defs/CertificationBasis"
        },
        "means_of_compliance": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/MeansOfCompliance"
          }
        },
        "approvals": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/CertificationApproval"
          }
        },
        "artifacts": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/ArtifactReference"
          }
        },
        "approval_gate":  {
          "$ref": "#/$defs/ApprovalGate"
        }
      },
      "if": {
        "properties": {
          "status":  { "const": "N/A" }
        }
      },
      "then": {
        "required": ["status", "na_justification"]
      }
    },

    "CertificationBasis": {
      "type": "object",
      "required": ["applicable_regulations"],
      "properties":  {
        "applicable_regulations": {
          "type": "array",
          "items": {
            "type": "string"
          },
          "minItems": 1,
          "examples": [["CS-25.831", "CS-25.841", "FAR-25.831"]]
        },
        "special_conditions": {
          "type": "array",
          "items":  {
            "type": "string"
          }
        },
        "equivalent_safety_findings": {
          "type": "array",
          "items":  {
            "type": "string"
          }
        },
        "exemptions": {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      }
    },

    "MeansOfCompliance": {
      "type": "object",
      "required": ["regulation_ref", "compliance_method", "status"],
      "properties": {
        "regulation_ref": {
          "type":  "string"
        },
        "compliance_method": {
          "type": "string",
          "enum": [
            "MC0_Compliance_Statement",
            "MC1_Design_Review",
            "MC2_Calculation",
            "MC3_Safety_Assessment",
            "MC4_Laboratory_Test",
            "MC5_Ground_Test",
            "MC6_Flight_Test",
            "MC7_Simulation",
            "MC8_Equipment_Qualification",
            "MC9_Analysis",
            "MC10_Similarity"
          ]
        },
        "evidence_reference": {
          "type": "string"
        },
        "status": {
          "type": "string",
          "enum": ["Open", "Submitted", "Under_Review", "Approved", "Rejected"]
        }
      }
    },

    "CertificationApproval": {
      "type": "object",
      "required":  ["authority", "approval_type", "status"],
      "properties": {
        "authority":  {
          "type": "string",
          "enum": ["EASA", "FAA", "TCCA", "ANAC", "CAAC", "Other_NAA"]
        },
        "approval_type": {
          "type": "string",
          "enum":  ["Type_Certificate", "STC", "ETSO", "TSO", "PMA", "Minor_Change", "Major_Change"]
        },
        "approval_reference": {
          "type": "string"
        },
        "status": {
          "type": "string",
          "enum":  ["Applied", "Under_Review", "Approved", "Suspended", "Revoked"]
        },
        "issue_date": {
          "type": "string",
          "format": "date"
        },
        "limitations": {
          "type": "array",
          "items":  {
            "type": "string"
          }
        }
      }
    },

    "LC6_Operation": {
      "type":  "object",
      "description": "LC-6: Operation & Maintenance - ¿Cómo se mantiene seguro en servicio?",
      "required": ["status"],
      "properties": {
        "status": {
          "$ref": "#/$defs/PhaseStatus"
        },
        "na_justification": {
          "$ref": "#/$defs/NAJustification"
        },
        "operational_documents": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/OperationalDocument"
          }
        },
        "service_bulletins": {
          "type": "array",
          "items": {
            "$ref": "#/$defs/ServiceBulletin"
          }
        },
        "airworthiness_directives": {
          "type": "array",
          "items": {
            "$ref": "#/$defs/AirworthinessDirective"
          }
        },
        "in_service_events": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/InServiceEvent"
          }
        },
        "artifacts": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/ArtifactReference"
          }
        },
        "approval_gate":  {
          "$ref": "#/$defs/ApprovalGate"
        }
      },
      "if": {
        "properties": {
          "status":  { "const": "N/A" }
        }
      },
      "then": {
        "required": ["status", "na_justification"]
      }
    },

    "OperationalDocument":  {
      "type": "object",
      "required": ["document_type", "document_id", "revision"],
      "properties":  {
        "document_type": {
          "type": "string",
          "enum": ["AMM", "CMM", "IPC", "SRM", "WDM", "FIM", "TSM", "MEL", "CDL"]
        },
        "document_id": {
          "type": "string"
        },
        "revision": {
          "type": "string"
        },
        "s1000d_dmc":  {
          "type": "string",
          "description": "S1000D Data Module Code if applicable"
        },
        "effectivity":  {
          "type": "string"
        }
      }
    },

    "ServiceBulletin":  {
      "type": "object",
      "required": ["sb_number", "title", "compliance_category"],
      "properties":  {
        "sb_number": {
          "type": "string"
        },
        "title": {
          "type": "string"
        },
        "issue_date": {
          "type": "string",
          "format": "date"
        },
        "revision": {
          "type": "string"
        },
        "compliance_category":  {
          "type": "string",
          "enum": ["Mandatory", "Alert", "Recommended", "Optional"]
        },
        "effectivity": {
          "type": "string"
        },
        "compliance_status": {
          "type": "string",
          "enum":  ["Not_Started", "In_Progress", "Complied", "Not_Applicable"]
        }
      }
    },

    "AirworthinessDirective": {
      "type": "object",
      "required": ["ad_number", "issuing_authority", "compliance_status"],
      "properties": {
        "ad_number": {
          "type": "string"
        },
        "issuing_authority": {
          "type": "string",
          "enum":  ["EASA", "FAA", "Other"]
        },
        "effective_date": {
          "type": "string",
          "format": "date"
        },
        "compliance_time": {
          "type": "string"
        },
        "compliance_status":  {
          "type": "string",
          "enum": ["Open", "Complied", "Terminated", "Not_Applicable"]
        },
        "compliance_date": {
          "type": "string",
          "format":  "date"
        }
      }
    },

    "InServiceEvent": {
      "type":  "object",
      "required": ["event_id", "event_type", "date"],
      "properties":  {
        "event_id": {
          "type": "string"
        },
        "event_type": {
          "type": "string",
          "enum": [
            "Failure",
            "Malfunction",
            "Degradation",
            "Incident",
            "Accident",
            "Pilot_Report",
            "Maintenance_Finding"
          ]
        },
        "date": {
          "type": "string",
          "format":  "date"
        },
        "description": {
          "type": "string"
        },
        "corrective_action": {
          "type": "string"
        },
        "feedback_to_lc1": {
          "type": "boolean",
          "default":  false,
          "description":  "Indicates if event triggered requirement update"
        },
        "linked_requirement":  {
          "type": "string",
          "description":  "Requirement ID if feedback_to_lc1 is true"
        }
      }
    },

    "LC7_Decommissioning": {
      "type": "object",
      "description": "LC-7: Decommissioning - ¿Cómo se retira sin riesgo ni deuda?",
      "required": ["status"],
      "properties":  {
        "status": {
          "$ref": "#/$defs/PhaseStatus"
        },
        "na_justification": {
          "$ref": "#/$defs/NAJustification"
        },
        "disposal_procedure": {
          "$ref": "#/$defs/DisposalProcedure"
        },
        "closure_record": {
          "$ref": "#/$defs/ClosureRecord"
        },
        "artifacts": {
          "type": "array",
          "items":  {
            "$ref": "#/$defs/ArtifactReference"
          }
        },
        "approval_gate":  {
          "$ref": "#/$defs/ApprovalGate"
        }
      },
      "if":  {
        "properties": {
          "status": { "const": "N/A" }
        }
      },
      "then": {
        "required": ["status", "na_justification"]
      }
    },

    "DisposalProcedure":  {
      "type": "object",
      "required": ["procedure_id", "environmental_compliance"],
      "properties":  {
        "procedure_id": {
          "type": "string"
        },
        "hazardous_materials":  {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "material":  {
                "type": "string"
              },
              "handling_instructions": {
                "type": "string"
              }
            }
          }
        },
        "recyclable_components": {
          "type": "array",
          "items":  {
            "type": "string"
          }
        },
        "recycling_instructions": {
          "type": "string"
        },
        "environmental_compliance":  {
          "type": "array",
          "items": {
            "type": "string"
          },
          "description": "Applicable environmental regulations",
          "examples": [["REACH", "RoHS", "WEEE"]]
        }
      }
    },

    "ClosureRecord": {
      "type":  "object",
      "required": ["final_configuration", "archive_location", "retention_period", "closure_date"],
      "properties": {
        "final_configuration": {
          "type": "string",
          "description":  "Final configuration state at decommissioning"
        },
        "archive_location": {
          "type":  "string",
          "format": "uri",
          "description":  "Location of archived lifecycle records"
        },
        "retention_period": {
          "type": "string",
          "description":  "Required retention period for records",
          "examples": ["Design life + 2 years", "30 years"]
        },
        "closure_date": {
          "type": "string",
          "format": "date"
        },
        "authorized_by": {
          "type": "string"
        },
        "authorization_reference": {
          "type": "string"
        }
      }
    }
  }
}
