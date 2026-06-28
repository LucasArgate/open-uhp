# Open UHP — Mensagens (`u.health`)

Payloads JSON do **Universal Health Protocol**. Toda mensagem `u.health` trafega encapsulada no envelope de transporte do [USP](https://github.com/LucasArgate/open-usp) (*transport-agnostic*; `payload_type: EVENT` ou `INFERENCE`/`INSTRUCTION`), preservando soberania do dado e trilha imutável. *(A entrega física de insumos é da esfera [UDP](https://github.com/LucasArgate/open-udp).)*

---

## 1. Envelope comum

Todo payload `u.health` compartilha um cabeçalho:

```json
{
  "ns": "u.health",
  "type": "OBSERVE_SIGNAL",
  "message_id": "uuid-v4",
  "partition_key": "region-or-node-id",
  "timestamp": "2026-06-24T11:22:33Z",
  "source": "node://establishment-id",
  "consent_ref": "consent-uuid-or-null",
  "anonymized": true,
  "signature": "base64-node-signature"
}
```

| Campo | Descrição |
| --- | --- |
| `ns` | Namespace fixo `u.health`. |
| `type` | Tipo da mensagem (ver §2). |
| `partition_key` | Roteamento por região/estabelecimento (sharding do transporte USP). |
| `consent_ref` | Referência ao consentimento; obrigatório quando `anonymized: false`. |
| `anonymized` | `true` por padrão (L3); `false` exige `consent_ref`. |
| `signature` | Assinatura do nó emissor (integridade, L4). |

---

## 2. Tipos de mensagem

| Tipo | Direção | Função |
| --- | --- | --- |
| `GRANT_CONSENT` | Citizen → Node | Concede acesso ao histórico identificado |
| `REVOKE_CONSENT` | Citizen → Node | Revoga consentimento previamente dado |
| `OBSERVE_SIGNAL` | Node → Mother Entity | Sinal anonimizado (clínico/logístico/epidemiológico) |
| `REQUEST_CARE` | Node / Citizen → Mother Entity | Necessidade de cuidado ou recurso |
| `ASSESS_PRIORITY` | Mother Entity (interno) | Resultado determinístico de priorização |
| `ALLOCATE_RESOURCE` | Mother Entity → Node | Orquestra insumo, leito ou atenção |
| `UPDATE_STATUS` | Bidirecional | Atualiza estado da execução |
| `RAISE_ALERT` | Mother Entity → Observer | Alerta de surto, ruptura ou fraude |

---

## 3. GRANT_CONSENT

```json
{
  "ns": "u.health",
  "type": "GRANT_CONSENT",
  "message_id": "…",
  "citizen_did": "did:gov.br:abc123",
  "scope": ["read:record", "share:aggregate"],
  "granted_to": "node://establishment-id",
  "expires_at": "2026-12-31T23:59:59Z",
  "auth_method": "webauthn",
  "signature": "base64-citizen-signature"
}
```

> Sem `GRANT_CONSENT` válido, nenhuma mensagem identificada (`anonymized: false`) é aceita — fail-closed (L3).

---

## 4. OBSERVE_SIGNAL

```json
{
  "ns": "u.health",
  "type": "OBSERVE_SIGNAL",
  "message_id": "…",
  "partition_key": "region-31",
  "anonymized": true,
  "signal_class": "EPIDEMIOLOGICAL",
  "metric": "syndromic.respiratory",
  "value": 42,
  "baseline": 18,
  "confidence": 0.81,
  "weak_signals": ["weather.humidity_high", "trends.spike"],
  "dp_epsilon": 1.0,
  "signature": "…"
}
```

| Campo | Descrição |
| --- | --- |
| `signal_class` | `CLINICAL` \| `LOGISTICAL` \| `EPIDEMIOLOGICAL` \| `RESOURCE` |
| `metric` | Identificador da métrica observada |
| `value` / `baseline` | Valor observado vs. linha de base |
| `confidence` | Confiança da inferência S1 (0–1) |
| `dp_epsilon` | Orçamento de privacidade diferencial aplicado |

---

## 5. REQUEST_CARE

```json
{
  "ns": "u.health",
  "type": "REQUEST_CARE",
  "message_id": "…",
  "anonymized": true,
  "care_type": "specialty.cardiology",
  "factors": {
    "clinical_risk": 0.7,
    "wait_time_days": 90,
    "functional_impact": 0.5,
    "vulnerability": 0.6
  },
  "offline_capable": false,
  "signature": "…"
}
```

O campo `factors` alimenta o cálculo determinístico de `ASSESS_PRIORITY` (ver [especificação §6](./specification.md)).

---

## 6. ASSESS_PRIORITY

Resultado determinístico, gravado na trilha imutável (L4):

```json
{
  "ns": "u.health",
  "type": "ASSESS_PRIORITY",
  "message_id": "…",
  "ref": "request-care-uuid",
  "priority_index": 0.78,
  "band": "P2",
  "urgency_score": 0.78,
  "law_checks": ["L2:pass", "L3:pass", "L4:recorded"],
  "rationale_hash": "blake3:…",
  "deterministic": true
}
```

> `rationale_hash` referencia o raciocínio determinístico no Ledger — nunca texto livre de LLM (L4).

---

## 7. ALLOCATE_RESOURCE

```json
{
  "ns": "u.health",
  "type": "ALLOCATE_RESOURCE",
  "message_id": "…",
  "ref": "assess-priority-uuid",
  "resource_type": "SUPPLY",
  "resource": "oxygen.cylinder",
  "quantity": 20,
  "from_node": "node://warehouse-7",
  "to_node": "node://establishment-id",
  "band": "P1",
  "rationale_hash": "blake3:…",
  "signature": "…"
}
```

| `resource_type` | Exemplos |
| --- | --- |
| `SUPPLY` | Medicamentos, oxigênio, vacinas |
| `BED` | Leitos, UTI |
| `ATTENTION` | Agendamento de consulta/especialista |

---

## 8. UPDATE_STATUS

```json
{
  "ns": "u.health",
  "type": "UPDATE_STATUS",
  "message_id": "…",
  "ref": "allocate-resource-uuid",
  "state": "IN_PROGRESS",
  "note_hash": "blake3:…",
  "timestamp": "2026-06-24T12:00:00Z",
  "signature": "…"
}
```

`state` ∈ `{ PROPOSED, AUTHORIZED, IN_PROGRESS, COMPLETED, REJECTED, ESCALATED, FROZEN }` (ver [especificação §5](./specification.md)).

---

## 9. RAISE_ALERT

```json
{
  "ns": "u.health",
  "type": "RAISE_ALERT",
  "message_id": "…",
  "alert_class": "OUTBREAK",
  "region": "region-31",
  "severity": "P1",
  "evidence_hash": "blake3:…",
  "recommended_action": "surge.supply.respiratory",
  "escalate_to_human": true,
  "signature": "…"
}
```

| `alert_class` | Descrição |
| --- | --- |
| `OUTBREAK` | Surto epidemiológico detectado |
| `RUPTURE` | Ruptura logística iminente (estoque/insumo) |
| `FRAUD` | Anomalia de compra/licitação vs. capacidade instalada |

---

## 10. Regras de conformidade

1. **Anonimização padrão (L3):** `anonymized: true` é o default; `false` exige `consent_ref` válido.
2. **Determinismo (L4):** `ASSESS_PRIORITY`, `ALLOCATE_RESOURCE` e `RAISE_ALERT` referenciam `*_hash` no Ledger; nunca texto livre de LLM como justificativa final.
3. **Prioridade (L1):** `band: P1` / `urgency_score ≥ 0.9` ativa bypass preemptivo.
4. **Equidade (L2):** payloads com variável política/comercial como peso são rejeitados.
5. **Resiliência (L5):** mensagens `offline_capable: true` podem ser deliberadas localmente e reconciliadas via `SYNC` (transporte USP).

---

## 11. Referências

- [Especificação técnica](./specification.md) · [Contratos](./contracts.md) · [Segurança](./security.md)
- [Open USP — Mensagens](https://github.com/LucasArgate/open-usp/blob/main/manifest/messages.md) (envelope de transporte de dados) · [Open UDP — Mensagens](https://github.com/LucasArgate/open-udp/blob/main/manifest/messages.md) (entrega física)
- HL7 FHIR R4 — [hl7.org/fhir/R4](https://hl7.org/fhir/R4/) (perfis de payload clínico; ver [Extensões](./extensions.md))

---

*UHP v0.1.0 — especificação documental*
