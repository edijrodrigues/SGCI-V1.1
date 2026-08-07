# 16 - Auditoria da Tabela `tb_frequencia_aluno`

## Identificação

**Tabela:** `tb_frequencia_aluno`

**Módulo:** Planejamento Pedagógico

**Responsabilidade:** Registro da frequência dos alunos

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_frequencia_aluno` registra a participação dos alunos nas aulas ministradas.

Cada registro representa a situação de frequência de um aluno matriculado em uma determinada aula, permitindo o acompanhamento da assiduidade durante todo o período letivo.

As informações registradas nesta tabela servirão como base para cálculos de presença, indicadores acadêmicos e emissão do Histórico Escolar.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- registrar presença do aluno;
- registrar faltas;
- registrar atrasos;
- registrar faltas justificadas;
- manter observações relacionadas à frequência;
- identificar o Instrutor responsável pelo lançamento.

---

# Estrutura Atual

| Campo | Tipo | Obrigatório | Observação |
|---------|------|------------|------------|
| id_frequencia | INT | Sim | Chave primária |
| matricula_id | INT | Sim | Matrícula do aluno |
| turma_id | INT | Sim | Turma |
| plano_aula_id | INT | Sim | Aula ministrada |
| data_aula | DATE | Sim | Data da aula |
| status_frequencia | ENUM | Sim | Situação da presença |
| observacao | TEXT | Não | Observações |
| instrutor_id | INT | Sim | Responsável pelo lançamento |
| ativo | BOOLEAN | Sim | Controle lógico |
| criado_em | DATETIME | Sim | Auditoria |
| atualizado_em | DATETIME | Sim | Auditoria |
| deletado_em | DATETIME | Não | Soft Delete |

---

# Chave Primária

```text
PK

id_frequencia
```

---

# Chave de Negócio

```text
UNIQUE

(matricula_id,
plano_aula_id,
data_aula)
```

Avaliação:

Excelente.

Garante que um aluno possua apenas um registro de frequência para a mesma aula.

---

# Relacionamentos

## Matrícula

```text
Matrícula

1:N

Frequência
```

---

## Turma

```text
Turma

1:N

Frequência
```

---

## Plano de Aula

```text
Plano de Aula

1:N

Frequência
```

---

## Instrutor

```text
Instrutor

1:N

Frequência
```

---

# Cardinalidade

```text
Aluno

↓

Matrícula

↓

Frequência

↑

Plano de Aula
```

Cada matrícula possui diversos registros de frequência.

Cada Plano de Aula gera registros para diversos alunos.

---

# Regras de Negócio

### RN-PED-FRQ-001

Toda Frequência pertence a uma Matrícula.

---

### RN-PED-FRQ-002

Toda Frequência pertence a um Plano de Aula.

---

### RN-PED-FRQ-003

Toda Frequência deve possuir uma data.

---

### RN-PED-FRQ-004

Cada aluno pode possuir apenas uma frequência por aula.

---

### RN-PED-FRQ-005

O lançamento deve identificar o Instrutor responsável.

---

### RN-PED-FRQ-006

A frequência poderá assumir os estados:

- presente;
- falta;
- atraso;
- justificado.

---

# Normalização

A tabela atende à Terceira Forma Normal (3FN).

Não existem redundâncias significativas.

A chave de negócio composta protege a consistência dos registros.

---

# Pontos Fortes

- excelente chave UNIQUE;
- boa separação da frequência;
- estrutura simples;
- preparada para indicadores acadêmicos;
- permite rastreabilidade do responsável pelo lançamento.

---

# Pontos de Atenção

A tabela registra:

```text
turma_id

plano_aula_id
```

Entretanto, o Plano de Aula já pode estar relacionado à Turma.

No cenário atual não há inconsistência, porém recomenda-se validar na aplicação que ambos pertençam à mesma Turma.

---

# Observações Arquiteturais

A frequência foi modelada como uma entidade independente do Diário de Aula.

Essa decisão desacopla o controle de presença do registro pedagógico da execução da aula.

A separação aumenta a flexibilidade operacional e simplifica futuras correções de frequência.

> **Nota:** A justificativa completa desta decisão poderá ser registrada futuramente na seção **Decisões Arquiteturais (ADR)**.

---

# Melhorias Futuras

## V2

Avaliar:

```text
horario_entrada

horario_saida
```

---

## V3

Avaliar:

```text
origem_lancamento

manual

importado

biometria
```

---

## V4

Avaliar integração com:

- reconhecimento facial;
- QR Code;
- biometria.

---

# Conclusão

A tabela `tb_frequencia_aluno` apresenta uma modelagem consistente, bem normalizada e alinhada aos objetivos do módulo pedagógico.

Sua principal qualidade é tratar a frequência como uma entidade própria, garantindo flexibilidade operacional e permitindo a geração de indicadores acadêmicos confiáveis.

A auditoria considera a modelagem plenamente aprovada para a versão V1.1.