# Agentic Factory Public Interface Specifications

[![ISO 13485:2016](https://img.shields.io/badge/Certified-ISO_13485:2016-blue.svg)](https://www.hudhudtpl.com)
[![ISO/IEC 27001:2022](https://img.shields.io/badge/Certified-ISO/IEC_27001:2022-green.svg)](https://www.hudhudtpl.com)
[![ISO 9001:2015](https://img.shields.io/badge/Certified-ISO_9001:2015-orange.svg)](https://www.hudhudtpl.com)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)

**Public schemas, API/webhook contracts, and security whitepapers for Agentic Factory (AF).**

Developed by **[Hudhud Technologies](https://www.hudhudtpl.com)**, Agentic Factory is an AI-assisted systems engineering and SDLC control plane for regulated delivery (MedTech, connected devices, SaMD, and aerospace). AF orchestrates programs from requirements through architecture, design, verification, and release—with AI makers, deterministic automated checkers, and named human gates for engineering and quality sign-off.

> **Zero IP Risk Notice:** This repository contains only public outward-facing schemas, integration contracts, and compliance mapping documentation. The underlying deterministic execution harnesses, gate admission controllers, and proprietary engine internals remain closed-source and private.

> **Alignment policy:** Schemas and samples in this repository track the **shipped** Agentic Factory platform (`HudhudTPL/AgenticFactoryPlatform`). Aspirational v1.1 shapes are not published as normative samples.

---

## Repository Structure

```text
agentic-factory-specs/
├── schemas/
│   ├── af-audit-evidence-pack-v1.schema.json              # INDEX.json for Audit Evidence Pack
│   ├── af-aims-transparency-register-v1.schema.json       # transparency-register.json (evidence rows)
│   ├── af-sovereign-zero-egress-attestation-v1.schema.json # Sovereign configured-endpoint attestation
│   └── examples/
│       ├── audit-evidence-pack-index-sample.json
│       ├── transparency-register-sample.json
│       └── sovereign-zero-egress-attestation-sample.json
├── contracts/
│   ├── sor-bridge-lite-v1.openapi.yaml
│   ├── sor-bridge-lite-v1.md
│   └── examples/
│       ├── sor-bridge-lite-sample-payload.json
│       ├── sor-bridge-revision-pointers.md               # Gate-evidence markdown (as shipped)
│       └── README.md
├── whitepapers/
│   ├── iso27001-soc2-tsc-mapping-whitepaper.md
│   └── iso27001-soc2-tsc-mapping-whitepaper.pdf
├── LICENSE
└── README.md
```

---

## 1. Audit Evidence Pack (`af-audit-evidence-pack/v1`)

The **Audit Evidence Pack** (`AF-AUDIT-PACK-001`) defines a standardized sidecar manifest for exportable regulatory evidence. It stitches:

- **Design Controls (FDA 21 CFR 820.30 / ISO 13485 §7.3):** Requirements, DHF index pointers, risk/verification evidence when present on the program.
- **AI Transparency (AIMS-oriented):** Evidence rows pointing at CQC/PAQ, MSA exhibit, gate receipts, ABOM, and program id — **not** an ISO/IEC 42001 accreditation certificate and **not** a complete EU AI Act high-risk dossier.
- **Deterministic Checkers & E-Signatures:** Gate receipts and Part 11-oriented e-sign trails when present; human Mark Complete remains mandatory (`claim_boundary`).

### Benchmarked ROI
* **Manual DHF & Evidence Compilation:** ~90 minutes (experienced QM/RA).
* **Automated Sidecar Export:** **2.3 seconds** (deterministic, cryptographic SHA-256 manifest).

Explore:
* [Audit Evidence Pack Schema](schemas/af-audit-evidence-pack-v1.schema.json)
* [AI Transparency Register Schema](schemas/af-aims-transparency-register-v1.schema.json)
* [Sanitized Manifest Example](schemas/examples/audit-evidence-pack-index-sample.json)
* [Transparency Register Example](schemas/examples/transparency-register-sample.json)

---

## 2. System of Record (SoR) Bridge Lite (`af-sor-bridge-lite/v1`)

The **Bridge Lite Contract** (`AF-BRIDGE-LITE-001`) defines an open REST and webhook specification that bridges enterprise engineering tools without displacing them.

* **No Rip-and-Replace:** Your PLM (Windchill, Teamcenter, Arena), ALM (Jira, DOORS), CAD, and Git remain authoritative systems of record.
* **Zero Byte Storage:** Agentic Factory never stores customer CAD geometries, proprietary binary blobs, or native files. It stores revision ids, optional content digests, markers/excerpts, and verification evidence URIs.
* **Credentialed Read-Verify (`AF-TOOL-READ-VERIFY-001`):** Incorporation checks against the Bridge Lite revision resource (Call 4 marker/excerpt rules). Gate evidence pointers are append-only markdown under `artifacts/<PRJ>--project/gate-evidence/sor-bridge-revision-pointers.md`.

Explore:
* [OpenAPI 3.0.3 Contract](contracts/sor-bridge-lite-v1.openapi.yaml)
* [Integration Specification](contracts/sor-bridge-lite-v1.md)
* [Sample Revision Payload](contracts/examples/sor-bridge-lite-sample-payload.json)
* [Sample Gate Evidence Pointers (markdown)](contracts/examples/sor-bridge-revision-pointers.md)

---

## 3. Sovereign Runtime (`af-sovereign-zero-egress-attestation/v1`)

For defense, aerospace, and high-risk medical device deployments, Agentic Factory offers a **Sovereign Runtime SKU** (`AF-SOVEREIGN-SKU-001`):

* **Configured zero-egress attestation:** Fail-closed evaluation of LLM provider settings and base-URL hosts against a public-LLM deny-list when `AGENTIC_FACTORY_SOVEREIGN_MODE` is on. Output lands under `artifacts/sovereign-attestations/`.
* **Honest residual:** This is **configured** endpoint policy, not kernel/OS zero-outbound or classified accreditation.
* **SOC 2 mapping (not Type II):** Whitepaper maps Hudhud’s certified **ISO/IEC 27001:2022 ISMS** to AICPA Trust Services Criteria for procurement — it is **not** a SOC 2 Type II opinion.

Explore:
* [Sovereign Attestation Schema](schemas/af-sovereign-zero-egress-attestation-v1.schema.json)
* [Sanitized Attestation Example](schemas/examples/sovereign-zero-egress-attestation-sample.json)
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
