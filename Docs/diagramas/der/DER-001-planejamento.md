# Planejamento do DER Oficial — SGCI V1.1

**Documento:** DER-001

**Projeto:** SGCI - Sistema de Gestão de Cursos e Instituições

**Versão:** V1.1

**Status:** Em Planejamento

---

# Objetivo

Este documento define os critérios para elaboração do **Diagrama Entidade-Relacionamento (DER) Oficial** da versão V1.1 do SGCI.

Seu objetivo é estabelecer um padrão único para representação gráfica da modelagem do banco de dados, garantindo consistência entre a documentação técnica, as Regras de Negócio, as Decisões Arquiteturais (ADR) e a implementação do sistema.

O DER Oficial representará a modelagem consolidada após a conclusão da Auditoria da Modelagem.

---

# Escopo

O DER Oficial deverá representar integralmente as **24 entidades** da versão V1.1.

Serão representados:

- entidades;
- atributos;
- chaves primárias (PK);
- chaves estrangeiras (FK);
- relacionamentos;
- cardinalidades.

Não fazem parte do escopo desta documentação:

- Procedures;
- Triggers;
- Views;
- Índices secundários;
- Eventos;
- Scripts SQL.

Esses elementos permanecem documentados diretamente no banco de dados.

---

# Ferramenta Oficial

A ferramenta oficial para elaboração do DER será:

**Draw.io (diagrams.net)**

Justificativa:

- software gratuito;
- formato aberto;
- arquivos versionáveis no Git;
- fácil manutenção;
- exportação para PNG, SVG e PDF;
- independência de SGBD.

Outras ferramentas poderão ser utilizadas apenas como apoio.

| Ferramenta      | Finalidade             |
|-----------------|------------------------|
| Draw.io         | DER Oficial            |
| MySQL Workbench | Validação da modelagem |
| PlantUML        | Diagramas UML futuros  |

---

# Organização dos Diagramas

O DER será desenvolvido por módulos.

Cada módulo será revisado individualmente antes da consolidação final.

Planejamento:

```text
DER-001 — Planejamento

DER-002 — Módulo Acadêmico

DER-003 — Estrutura Organizacional

DER-004 — Planejamento Pedagógico

DER-005 — Execução Pedagógica

DER-006 — Calendário

DER-007 — Histórico Escolar

DER-008 — Financeiro

DER-009 — DER Consolidado
```

---

# Ordem de Construção

Os diagramas deverão seguir a mesma ordem utilizada durante a Auditoria da Modelagem.

```text
Módulo Acadêmico

↓

Estrutura Organizacional

↓

Planejamento Pedagógico

↓

Execução Pedagógica

↓

Calendário

↓

Histórico Escolar

↓

Financeiro

↓

DER Consolidado
```

Esta sequência preserva a lógica funcional do sistema e facilita as revisões.

---

# Padrão de Representação

Todos os diagramas deverão seguir o mesmo padrão visual.

## Entidades

Cada entidade será representada contendo:

- nome da tabela;
- chave primária;
- atributos;
- chaves estrangeiras.

---

## Relacionamentos

Todos os relacionamentos deverão apresentar:

- cardinalidade;
- direção lógica;
- identificação visual clara.

---

## Nomenclatura

As entidades utilizarão exatamente os mesmos nomes adotados na modelagem física.

Exemplo:

```text
tb_aluno

tb_matricula

tb_turma

tb_plano_aula
```

Não serão utilizados nomes simplificados.

---

# Critérios de Construção

Durante a elaboração do DER deverão ser observados:

- modelagem física consolidada;
- Auditoria da Modelagem;
- Regras de Negócio;
- Decisões Arquiteturais (ADR);
- Backlog da V1.1.

Nenhuma alteração estrutural deverá ser realizada diretamente durante a construção do DER.

Caso seja identificada alguma inconsistência, ela deverá ser analisada antes da modificação da modelagem.

---

# Entregáveis

Ao término desta etapa deverão existir os seguintes artefatos:

- arquivo fonte Draw.io;
- exportação em SVG;
- exportação em PNG;
- versão PDF;
- DER Consolidado da V1.1.

---

# Próximo Marco

Após a aprovação do DER Oficial será iniciado o processo de **Congelamento da Modelagem da versão V1.1**.

A partir desse momento:

- a modelagem passará a ser considerada oficial;
- alterações estruturais somente poderão ocorrer mediante atualização da documentação, do Backlog e, quando necessário, das Decisões Arquiteturais (ADR).

---

# Controle de Alterações

| Versão | Data | Alteração |
|---------|------|-----------|
| V1.1 | 2026 | Criação do documento |
| V1.1 | 2026 | Definição do planejamento do DER Oficial |

---

# Observações

O DER Oficial representa a consolidação visual da modelagem do SGCI.

Sua elaboração não tem como objetivo redefinir a estrutura do banco de dados, mas documentar de forma gráfica a modelagem já consolidada durante a Auditoria da Modelagem.

Qualquer alteração estrutural identificada durante esta etapa deverá seguir o processo oficial de evolução do projeto.

## Estratégia de Representação

O SGCI V1.1 utiliza diferentes ferramentas para representar
a modelagem, cada uma com finalidade específica.

### MySQL Workbench

Utilizado como referência da modelagem física atual do banco
de dados e como representação consolidada das entidades e
relacionamentos.

### PlantUML

Utilizado como documentação técnica versionável da modelagem.

Os diagramas PlantUML possuem caráter visual e estrutural.
Alguns campos são deliberadamente omitidos para preservar a
legibilidade dos diagramas.

A documentação detalhada dos campos, tipos, constraints,
índices e demais características físicas encontra-se nas
auditorias individuais das tabelas.

### Draw.io

Utilizado para representações visuais específicas ou
apresentações futuras, quando necessário.

A otimização estética do DER consolidado não constitui
requisito da versão V1.1.