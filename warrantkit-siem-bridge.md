# warrantkit-siem-bridge

**SIEM integration and Helm packaging for WarrantKit**

Companion project providing the operational layer for [WarrantKit](https://github.com/Therealdk8890/WarrantKit), a runtime enforcement and proof platform for autonomous agents developed by Daniel Kissel.

This component focuses on evidence normalization, SIEM forwarders, and Kubernetes deployment so security teams can adopt WarrantKit without building integration infrastructure from source.

---

## Capabilities

- Consumes WarrantKit Evidence API / EvidenceEnvelope objects
- Verifies receipt integrity
- Normalizes events into a stable `AgentEvent` schema
- Forwards to Splunk HEC, Datadog Logs, or generic webhooks
- Provides Helm charts for bridge deployment and optional runtime packaging

**Core constraint:** Evidence flows outbound from the runtime. Authority remains exclusively with the WarrantKit runtime. The bridge does not elevate or reinterpret enforcement outcomes.

---

## Architecture

```
WarrantKit Runtime
        │
        ▼ Evidence API / EvidenceEnvelope
┌───────────────────────┐
│  warrantkit-siem-bridge │
│  • verify receipts      │
│  • normalize            │
│  • deduplicate          │
│  • forward              │
└────────────────────────┘
        │
   ┌────┴────┬──────────┐
   ▼         ▼          ▼
Splunk    Datadog    Webhook
```

---

## Relationship to agent-evidence-bridge

| Component | Focus |
|-----------|-------|
| `warrantkit-siem-bridge` | WarrantKit-specific packaging and Helm deployment |
| `agent-evidence-bridge` | Multi-source bridge (WarrantKit, OTLP, webhooks) |

Both components share the same design principles and trust model.

---

## Attribution

- **WarrantKit**, AgentContainment, Evidence API, and all runtime authority semantics — Daniel Kissel ([Therealdk8890](https://github.com/Therealdk8890))
- Bridge implementation, SIEM adapters, and Helm packaging — Th3Krack3r / West Electronics LLC

This project is a companion integration layer and is not a fork of WarrantKit.

---

## License

Apache License 2.0
