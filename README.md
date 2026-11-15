# Agentic Factory Public Interface Specifications

[![ISO 13485:2016](https://img.shields.io/badge/Certified-ISO_13485:2016-blue.svg)](https://www.hudhudtpl.com)
[![ISO/IEC 27001:2022](https://img.shields.io/badge/Certified-ISO/IEC_27001:2022-green.svg)](https://www.hudhudtpl.com)
[![ISO 9001:2015](https://img.shields.io/badge/Certified-ISO_9001:2015-orange.svg)](https://www.hudhudtpl.com)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)

**Public schemas, API/webhook contracts, and security whitepapers for Agentic Factory (AF).**

Developed by **[Hudhud Technologies](https://www.hudhudtpl.com)**, Agentic Factory is an AI-assisted systems engineering and SDLC control plane for regulated delivery (MedTech, connected devices, SaMD, and aerospace). AF orchestrates programs from requirements through architecture, design, verification, and release—with AI makers, deterministic automated checkers, and named human gates for engineering and quality sign-off.

> **Zero IP Risk Notice:** This repository contains only public outward-facing schemas, integration contracts, and compliance mapping documentation. The underlying deterministic execution harnesses, gate admission controllers, and proprietary engine internals remain closed-source and private.

---

## Repository Structure

```text
agentic-factory-specs/
├── schemas/
│   ├── af-audit-evidence-pack-v1.schema.json         # JSON Schema for continuous DHF / evidence bundles
│   ├── af-aims-transparency-register-v1.schema.json  # Schema for ISO 42001 / EU AI Act model disclosures
│   └── examples/
│       ├── audit-evidence-pack-index-sample.json     # Sanitized evidence pack manifest (INDEX.json)
│       └── transparency-register-sample.json         # Sanitized AI model & prompt template inventory
├── contracts/
│   ├── sor-bridge-lite-v1.openapi.yaml              # OpenAPI 3.0.3 specification for SoR Bridge Lite
│   ├── sor-bridge-lite-v1.md                        # Contract integration & webhook specification
│   └── examples/
│       ├── sor-bridge-lite-sample-payload.json       # Sample revision resource payload
│       └── sor-bridge-revision-pointer.json          # Gate evidence pointer linked to SoR revision IDs
├── whitepapers/
│   ├── iso27001-soc2-tsc-mapping-whitepaper.md      # Markdown source for security mapping whitepaper
│   └── iso27001-soc2-tsc-mapping-whitepaper.pdf     # Publication-grade PDF whitepaper
├── LICENSE                                          # Apache 2.0 open-specification license
└── README.md
```

---

## 1. Audit Evidence Pack (`af-audit-evidence-pack/v1`)

The **Audit Evidence Pack** (`AF-AUDIT-PACK-001`) defines a standardized sidecar manifest for exportable regulatory evidence. It continuously stitches:
- **Design Controls (FDA 21 CFR 820.30 / ISO 13485 §7.3):** Requirements, trace matrices (RTM), risk management states, and verification reports.
- **AI Transparency (ISO/IEC 42001 & EU AI Act):** Model identifiers, immutable prompt template hashes, tool allow-lists, and egress boundaries.
- **Deterministic Checkers & E-Signatures:** Tier-1 deterministic test verdicts, gate outcomes, and 21 CFR Part 11 electronic signature audit trails.

### Benchmarked ROI
* **Manual DHF & Evidence Compilation:** ~90 minutes (experienced QM/RA).
* **Automated Sidecar Export:** **2.3 seconds** (deterministic, cryptographic SHA-256 manifest).

Explore:
* [Audit Evidence Pack Schema](schemas/af-audit-evidence-pack-v1.schema.json)
* [AI Transparency Register Schema](schemas/af-aims-transparency-register-v1.schema.json)
* [Sanitized Manifest Example](schemas/examples/audit-evidence-pack-index-sample.json)

---

## 2. System of Record (SoR) Bridge Lite (`af-sor-bridge-lite/v1`)

The **Bridge Lite Contract** (`AF-BRIDGE-LITE-001`) defines an open REST and webhook specification that bridges enterprise engineering tools without displacing them.

* **No Rip-and-Replace:** Your PLM (Windchill, Teamcenter, Arena), ALM (Jira, DOORS), CAD, and Git remain authoritative systems of record.
* **Zero Byte Storage:** Agentic Factory never stores customer CAD geometries, proprietary binary blobs, or native files. It stores only cryptographic SHA-256 content fingerprints and revision statuses.
* **Credentialed Read-Verify (`AF-TOOL-READ-VERIFY-001`):** Productizes automated incorporation checks to ensure software and firmware revisions match approved upstream baselines before lifecycle gates advance.

Explore:
* [OpenAPI 3.0.3 Contract](contracts/sor-bridge-lite-v1.openapi.yaml)
* [Integration Specification](contracts/sor-bridge-lite-v1.md)
* [Sample Revision Payload](contracts/examples/sor-bridge-lite-sample-payload.json)

---

## 3. Sovereign Runtime & Security Mapping Whitepaper

For defense, aerospace, and high-risk medical device deployments, Agentic Factory deploys as a **Sovereign Runtime SKU** (`AF-SOVEREIGN-SKU-001`):
* **Zero-Egress Guardrails:** Intercepts and blocks public LLM HTTP calls, forcing execution through local air-gapped SLMs or customer-managed private VPC endpoints.
* **SOC 2 Alignment:** Provides enterprise procurement teams with a direct mapping from Hudhud’s certified **ISO/IEC 27001:2022 ISMS** to the **AICPA Trust Services Criteria (Security, Availability, Confidentiality, Processing Integrity, Privacy)**.

Explore:
* [Download Whitepaper (PDF)](whitepapers/iso27001-soc2-tsc-mapping-whitepaper.pdf)
* [View Whitepaper Source (Markdown)](whitepapers/iso27001-soc2-tsc-mapping-whitepaper.md)

---

## Commercial Engagement Models

1. **Turnkey Companion App / Firmware (Startups):** Co-develop or build connected products, delivering an audit-ready DHF compiled under Hudhud's ISO 13485:2016 certified QMS.
2. **Co-Development Acceleration (Mid-Market MedTech):** Embed Agentic Factory alongside existing ALM/PLM tools to ledger continuous digital traceability in real time.
3. **Internal Control Plane Licensing (CDMOs & Engineering Houses):** License Agentic Factory to automate DHF assembly and trace matrix generation, protecting fixed-bid delivery margins.

---

## About Hudhud Technologies

Hudhud Technologies is an engineering technology company certified to:
* **ISO 13485:2016** (Medical devices — Quality management systems)
* **ISO/IEC 27001:2022** (Information security, cybersecurity and privacy protection)
* **ISO 9001:2015** (Quality management systems)

For commercial inquiries, platform walkthroughs, or partnership discussions:
* **Website:** [www.hudhudtpl.com](https://www.hudhudtpl.com)
* **Contact:** [ayesha.irshad@hudhudtpl.com](mailto:ayesha.irshad@hudhudtpl.com)

---

## License

All schemas, OpenAPI specifications, and integration contracts in this repository are licensed under the [Apache License 2.0](LICENSE).
