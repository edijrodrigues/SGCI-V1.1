# 20 - Auditoria da Tabela `tb_calendario_evento`

## Identificação

**Tabela:** `tb_calendario_evento`

**Módulo:** Calendário

**Categoria:** Eventos Institucionais

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_calendario_evento` registra eventos institucionais que afetam o Calendário Letivo.

Os eventos representam regras temporais aplicadas ao calendário, permitindo registrar feriados, recessos, férias, suspensões, atividades pedagógicas e avaliações.

Esses registros podem afetar toda a instituição ou apenas partes específicas da organização.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- registrar eventos institucionais;
- definir período de ocorrência;
- determinar o período do dia afetado;
- definir a abrangência do evento;
- registrar descrição do evento.

---

# Estrutura Atual

| Campo | Tipo | Obrigatório | Observação |
|--------|------|-------------|------------|
| id_evento | INT | Sim | Chave primária |
| calendario_id | INT | Sim | Calendário Letivo |
| data_inicio | DATE | Sim | Início do evento |
| data_fim | DATE | Não | Fim do evento |
| tipo_evento | ENUM | Sim | Classificação |
| periodo_afetado | ENUM | Não | Período do dia |
| aplicavel_a | ENUM | Não | Abrangência |
| referencia_id | INT | Não | Entidade afetada |
| descricao | TEXT | Não | Observações |
| criado_em | DATETIME | Sim | Auditoria |
| atualizado_em | DATETIME | Sim | Auditoria |

---

# Chave Primária

PK

id_evento

---

# Relacionamentos

## Calendário Letivo

```text
Calendário

1:N

Eventos
```

---

# Cardinalidade

```text
Calendário

↓

Eventos
```

Cada Calendário pode possuir diversos eventos.

---

# Regras de Negócio

### RN-CAL-EVT-001

Todo Evento pertence a um Calendário Letivo.

---

### RN-CAL-EVT-002

Todo Evento deve possuir uma data de início.

---

### RN-CAL-EVT-003

Todo Evento deve possuir um tipo.

---

### RN-CAL-EVT-004

O Evento poderá possuir data final.

---

### RN-CAL-EVT-005

Todo Evento poderá afetar apenas parte da organização.

---

### RN-CAL-EVT-006

Todo Evento poderá possuir descrição.

---

# Normalização

A tabela atende à Terceira Forma Normal (3FN).

Sua responsabilidade está claramente delimitada ao registro dos eventos institucionais.

---

# Pontos Fortes

- excelente separação entre calendário e eventos;
- suporta eventos de um ou vários dias;
- suporta eventos parciais;
- suporta abrangência institucional;
- preparada para evolução futura.

---

# Pontos de Atenção

O campo:

referencia_id

é genérico.

Sua interpretação depende do valor de:

aplicavel_a

Essa decisão aumenta a flexibilidade, porém exige validações na camada de aplicação.

---

# Observações Arquiteturais

A modelagem separa corretamente o conceito de "Evento" do conceito de "Dia do Calendário".

Enquanto a tabela `tb_calendario_letivo_detalhe` representa o calendário diário, esta tabela representa os eventos institucionais que modificam o comportamento desses dias.

Essa separação favorece reutilização, automação e futuras expansões do módulo Calendário.

> **Nota:** A evolução desta arquitetura será documentada futuramente na seção Decisões Arquiteturais (ADR).

---

# Melhorias Futuras

## V2

Avaliar parametrização dos tipos de evento.

---

## V3

Avaliar tabela específica para abrangência dos eventos.

---

## V5

Integrar o mecanismo de geração automática do Calendário Institucional Inteligente.

---

# Conclusão

A tabela `tb_calendario_evento` apresenta modelagem consistente e alinhada ao restante do módulo Calendário.

Sua principal característica é representar eventos institucionais de forma desacoplada do calendário diário, permitindo que futuras automações sejam implementadas sem alterações estruturais significativas.

Status Final:

APROVADA PARA V1.1