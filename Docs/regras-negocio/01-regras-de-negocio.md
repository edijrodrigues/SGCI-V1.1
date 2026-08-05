# Regras de Negócio do SGCI

**Documento:** RN-001

**Projeto:** SGCI - Sistema de Gestão de Cursos e Instituições

**Versão:** V1.1

**Status:** Em Construção

---

# Objetivo

Este documento centraliza todas as regras de negócio identificadas durante o desenvolvimento e durante a auditoria da modelagem do SGCI.

Seu objetivo é registrar, de forma organizada, as normas institucionais que orientam o funcionamento do sistema, independentemente da implementação técnica.

As regras aqui descritas representam o comportamento esperado da aplicação e servem como referência para análise, desenvolvimento, testes e futuras evoluções.

---

# Organização

As regras estão agrupadas em três níveis:

```text
Domínio
    │
Subdomínio
    │
Regra de Negócio
```

Cada regra recebe um identificador único seguindo o padrão:

```text
RN-[DOMÍNIO]-[SUBDOMÍNIO]-[SEQUÊNCIA]
```

## Domínios

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

## Instituição / Unidade / Sala / Turno

### RN-EST-ORG-001

Toda Unidade deve pertencer a uma Instituição.

---

### RN-EST-ORG-002

Toda Sala deve pertencer a uma Unidade.

---

### RN-EST-ORG-003

Toda Turma deve estar vinculada a uma Sala.

---

### RN-EST-ORG-004

Toda Turma deve possuir um Turno.

---

### RN-EST-ORG-005

A capacidade máxima de alunos de uma Turma é limitada pela capacidade da Sala utilizada.

---

# Cadastro Acadêmico

## Aluno

### RN-CAD-ALU-001

Todo Aluno deve possuir matrícula única.

---

## Matrícula

### RN-CAD-MAT-001

Toda Matrícula pertence a um único Aluno.

---

### RN-CAD-MAT-002

Toda Matrícula pertence a uma única Turma.

---

### RN-CAD-MAT-003

Um Aluno pode possuir diversas Matrículas ao longo de sua vida acadêmica.

---

# Planejamento Pedagógico

## Plano de Curso

### RN-PED-PC-001

Todo Curso deve possuir um Plano de Curso.

---

### RN-PED-PC-002

Todo Plano de Curso pertence exclusivamente a um Curso.

---

### RN-PED-PC-003

Todo Plano de Curso deve possuir pelo menos um Item de Plano de Curso.

---

### RN-PED-PC-004

O Plano de Curso representa o documento pedagógico oficial do Curso.

---

## Item do Plano de Curso

### RN-PED-IP-001

Todo Item do Plano de Curso deve pertencer a um único Plano de Curso.

---

### RN-PED-IP-002

Um Plano de Curso deve possuir um ou mais Itens de Plano.

---

### RN-PED-IP-003

A numeração (`numero_item`) deve manter uma sequência lógica dentro do Plano de Curso.

---

### RN-PED-IP-004

Todo Item deve possuir objetivo específico claramente definido.

---

### RN-PED-IP-005

Todo Item deve possuir conteúdo programático.

---

### RN-PED-IP-006

Todo Item deve definir as atividades e recursos didáticos previstos.

---

### RN-PED-IP-007

Todo Item deve possuir carga horária prevista.

---

## Plano de Aula

### RN-PED-PA-001

Os Planos de Aula devem ser derivados exclusivamente dos Itens do Plano de Curso.

### RN-PED-PA-002

Todo Plano de Aula deve possuir um Instrutor responsável.

### RN-PED-PA-003

Todo Plano de Aula deve possuir um título.

### RN-PED-PA-004

Todo Plano de Aula deve possuir carga horária prevista.

### RN-PED-PA-005

Um Plano de Aula pode estar vinculado a uma Turma específica.

### RN-PED-PA-006

A exclusão de uma Turma não deve excluir o Plano de Aula correspondente.

### RN-PED-PA-007

Um Item do Plano pode originar diversos Planos de Aula.

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
| V1.1 | 2026 | Refatoração da estrutura das regras de negócio |
| V1.1 | 2026 | Inclusão das regras da Estrutura Organizacional |
| V1.1 | 2026 | Inclusão das regras do Planejamento Pedagógico |
| V1.1 | 2026 | Inclusão das regras dos Itens do Plano de Curso |

---

## Anexos do Diário de Aula

RN-PED-ANX-001

Todo Anexo deve pertencer a um Diário de Aula.

---

RN-PED-ANX-002

Um Diário de Aula pode possuir vários anexos.

---

RN-PED-ANX-003

Todo Anexo deve possuir um caminho de armazenamento válido.

---

RN-PED-ANX-004

O nome original do arquivo poderá ser preservado para fins de identificação.

# Observações

Este documento é incremental.

Novas regras serão adicionadas à medida que as auditorias forem concluídas.

As regras são organizadas por Domínio e Subdomínio para facilitar sua localização, rastreabilidade e manutenção durante a evolução do SGCI.