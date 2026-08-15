# 10 - Auditoria da Tabela tb_plano_curso

## Identificação

**Tabela:** tb_plano_curso

**Módulo:** Planejamento Pedagógico

**Categoria:** Entidade Pedagógica Estruturante

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_plano_curso` representa o planejamento pedagógico oficial de um curso.

Ela define os objetivos educacionais, a carga horária, a versão do plano e todas as diretrizes que orientarão o desenvolvimento das aulas.

É a principal referência pedagógica do curso e serve como base para elaboração dos planos de aula e execução das atividades acadêmicas.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

* Definir o planejamento pedagógico do curso;
* Armazenar objetivos gerais;
* Armazenar objetivos específicos;
* Definir carga horária oficial;
* Permitir versionamento dos planos;
* Servir como base para os Planos de Aula;
* Garantir padronização pedagógica entre turmas.

---

# Estrutura Atual

| Campo | Tipo | Observação |
|---------|---------|---------|
| id_plano_curso | int | Chave Primária |
| curso_id | int | FK Curso |
| codigo_plano | varchar(30) | Código do plano |
| versao | varchar(20) | Controle de versão |
| objetivo_geral | text | Objetivo geral |
| objetivos_especificos | text | Objetivos específicos |
| carga_horaria_total | int | Carga horária oficial |
| observacoes | text | Informações complementares |
| criado_em | datetime | Auditoria |
| atualizado_em | datetime | Auditoria |

---

# Chave Primária

```text
PK: id_plano_curso
```

Avaliação:

✅ Adequada.

---

# Relacionamentos

## Curso

```text
Curso
 1:N
Plano de Curso
```

Implementado por:

```text
tb_plano_curso.curso_id
```

Avaliação:

✅ Correto.

Permite manter histórico de diferentes versões do plano de um mesmo curso.

---

## Plano de Curso → Itens

```text
Plano de Curso
 1:N
Itens do Plano
```

Implementado por:

```text
tb_plano_curso_item.plano_curso_id
```

Avaliação:

✅ Correto.

O conteúdo programático foi corretamente separado em uma entidade própria.

---

# Cardinalidade

## Atual

```text
Curso
 1:N
Plano de Curso

Plano de Curso
 1:N
Plano de Curso Item
```

Avaliação:

✅ Consistente.

---

# Regras de Negócio

## RN-001

Todo Plano de Curso deve pertencer a um Curso.

---

## RN-002

Todo Plano de Curso deve possuir um objetivo geral.

---

## RN-003

Todo Plano de Curso deve possuir carga horária definida.

---

## RN-004

Um Curso pode possuir várias versões do Plano de Curso.

---

## RN-005

Todo Plano de Curso deve possuir pelo menos um Item de Plano de Curso.

(Regra documental do projeto.)

---

## RN-006

Os Planos de Aula devem ser derivados exclusivamente dos Itens do Plano de Curso.

(Regra documental do projeto.)

---

## RN-007

O Plano de Curso representa o documento pedagógico oficial do curso.

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

* Permite versionamento;
* Boa separação entre planejamento e execução;
* Estrutura simples;
* Excelente base para o módulo pedagógico;
* Favorece padronização institucional.

---

# Pontos de Atenção

## Código do Plano

Atualmente:

```text
codigo_plano
```

Não possui restrição UNIQUE.

Dependendo da política institucional, poderá ser interessante garantir unicidade.

---

## Versão

Atualmente:

```text
versao
```

É um campo textual.

O controle das versões depende da aplicação.

---

# Melhorias Futuras

## V2

Avaliar:

```text
status_plano

Rascunho

Em revisão

Aprovado

Obsoleto
```

---

## V3

Avaliar:

```text
autor

revisor

data_aprovacao
```

---

## V4

Fluxo de aprovação pedagógica.

```text
Elaboração

Revisão

Aprovação

Publicação
```

---

## V5

Integração com:

```text
Calendário Institucional

Indicadores Pedagógicos

Controle de Competências

Matriz Curricular
```

---

# Observações de Arquitetura

## OA-001 — Versionamento Pedagógico

### Situação Atual

A entidade permite múltiplos planos para um mesmo curso através do campo:

```text
versao
```

---

### Observação

Durante a auditoria verificou-se que o versionamento foi corretamente previsto desde a modelagem inicial.

Entretanto, ainda não existe um mecanismo que determine qual versão está vigente.

---

### Impacto

Baixo.

A estrutura suporta a evolução.

A regra ficará sob responsabilidade da aplicação.

---

### Classificação

Nível 2 — Evolução

---

### Versão Prevista

V2

---

### Justificativa

No futuro será interessante permitir que apenas um Plano de Curso esteja ativo por curso, preservando o histórico das versões anteriores.

---

### Decisão da Auditoria

A modelagem atual permanece adequada para a V1.1.

A evolução será tratada em versões futuras.

---

# Conclusão

A tabela `tb_plano_curso` representa corretamente o documento pedagógico central do SGCI.

Sua modelagem está consistente, normalizada e preparada para evolução.

O suporte ao versionamento demonstra uma visão arquitetural madura e fornece base sólida para os módulos de planejamento, execução e avaliação do processo de ensino.

Status Final:

```text
APROVADA PARA V1.1
```