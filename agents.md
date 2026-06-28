# Open UHP — Universal Health Protocol

## Purpose
Official open specification of the Universal Health Protocol in protocol mode. Open protocol for the health domain (perception, prioritization, orchestration of care); namespace `u.health`; reuses Open USP (`u.service`) for execution/audit and data transport (transport-agnostic), and Open UDP (`u.delivery`) for physical Last Mile delivery of supplies. Use for implementation and spec reference. The concrete application (SUS/Brazil) lives in the UHP repo `docs/protocolos/`.

## Context
- **manifest/** — Full specification: Abstract (PT/EN), README overview (PT/EN), specification, contracts, messages, security, extensions.
- **examples/** — Placeholder for basic and advanced implementation examples (GRANT_CONSENT → OBSERVE_SIGNAL → ASSESS_PRIORITY → ALLOCATE_RESOURCE → UPDATE_STATUS).
- **REPO_DESCRIPTION.md** — Short description (max 350 chars) for GitHub repo settings.

## Key terms
UHP, u.health, Citizen, Node, Mother Entity, Observer, S1/S2 dual process, GRANT_CONSENT, OBSERVE_SIGNAL, REQUEST_CARE, ASSESS_PRIORITY, ALLOCATE_RESOURCE, UPDATE_STATUS, RAISE_ALERT, Priority Index (P1–P4), Immutable Laws (L1 Supremacy of Care, L2 Algorithmic Equity, L3 Data Sovereignty, L4 Deterministic Transparency, L5 Distributed Resilience), differential privacy, append-only ledger.

## Conventions
- This folder is documentation only. No test files, no code execution. Use pnpm if tooling is ever added.
- Immutable Laws (L1–L5) and the message envelope are the permanent core; everything else is an upper-layer extension.
- The specification here is generic/reusable; do not mix it with the SUS-specific applied vision in `docs/protocolos/`.

## Retrieval
Use `manifest/` for all protocol details. Use `manifest/README.md` for index; `manifest/specification.md` and `manifest/messages.md` for implementation; `manifest/security.md` for the Immutable Laws and compliance.
