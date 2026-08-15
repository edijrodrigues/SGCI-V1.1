# Backlog da Versão V1.1

**Documento:** BL-001

**Projeto:** SGCI - Sistema de Gestão de Cursos e Instituições

**Versão:** V1.1

**Status:** Ativo

---

# Objetivo

Este documento consolida todas as melhorias identificadas durante a Auditoria da Modelagem da versão V1.1 do SGCI.

Seu objetivo é registrar evoluções que não serão implementadas na versão atual, preservando a estabilidade da modelagem e servindo como base para o planejamento das próximas versões do sistema.

Todas as propostas aqui registradas deverão ser avaliadas antes de sua implementação e poderão resultar em alterações na modelagem, nas regras de negócio ou nas decisões arquiteturais.

---

# Organização

As melhorias estão agrupadas por domínio funcional.

Cada item recebe um identificador único para facilitar sua rastreabilidade durante a evolução do projeto.

Padrão utilizado:

```text
DOM-001
```

Exemplo:

```text
ARQ-001

PED-001

HIS-001

FIN-001
```

---

# Arquitetura

## ARQ-001 — Documentação Técnica da Arquitetura

**Objetivo**

Consolidar toda a documentação técnica da arquitetura do SGCI.

### Documentos previstos

- Documentação das linguagens utilizadas;
- Documentação do servidor;
- Arquitetura MVC;
- Estrutura de pastas;
- Banco de Dados;
- Padrões de desenvolvimento;
- Autenticação;
- Controle de sessão.

**Prioridade**

🟡 Média

**Versão Prevista**

V1.1

**Status**

Backlog

---

# Planejamento Pedagógico

## PED-001 — Garantir numeração única dos Itens do Plano de Curso

**Situação Atual**

A tabela `tb_plano_curso_item` não impede que dois itens do mesmo Plano possuam a mesma numeração.

**Alteração Proposta**

```sql
UNIQUE (plano_curso_id, numero_item)
```

**Benefícios**

- preserva a sequência lógica;
- evita duplicidades;
- reforça a integridade do Plano de Curso.

**Prioridade**

🟡 Média

**Versão Prevista**

V2

**Status**

Backlog

---

## PED-002 — Evitar agendamentos duplicados

**Situação Atual**

A tabela `tb_diario_aula_previsto` permite registros repetidos para uma mesma turma, data e plano de aula.

**Alteração Proposta**

```sql
UNIQUE (turma_id, data_prevista, plano_aula_id)
```

**Benefícios**

- evita duplicidade de planejamento;
- reforça a integridade do cronograma.

**Prioridade**

🟡 Média

**Versão Prevista**

V2

**Status**

Backlog

---

# Histórico Escolar

## HIS-001 — Garantir um único Histórico Escolar por Matrícula

**Situação Atual**

A tabela `tb_historico_aluno` permite tecnicamente mais de um Histórico para uma mesma Matrícula.

**Justificativa**

Pelas regras atuais do SGCI, cada Matrícula deve gerar apenas um Histórico Escolar consolidado.

**Alteração Proposta**

```sql
UNIQUE (matricula_id)
```

**Impacto**

- reforça a integridade referencial;
- garante um único Histórico por Matrícula;
- simplifica consultas;
- facilita a emissão de Certificados.

**Prioridade**

🟡 Média

**Versão Prevista**

V2

**Status**

Backlog

---

## HIS-002 — Garantir um único Certificado por Histórico Escolar

**Situação Atual**

A tabela `tb_certificado` permite tecnicamente mais de um Certificado para um mesmo Histórico Escolar.

**Justificativa**

Cada Histórico Escolar consolidado deve originar apenas um Certificado oficial.

**Alteração Proposta**

```sql
UNIQUE (historico_id)
```

**Impacto**

- reforça a regra de negócio;
- evita emissão duplicada;
- simplifica auditorias.

**Prioridade**

🟡 Média

**Versão Prevista**

V2

**Status**

Backlog

---

# Financeiro

## FIN-001 — Evolução do Modelo Financeiro

**Situação Atual**

A tabela `tb_pagamento` reúne informações da cobrança e da liquidação em uma única entidade.

**Justificativa**

Instituições com maior complexidade financeira poderão necessitar separar os conceitos de:

- Título Financeiro;
- Pagamento;
- Negociação;
- Recebimento.

**Alteração Proposta**

Avaliar a criação de novas entidades específicas para o módulo financeiro.

**Prioridade**

🟢 Baixa

**Versão Prevista**

V3

**Status**

Backlog

---

# Controle de Alterações

| Versão | Data | Alteração |
|---------|------|-----------|
| V1.1 | 2026 | Criação do documento |
| V1.1 | 2026 | Consolidação das melhorias identificadas durante a Auditoria da Modelagem |
| V1.1 | 2026 | Padronização estrutural do Backlog |

---

# Observações

Este documento representa o backlog oficial da versão V1.1.

As melhorias aqui registradas não fazem parte do escopo da versão atual e somente deverão ser implementadas após análise de impacto, revisão das Regras de Negócio e, quando necessário, atualização das Decisões Arquiteturais (ADR).

Novas propostas poderão ser adicionadas durante a evolução do SGCI, mantendo a rastreabilidade entre Auditoria da Modelagem, Backlog, Regras de Negócio e documentação técnica.