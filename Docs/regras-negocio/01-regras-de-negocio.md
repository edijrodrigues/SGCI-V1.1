# Regras de Negócio do SGCI

**Documento:** RN-001

**Projeto:** SGCI - Sistema de Gestão de Cursos e Instituições

**Versão:** V1.1

**Status:** Em Construção

---

# Objetivo

Este documento centraliza todas as regras de negócio identificadas durante o desenvolvimento e a auditoria da modelagem do SGCI.

Seu objetivo é registrar, de forma organizada, as normas institucionais que orientam o funcionamento do sistema, independentemente da implementação técnica.

As regras aqui descritas representam o comportamento esperado da aplicação e servem como referência para análise, desenvolvimento, testes e futuras evoluções.

---

# Organização

As regras estão agrupadas por domínio funcional.

Cada regra recebe um identificador único para facilitar sua rastreabilidade.

Padrão:

```text
RN-XXX-001
```

Onde:

```text
EST = Estrutura Organizacional

CAD = Cadastro Acadêmico

PED = Planejamento Pedagógico

EXE = Execução Pedagógica

AVA = Avaliação

HIS = Histórico Escolar

CER = Certificação

FIN = Financeiro

CAL = Calendário

SEG = Segurança
```

---

# Estrutura Organizacional

## RN-EST-001

Toda Unidade deve pertencer a uma Instituição.

---

## RN-EST-002

Toda Sala deve pertencer a uma Unidade.

---

## RN-EST-003

Toda Turma deve estar vinculada a uma Sala.

---

## RN-EST-004

Toda Turma deve possuir um Turno.

---

## RN-EST-005

A capacidade máxima de alunos de uma Turma é limitada pela capacidade da Sala utilizada.

---

# Cadastro Acadêmico

## RN-CAD-001

Todo Aluno deve possuir matrícula única.

---

## RN-CAD-002

Toda Matrícula pertence a um único Aluno.

---

## RN-CAD-003

Toda Matrícula pertence a uma única Turma.

---

## RN-CAD-004

Um Aluno pode possuir diversas Matrículas ao longo da vida acadêmica.

---

# Planejamento Pedagógico

## RN-PED-001

Todo Curso deve possuir um Plano de Curso.

---

## RN-PED-002

Todo Plano de Curso pertence a um único Curso.

---

## RN-PED-003

Todo Plano de Curso deve possuir pelo menos um Item de Plano de Curso.

---

## RN-PED-004

Os Planos de Aula devem ser derivados exclusivamente dos Itens do Plano de Curso.

---

## RN-PED-005

O Plano de Curso representa o documento pedagógico oficial do Curso.

---

# Execução Pedagógica

*Aguardando auditoria.*

---

# Avaliação

*Aguardando auditoria.*

---

# Histórico Escolar

*Aguardando auditoria.*

---

# Certificação

*Aguardando auditoria.*

---

# Financeiro

*Aguardando auditoria.*

---

# Calendário

*Aguardando auditoria.*

---

# Segurança

*Aguardando auditoria.*

---

# Controle de Alterações

| Versão | Data | Alteração |
|---------|------|-----------|
| V1.1 | 2026 | Criação do documento |
| V1.1 | 2026 | Inclusão das regras da Estrutura Organizacional |
| V1.1 | 2026 | Inclusão das regras do Planejamento Pedagógico |

---

# Observações

Este documento é incremental.

Novas regras de negócio serão adicionadas conforme a auditoria das entidades for sendo concluída.

O objetivo é que, ao término da auditoria da V1.1, este documento represente a especificação funcional consolidada do SGCI.