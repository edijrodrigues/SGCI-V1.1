# 24 - Auditoria da Tabela `tb_turma_dias`

## Identificação

**Tabela:** `tb_turma_dias`

**Módulo:** Estrutura Organizacional

**Categoria:** Agenda da Turma

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_turma_dias` define os dias da semana em que uma Turma possui atividades programadas.

Ela complementa a entidade `tb_turma`, permitindo representar a distribuição semanal das aulas sem duplicar informações na própria tabela da turma.

Essa modelagem oferece flexibilidade para turmas que ocorrem em múltiplos dias da semana.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- registrar os dias da semana de uma Turma;
- impedir duplicidade de dias para a mesma Turma;
- servir como base para o planejamento semanal das aulas;
- apoiar futuras automações do Calendário Institucional.

---

# Estrutura Atual

| Campo | Tipo | Obrigatório | Observação |
|--------|------|-------------|------------|
| id_turma_dia | INT | Sim | Chave primária |
| turma_id | INT | Sim | Turma |
| dia_semana | ENUM | Sim | Dia da semana |
| ativo | BOOLEAN | Sim | Controle lógico |
| criado_em | DATETIME | Sim | Auditoria |
| atualizado_em | DATETIME | Sim | Auditoria |
| deletado_em | DATETIME | Não | Soft Delete |

---

# Chave Primária

```text
PK

id_turma_dia
```

---

# Chave de Negócio

```text
UNIQUE (turma_id, dia_semana)
```

Avaliação:

Excelente.

Garante que um mesmo dia da semana seja cadastrado apenas uma vez para cada Turma.

---

# Relacionamentos

## Turma

```text
Turma

1:N

Dias da Turma
```

Uma Turma pode ocorrer em vários dias da semana.

---

# Cardinalidade

```text
Turma

↓

Dias da Turma
```

Exemplo:

```text
Turma INFO-2026A

↓

Segunda-feira

↓

Quarta-feira

↓

Sexta-feira
```

---

# Regras de Negócio

### RN-EST-006

Toda configuração de dia da semana pertence a uma Turma.

---

### RN-EST-007

Uma Turma poderá possuir um ou mais dias da semana.

---

### RN-EST-008

Não poderá existir duplicidade do mesmo dia da semana para uma mesma Turma.

(Regra implementada por `UNIQUE (turma_id, dia_semana)`.)

---

# Normalização

A tabela atende à Terceira Forma Normal (3FN).

Sua responsabilidade está limitada à definição da agenda semanal das Turmas, evitando repetição de atributos na tabela `tb_turma`.

---

# Pontos Fortes

- excelente normalização;
- permite turmas com múltiplos dias;
- evita redundância;
- preparada para integração com o calendário;
- chave de negócio adequada.

---

# Pontos de Atenção

Atualmente a tabela registra apenas o dia da semana.

Ela não define:

- horário inicial;
- horário final;
- carga horária diária.

Essas informações permanecem sob responsabilidade de outras entidades ou regras da aplicação.

---

# Observações Arquiteturais

A separação entre `tb_turma` e `tb_turma_dias` representa uma decisão de modelagem adequada.

Enquanto `tb_turma` descreve a identidade e características da turma, `tb_turma_dias` descreve sua recorrência semanal.

Essa separação reduz redundância e prepara o sistema para futuras integrações com o módulo de Calendário e com o Planejamento Institucional Inteligente.

> **Nota:** Essa integração poderá ser detalhada futuramente em uma Decisão Arquitetural (ADR).

---

# Melhorias Futuras

## V3

Avaliar inclusão de:

- horário inicial;
- horário final;
- duração diária.

---

## V5

Integrar a agenda semanal das Turmas ao mecanismo de geração automática do Calendário Institucional Inteligente.

---

# Conclusão

A tabela `tb_turma_dias` complementa adequadamente a modelagem da entidade `tb_turma`, permitindo representar a recorrência semanal das aulas de forma normalizada e flexível.

Sua estrutura está consistente e alinhada com os objetivos da versão V1.1.

**Status Final:**

```text
APROVADA PARA V1.1
```