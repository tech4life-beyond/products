# Technical Summary
## KIVAI (Intent Gateway & Interoperability Layer)

---

## 1. Overview

**KIVAI** is a schema-first, deterministic interoperability platform that routes **canonical Intent JSON** into authorized actions across physical and digital devices.

KIVAI is:

- **not** a chatbot or assistant
- **not** a UI product
- **not** a product registry

KIVAI is an **execution gateway**:

AI / UI / Button → Intent JSON → KIVAI → Adapter → Device → ACK + audit log

---

## 2. System Context

Modern ecosystems are fragmented:

- voice assistants are proprietary
- devices use different protocols (Wi-Fi, BLE, Zigbee, IR, HTTP, MQTT)
- “smart home” logic is inconsistent and hard to audit

KIVAI introduces a unified, auditable layer so any front-end can trigger consistent, authorized execution.

---

## 3. Core Architecture

### 3.1 Canonical Intent Contract

KIVAI defines a canonical **Intent JSON** schema (contract-first).

The schema enables:

- validation before execution
- consistent routing fields (device_id / capability / zone)
- traceability metadata (timestamp, language, confidence, request_id)

---

### 3.2 Validation & Normalization

Before any action is executed, KIVAI:

- validates the intent against the schema
- normalizes fields into a deterministic form
- rejects malformed or incomplete intents

---

### 3.3 Authorization & Policy

KIVAI enforces:

- authentication (who is calling)
- authorization (what they can do)
- policy gates (ethical / safety constraints where applicable)

Unauthorized intents must be rejected deterministically.

---

### 3.4 Routing Layer

KIVAI routes intents to an execution target by:

- direct `device_id`, or
- `capability + zone`, resolved via routing rules

Routing produces a deterministic execution plan.

---

### 3.5 Adapter Execution Layer

Execution occurs via **adapters**, which translate intents into device/protocol-specific commands.

Adapters may target:

- Wi-Fi devices (HTTP/REST)
- BLE devices
- IR blasters
- MQTT endpoints
- microcontrollers (e.g., ESP32 as an endpoint)

Adapters are replaceable and device-agnostic.

---

### 3.6 Acknowledgement & Audit

Every execution produces:

- `execution_id`
- deterministic ACK response
- audit record (intent + auth + routing + adapter result)

Auditability is mandatory for safe automation.

---

## 4. Multi-Front-End Model (Voice, App, Button)

KIVAI does not depend on any single input interface.

Typical front-ends include:

- mobile app (sends Intent JSON)
- physical button / remote (sends Intent JSON through a small gateway)
- AI system / LLM (produces Intent JSON)
- voice assistant integrations (future adapters/connectors)

KIVAI remains the stable execution layer regardless of front-end.

---

## 5. Deployment Targets

Recommended deployment model v1.0:

- **Gateway host:** Raspberry Pi / router / local server
- **Network:** local LAN (Ethernet/Wi-Fi)
- **Endpoints:** devices or microcontrollers reachable via adapters

This enables practical demonstrations and real-world pilots.

---

## 6. Operational Behavior

### Normal Operation

- intent received
- schema validated
- authorization applied
- routed to adapter
- device command executed
- ACK returned with `execution_id`
- audit logged

### Failure Modes (Deterministic)

- invalid schema → reject with error
- unauthorized request → reject with error
- adapter failure → ACK indicates failure + audit captures details

---

## 7. Safety & Reliability Considerations

KIVAI emphasizes:

- deterministic processing (no “guessing” at execution time)
- auditable traces for accountability
- policy enforcement before action
- adapter isolation (failures do not corrupt routing logic)

---

## 8. Technical Scope Statement

This summary describes KIVAI’s functional and architectural characteristics for licensing, deployment, and integration purposes.

Detailed implementation, adapters, and deployment scripts are maintained in the `kivai` repository.

---

**End of Technical Summary — KIVAI**
