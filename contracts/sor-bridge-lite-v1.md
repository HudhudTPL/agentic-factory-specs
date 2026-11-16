# SoR Bridge Lite contract v1 (AF-BRIDGE-LITE-001)

| Field | Value |
| --- | --- |
| **Schema** | `af-sor-bridge-lite/v1` (resources) · `af-sor-bridge-lite-event/v1` (webhooks) |
| **Version** | 1.0.0 |
| **OpenAPI** | [sor-bridge-lite-v1.openapi.yaml](sor-bridge-lite-v1.openapi.yaml) |
| **Non-goals** | Enterprise PLM SDKs (Teamcenter / Windchill / DOORS) — see **AF-BRIDGE-EXT-VENDOR** |

Agentic Factory Bridge Lite is a modular integration layer. The core product runs Git/cloud agentic workflow and evidence compilation; adapters map via webhooks/API to whatever SoR you already run.

## REST revision resource

`GET/PUT /sor/v1/revisions/{revision_id}`

```json
{
  "schema": "af-sor-bridge-lite/v1",
  "revision_id": "REV-C",
  "status": "released",
  "publish_ack": true,
  "verification_evidence_uri": "https://example.invalid/evidence/REV-C",
  "requirements_stub": "optional short requirements pointer",
  "content_sha256": "optional 64-char hex of released bytes (AF does not store the file)",
  "markers_present": ["AF-INPUT-001"],
  "markers_absent": [],
  "text_excerpt": "optional short plain text for marker search",
  "alternative_summary": "",
  "source_system": "file",
  "program_id": "PRJ_HUD_2026_0200",
  "customer_id": "dogfood"
}
```

`status`: `draft` | `released` | `superseded` | `withdrawn`.  
AF never accepts `file_bytes`, `cad_blob`, `geometry`, `mesh`, `bom_items`, or `work_instruction` in this body (same refuse list as RG-051 Call 4).

## Webhook event

`POST /sor/v1/events` (adapter → Factory)

```json
{
  "schema": "af-sor-bridge-lite-event/v1",
  "source_system": "github",
  "event_type": "revision_released",
  "external_id": "ECO-2026-041",
  "revision_id": "REV-C",
  "program_id": "PRJ_HUD_2026_0200",
  "customer_id": "dogfood",
  "verification_evidence_uri": "https://example.invalid/evidence/REV-C"
}
```

Idempotent on `(source_system, event_type, external_id)`.  
`program_id` and `customer_id` must both be set or both empty.

## Read-verify (AF-TOOL-READ-VERIFY-001)

Bridge Lite productizes Call 4 incorporation verify against any revision resource that satisfies the marker/excerpt rules in `external_tool_read_service.parse_revision_payload`. Dispositions remain `incorporated` | `alternative_agreed` | `not_incorporated`.

## Dogfood

```text
python scripts/dogfood_sor_bridge_lite.py
```

File-backed store: `data/sor_bridge_lite_dogfood.json`. Optional GitHub Issues adapter maps an issue to a revision resource when `GITHUB_TOKEN` is set.

### Gate evidence pointers (as shipped)

Factory writes append-only markdown at `artifacts/<PRJ>--project/gate-evidence/sor-bridge-revision-pointers.md` (see [examples/sor-bridge-revision-pointers.md](examples/sor-bridge-revision-pointers.md)). There is no separate normative `af-sor-bridge-revision-pointer/v1` JSON object in the current platform release.

## Honest boundary

This contract does **not** claim bi-directional dual-master sync, vendor SDK certification, or that AF becomes the SoR. The connected product remains the system of record.
