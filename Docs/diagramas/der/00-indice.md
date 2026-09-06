# Índice do DER Oficial — SGCI V1.1

## Objetivo

Este documento funciona como índice dos Diagramas Entidade-Relacionamento (DER) da versão V1.1 do SGCI.

Ele organiza os diagramas por módulo e acompanha o progresso de sua elaboração, revisão e consolidação.

O DER Oficial será construído de forma modular, permitindo que cada parte da modelagem seja revisada individualmente antes da elaboração do diagrama consolidado.

---

# Planejamento

- [x] DER-001-planejamento.md

---

# Diagramas por Módulo

## Módulo Acadêmico

- [ ] DER-002-academico.drawio

Entidades:

- `tb_aluno`
- `tb_instrutor`
- `tb_curso`
- `tb_turma`
- `tb_turma_dias`
- `tb_matricula`

---

## Estrutura Organizacional

- [ ] DER-003-estrutura-organizacional.drawio

Entidades:

- `tb_instituicao`
- `tb_unidade`
- `tb_sala`
- `tb_turno`

---

## Planejamento Pedagógico

- [ ] DER-004-planejamento-pedagogico.drawio

Entidades:

- `tb_plano_curso`
- `tb_plano_curso_item`
- `tb_plano_aula`

---

## Execução Pedagógica

- [ ] DER-005-execucao-pedagogica.drawio

Entidades:

- `tb_diario_aula_previsto`
- `tb_diario_aula`
- `tb_diario_anexo`
- `tb_frequencia_aluno`
- `tb_avaliacao_aluno`

---

## Calendário

- [ ] DER-006-calendario.drawio

Entidades:

- `tb_calendario_letivo`
- `tb_calendario_letivo_detalhe`
- `tb_calendario_evento`

---

## Histórico Escolar

- [ ] DER-007-historico.drawio

Entidades:

- `tb_historico_aluno`
- `tb_certificado`

---

## Financeiro

- [ ] DER-008-financeiro.drawio

Entidade:

- `tb_pagamento`

---

# Consolidação

## DER Consolidado

- [ ] DER-009-consolidado.drawio

O DER Consolidado reunirá todas as 24 entidades da versão V1.1 em um único diagrama.

---

# Controle de Progresso

| Código | Diagrama | Status |
|--------|----------|--------|
| DER-001 | Planejamento | ✅ Concluído |
| DER-002 | Módulo Acadêmico | ⏳ Pendente |
| DER-003 | Estrutura Organizacional | ⏳ Pendente |
| DER-004 | Planejamento Pedagógico | ⏳ Pendente |
| DER-005 | Execução Pedagógica | ⏳ Pendente |
| DER-006 | Calendário | ⏳ Pendente |
| DER-007 | Histórico Escolar | ⏳ Pendente |
| DER-008 | Financeiro | ⏳ Pendente |
| DER-009 | DER Consolidado | ⏳ Pendente |

---

# Observações

Os diagramas deverão ser elaborados e revisados individualmente antes de sua incorporação ao DER Consolidado.

A conclusão de um diagrama modular não implica alteração automática da modelagem do banco de dados.

Caso seja identificada alguma inconsistência durante a elaboração ou revisão dos diagramas, a questão deverá ser analisada e, quando necessário, registrada no Backlog ou nas Decisões Arquiteturais (ADR).

O DER Consolidado somente será considerado concluído após a revisão de todos os diagramas modulares.