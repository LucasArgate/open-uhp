# Open UHP Manifest — Universal Health Protocol

**Language**: [🇧🇷 Português](#-visão-geral) | [🇺🇸 English](#-overview)

**Namespace:** `u.health`  
**Version:** 0.1.0  
**Base protocol + data transport:** [Open USP (Universal Service Protocol)](https://github.com/LucasArgate/open-usp) (`u.service`)  
**Physical delivery:** [Open UDP (Universal Delivery Protocol)](https://github.com/LucasArgate/open-udp) (`u.delivery`)

---

## 📖 Visão Geral

O **Universal Health Protocol (UHP)** é um **protocolo aberto** para o domínio da saúde que opera no namespace `u.health`. Define como **sinais de saúde** (clínicos, logísticos, epidemiológicos) são observados, priorizados e respondidos por uma rede de nós — com soberania do dado, equidade algorítmica e transparência determinística como variáveis explícitas do protocolo.

O UHP atua como **camada neural** sobre sistemas existentes: percepção na borda (Sistema 1), deliberação determinística no núcleo (Sistema 2) e auditoria imutável. Não substitui prontuários, RNDS ou e-SUS — **integra** os existentes.

Este manifesto contém a especificação completa: arquitetura (S1/S2 + Entidade Mãe), contratos, mensagens JSON, segurança (soberania do dado, privacidade diferencial, consentimento) e extensões. Reutiliza o [USP](https://github.com/LucasArgate/open-usp) para **descoberta/cotação/reserva de serviços** (prestadores CLT/PJ) **e transporte de dados** (agnóstico), o [UDP](https://github.com/LucasArgate/open-udp) para **entrega física Last Mile** de insumos, e o campo comum `u.core` para **execução/auditoria determinística**.

## 🎯 Princípios Fundamentais

As cinco **Leis Imutáveis** são invariantes do protocolo, validadas na camada de deliberação (S2):

1. **L1 — Supremacia do Cuidado:** Risco de morte/agravamento prioriza preemptivamente sobre burocracia.
2. **L2 — Equidade Algorítmica:** Alocação cega a status político/comercial/socioeconômico.
3. **L3 — Soberania do Dado:** Cidadão é dono do dado; anonimização padrão; consentimento criptográfico.
4. **L4 — Transparência Determinística:** IA propõe, matemática determinística valida e executa, com trilha imutável.
5. **L5 — Resiliência Distribuída:** Offline-first; nó na borda opera mesmo sem o núcleo.

## 📚 Documentação

### Visão e negócio

- [Abstract](./ABSTRACT.md) — Manifesto fundador (PT)
- [Abstract](./ABSTRACT.en.md) — Founding manifesto (EN)

### Especificações técnicas

- [Especificação técnica](./specification.md) — Arquitetura S1/S2, Entidade Mãe, fluxo, estados, exceções
- [Contratos](./contracts.md) — Citizen, Node, Mother Entity, Observer; obrigações
- [Mensagens](./messages.md) — Payloads `u.health`
- [Segurança](./security.md) — Soberania do dado, privacidade diferencial, consentimento, Leis Imutáveis
- [Extensões](./extensions.md) — FHIR, índice de prioridade, motores epidemiológicos, roadmap

## 🏗️ Arquitetura em uma frase

**Node** publica `OBSERVE_SIGNAL` → núcleo computa `ASSESS_PRIORITY` (determinístico) → **Mother Entity** emite `ALLOCATE_RESOURCE` → execução com `UPDATE_STATUS` e, se crítico, `RAISE_ALERT` aos **Observers** — sempre sob `GRANT_CONSENT` quando há PII.

## 🔄 Fluxo resumido

1. **Percepção:** Nós na borda observam sinais (estoque, sintomas anonimizados, telemetria, sinais fracos) e emitem `OBSERVE_SIGNAL`.
2. **Priorização:** O núcleo (S2) computa o `ASSESS_PRIORITY` determinístico (urgência clínica + tempo de espera + impacto funcional + vulnerabilidade).
3. **Orquestração:** A Entidade Mãe emite `ALLOCATE_RESOURCE` (insumo, leito, atenção) com equidade algorítmica.
4. **Execução:** Estados PROPOSED → AUTHORIZED → IN_PROGRESS → COMPLETED (com trilha imutável L4).
5. **Exceções:** `RAISE_ALERT` (surto, ruptura, fraude) aos órgãos de controle; bypass de emergência (L1) quando o risco é iminente.

## 📦 Componentes principais

| Componente | Descrição |
|-------------|-----------|
| **Citizen** | Dono soberano do histórico longitudinal; concede/revoga consentimento. |
| **Node** | Agente na borda (UBS, hospital, clínica, sensor) — percepção e execução local (S1). |
| **Mother Entity** | Núcleo central — deliberação determinística (S2), orquestração e digestor global. |
| **Observer** | Opcional: órgãos de controle, auditoria, comitês de ética (Sistema 3 — Human-in-the-Loop). |
| **Mensagens** | OBSERVE_SIGNAL, REQUEST_CARE, ASSESS_PRIORITY, ALLOCATE_RESOURCE, UPDATE_STATUS, RAISE_ALERT, GRANT_CONSENT. |
| **Estados** | PROPOSED, AUTHORIZED, IN_PROGRESS, COMPLETED, REJECTED, ESCALATED, FROZEN. |

## 🚀 Próximos passos

- Ler a [Especificação técnica](./specification.md) para implementação.
- Consultar [Mensagens](./messages.md) para integração.
- Revisar [Segurança](./security.md) para conformidade (LGPD, consentimento, privacidade diferencial).

---

## 🌐 Overview

The **Universal Health Protocol (UHP)** is an **open protocol** for the health domain operating in the namespace `u.health`. It defines how **health signals** (clinical, logistical, epidemiological) are observed, prioritized, and responded to by a network of nodes — with data sovereignty, algorithmic equity, and deterministic transparency as explicit protocol variables.

UHP acts as a **neural layer** over existing systems: edge perception (System 1), deterministic core deliberation (System 2), and immutable audit. It does not replace medical records or national health systems — it **integrates** existing ones.

This manifest contains the full specification: architecture (S1/S2 + Mother Entity), contracts, JSON messages, security (data sovereignty, differential privacy, consent), and extensions. It reuses [USP](https://github.com/LucasArgate/open-usp) for skill execution/audit **and data transport** (transport-agnostic), and [UDP](https://github.com/LucasArgate/open-udp) for **physical Last Mile delivery** of supplies.

## 🎯 Fundamental principles

The five **Immutable Laws** are protocol invariants, validated at the deliberation layer (S2):

1. **L1 — Supremacy of Care:** Risk of death/deterioration preempts bureaucracy.
2. **L2 — Algorithmic Equity:** Allocation blind to political/commercial/socioeconomic status.
3. **L3 — Data Sovereignty:** Citizen owns the data; anonymization is default; cryptographic consent.
4. **L4 — Deterministic Transparency:** AI proposes, deterministic math validates and executes, with an immutable trail.
5. **L5 — Distributed Resilience:** Offline-first; the edge node operates even without the core.

## 📚 Documentation

- [Abstract (EN)](./ABSTRACT.en.md)
- [Technical specification](./specification.md)
- [Contracts](./contracts.md)
- [Messages](./messages.md)
- [Security](./security.md)
- [Extensions](./extensions.md)

## 🏗️ Architecture in one sentence

**Node** publishes `OBSERVE_SIGNAL` → core computes `ASSESS_PRIORITY` (deterministic) → **Mother Entity** issues `ALLOCATE_RESOURCE` → execution with `UPDATE_STATUS` and, if critical, `RAISE_ALERT` to **Observers** — always under `GRANT_CONSENT` when PII is involved.

---

**Version:** 0.1.0  
**Last update:** June 2026
