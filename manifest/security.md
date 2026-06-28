# Open UHP — Segurança e Leis Imutáveis

A segurança do `u.health` não é uma camada adicional: é o **núcleo do desenho**. Saúde lida com dados sensíveis (LGPD art. 11) e decisões que afetam vidas. Este documento detalha as cinco **Leis Imutáveis** — invariantes do protocolo — e os mecanismos de segurança, privacidade e auditoria.

> As Leis Imutáveis são **axiomas de execução** (P6): escritas uma vez, não mudam. Adaptações ocorrem em camadas superiores. Ver [Extensões](./extensions.md).

---

## 1. As cinco Leis Imutáveis

### L1 — Lei da Supremacia do Cuidado

A alocação de recursos físicos ou de atenção deve **sempre priorizar a minimização do risco de morte ou agravamento**. Fricções burocráticas são ignoradas no momento do socorro.

- **Fundamento:** Protocolo de Triagem de Manchester; escalonamento preemptivo por prioridade.
- **No protocolo:** `band: P1` / `urgency_score ≥ 0.9` ativa bypass de emergência (S1 age antes de S2; reporte determinístico após o fato).

### L2 — Lei da Equidade Algorítmica

O sistema é **cego** para status socioeconômico, influência política e pressão comercial. A distribuição obedece estritamente à matriz matemática de risco e vulnerabilidade.

- **Fundamento:** Modelo SIR, $R_0 = \beta \cdot c \cdot d$; otimização convexa.
- **No protocolo:** `ASSESS_PRIORITY` rejeita payloads que usem variáveis políticas/comerciais como peso de alocação.

$$\min \sum_{i=1}^{n} \left( \beta_i \cdot c_i \cdot d_i \right)$$

### L3 — Lei da Soberania do Dado

O **cidadão é o único dono** do histórico longitudinal. O protocolo opera em **anonimização padrão**; prontuários identificados só são acessados sob demanda justificada e rastreável.

- **Fundamento:** LGPD art. 11 (dados sensíveis); Privacidade Diferencial (Dwork, 2006); sigilo médico (CFM).
- **No protocolo:** PII processada no Nó local; `anonymized: true` por padrão; `consent_ref` obrigatório para dado identificado; chaves clínicas fora do núcleo.

### L4 — Lei da Transparência Determinística

**Nenhuma decisão crítica** pode ser caixa-preta de LLM. A IA **propõe**; a matemática determinística **valida e executa**, com trilha imutável.

- **Fundamento:** Medicina Baseada em Evidências; IA neurosimbólica; ledger append-only (BLAKE3).
- **No protocolo:** toda decisão crítica referencia `rationale_hash`/`evidence_hash` no Ledger; reverts não apagam histórico.

### L5 — Lei da Resiliência Distribuída

A infraestrutura crítica é **offline-first**. Se o núcleo cair, o Nó local continua operando e salvando vidas. Sincronização por **consistência eventual**.

- **Fundamento:** Teorema CAP — durante partição, o UHP escolhe **disponibilidade local**.
- **No protocolo:** sinais `offline_capable` deliberados localmente; reconciliação via `SYNC` (transporte USP) quando a rede retorna.

---

## 2. Camadas de segurança

| Camada | Mecanismo |
| --- | --- |
| **Transporte** | TLS 1.3 (herdado do transporte do [USP](https://github.com/LucasArgate/open-usp)) |
| **Autenticação de Nó** | Certificado mTLS por estabelecimento |
| **Identidade do cidadão** | WebAuthn / gov.br — consentimento criptográfico |
| **Integridade de mensagem** | Assinatura por mensagem + hash encadeado (BLAKE3) |
| **Confidencialidade** | PII processada no edge; AES-256 em repouso; nunca sobe sem anonimização |

---

## 3. Privacidade diferencial

Para vigilância epidemiológica, o núcleo necessita de **agregados estatísticos** — não de prontuários. A privacidade diferencial (Dwork, 2006) injeta ruído criptográfico controlado, permitindo consultas populacionais precisas enquanto torna a reidentificação individual matematicamente inviável.

- Campo `dp_epsilon` em `OBSERVE_SIGNAL` declara o orçamento de privacidade aplicado.
- Inferências sobem ao digestor global **após** a camada de privacidade diferencial.

---

## 4. Consentimento e acesso

```text
Citizen --GRANT_CONSENT(scope, expires)--> Node
Node    --acesso identificado dentro do scope--> registro
Citizen --REVOKE_CONSENT--> Node  (acesso cessa; trilha permanece)
```

| Regra | Descrição |
| --- | --- |
| **Fail-closed** | Sem consentimento válido, dado identificado não é processado. |
| **Escopo mínimo** | Consentimento declara `scope` explícito (ex.: `read:record`). |
| **Expiração** | Consentimento tem validade; renovação é explícita. |
| **Emergência (L1)** | Acesso sob emergência clínica documentada gera trilha reforçada. |

---

## 5. Trilha imutável (auditoria L4)

- Toda transição crítica gera registro **append-only** com hash encadeado (BLAKE3).
- Registros guardam **hashes**, não conteúdo clínico bruto.
- Alteração retroativa é matematicamente detectável.
- A camada de execução/auditoria determinística das ações (`ExecutionRecord`) é do campo comum `u.core`, herdado por todas as esferas; o [USP](https://github.com/LucasArgate/open-usp) (`u.service`) cuida da descoberta/cotação/reserva de serviços e do transporte de dados.

---

## 6. Modelo de ameaças (resumo)

| Ameaça | Defesa |
| --- | --- |
| Reidentificação de cidadão | Privacidade diferencial + PII no edge (L3) |
| Viés político/comercial na alocação | Equidade algorítmica + open source (L2) |
| Decisão opaca / alucinação de LLM | Validação determinística + trilha (L4) |
| Adulteração de histórico | Hash encadeado append-only (L4) |
| Queda do núcleo | Operação offline-first (L5) |
| Nó comprometido | mTLS + assinatura + escopo por `partition_key` |

---

## 7. Conformidade legal

- **LGPD** (Lei nº 13.709/2018), especialmente art. 7º (bases legais) e art. 11 (dados sensíveis de saúde).
- **Marco Civil da Internet** (Lei nº 12.965/2014).
- **Código de Ética Médica** (Resolução CFM nº 2.217/2018) — sigilo profissional.

> Operar à luz pública, com chancela institucional, é o maior escudo do protocolo. Ver Princípios P3/P4 no [repositório de aplicação](https://github.com/LucasArgate/uhp).

---

## 8. Referências

- Dwork, C. (2006). Differential Privacy. *ICALP*.
- Gilbert & Lynch (2002) — Teorema CAP.
- BLAKE3 — [github.com/BLAKE3-team/BLAKE3](https://github.com/BLAKE3-team/BLAKE3)
- Lei nº 13.709/2018 (LGPD); Resolução CFM nº 2.217/2018.
- [Especificação técnica](./specification.md) · [Contratos](./contracts.md) · [Mensagens](./messages.md)

---

*UHP v0.1.0 — especificação documental*
