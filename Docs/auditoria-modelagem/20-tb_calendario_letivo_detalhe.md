# 19 - Auditoria da Tabela `tb_calendario_letivo_detalhe`

## Identificação

**Tabela:** `tb_calendario_letivo_detalhe`

**Módulo:** Calendário

**Categoria:** Calendário Diário

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_calendario_letivo_detalhe` representa cada dia pertencente a um Calendário Letivo.

Cada registro corresponde a uma data específica, armazenando informações sobre sua natureza acadêmica, permitindo identificar dias letivos, feriados, recessos, eventos institucionais e demais características relevantes ao planejamento escolar.

Esta tabela constitui a base operacional do módulo Calendário.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- representar individualmente cada dia do Calendário Letivo;
- identificar dias letivos;
- identificar períodos do dia;
- registrar eventos institucionais;
- registrar períodos letivos;
- permitir observações específicas para cada data.

---

# Estrutura Atual

| Campo | Tipo | Obrigatório | Observação |
|--------|------|-------------|------------|
| id_dia | INT | Sim | Chave primária |
| calendario_id | INT | Sim | Calendário Letivo |
| data | DATE | Sim | Data |
| dia_semana | TINYINT | Sim | Dia da semana |
| eh_letivo | BOOLEAN | Sim | Dia letivo |
| periodo_do_dia | ENUM | Não | Período |
| tipo_evento | ENUM | Não | Classificação do dia |
| periodo_letivo | ENUM | Não | Bimestre, trimestre ou semestre |
| evento_id | INT | Não | Evento associado |
| observacao | TEXT | Não | Observações |
| criado_em | DATETIME | Sim | Auditoria |
| atualizado_em | DATETIME | Sim | Auditoria |

---

# Chave Primária

PK

id_dia

---

# Chave de Negócio

UNIQUE

(calendario_id, data)

Avaliação:

Excelente.

Garante apenas um registro para cada data dentro do mesmo Calendário.

---

# Relacionamentos

## Calendário Letivo

```text
Calendário Letivo

1:N

Dias
```

---

## Evento

```text
Evento

1:N

Dias
```

Relacionamento opcional.

Implementado por:

ON DELETE SET NULL

---

# Cardinalidade

```text
Calendário

↓

Dias

↓

Eventos
```

---

# Regras de Negócio

### RN-CAL-DIA-001

Todo Dia pertence a um Calendário Letivo.

---

### RN-CAL-DIA-002

Cada data pode existir apenas uma vez dentro do Calendário.

---

### RN-CAL-DIA-003

Todo Dia deve possuir uma data válida.

---

### RN-CAL-DIA-004

Todo Dia deve indicar se é letivo.

---

### RN-CAL-DIA-005

Um Dia poderá possuir um Evento associado.

---

### RN-CAL-DIA-006

Um Dia poderá possuir um Período Letivo.

---

# Normalização

A tabela atende à Terceira Forma Normal (3FN).

Cada atributo descreve exclusivamente a data representada.

---

# Pontos Fortes

- excelente granularidade;
- excelente chave UNIQUE;
- estrutura extremamente flexível;
- preparada para automações futuras;
- boa separação entre calendário e eventos.

---

# Pontos de Atenção

Os valores de:

- periodo_letivo
- tipo_evento

estão implementados como ENUM.

Caso novas modalidades acadêmicas sejam incorporadas futuramente, poderá ser interessante avaliar tabelas parametrizadas.

Para a V1.1 a implementação é adequada.

---

# Observações Arquiteturais

A modelagem adota uma abordagem baseada em registros diários.

Em vez de representar apenas períodos, o sistema mantém uma entidade para cada dia do Ano Letivo.

Essa estratégia oferece elevada flexibilidade para futuras automações, planejamento institucional e integração com os demais módulos do SGCI.

> **Nota:** A evolução desta arquitetura será documentada futuramente na seção Decisões Arquiteturais (ADR).

---

# Melhorias Futuras

## V2

Avaliar parametrização dos tipos de evento.

---

## V3

Avaliar parametrização dos períodos letivos.

---

## V5

Avaliar geração automática do Calendário Institucional Inteligente.

---

# Conclusão

A tabela `tb_calendario_letivo_detalhe` apresenta excelente modelagem conceitual.

Sua granularidade diária proporciona elevada flexibilidade e estabelece uma base sólida para futuras evoluções do módulo Calendário.

A auditoria considera a estrutura plenamente adequada para a versão V1.1.

Status Final:

APROVADA PARA V1.1