# ISO/IEC 27001 ↔ SOC 2 Trust Services Criteria — mapping whitepaper

| Field | Value |
| --- | --- |
| **Doc ID** | AF-SOVEREIGN-27001-SOC2-MAP-001 |
| **SKU** | **AF-SOVEREIGN-SKU-001** |
| **Status** | 1.0-Draft — mapping aid for sovereign runtime conversations |
| **Owner** | SEC-PO / QM |
| **Disclaimer** | This is a **control mapping whitepaper**, not a SOC 2 Type II report, not an accreditation, and not evidence of Hudhud SOC 2 attestation. Paid Type II remains **AF-SOVEREIGN-EXT-SOC2**. |

## Purpose

Help customers and auditors relate Hudhud’s ISO/IEC 27001 ISMS posture (SoA + SOP-QMS-011) to the AICPA **Trust Services Criteria (TSC)** used in SOC 2. Use it in sovereign / VPC / air-gap deals where buyers ask “how does your 27001 map to SOC 2?” without confusing a map for an audit opinion.

## Sources

| Artifact | Role |
| --- | --- |
| [`iso-27001-statement-of-applicability.md`](iso-27001-statement-of-applicability.md) | Annex A SoA (ISMS-SOA-001) |
| [`../eqms/SOP-QMS-011-information-security-privacy-governance.md`](../eqms/SOP-QMS-011-information-security-privacy-governance.md) | Security/privacy governance; mentions TSC analogy |
| Sovereign zero-egress attestation (`af-sovereign-zero-egress-attestation/v1`) | Technical evidence for configured LLM endpoint deny-list (not OS lockdown) |

## Mapping (indicative)

| TSC category | Example TSC themes | Illustrative 27001 / Hudhud controls |
| --- | --- | --- |
| **Security** | Logical access, change management, system operations | A.5 / A.8 access; Git + CODEOWNERS; runtime hardening; sandbox DENY_ALL |
| **Availability** | Capacity, backup/restore | Ops runbooks; RG-050 bare-metal restore notes |
| **Confidentiality** | Encryption, data classification | TLS in transit (deploy); secrets fail-closed; sovereign mode public-LLM deny |
| **Processing Integrity** | Complete / accurate / timely processing | Deterministic execution mode; dual coverage / Gate 0; gate Mark Complete |
| **Privacy** | Notice, retention, disclosure | SOP-QMS-011 privacy; PHI → privacy_first / deterministic CRS rules |

## Sovereign SKU note

Zero-egress attestation proves **configured** LLM endpoints are not on the public deny-list under sovereign mode. It does **not** replace customer host firewall, private DNS, or classified OS accreditation (RG-036 residual).

## Change control

Revise when SoA Annex A set changes materially or when a paid SOC 2 engagement starts (**AF-SOVEREIGN-EXT-SOC2**).
