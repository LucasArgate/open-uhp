# Universal Health Protocol (UHP)

### *O paciente não é um registro. É uma vida com risco, dono do próprio histórico.*

**Language**: [🇧🇷 Português](#1-resumo) | [🇺🇸 English](./ABSTRACT.en.md)

**Namespace:** `u.health` | **Base/Transporte de dados:** [Open USP](https://github.com/LucasArgate/open-usp) (`u.service`) | **Entrega física:** [Open UDP](https://github.com/LucasArgate/open-udp) (`u.delivery`)

---

## 1. Resumo

O **Universal Health Protocol (UHP)** é um padrão aberto de protocolo para o domínio da saúde — um **protocolo em si**, não uma aplicação. Opera no namespace `u.health` e é a **esfera de saúde** (um hólon autossuficiente e interdependente) da [holarquia universal `u.*`](https://github.com/LucasArgate/uhp/tree/main/docs/protocolos/mapa-protocolos.md), reutilizando o [Open USP (Universal Service Protocol)](https://github.com/LucasArgate/open-usp) (`u.service`) para execução/auditoria e **transporte de dados** (agnóstico) e o [Open UDP](https://github.com/LucasArgate/open-udp) (`u.delivery`) para **entrega física Last Mile** (medicamentos, vacinas, amostras, insumos). Na tendência em que Google e big techs investem em protocolos como o UCP (Universal Commerce Protocol), o futuro é mais protocolos que aplicações; o UHP posiciona-se como um deles.

Ele especifica como uma rede de **Nós** (UBS, hospitais, clínicas, sensores) **observa** sinais de saúde, como o núcleo **delibera** sobre prioridade e equidade, e como recursos (insumos, leitos, atenção) são **orquestrados** — com a soberania do dado do cidadão e a segurança clínica no centro do desenho.

No modelo atual (arquipélago de sistemas que não conversam), a saúde pública opera às cegas: estoques rompem sem aviso, surtos são detectados tarde, fraudes passam despercebidas e o dado do cidadão fica preso em silos. O UHP propõe uma **camada neural** sobre os sistemas existentes — percepção na borda, deliberação determinística no núcleo, auditoria imutável — sem substituí-los.

---

## 2. O problema que o UHP endereça

- **Cegueira sistêmica:** Sem visão em tempo quasi-real, gestores reagem a rupturas e surtos em vez de antecipá-los.
- **Caixa-preta na alocação:** Decisões sobre quem recebe insumo, leito ou atenção carecem de trilha auditável e cedem a pressão política/comercial.
- **Dado preso e exposto:** Históricos clínicos ficam em silos incompatíveis e, paradoxalmente, vulneráveis — o cidadão não controla o próprio dado.
- **Fragilidade na borda:** Quando a conectividade cai, a unidade de saúde fica sem suporte de decisão.

O UHP não resolve sozinho a desigualdade em saúde; fornece as **ferramentas tecnológicas** para que a rede perceba, delibere e aja com mais equidade, transparência e dignidade.

---

## 3. Pilares do protocolo

### I. Percepção rápida na borda (Sistema 1)

Cada Nó executa um agente local que integra APIs oficiais, sensores e sinais fracos (clima, mobilidade), detecta anomalias e **propõe** ações — sem jamais decidir sozinho sobre recurso crítico. PII é processada localmente; só sobem inferências anonimizadas.

### II. Deliberação determinística no núcleo (Sistema 2)

A IA propõe; a **matemática determinística valida e executa**. Otimização epidemiológica, índices de prioridade e gates de lei rodam em máquinas de estado auditáveis — nunca em caixa-preta de LLM. Toda decisão crítica gera trilha imutável.

### III. Soberania do dado do cidadão

Identidade e consentimento são criptográficos (ex.: WebAuthn/gov.br) e **pertencem ao cidadão**. O protocolo opera em anonimização padrão; prontuários identificados só abrem sob consentimento ou emergência clínica documentada — sempre rastreável.

### IV. Equidade como invariante

A alocação obedece à matriz matemática de risco e vulnerabilidade — **cega** a status político, comercial ou socioeconômico. A equidade não é uma política configurável; é uma lei imutável do protocolo.

---

## 4. As cinco Leis Imutáveis

O UHP codifica cinco invariantes operacionais, validados na camada de deliberação:

| Lei | Enunciado | Fundamento |
| --- | --- | --- |
| **L1 Supremacia do Cuidado** | Risco de morte/agravamento prioriza preemptivamente sobre burocracia. | Triagem de Manchester; escalonamento preemptivo. |
| **L2 Equidade Algorítmica** | Alocação cega a status político/comercial/socioeconômico. | Modelo SIR ($R_0$); otimização convexa. |
| **L3 Soberania do Dado** | Cidadão é dono; anonimização padrão; consentimento criptográfico. | LGPD art. 11; privacidade diferencial. |
| **L4 Transparência Determinística** | IA propõe; matemática valida e executa; trilha imutável. | MBE; IA neurosimbólica; ledger append-only. |
| **L5 Resiliência Distribuída** | Offline-first; nó na borda opera sem o núcleo. | Teorema CAP (disponibilidade local). |

---

## 5. Visão 2026

- **Nós na borda** (UBS, hospitais) com agentes que percebem rupturas de estoque e sinais clínicos, operando offline-first.
- **Núcleo** que antecipa surtos cruzando clima, mobilidade e dados oficiais, e orquestra insumos com equidade algorítmica.
- **Cidadãos** donos do próprio histórico, concedendo acesso por consentimento criptográfico.
- **Órgãos de controle** recebendo alertas determinísticos de fraude e ruptura, com trilha auditável.

---

## 6. Compromisso

O Open UHP compromete-se a:

- Tratar o cuidado como **rede que percebe, delibera e age**, removendo a caixa-preta algorítmica.
- Incorporar **soberania do dado e segurança clínica** como variáveis explícitas e imutáveis (Leis L1–L5).
- Manter **conformidade legal** (LGPD) e **chancela institucional** como escudo, à luz pública.
- Manter o protocolo **extensível e aberto**, reutilizando UDP/USP, para que novos perfis (FHIR, índices, motores epidemiológicos) sejam adotados sem quebrar a base.

---

## 7. Governança aberta — o "GitHub dos médicos"

Este protocolo é **público**. Qualquer médico — ou o **agente programador do médico** — pode propor uma mudança por meio de uma issue ou de um *pull request*, com evidência e fundamentação anexadas.

A medicina já possui processos globais de consenso, e o UHP **não os substitui**:

- A **OMS** publica diretrizes (metodologia **GRADE**) e mantém a **CID-11**;
- A **Cochrane** sintetiza evidência em revisões sistemáticas;
- Sociedades de especialidade emitem *guidelines*;
- Terminologias e interoperabilidade são governadas por processos formais — **SNOMED CT**, **LOINC** e o *balloting* do **HL7 FHIR**.

Há, inclusive, plataformas **versionadas e governadas** de conhecimento clínico: o [openEHR Clinical Knowledge Manager (CKM)](https://ckm.openehr.org/) governa arquétipos clínicos com versionamento semântico e rodadas de revisão abertas; o [MAGICapp / MAGIC Evidence Ecosystem](https://www.magicevidence.org/) (em parceria com a Cochrane) mantém *living guidelines* com histórico de versões. São avanços reais — porém centrados em **modelos de dados** e **diretrizes de evidência**, e explicitamente **distintos** do fluxo *fork* + *pull request* do desenvolvimento de software.

O que ainda **não existe** é um "GitHub dos médicos": uma camada de protocolo **publicamente bifurcável (fork) e governada por proposta de mudança (pull request)**, em que a **lógica operacional do cuidado** — critérios de priorização, gatilhos de alerta, fluxos de alocação — seja ao mesmo tempo legível por humanos e **executável por máquinas**, com **proveniência imutável** de quem propôs, revisou e aprovou cada alteração.

O Open UHP é esse substrato. Por ser público e MIT:

- **Proposta por qualquer um, revisão aberta:** issue/PR carrega autoria, evidência e trilha — coerente com a Lei da Transparência Determinística (L4).
- **Núcleo imutável, camadas evolutivas:** as cinco Leis Imutáveis e o envelope de mensagem só mudam por revisão formal (P6); o que é contextualmente variável — pesos do Índice de Prioridade, perfis FHIR, motores epidemiológicos — evolui por PR.
- **Ponte, não muro:** a evidência continua nascendo nos processos científicos existentes; o UHP dá a ela forma **versionada, auditável e executável** — do consenso clínico ao código que orquestra o cuidado.

---

## 8. Licença e governança

O UHP é lançado sob **licença MIT**, como padrão aberto e dirigido pela comunidade. É um protocolo próprio, o domínio de saúde do ecossistema [Open USP](https://github.com/LucasArgate/open-usp), compatível com o [Open UDP](https://github.com/LucasArgate/open-udp).

> A especificação aqui é genérica e reutilizável. A aplicação concreta no SUS/Brasil — com sistemas, números e enquadramento institucional específicos — vive na documentação do [repositório UHP](https://github.com/LucasArgate/uhp).

---

*Não estamos construindo mais um sistema de saúde. Estamos construindo a linguagem que permite que sistemas de saúde percebam, deliberem e ajam como uma rede — com equidade e soberania do dado. Junte-se a nós na construção do protocolo do cuidado justo e transparente.*

---

**Versão:** 0.1.0  
**Última atualização:** Junho 2026  
**English:** [ABSTRACT.en.md](./ABSTRACT.en.md)
