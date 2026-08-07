# 11 - Auditoria da Tabela `tb_plano_curso_item`

## Identificação

**Tabela:** `tb_plano_curso_item`

**Módulo:** Planejamento Pedagógico

**Versão da Auditoria:** V1.1

**Status:** Aprovada

---

# Objetivo

A tabela `tb_plano_curso_item` é responsável por detalhar o Plano de Curso, organizando seu conteúdo em unidades ou itens pedagógicos.

Cada registro representa uma parte estruturada do plano, contendo os objetivos específicos, conteúdos, estratégias de ensino e carga horária prevista.

Ela estabelece a transição entre o planejamento geral do curso e o planejamento individual das aulas.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- Organizar o Plano de Curso em itens sequenciais.
- Definir os objetivos específicos de aprendizagem.
- Descrever o conteúdo programático de cada item.
- Registrar as atividades e recursos didáticos previstos.
- Definir a carga horária destinada a cada item.
- Servir como base para elaboração dos Planos de Aula.

---

# Estrutura Atual

| Campo | Tipo | Obrigatório | Observação |
|---------|------|------------|------------|
| id_item | INT | Sim | Chave primária |
| plano_curso_id | INT | Sim | Plano de Curso |
| numero_item | INT | Sim | Ordem do item dentro do plano |
| objetivo_especifico | TEXT | Sim | Objetivo de aprendizagem |
| conteudo | TEXT | Sim | Conteúdo programático |
| atividades_recursos | TEXT | Sim | Estratégias e recursos didáticos |
| carga_horaria | DECIMAL(5,2) | Sim | Carga horária prevista |
| criado_em | DATETIME | Sim | Data de criação |
| atualizado_em | DATETIME | Sim | Última atualização |

---

# Chave Primária

```text
PK

id_item
```

A chave primária identifica exclusivamente cada item pertencente ao Plano de Curso.

---

# Relacionamentos

## Plano de Curso

```text
Plano de Curso

1 ---- N

Itens do Plano
```

Relacionamento realizado por:

```text
plano_curso_id
```

Integridade referencial:

```text
ON UPDATE CASCADE

ON DELETE CASCADE
```

Caso um Plano de Curso seja removido, todos os seus itens também serão removidos automaticamente.

---

# Cardinalidade

```text
Plano de Curso

1:N

Itens do Plano de Curso
```

Um Plano de Curso deve possuir um ou mais itens.

Cada Item pertence exclusivamente a um único Plano de Curso.

---

# Regras de Negócio

### RN-PED-006

Todo Item de Plano de Curso deve pertencer a um único Plano de Curso.

---

### RN-PED-007

Um Plano de Curso deve possuir um ou mais Itens de Plano.

---

### RN-PED-008

A numeração (`numero_item`) deve manter a sequência lógica do Plano de Curso.

---

### RN-PED-009

Todo Item deve possuir um objetivo específico claramente definido.

---

### RN-PED-010

Todo Item deve possuir conteúdo programático.

---

### RN-PED-011

Todo Item deve definir as atividades e recursos previstos para o processo de ensino.

---

### RN-PED-012

Todo Item deve possuir carga horária prevista.

---

# Normalização

A tabela encontra-se adequadamente normalizada.

Observações:

- Não existem grupos repetitivos.
- Todos os atributos dependem exclusivamente da chave primária.
- Não há dependências transitivas.
- Os campos TEXT armazenam informações pedagógicas que não justificam normalização adicional.

Situação atual:

**Atende à Terceira Forma Normal (3FN).**

---

# Pontos Fortes

- Estrutura simples e objetiva.
- Excelente separação entre planejamento macro e detalhamento.
- Boa organização pedagógica.
- Permite cursos de qualquer complexidade.
- Facilita futuras expansões.

---

# Pontos de Atenção

Atualmente não existe um mecanismo que impeça a duplicidade do campo:

```text
numero_item
```

dentro do mesmo Plano de Curso.

Exemplo:

Plano 5

Item 1

Item 1

Item 2
```

Embora essa validação possa ser feita pela aplicação, recomenda-se avaliar a criação de uma restrição de unicidade composta em versões futuras.

---

# Observações de Arquitetura

## Situação Atual

Cada Item do Plano de Curso representa uma unidade lógica de ensino, funcionando como um agrupador de conteúdos que posteriormente dará origem aos Planos de Aula.

---

## Observação

A modelagem estabelece corretamente três níveis distintos de planejamento:

```text
Curso
        │
Plano de Curso
        │
Itens do Plano
        │
Plano de Aula
```

Essa separação torna o sistema aderente às práticas pedagógicas, permitindo que um mesmo item origine diversas aulas sem duplicação de informações.

---

## Impacto

Baixo.

A estrutura é consistente e favorece reutilização e manutenção.

---

## Classificação

Arquitetura consolidada.

---

## Versão Prevista

Sem alterações previstas para a V1.1.

---

## Justificativa

A separação entre Plano de Curso, Itens e Planos de Aula evita redundâncias e melhora a escalabilidade da modelagem pedagógica.

---

## Decisão da Auditoria

**Manter a estrutura atual.**

Como melhoria futura, avaliar a criação de uma restrição `UNIQUE (plano_curso_id, numero_item)` para impedir numeração duplicada dentro do mesmo Plano de Curso.

---

# Melhorias Futuras

- Controle de versão dos Itens do Plano.
- Registro do responsável pela alteração.
- Aprovação pedagógica.
- Histórico de alterações.
- Associação de competências e habilidades (BNCC ou modelo institucional).
- Inclusão de bibliografia específica por item.

---

# Conclusão

A tabela `tb_plano_curso_item` apresenta uma modelagem sólida e bem estruturada.

Sua responsabilidade está claramente delimitada, estabelecendo o nível intermediário entre o Plano de Curso e os Planos de Aula.

A auditoria conclui que a modelagem atende plenamente aos objetivos da V1.1, mantendo boa normalização, baixo acoplamento e excelente organização pedagógica, restando apenas oportunidades de evolução para versões futuras.

---

### Recomendação para Evolução

Avaliar a criação de uma restrição de unicidade composta:

UNIQUE (plano_curso_id, numero_item)

Objetivo:

Garantir que não existam dois itens com a mesma numeração dentro de um mesmo Plano de Curso.

Versão prevista:

V2.0 ou superior.