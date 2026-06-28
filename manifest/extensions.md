# Open UHP — Extensões

O `u.health` é **extensível por desenho** (P6): as cinco Leis Imutáveis e o envelope de mensagem são o núcleo permanente; tudo o que é contextualmente variável vive em **camadas superiores**. Extensões não podem violar as Leis Imutáveis nem o envelope.

---

## 1. Modelo de extensão

Toda extensão se declara via campo `meta` no envelope da mensagem:

```json
{
  "ns": "u.health",
  "type": "OBSERVE_SIGNAL",
  "meta": {
    "ext": "fhir.r4",
    "ext_version": "1.0.0",
    "profile": "br-core"
  }
}
```

| Regra | Descrição |
| --- | --- |
| **Não-quebra** | Receptores que não conhecem a extensão ignoram `meta` sem falhar. |
| **Subordinação** | Extensões nunca relaxam L1–L5. |
| **Versionada** | `ext_version` segue semver. |

---

## 2. Extensões previstas

### 2.1 Interoperabilidade clínica (FHIR)

- Encapsular recursos **HL7 FHIR R4** (e perfis nacionais, ex.: BR-Core) dentro do payload clínico.
- Mapear `care_type` e `metric` para terminologias (SNOMED CT, CID-10/11, LOINC).

### 2.2 Índice de Prioridade configurável

- Calibração dos pesos `w1..w4` e faixas P1–P4 por perfil regional (ver [especificação §6](./specification.md)).
- Sempre **determinístico** e **cego a status político/comercial** (L2).

### 2.3 Motores epidemiológicos

- Plugins de projeção ($R_0$, modelos SIR/SEIR) consumindo `OBSERVE_SIGNAL` agregados.
- Saída alimenta `RAISE_ALERT` com `evidence_hash` determinístico.

### 2.4 Telemetria IoT e rede de frio

- `signal_class: RESOURCE` para sensores (temperatura de vacinas, pressão de oxigênio).
- Burn rate e previsão de ruptura → `RAISE_ALERT` (`alert_class: RUPTURE`).

### 2.5 Auditoria de fraude

- Cruzamento de compras/licitações vs. capacidade instalada e histórico de preços.
- Anomalia → `RAISE_ALERT` (`alert_class: FRAUD`) + escalonamento humano (Sistema 3 — Human-in-the-Loop).

---

## 3. Integração com o ecossistema

| Camada | Protocolo | Papel |
| --- | --- | --- |
| Serviços + transporte de dados | [Open USP](https://github.com/LucasArgate/open-usp) (`u.service`) | Descobre/cota/reserva serviços (prestadores CLT/PJ) e transfere estado núcleo ↔ borda (agnóstico) |
| Entrega física | [Open UDP](https://github.com/LucasArgate/open-udp) (`u.delivery`) | Move medicamentos/vacinas/amostras/insumos (Last Mile) |
| Execução/Auditoria | `u.core` | Execução determinística + registro imutável das ações (campo comum) |
| Domínio de saúde | **Open UHP** | Observa, prioriza, orquestra cuidado |

> Conectores (MCP) como `rnds-fhir`, `cnes-capacity`, `horus-stock` e `iot-telemetry` são **Gateways** (adaptadores a sistemas externos, no sentido canônico do USP) consumidos pelo UHP; sua **execução é auditada por `u.core`** — não fazem parte do núcleo do protocolo de saúde.

---

## 4. Roadmap

| Fase | Entrega |
| --- | --- |
| **v0.1** (atual) | Núcleo: atores, fluxo, estados, Leis Imutáveis, mensagens base |
| **v0.2** | Schemas JSON formais + exemplos `basic/` |
| **v0.3** | Perfil FHIR R4 + índice de prioridade de referência |
| **v0.4** | Motores epidemiológicos plugáveis + telemetria IoT |
| **v1.0** | Especificação estável + conjunto de conformidade |

---

## 5. Como propor uma extensão

1. Abra uma issue descrevendo o caso de uso e o impacto nas Leis Imutáveis (deve ser **nenhum**).
2. Defina o bloco `meta` e, se aplicável, novos `signal_class`/`alert_class`.
3. Garanta compatibilidade retroativa do envelope.
4. Submeta PR com exemplo em `examples/`.

---

## 6. Referências

- HL7 FHIR R4 — [hl7.org/fhir/R4](https://hl7.org/fhir/R4/)
- SNOMED CT, LOINC, CID-11 (OMS)
- [Especificação técnica](./specification.md) · [Mensagens](./messages.md) · [Segurança](./security.md)

---

*UHP v0.1.0 — especificação documental*
