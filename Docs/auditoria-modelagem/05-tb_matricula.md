# 05 - Auditoria da Tabela tb_matricula

## Identificação

**Tabela:** tb_matricula

**Módulo:** Acadêmico

**Categoria:** Entidade Associativa

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_matricula` representa o vínculo formal entre um aluno e uma turma.

Ela é responsável por registrar a participação do aluno em determinado curso, através de uma turma específica, servindo como ponto de integração entre os módulos acadêmico, pedagógico, financeiro e de certificação.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

* Vincular alunos às turmas;
* Registrar a data da matrícula;
* Controlar o status acadêmico do aluno na turma;
* Servir como base para frequência;
* Servir como base para avaliações;
* Servir como base para pagamentos;
* Servir como base para histórico escolar;
* Servir como base para emissão de certificados.

---

# Estrutura Atual

| Campo            | Tipo       | Observação                |
|------------------|------------|---------------------------|
| id_matricula     | int        | Chave Primária            |
| aluno_id         | int        | FK Aluno                  |
| turma_id         | int        | FK Turma                  |
| data_matricula   | date       | Data da matrícula         |
| status_matricula | enum       | Situação acadêmica        |
| observacao       | text       | Informações complementares|
| ativo            | tinyint(1) | Controle lógico           |
| criado_em        | datetime   | Auditoria                 |
| atualizado_em    | datetime   | Auditoria                 |
| deletado_em      | datetime   | Soft Delete               |

---

# Chave Primária

```text
PK: id_matricula
```

Avaliação:

✅ Adequada.

---

# Chave de Negócio

Implementada por:

```sql
UNIQUE(aluno_id, turma_id)
```

Avaliação:

✅ Excelente prática.

Garante que um aluno não possa ser matriculado duas vezes na mesma turma.

---

# Relacionamentos

## Aluno

```text
Aluno
 1:N
Matrícula
```

Implementado por:

```text
tb_matricula.aluno_id
```

Avaliação:

✅ Correto.

Um aluno pode realizar diversas matrículas ao longo da vida acadêmica.

---

## Turma

```text
Turma
 1:N
Matrícula
```

Implementado por:

```text
tb_matricula.turma_id
```

Avaliação:

✅ Correto.

Uma turma pode possuir diversos alunos matriculados.

---

## Pagamento

```text
Matrícula
 1:N
Pagamento
```

Implementado por:

```text
tb_pagamento.matricula_id
```

Avaliação:

✅ Correto.

Todos os lançamentos financeiros devem estar vinculados a uma matrícula.

---

## Frequência

```text
Matrícula
 1:N
Frequência
```

Implementado por:

```text
tb_frequencia_aluno.matricula_id
```

Avaliação:

✅ Correto.

---

## Avaliação

```text
Matrícula
 1:N
Avaliação
```

Implementado por:

```text
tb_avaliacao_aluno.matricula_id
```

Avaliação:

✅ Correto.

---

## Histórico Escolar

```text
Matrícula
 1:N
Histórico
```

Implementado por:

```text
tb_historico_aluno.matricula_id
```

Avaliação:

✅ Correto.

---

# Cardinalidade

## Atual

```text
Aluno
 1:N
Matrícula

Turma
 1:N
Matrícula

Matrícula
 1:N
Pagamento

Matrícula
 1:N
Frequência

Matrícula
 1:N
Avaliação

Matrícula
 1:N
Histórico
```

Avaliação:

✅ Consistente.

---

# Regras de Negócio

## RN-001

Toda matrícula deve estar vinculada a um aluno.

---

## RN-002

Toda matrícula deve estar vinculada a uma turma.

---

## RN-003

Um aluno não pode possuir duas matrículas na mesma turma.

Implementado por:

```sql
UNIQUE(aluno_id, turma_id)
```

---

## RN-004

Uma matrícula deve possuir data de matrícula.

---

## RN-005

Uma matrícula pode assumir diferentes situações acadêmicas.

Atualmente:

```text
ativa

trancada

cancelada

concluida
```

---

## RN-006

Todos os registros pedagógicos devem estar vinculados a uma matrícula.

---

## RN-007

Todo histórico escolar deve estar vinculado a uma matrícula.

---

## RN-008

Todo pagamento deve estar vinculado a uma matrícula.

---

# Normalização

## Primeira Forma Normal (1FN)

Atendida.

---

## Segunda Forma Normal (2FN)

Atendida.

---

## Terceira Forma Normal (3FN)

Atendida.

---

# Pontos Fortes

* Resolve corretamente a relação N:N entre aluno e turma;
* Possui restrição de matrícula única;
* Centraliza a vida acadêmica do aluno;
* Integra todos os módulos do sistema;
* Soft delete implementado;
* Campos de auditoria presentes.

---

# Pontos de Atenção

## Status da Matrícula

Atualmente:

```text
ativa

trancada

cancelada

concluida
```

Atende plenamente ao cenário atual.

Entretanto poderá exigir novos estados em versões futuras.

---

## Histórico de Alterações

Atualmente o sistema mantém apenas o status atual da matrícula.

Não existe rastreamento histórico de mudanças de situação.

---

# Melhorias Futuras

## V2

Avaliar:

```text
data_trancamento

data_cancelamento

motivo_cancelamento
```

---

## V3

Avaliar histórico de movimentações acadêmicas.

Exemplo:

```text
tb_matricula_movimentacao
```

---

## V4

Integração com:

```text
Contrato

Parcelas

Financeiro
```

---

## V5

Automação completa do ciclo acadêmico:

```text
Matrícula

Contrato

Parcelas

Pagamentos

Histórico

Certificação
```

---

# Conclusão

A tabela `tb_matricula` apresenta modelagem sólida e bem normalizada.

Sua estrutura resolve corretamente o relacionamento entre alunos e turmas, além de servir como entidade central de integração entre os módulos acadêmico, pedagógico, financeiro e de certificação.

Não foram identificadas necessidades de alteração estrutural para a V1.1.

Status Final:

```text
APROVADA PARA V1.1
```