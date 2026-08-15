# 14 - Auditoria da Tabela `tb_diario_aula`

## Identificação

**Tabela:** `tb_diario_aula`

**Módulo:** Planejamento Pedagógico

**Responsabilidade:** Registro oficial da execução das aulas

---

# Objetivo

Registrar oficialmente a execução de uma aula previamente planejada.

Cada registro representa a realização (ou não realização) de uma aula prevista para uma Turma, documentando o conteúdo efetivamente ministrado, carga horária realizada e eventuais ocorrências.

Esta tabela constitui o documento oficial da execução pedagógica.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- registrar a realização da aula;
- vincular a execução ao planejamento previamente definido;
- registrar o conteúdo realmente ministrado;
- informar a carga horária efetivamente executada;
- registrar ocorrências da aula;
- controlar a situação da execução.

---

# Estrutura

## Chave Primária

```text
id_diario
```

---

## Chaves Estrangeiras

### Diário Previsto

```text
previsto_id

→ tb_diario_aula_previsto
```

---

### Turma

```text
turma_id

→ tb_turma
```

---

### Instrutor

```text
instrutor_id

→ tb_instrutor
```

---

### Plano de Aula

```text
plano_aula_id

→ tb_plano_aula
```

---

# Relacionamentos

## Diário Previsto

```text
Diário Previsto

1:1

Diário de Aula
```

Implementado por:

```text
UNIQUE(previsto_id)
```

Excelente decisão arquitetural.

Cada planejamento gera apenas um registro oficial de execução.

---

## Turma

```text
Turma

1:N

Diário de Aula
```

---

## Instrutor

```text
Instrutor

1:N

Diário de Aula
```

---

## Plano de Aula

```text
Plano de Aula

1:N

Diário de Aula
```

---

# Cardinalidade

```text
Plano de Aula

1:N

Diário Previsto

1:1

Diário de Aula
```

A modelagem garante que o planejamento não seja executado mais de uma vez.

---

# Índices

## ux_diario_previsto

```text
UNIQUE(previsto_id)
```

Garante integridade entre planejamento e execução.

---

## idx_diario_turma_data

```text
(turma_id, data_aula)
```

Excelente índice.

Favorece consultas como:

- diário da turma;
- diário do dia;
- histórico de aulas.

---

# Regras de Negócio

### RN-PED-DA-001

Todo Diário de Aula deve estar vinculado a um Diário Previsto.

---

### RN-PED-DA-002

Cada Diário Previsto pode gerar apenas um Diário de Aula.

---

### RN-PED-DA-003

Todo Diário de Aula pertence a uma Turma.

---

### RN-PED-DA-004

Todo Diário de Aula possui um Instrutor responsável.

---

### RN-PED-DA-005

Todo Diário de Aula referencia um Plano de Aula.

---

### RN-PED-DA-006

A data registrada representa a data efetiva da realização da aula.

---

### RN-PED-DA-007

O conteúdo ministrado pode diferir do conteúdo originalmente planejado.

---

### RN-PED-DA-008

A carga horária realizada pode ser diferente da carga horária prevista.

---

### RN-PED-DA-009

Toda ocorrência relevante deve ser registrada.

---

### RN-PED-DA-010

Uma aula pode ser registrada como não realizada.

---

# Normalização

A tabela atende à Terceira Forma Normal (3FN).

A separação entre planejamento e execução elimina redundâncias e preserva o histórico pedagógico.

---

# Pontos Fortes

- Excelente separação entre planejamento e execução.
- Integridade garantida pelo vínculo 1:1 com o Diário Previsto.
- Registro histórico consistente.
- Boa utilização de índices.
- Estrutura preparada para auditoria institucional.

---

# Pontos de Atenção

O campo:

```text
status
```

Atualmente possui apenas:

- realizada
- nao_realizada

Em versões futuras poderá ser interessante avaliar estados como:

- parcialmente realizada
- remarcada
- interrompida

Sem necessidade de alteração para a V1.1.

---

# Observações Arquiteturais

Esta tabela representa o encerramento do ciclo de planejamento pedagógico.

Enquanto o Diário Previsto registra aquilo que deveria acontecer, o Diário de Aula registra aquilo que efetivamente ocorreu.

A existência da restrição:

```text
UNIQUE(previsto_id)
```

transforma o Diário Previsto em uma ordem formal de execução pedagógica, garantindo que cada planejamento produza um único registro oficial de realização.

Esta decisão preserva a rastreabilidade entre planejamento e execução.

> **Nota:** A justificativa completa desta decisão será documentada futuramente na seção **Decisões Arquiteturais (ADR)**.

---

# Melhorias Futuras

- assinatura eletrônica do Instrutor;
- assinatura da Coordenação;
- controle de revisão do Diário;
- bloqueio após homologação;
- workflow de aprovação.

---

# Conclusão

A tabela `tb_diario_aula` representa o núcleo operacional do módulo pedagógico do SGCI.

Sua modelagem demonstra excelente separação entre planejamento e execução, preservando a integridade do processo acadêmico e garantindo rastreabilidade completa entre o Plano de Aula previsto e sua efetiva realização.

A auditoria considera a modelagem plenamente aprovada para a versão V1.1.