# 18 - Auditoria da Tabela `tb_calendario_letivo`

## Identificação

**Tabela:** `tb_calendario_letivo`

**Módulo:** Calendário

**Categoria:** Calendário Acadêmico

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_calendario_letivo` representa o Ano Letivo da instituição.

Ela define o período oficial de funcionamento das atividades acadêmicas e serve como entidade raiz para organização do calendário institucional.

Todas as datas letivas, eventos acadêmicos, feriados e demais registros temporais deverão estar vinculados a um Calendário Letivo.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- definir o ano letivo;
- registrar a data oficial de início;
- registrar a data oficial de encerramento;
- identificar o calendário por meio de uma descrição;
- servir como entidade raiz do módulo Calendário.

---

# Estrutura Atual

| Campo | Tipo | Obrigatório | Observação |
|--------|------|-------------|------------|
| id_calendario | INT | Sim | Chave primária |
| ano | INT | Sim | Ano letivo |
| data_inicio | DATE | Sim | Início oficial |
| data_fim | DATE | Sim | Encerramento oficial |
| descricao | VARCHAR(255) | Não | Identificação complementar |
| criado_em | DATETIME | Sim | Auditoria |
| atualizado_em | DATETIME | Sim | Auditoria |

---

# Chave Primária

```text
PK

id_calendario
```

---

# Chave de Negócio

```text
UNIQUE

ano
```

Avaliação:

Excelente.

Garante apenas um Calendário Letivo para cada ano.

---

# Relacionamentos

## Calendário Letivo

Esta tabela funciona como entidade raiz.

Os relacionamentos serão estabelecidos pelas tabelas:

- tb_calendario_letivo_detalhe
- tb_calendario_evento

---

# Cardinalidade

```text
Calendário Letivo

1:N

Detalhes

1:N

Eventos
```

A cardinalidade será consolidada após a auditoria das tabelas dependentes.

---

# Regras de Negócio

### RN-CAL-LET-001

Cada Ano Letivo deve possuir apenas um Calendário Letivo.

---

### RN-CAL-LET-002

Todo Calendário Letivo deve possuir uma data de início.

---

### RN-CAL-LET-003

Todo Calendário Letivo deve possuir uma data de encerramento.

---

### RN-CAL-LET-004

A data de encerramento deve ser posterior à data de início.

(Validação realizada pela aplicação.)

---

# Normalização

A tabela atende integralmente à Terceira Forma Normal (3FN).

Sua estrutura é simples e adequada para representar o calendário institucional.

---

# Pontos Fortes

- modelagem simples;
- chave de negócio bem definida;
- boa separação de responsabilidades;
- entidade raiz do módulo Calendário.

---

# Pontos de Atenção

A tabela representa apenas o período geral do Ano Letivo.

As informações detalhadas do calendário encontram-se em entidades específicas.

Essa separação mantém a modelagem desacoplada e favorece futuras expansões.

---

# Observações Arquiteturais

A decisão de manter o Calendário Letivo como uma entidade independente permite separar o conceito de "Ano Letivo" das atividades que ocorrerão durante esse período.

Essa abordagem favorece a evolução do módulo Calendário sem necessidade de alterar a entidade principal.

> **Nota:** Evoluções futuras relacionadas ao Calendário Institucional Inteligente serão documentadas futuramente na seção **Decisões Arquiteturais (ADR)**.

---

# Melhorias Futuras

## V2

Avaliar:

- status do calendário;
- calendário vigente.

---

## V3

Avaliar:

- múltiplos calendários por instituição.

---

## V4

Avaliar:

- múltiplos calendários por unidade.

---

## V5

Avaliar integração com o Calendário Institucional Inteligente, permitindo geração automática de eventos acadêmicos, cronogramas de cursos, períodos de matrícula e demais atividades institucionais.

---

# Conclusão

A tabela `tb_calendario_letivo` apresenta modelagem consistente, simples e adequada ao seu propósito.

Sua principal função é servir como entidade raiz do módulo Calendário, permitindo que eventos e atividades acadêmicas sejam organizados de forma estruturada.

A auditoria considera a estrutura plenamente adequada para a versão V1.1.

**Status Final:**

```text
APROVADA PARA V1.1
```
