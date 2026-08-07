# 12 - Auditoria da Tabela `tb_plano_aula`

## Identificação

**Tabela:** `tb_plano_aula`

**Módulo:** Planejamento Pedagógico

**Versão da Auditoria:** V1.1

**Status:** Aprovada

---

# Objetivo

A tabela `tb_plano_aula` é responsável pelo planejamento detalhado de cada aula pertencente aos Itens do Plano de Curso.

Enquanto o Plano de Curso estabelece o planejamento macro e os Itens organizam os conteúdos em unidades pedagógicas, o Plano de Aula define como cada conteúdo será efetivamente ministrado.

Cada registro representa uma aula planejada, contendo metodologia, recursos didáticos, critérios de avaliação, carga horária e observações pertinentes.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- Planejar individualmente cada aula.
- Definir o título da aula.
- Registrar a metodologia de ensino.
- Registrar os recursos didáticos utilizados.
- Definir os critérios de avaliação.
- Informar a carga horária prevista.
- Registrar observações pedagógicas.
- Relacionar o planejamento ao Instrutor responsável.
- Opcionalmente associar o planejamento a uma Turma específica.

---

# Estrutura Atual

| Campo | Tipo | Obrigatório | Observação |
|--------|------|-------------|------------|
| id_plano_aula | INT | Sim | Chave primária |
| plano_curso_item_id | INT | Sim | Item do Plano |
| instrutor_id | INT | Sim | Responsável pela aula |
| turma_id | INT | Não | Turma específica |
| titulo_aula | VARCHAR(150) | Sim | Nome da aula |
| metodologia | TEXT | Não | Estratégia de ensino |
| recursos | TEXT | Não | Recursos didáticos |
| avaliacao | TEXT | Não | Critérios de avaliação |
| carga_horaria | DECIMAL(5,2) | Sim | Carga horária prevista |
| observacoes | TEXT | Não | Observações |
| ativo | BOOLEAN | Sim | Controle lógico |
| criado_em | DATETIME | Sim | Criação |
| atualizado_em | DATETIME | Sim | Atualização |

---

# Chave Primária

id_plano_aula

---

# Relacionamentos

## Item do Plano

```text
Item do Plano

1:N

Plano de Aula
```

---

## Instrutor

```text
Instrutor

1:N

Plano de Aula
```

---

## Turma

```text
Turma

1:N

Plano de Aula
```

Relacionamento opcional.

Caso a Turma seja removida:

```text
ON DELETE SET NULL
```

O planejamento permanece preservado.

---

# Cardinalidade

```text
Plano de Curso

1:N

Itens do Plano

1:N

Plano de Aula
```

Cada Plano de Aula pertence a um único Item do Plano.

Cada Item pode originar diversas aulas.

---

# Regras de Negócio

### RN-PED-PA-001

Todo Plano de Aula deve pertencer a um único Item do Plano de Curso.

---

### RN-PED-PA-002

Todo Plano de Aula deve possuir um Instrutor responsável.

---

### RN-PED-PA-003

Todo Plano de Aula deve possuir um título.

---

### RN-PED-PA-004

Todo Plano de Aula deve possuir carga horária prevista.

---

### RN-PED-PA-005

Um Plano de Aula pode estar vinculado a uma Turma específica.

---

### RN-PED-PA-006

A exclusão de uma Turma não deve excluir o Plano de Aula correspondente.

---

### RN-PED-PA-007

Um Item do Plano pode originar diversos Planos de Aula.

---

# Normalização

A tabela encontra-se adequadamente normalizada.

Todos os atributos dependem exclusivamente da chave primária.

Os campos textuais representam informações pedagógicas e não justificam decomposição adicional.

A modelagem atende à Terceira Forma Normal (3FN).

---

# Pontos Fortes

- Excelente separação entre planejamento e execução.
- Permite reutilização de conteúdos.
- Permite vinculação opcional à Turma.
- Mantém histórico mesmo após alterações organizacionais.
- Estrutura flexível.

---

# Pontos de Atenção

A tabela permite a criação de múltiplos Planos de Aula com o mesmo título para um mesmo Item do Plano.

Embora isso possa ser aceitável em determinadas situações, recomenda-se avaliar futuramente mecanismos de validação na aplicação.

---

# Observações de Arquitetura

## Situação Atual

O planejamento pedagógico foi dividido em três níveis distintos:

Curso

↓

Plano de Curso

↓

Item do Plano

↓

Plano de Aula

---

## Observação

Esta divisão demonstra excelente desacoplamento entre os níveis de planejamento institucional.

Cada entidade possui responsabilidades bem definidas.

---

## Impacto

Muito positivo.

A estrutura favorece reutilização, manutenção e escalabilidade.

---

## Classificação

Arquitetura consolidada.

---

## Versão Prevista

Sem alterações previstas para a V1.1.

---

## Justificativa

A separação entre Plano de Curso, Item do Plano e Plano de Aula representa fielmente o fluxo pedagógico adotado por instituições de ensino.

---

## Decisão da Auditoria

Manter a estrutura atual.

Como melhoria futura, avaliar mecanismos para evitar duplicidade de títulos de aula dentro de um mesmo Item do Plano quando essa restrição fizer sentido para a instituição.

---

# Melhorias Futuras

- Controle de versão dos Planos de Aula.
- Aprovação pedagógica.
- Histórico de revisões.
- Associação de competências e habilidades.
- Objetivos de aprendizagem por aula.
- Referências bibliográficas.
- Controle de materiais de apoio.

---

# Conclusão

A tabela `tb_plano_aula` apresenta excelente modelagem conceitual.

Sua separação em relação aos Itens do Plano de Curso demonstra maturidade arquitetural e proporciona flexibilidade suficiente para atender diferentes metodologias de ensino.

A auditoria conclui que a modelagem atende plenamente aos objetivos da versão V1.1.

## Observações de Arquitetura

### Decisão Arquitetural

A modelagem da tabela `tb_plano_aula` evidencia que o Plano de Aula foi concebido como um recurso pedagógico, e não como um documento exclusivo de uma Turma.

O relacionamento opcional com `tb_turma`, aliado à política `ON DELETE SET NULL`, preserva o planejamento pedagógico independentemente da existência de uma oferta específica.

Esta decisão favorece a reutilização do planejamento, a padronização do conteúdo e a preservação do histórico pedagógico.

> **Nota:** A justificativa completa desta decisão será documentada futuramente na seção **Decisões Arquiteturais**, em documento específico (ADR).