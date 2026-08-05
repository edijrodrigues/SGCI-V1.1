# DA-003 - Plano de Aula como Recurso Pedagógico

**Documento:** DA-003

**Projeto:** SGCI - Sistema de Gestão de Cursos e Instituições

**Categoria:** Decisão Arquitetural

**Versão:** V1.1

**Status:** Aprovada

---

# Objetivo

Registrar a decisão arquitetural que definiu o Plano de Aula como um recurso pedagógico reutilizável, independente da existência de uma Turma específica.

Esta decisão orienta a modelagem do banco de dados e influencia diretamente o comportamento funcional do módulo de Planejamento Pedagógico.

---

# Contexto

Durante a modelagem do módulo de Planejamento Pedagógico foi necessário definir o papel do Plano de Aula dentro do sistema.

Duas abordagens foram consideradas:

## Alternativa 1

Modelar o Plano de Aula como um documento pertencente exclusivamente a uma Turma.

Nesta abordagem, cada Turma possuiria seus próprios Planos de Aula.

Consequências:

- duplicação de planejamento;
- maior esforço de manutenção;
- necessidade de recriar o planejamento para novas ofertas do mesmo Curso;
- dificuldade de padronização institucional.

---

## Alternativa 2

Modelar o Plano de Aula como um recurso pedagógico pertencente ao planejamento do Curso.

Nesta abordagem, o Plano de Aula representa a forma como determinado conteúdo deverá ser ministrado, podendo posteriormente ser associado a diferentes Turmas.

---

# Decisão

Foi adotada a segunda abordagem.

O Plano de Aula passou a ser tratado como um recurso pedagógico derivado do Item do Plano de Curso.

Seu relacionamento com a Turma tornou-se opcional, permitindo que o planejamento permaneça válido independentemente da existência de uma oferta específica.

---

# Justificativa

Esta decisão proporciona uma separação clara entre planejamento pedagógico e execução acadêmica.

O planejamento representa o conhecimento institucional.

A Turma representa apenas uma oferta daquele planejamento.

Essa separação reduz duplicidades e favorece a reutilização do trabalho pedagógico.

---

# Implementação

A decisão foi refletida na modelagem através das seguintes características:

- relacionamento obrigatório com o Item do Plano de Curso;
- relacionamento obrigatório com o Instrutor responsável;
- relacionamento opcional com a Turma;
- política `ON DELETE SET NULL` para a chave estrangeira da Turma.

Essa estratégia garante que a exclusão de uma Turma não implique na perda do planejamento pedagógico.

---

# Benefícios

## Reutilização

O mesmo Plano de Aula pode ser utilizado em diferentes ofertas do Curso.

---

## Padronização

As Turmas seguem um planejamento institucional único.

---

## Preservação Histórica

O planejamento permanece registrado mesmo após alterações organizacionais.

---

## Evolução

Novas Turmas podem reutilizar o planejamento existente sem necessidade de recriação.

---

## Manutenção

Alterações pedagógicas são realizadas em um único local.

---

# Consequências

## Positivas

- menor redundância de dados;
- maior consistência pedagógica;
- melhor organização do domínio;
- maior facilidade de manutenção.

---

## Pontos de Atenção

Caso uma instituição deseje permitir adaptações específicas para determinadas Turmas, essas personalizações deverão ocorrer em entidades próprias da execução pedagógica, preservando o Plano de Aula como referência institucional.

---

# Impacto na Arquitetura

Esta decisão estabelece a seguinte hierarquia pedagógica:

```text
Curso
    │
Plano de Curso
    │
Itens do Plano
    │
Plano de Aula
    │
Execução da Aula
```

O planejamento permanece separado da execução.

---

# Tabelas Impactadas

- tb_plano_curso
- tb_plano_curso_item
- tb_plano_aula

Futuramente:

- tb_diario_aula
- tb_frequencia
- tb_avaliacao

---

# Referências

Esta decisão está relacionada aos seguintes documentos:

- Auditoria da tabela `tb_plano_aula`
- RN-PED-PC-001 a RN-PED-PC-004
- RN-PED-IP-001 a RN-PED-IP-007
- RN-PED-PA-001 a RN-PED-PA-007

---

# Revisões Futuras

Esta decisão poderá ser revisada caso versões futuras do SGCI passem a suportar múltiplas metodologias pedagógicas específicas por Turma.

Até que esse cenário exista, esta decisão permanece válida.

---

# Histórico de Alterações

| Versão | Data | Alteração |
|---------|------|-----------|
| V1.1 | 2026 | Criação do documento |