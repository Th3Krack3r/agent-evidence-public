# warrantkit-siem-bridge

**SIEM + Helm packaging layer for WarrantKit**

Companion project that makes [WarrantKit](https://github.com/Therealdk8890/WarrantKit) usable by security teams.

WarrantKit (by Daniel Kissel) is the runtime enforcement and proof platform.  
This repository is the operational layer on top of it: evidence normalization, SIEM forwarders, and Helm charts so teams can deploy without compiling from source.

---

## What it does

- Consumes WarrantKit Evidence API / EvidenceEnvelope objects
- Verifies receipt integrity
- Normalizes into SIEM-friendly `AgentEvent` records
- Forwards to Splunk HEC, Datadog, or generic webhooks
- Provides Helm chart for the bridge + optional runtime packaging

**Core design rule:** evidence flows out. Authority stays with the WarrantKit runtime. The bridge never upgrades an enforcement claim.

---

## Architecture (high level)

```
WarrantKit Runtime
        │
        ▼ Evidence API / EvidenceEnvelope
┌───────────────────────┐
│  warrantkit-siem-bridge │
│  • verify receipts      │
│  • normalize            │
│  • dedupe by event_id   │
│  • forward              │
└────────────────────────┘
        │
   ┌────┴────┬──────────┐
   ▼         ▼          ▼
Splunk    Datadog    Webhook
```

---

## Relationship to agent-evidence-bridge

`warrantkit-siem-bridge` is the WarrantKit-specific packaging and deployment focus.  
`agent-evidence-bridge` is the more general multi-source bridge (WarrantKit + OTLP + webhooks).

Both share the same design principles and can be used together.

---

## Credits

- **WarrantKit, AgentContainment, Evidence API, and all runtime authority semantics** — Daniel Kissel ([Therealdk8890](https://github.com/Therealdk8890))
- Bridge, SIEM adapters, and Helm packaging — Th3Krack3r / West Electronics LLC

This is a companion product, not a fork.

---

## License

Apache-2.0
