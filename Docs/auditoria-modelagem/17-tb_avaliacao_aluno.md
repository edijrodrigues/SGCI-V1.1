# 17 - Auditoria da Tabela `tb_avaliacao_aluno`

## Identificação

**Tabela:** `tb_avaliacao_aluno`

**Módulo:** Planejamento Pedagógico

**Categoria:** Avaliação da Aprendizagem

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_avaliacao_aluno` registra os resultados das avaliações realizadas pelos alunos durante o desenvolvimento do Curso.

Cada registro representa uma avaliação vinculada ao conteúdo previsto no Plano de Curso, permitindo acompanhar o desempenho acadêmico ao longo do processo de aprendizagem.

As informações registradas nesta tabela servirão posteriormente como base para composição do Histórico Escolar e emissão de Certificados.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- registrar avaliações dos alunos;
- registrar notas ou conceitos;
- identificar o tipo de avaliação;
- registrar a data da avaliação;
- relacionar a avaliação ao conteúdo previsto;
- identificar o Instrutor responsável.

---

# Estrutura Atual

| Campo | Tipo | Obrigatório | Observação |
|--------|------|-------------|------------|
| id_avaliacao | INT | Sim | Chave primária |
| matricula_id | INT | Sim | Matrícula do aluno |
| turma_id | INT | Sim | Turma |
| plano_curso_item_id | INT | Sim | Conteúdo avaliado |
| plano_aula_id | INT | Não | Aula relacionada |
| tipo_avaliacao | ENUM | Sim | Tipo da avaliação |
| nota | DECIMAL(5,2) | Não | Nota obtida |
| conceito | VARCHAR(20) | Não | Conceito textual |
| data_avaliacao | DATE | Sim | Data da avaliação |
| observacao | TEXT | Não | Observações |
| instrutor_id | INT | Sim | Responsável |
| ativo | BOOLEAN | Sim | Controle lógico |
| criado_em | DATETIME | Sim | Auditoria |
| atualizado_em | DATETIME | Sim | Auditoria |
| deletado_em | DATETIME | Não | Soft Delete |

---

# Chave Primária

```text
PK

id_avaliacao
```

---

# Chave de Negócio

```text
UNIQUE
(
matricula_id,
plano_curso_item_id,
tipo_avaliacao
)
```

Avaliação:

Excelente.

Evita avaliações duplicadas do mesmo tipo para o mesmo conteúdo.

---

# Relacionamentos

## Matrícula

```text
Matrícula

1:N

Avaliação
```

---

## Turma

```text
Turma

1:N

Avaliação
```

---

## Item do Plano de Curso

```text
Item do Plano

1:N

Avaliação
```

---

## Plano de Aula

```text
Plano de Aula

1:N

Avaliação
```

Relacionamento opcional.

Implementado por:

```text
ON DELETE SET NULL
```

---

## Instrutor

```text
Instrutor

1:N

Avaliação
```

---

# Cardinalidade

```text
Matrícula

↓

Avaliação

↑

Item do Plano
```

Cada aluno pode possuir diversas avaliações.

Cada Item do Plano pode gerar avaliações para diversos alunos.

---

# Regras de Negócio

### RN-PED-AVL-001

Toda Avaliação pertence a uma Matrícula.

---

### RN-PED-AVL-002

Toda Avaliação deve estar vinculada a um Item do Plano de Curso.

---

### RN-PED-AVL-003

A Aula vinculada é opcional.

---

### RN-PED-AVL-004

Toda Avaliação possui um tipo.

---

### RN-PED-AVL-005

Toda Avaliação possui uma data.

---

### RN-PED-AVL-006

Toda Avaliação identifica o Instrutor responsável.

---

### RN-PED-AVL-007

Uma Matrícula não pode possuir duas avaliações iguais para o mesmo Item do Plano e mesmo tipo.

---

# Normalização

A tabela encontra-se adequadamente normalizada.

A separação entre Item do Plano e Plano de Aula reduz o acoplamento entre avaliação e execução da aula.

A modelagem atende à Terceira Forma Normal (3FN).

---

# Pontos Fortes

- excelente chave UNIQUE;
- avaliação centrada no conteúdo pedagógico;
- suporte simultâneo para nota e conceito;
- flexibilidade para diversos tipos de avaliação;
- boa rastreabilidade do responsável.

---

# Pontos de Atenção

O sistema atualmente permite registrar:

- nota;
- conceito;

simultaneamente.

A aplicação deverá definir se ambos poderão coexistir ou se serão mutuamente exclusivos conforme a política pedagógica da instituição.

---

# Observações Arquiteturais

A modelagem estabelece que o objeto principal da avaliação é o Item do Plano de Curso.

O vínculo opcional com o Plano de Aula demonstra que a avaliação mede a aprendizagem do conteúdo planejado e não necessariamente o resultado de uma aula específica.

Essa decisão reduz o acoplamento entre avaliação e execução da aula, preservando maior flexibilidade pedagógica.

> **Nota:** A justificativa completa desta decisão poderá ser registrada futuramente na seção **Decisões Arquiteturais (ADR)**.

---

# Melhorias Futuras

## V2

Avaliar:

- peso da avaliação;
- nota máxima;
- nota mínima.

---

## V3

Avaliar:

- rubricas de avaliação;
- competências avaliadas;
- habilidades desenvolvidas.

---

## V4

Avaliar integração com recuperação paralela.

---

## V5

Avaliar geração automática da média final por componente curricular.

---

# Conclusão

A tabela `tb_avaliacao_aluno` apresenta excelente modelagem conceitual.

A decisão de vincular a avaliação ao Item do Plano de Curso, mantendo opcional a associação ao Plano de Aula, demonstra uma arquitetura pedagógica consistente e alinhada ao processo de ensino-aprendizagem.

A auditoria considera a estrutura plenamente adequada para a versão V1.1.

**Status Final:**

```text
APROVADA PARA V1.1
```