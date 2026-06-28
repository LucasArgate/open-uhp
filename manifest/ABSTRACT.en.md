# Universal Health Protocol (UHP)

### *The patient is not a record. It is a life at risk, owner of their own history.*

**Language**: [🇧🇷 Português](./ABSTRACT.md) | [🇺🇸 English](#1-summary)

**Namespace:** `u.health` | **Base/Data transport:** [Open USP](https://github.com/LucasArgate/open-usp) (`u.service`) | **Physical delivery:** [Open UDP](https://github.com/LucasArgate/open-udp) (`u.delivery`)

---

## 1. Summary

The **Universal Health Protocol (UHP)** is an open protocol standard for the health domain — a **protocol in itself**, not an application. It operates in the namespace `u.health` and is the **health sphere** of the universal holarchy `u.*`, reusing [Open USP (Universal Service Protocol)](https://github.com/LucasArgate/open-usp) (`u.service`) for execution/audit and **data transport** (transport-agnostic), and [Open UDP](https://github.com/LucasArgate/open-udp) (`u.delivery`) for **physical Last Mile delivery** (medicines, vaccines, samples, supplies). As Google and big techs invest in protocols like UCP (Universal Commerce Protocol), the trend is toward more protocols than applications; UHP positions itself as one of them.

It specifies how a network of **Nodes** (clinics, hospitals, sensors) **observes** health signals, how the core **deliberates** on priority and equity, and how resources (supplies, beds, attention) are **orchestrated** — with citizen data sovereignty and clinical safety at the center of the design.

In today's model (an archipelago of systems that do not talk to each other), public health operates blind: stocks run out without warning, outbreaks are detected late, fraud goes unnoticed, and citizen data is trapped in silos. UHP proposes a **neural layer** over existing systems — edge perception, deterministic core deliberation, immutable audit — without replacing them.

---

## 2. The problem UHP addresses

- **Systemic blindness:** Without near-real-time visibility, managers react to ruptures and outbreaks instead of anticipating them.
- **Black-box allocation:** Decisions about who gets supplies, a bed, or attention lack an auditable trail and yield to political/commercial pressure.
- **Data trapped and exposed:** Clinical histories sit in incompatible silos and, paradoxically, remain vulnerable — citizens do not control their own data.
- **Fragility at the edge:** When connectivity drops, the health unit is left without decision support.

UHP does not solve health inequality alone; it provides the **technological tools** for the network to perceive, deliberate, and act with more equity, transparency, and dignity.

---

## 3. Protocol pillars

### I. Fast edge perception (System 1)

Each Node runs a local agent that integrates official APIs, sensors, and weak signals (weather, mobility), detects anomalies, and **proposes** actions — never deciding alone on a critical resource. PII is processed locally; only anonymized inferences leave the node.

### II. Deterministic core deliberation (System 2)

AI proposes; **deterministic math validates and executes**. Epidemiological optimization, priority indices, and law gates run on auditable state machines — never in an LLM black box. Every critical decision generates an immutable trail.

### III. Citizen data sovereignty

Identity and consent are cryptographic (e.g., WebAuthn/gov.br) and **belong to the citizen**. The protocol defaults to anonymization; identified records open only under consent or documented clinical emergency — always traceable.

### IV. Equity as an invariant

Allocation obeys the mathematical matrix of risk and vulnerability — **blind** to political, commercial, or socioeconomic status. Equity is not a configurable policy; it is an immutable law of the protocol.

---

## 4. The five Immutable Laws

UHP codifies five operational invariants, validated at the deliberation layer:

| Law | Statement | Foundation |
| --- | --- | --- |
| **L1 Supremacy of Care** | Risk of death/deterioration preempts bureaucracy. | Manchester Triage; preemptive scheduling. |
| **L2 Algorithmic Equity** | Allocation blind to political/commercial/socioeconomic status. | SIR model ($R_0$); convex optimization. |
| **L3 Data Sovereignty** | Citizen owns the data; anonymization default; cryptographic consent. | LGPD art. 11; differential privacy. |
| **L4 Deterministic Transparency** | AI proposes; math validates and executes; immutable trail. | EBM; neurosymbolic AI; append-only ledger. |
| **L5 Distributed Resilience** | Offline-first; the edge node operates without the core. | CAP theorem (local availability). |

---

## 5. 2026 Vision

- **Edge nodes** (clinics, hospitals) with agents that perceive stock ruptures and clinical signals, operating offline-first.
- **A core** that anticipates outbreaks by cross-referencing weather, mobility, and official data, and orchestrates supplies with algorithmic equity.
- **Citizens** owning their own history, granting access via cryptographic consent.
- **Control bodies** receiving deterministic alerts of fraud and rupture, with an auditable trail.

---

## 6. Commitment

Open UHP commits to:

- Treating care as a **network that perceives, deliberates, and acts**, removing the algorithmic black box.
- Embedding **data sovereignty and clinical safety** as explicit, immutable variables (Laws L1–L5).
- Maintaining **legal compliance** and **institutional endorsement** as a shield, in public light.
- Keeping the protocol **extensible and open**, reusing UDP/USP, so new profiles (FHIR, indices, epidemiological engines) can be adopted without breaking the base.

---

## 7. Open governance — the "GitHub for doctors"

This protocol is **public**. Any physician — or the **physician's programming agent** — can propose a change through an issue or a *pull request*, with evidence and rationale attached.

Medicine already has global consensus processes, and UHP **does not replace them**:

- The **WHO** publishes guidelines (the **GRADE** methodology) and maintains **ICD-11**;
- **Cochrane** synthesizes evidence into systematic reviews;
- Specialty societies issue *guidelines*;
- Terminologies and interoperability are governed by formal processes — **SNOMED CT**, **LOINC**, and the **HL7 FHIR** balloting process.

There are even **versioned, governed** clinical-knowledge platforms: the [openEHR Clinical Knowledge Manager (CKM)](https://ckm.openehr.org/) governs clinical archetypes with semantic versioning and open review rounds; [MAGICapp / MAGIC Evidence Ecosystem](https://www.magicevidence.org/) (with Cochrane) maintains *living guidelines* with version history. These are real advances — but they are centered on **data models** and **evidence guidelines**, and are explicitly **distinct** from the *fork* + *pull request* workflow of software development.

What does **not yet exist** is a "GitHub for doctors": a protocol layer that is **publicly forkable and governed by change proposals (pull requests)**, in which the **operational logic of care** — prioritization criteria, alert triggers, allocation flows — is both human-readable and **machine-executable**, with **immutable provenance** of who proposed, reviewed, and approved each change.

Open UHP is that substrate. Being public and MIT-licensed:

- **Anyone proposes, review is open:** an issue/PR carries authorship, evidence, and a trail — consistent with the Law of Deterministic Transparency (L4).
- **Immutable core, evolving layers:** the five Immutable Laws and the message envelope change only through formal review (P6); what is contextually variable — Priority Index weights, FHIR profiles, epidemiological engines — evolves via PR.
- **A bridge, not a wall:** evidence keeps being produced by existing scientific processes; UHP gives it a **versioned, auditable, executable** form — from clinical consensus to the code that orchestrates care.

---

## 8. License and governance

UHP is released under the **MIT License**, as an open, community-driven standard. It is a protocol of its own, the health domain of the [Open USP](https://github.com/LucasArgate/open-usp) ecosystem, compatible with [Open UDP](https://github.com/LucasArgate/open-udp).

> The specification here is generic and reusable. The concrete application to a national health system — with specific systems, numbers, and institutional framing — lives in the documentation of the [UHP repository](https://github.com/LucasArgate/uhp).

---

*We are not building yet another health system. We are building the language that lets health systems perceive, deliberate, and act as a network — with equity and data sovereignty. Join us in building the protocol of fair and transparent care.*

---

**Version:** 0.1.0  
**Last update:** June 2026  
**Português:** [ABSTRACT.md](./ABSTRACT.md)
