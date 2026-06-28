# Open UHP — Contratos

Definição dos **atores** do `u.health`, seus papéis, obrigações e garantias. Os contratos descrevem *quem* participa e *o que* cada um deve cumprir; as [Mensagens](./messages.md) descrevem *como* eles se comunicam.

---

## 1. Atores

| Ator | Papel | Analogia |
| --- | --- | --- |
| **Citizen** | Dono soberano do histórico longitudinal de saúde. | Paciente / cidadão |
| **Node** | Agente de percepção e execução na borda (S1). | UBS, hospital, clínica, sensor |
| **Mother Entity** | Núcleo de deliberação determinística e orquestração (S2). | Núcleo central / digestor global |
| **Observer** | Auditoria, controle, comitê de ética (opcional). | Órgão de controle, Sistema 3 (Human-in-the-Loop) |

---

## 2. Citizen (Cidadão)

O cidadão é o **único dono** do seu histórico longitudinal (L3 — Soberania do Dado).

### Direitos

- Conceder e revogar consentimento a qualquer momento (`GRANT_CONSENT` / `REVOKE_CONSENT`).
- Ter o dado processado em **anonimização padrão**; reidentificação exige base legal e trilha.
- Consultar a trilha de acessos ao próprio prontuário.

### Garantias do protocolo

- PII processada exclusivamente no Nó local (edge); só inferências anonimizadas sobem ao núcleo.
- Abertura de prontuário identificado exige consentimento criptográfico (ex.: WebAuthn/gov.br) **ou** emergência clínica documentada (L1).
- Chaves de descriptografia clínica não residem no núcleo central.

---

## 3. Node (Nó na borda)

Agente local de percepção (S1). Integra sistemas, sensores e sinais fracos; **propõe** ações.

### Obrigações

- Anonimizar inferências antes de emitir `OBSERVE_SIGNAL` (privacidade diferencial).
- Operar **offline-first** (L5): continuar deliberando localmente sobre sinais `offline_capable` quando o núcleo estiver indisponível.
- Nunca decidir sozinho sobre recurso crítico — apenas propor, salvo bypass de emergência autorizado (L1).
- Registrar localmente toda ação para reconciliação posterior (`SYNC`).

### Garantias

- Recebe manifesto dinâmico (`llm.txt`) roteado por `partition_key` (região/estabelecimento).
- Autenticado por certificado mTLS por estabelecimento.
- Não recebe instruções fora do seu escopo geográfico/funcional.

---

## 4. Mother Entity (Entidade Mãe / núcleo)

Núcleo de deliberação determinística (S2) e orquestração.

### Obrigações

- Computar `ASSESS_PRIORITY` de forma **determinística e auditável** — nunca caixa-preta de LLM (L4).
- Aplicar **equidade algorítmica** (L2): rejeitar payloads que usem variável política/comercial/socioeconômica como peso de alocação.
- Gerar **trilha imutável** (append-only) para toda decisão crítica.
- Emitir `RAISE_ALERT` a `Observers` diante de surto, ruptura logística ou fraude.
- Escalar para `Observer`/humano (Sistema 3 — Human-in-the-Loop) quando a incerteza exceder o limiar.

### Garantias

- Não detém PII bruta; opera sobre agregados anonimizados (L3).
- Publica instruções (`llm.txt`) sem distribuir código aos nós.

---

## 5. Observer (Observador)

Ator **opcional** de auditoria e controle (órgãos de controle, comitês de ética, Sistema 3 / Human-in-the-Loop).

### Direitos

- Receber `RAISE_ALERT` determinísticos (surto, ruptura, fraude).
- Auditar a trilha imutável (hashes, não conteúdo clínico bruto).
- Receber casos `ESCALATED` para decisão humana.

### Restrições

- Não acessa PII sem base legal e consentimento/trilha.
- Não altera decisões retroativamente; reverts não apagam histórico (L4).

---

## 6. Matriz de obrigações × Leis Imutáveis

| Lei | Citizen | Node | Mother Entity | Observer |
| --- | --- | --- | --- | --- |
| **L1 Supremacia** | — | Bypass autorizado | Validação pós-fato | Recebe escalonamento |
| **L2 Equidade** | — | Sinal sem viés | Otimização cega | Audita decisão |
| **L3 Soberania** | Consentimento | Anonimiza PII | Opera em agregados | Sem PII bruta |
| **L4 Transparência** | Vê trilha | Registra ação | Append-only | Audita hashes |
| **L5 Resiliência** | — | Offline-first | Sync batch | — |

---

## 7. Identidade e confiança

| Mecanismo | Aplicação |
| --- | --- |
| **WebAuthn / gov.br** | Consentimento criptográfico do cidadão |
| **mTLS por estabelecimento** | Autenticação de Nó |
| **Assinatura por mensagem** | Integridade e não-repúdio |
| **Hash encadeado (BLAKE3)** | Trilha imutável e detecção de alteração retroativa |

Ver [Segurança](./security.md) para detalhes.

---

## 8. Referências

- [Especificação técnica](./specification.md) · [Mensagens](./messages.md) · [Segurança](./security.md)
- Lei nº 13.709/2018 (LGPD), art. 11 — dados sensíveis de saúde
- W3C WebAuthn L2 — [w3.org/TR/webauthn-2](https://www.w3.org/TR/webauthn-2/)

---

*UHP v0.1.0 — especificação documental*
