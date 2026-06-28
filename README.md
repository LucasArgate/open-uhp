# Open UHP — Universal Health Protocol

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-v0-green.svg)](https://github.com/LucasArgate/uhp)
[![Protocol](https://img.shields.io/badge/protocol-Open%20Protocol-blue)](https://github.com/LucasArgate/open-usp)
[![Namespace](https://img.shields.io/badge/namespace-u.health-blue)](./manifest/)

**Language**: [🇧🇷 Português](#-sobre-o-projeto) | [🇺🇸 English](#-about-the-project)

---

## 📋 Sobre o Projeto

**Open UHP (Universal Health Protocol)** é um **protocolo aberto** para o **domínio da saúde**: percepção, deliberação e orquestração de cuidado, insumos e vigilância epidemiológica. Opera no namespace `u.health` e é a **esfera de saúde** da holarquia universal `u.*`, reutilizando o [Open USP (Universal Service Protocol)](https://github.com/LucasArgate/open-usp) (`u.service`) para execução/auditoria **e transporte de dados** (agnóstico) e o [Open UDP](https://github.com/LucasArgate/open-udp) (`u.delivery`) para **entrega física Last Mile** de insumos. Na tendência em que Google e big techs investem em protocolos como o UCP (Universal Commerce Protocol), o futuro é mais protocolos que aplicações — o UHP é um deles.

Enquanto o USP define *como* pedir um serviço e o UDP define *como* algo se move de A para B, o UHP define *como* sistemas de saúde **observam, priorizam e alocam cuidado** com **equidade**, **soberania do dado** e **transparência determinística** — em ambiente aberto, auditável e offline-first.

> **Posicionamento:** O Open UHP é para a saúde conectada o que o HTTP foi para a web: a **camada neural** que permite que sistemas clínicos, logísticos e epidemiológicos interoperem sem caixa-preta. Não substitui sistemas oficiais (RNDS, e-SUS, SINAN); é o protocolo que os integra como uma rede que percebe, delibera e age.
>
> Este repositório (`docs/open-uhp/`) é o **UHP em modo de protocolo aberto** — a especificação genérica e reutilizável. A aplicação concreta no SUS/Brasil vive na documentação do [repositório UHP](https://github.com/LucasArgate/uhp) (`docs/protocolos/`).

### Princípios de fundação

1. **Supremacia do Cuidado:** A minimização do risco de morte ou agravamento tem prioridade preemptiva absoluta sobre fricção burocrática (L1).
2. **Equidade Algorítmica:** A alocação é cega a status político, comercial ou socioeconômico — obedece à matriz matemática de risco e vulnerabilidade (L2).
3. **Soberania do Dado:** O cidadão é o único dono do histórico longitudinal; anonimização e consentimento criptográfico são padrão (L3).
4. **Transparência Determinística:** A IA propõe; a matemática determinística valida e executa, com trilha imutável (L4).
5. **Resiliência Distribuída:** Offline-first — o nó na borda continua salvando vidas mesmo sem o núcleo (L5).

## 🎯 Objetivos

- **Padronização do cuidado em rede:** Definir contratos e mensagens para observar sinais, priorizar e orquestrar recursos (insumos, leitos, atenção).
- **Interoperabilidade:** Permitir que sistemas legados, prontuários e sensores conversem via mesmo protocolo, sem substituí-los.
- **Soberania e conformidade:** Privacidade diferencial, consentimento criptográfico e conformidade legal (LGPD) por desenho.
- **Extensibilidade:** Suportar perfis FHIR, índices de prioridade, motores epidemiológicos e extensões de domínio sem quebrar a base.

## 📚 Documentação

Toda a especificação está em [`manifest/`](./manifest/):

### Visão e negócio

- [Abstract](./manifest/ABSTRACT.md) — Manifesto fundador (PT)
- [Abstract](./manifest/ABSTRACT.en.md) — Founding manifesto (EN)

### Especificações técnicas

- [Manifest (visão geral)](./manifest/README.md) — Arquitetura e índice
- [Especificação técnica](./manifest/specification.md) — Arquitetura S1/S2, Entidade Mãe, fluxo Observe–Assess–Orchestrate
- [Contratos](./manifest/contracts.md) — Citizen, Node, Mother Entity, Observer; obrigações
- [Mensagens](./manifest/messages.md) — Payloads JSON `u.health`
- [Segurança](./manifest/security.md) — Soberania do dado, privacidade diferencial, consentimento, Leis Imutáveis
- [Extensões](./manifest/extensions.md) — FHIR, índice de prioridade, motores epidemiológicos, roadmap

## 📁 Estrutura do Projeto

```
open-uhp/
├── manifest/              # Especificação e documentação do protocolo
│   ├── README.md          # Visão geral do manifesto
│   ├── ABSTRACT.md        # Manifesto fundador (PT)
│   ├── ABSTRACT.en.md     # Founding manifesto (EN)
│   ├── specification.md
│   ├── contracts.md
│   ├── messages.md
│   ├── security.md
│   └── extensions.md
├── examples/              # Exemplos de implementação (futuro)
│   ├── basic/
│   ├── advanced/
│   └── README.md
├── LICENSE
├── REPO_DESCRIPTION.md    # Descrição para GitHub (até 350 caracteres)
└── README.md
```

## 🤝 Contribuindo

1. Leia o [manifest/README.md](./manifest/README.md) e a [especificação](./manifest/specification.md).
2. Abra issues e PRs para melhorias de texto, schemas ou novos casos de uso.
3. Respeite o namespace `u.health`, as cinco Leis Imutáveis e a compatibilidade com [Open USP](https://github.com/LucasArgate/open-usp) e [Open UDP](https://github.com/LucasArgate/open-udp).

## 📄 Licença

Este projeto está sob a licença MIT. Veja [LICENSE](./LICENSE).

## 👤 Autor

**Lucas Argate** — [GitHub](https://github.com/lucasargate)

---

## 🌐 About the Project

**Open UHP (Universal Health Protocol)** is an **open protocol** for the **health domain**: perception, deliberation, and orchestration of care, supplies, and epidemiological surveillance. It operates under the namespace `u.health` and is the **health sphere** of the universal holarchy `u.*`, reusing [Open USP (Universal Service Protocol)](https://github.com/LucasArgate/open-usp) (`u.service`) for execution/audit **and data transport** (transport-agnostic), and [Open UDP](https://github.com/LucasArgate/open-udp) (`u.delivery`) for **physical Last Mile delivery** of supplies. As Google and big techs invest in protocols like UCP (Universal Commerce Protocol), the trend is toward more protocols than applications — UHP is one of them.

While USP defines *how* to request a service and UDP defines *how* something moves from A to B, UHP defines *how* health systems **observe, prioritize, and allocate care** with **equity**, **data sovereignty**, and **deterministic transparency** — in an open, auditable, offline-first environment.

> **Positioning:** Open UHP is to connected health what HTTP is to the web: the **neural layer** that lets clinical, logistical, and epidemiological systems interoperate without a black box. It does not replace official systems; it is the protocol that integrates them as a network that perceives, deliberates, and acts.

### Founding principles

1. **Supremacy of Care:** Minimizing the risk of death or deterioration has absolute preemptive priority over bureaucratic friction (L1).
2. **Algorithmic Equity:** Allocation is blind to political, commercial, or socioeconomic status — it obeys the mathematical matrix of risk and vulnerability (L2).
3. **Data Sovereignty:** The citizen is the sole owner of the longitudinal record; anonymization and cryptographic consent are the default (L3).
4. **Deterministic Transparency:** AI proposes; deterministic math validates and executes, with an immutable trail (L4).
5. **Distributed Resilience:** Offline-first — the edge node keeps saving lives even without the core (L5).

## 🎯 Goals

- **Networked care standardization:** Define contracts and messages to observe signals, prioritize, and orchestrate resources (supplies, beds, attention).
- **Interoperability:** Let legacy systems, records, and sensors interoperate via the same protocol, without replacing them.
- **Sovereignty and compliance:** Differential privacy, cryptographic consent, and legal compliance (LGPD) by design.
- **Extensibility:** Support FHIR profiles, priority indices, epidemiological engines, and domain extensions without breaking the base.

## 📚 Documentation

All specification is in [`manifest/`](./manifest/):

- [Abstract (EN)](./manifest/ABSTRACT.en.md)
- [Manifest overview](./manifest/README.md)
- [Technical specification](./manifest/specification.md)
- [Contracts](./manifest/contracts.md)
- [Messages](./manifest/messages.md)
- [Security](./manifest/security.md)
- [Extensions](./manifest/extensions.md)

## 📄 License

This project is licensed under the MIT License. See [LICENSE](./LICENSE).

**Version:** 0.1.0  
**Last update:** June 2026
