# Regras de Negócio do SGCI

**Documento:** RN-001

**Projeto:** SGCI - Sistema de Gestão de Cursos e Instituições

**Versão:** V1.1

**Status:** Consolidado (V1.1)

---

# Objetivo

Este documento consolida todas as Regras de Negócio identificadas durante a Auditoria da Modelagem da versão V1.1 do SGCI.

Seu objetivo é registrar, de forma organizada, as normas institucionais que orientam o funcionamento do sistema, independentemente da implementação técnica.

As regras aqui descritas representam o comportamento esperado da aplicação e servem como referência para:

- modelagem do banco de dados;
- desenvolvimento da aplicação;
- testes;
- documentação técnica;
- evolução do sistema.

---

# Organização

As regras estão organizadas por Domínio e Subdomínio.

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

## Agenda Semanal da Turma

### RN-EST-ORG-006

Toda configuração de dia da semana deve pertencer a uma Turma.

---

### RN-EST-ORG-007

Uma Turma poderá possuir um ou mais dias da semana cadastrados.

---

### RN-EST-ORG-008

Não poderá existir duplicidade do mesmo dia da semana para uma mesma Turma.

Esta regra é garantida por:

```sql
UNIQUE (turma_id, dia_semana)
```

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

Um Plano de Curso deve possuir um ou mais Itens.

---

### RN-PED-IP-003

A numeração (`numero_item`) deve manter sequência lógica dentro do Plano.

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

# Execução Pedagógica

## Diário de Aula

### RN-EXE-DIA-001

Toda Aula Ministrada deve possuir um Diário de Aula correspondente.

---

### RN-EXE-DIA-002

Cada Diário de Aula deve estar vinculado a um Diário Previsto.

---

### RN-EXE-DIA-003

Cada Diário Previsto pode originar apenas um Diário Executado.

---

## Anexos

### RN-EXE-ANX-001

Todo Anexo deve pertencer a um Diário de Aula.

---

### RN-EXE-ANX-002

Um Diário de Aula pode possuir vários anexos.

---

### RN-EXE-ANX-003

Todo Anexo deve possuir um caminho de armazenamento válido.

---

### RN-EXE-ANX-004

O nome original do arquivo poderá ser preservado para fins de identificação.

---

# Avaliação

### RN-AVA-001

Toda Avaliação pertence a uma Matrícula.

---

### RN-AVA-002

Toda Avaliação pertence a um Item do Plano de Curso.

---

### RN-AVA-003

Uma Avaliação poderá estar vinculada a um Plano de Aula.

---

### RN-AVA-004

Cada Avaliação registra um único resultado para o aluno.

---

# Calendário

## Calendário Letivo

### RN-CAL-LET-001

Cada Ano Letivo deve possuir apenas um Calendário Letivo.

---

### RN-CAL-LET-002

Todo Calendário Letivo deve possuir data de início.

---

### RN-CAL-LET-003

Todo Calendário Letivo deve possuir data de encerramento.

---

### RN-CAL-LET-004

A data de encerramento deve ser posterior à data de início.

---

## Eventos

### RN-CAL-EVT-001

Todo Evento pertence a um Calendário Letivo.

---

### RN-CAL-EVT-002

Eventos poderão afetar toda a instituição ou apenas parte dela.

---

# Histórico Escolar

### RN-HIS-001

Todo Histórico pertence a uma Matrícula.

---

### RN-HIS-002

Todo Histórico pertence a um Curso.

---

### RN-HIS-003

O Histórico registra o resultado acadêmico consolidado do aluno.

---

# Certificação

### RN-CER-001

Todo Certificado deve estar vinculado a um Histórico Escolar.

---

### RN-CER-002

Todo Certificado deve possuir um código único.

---

### RN-CER-003

Somente alunos aptos poderão receber Certificado.

---

# Financeiro

### RN-FIN-001

Todo Pagamento pertence a uma Matrícula.

---

### RN-FIN-002

Todo Pagamento deve possuir valor.

---

### RN-FIN-003

Todo Pagamento deve possuir data de vencimento.

---

### RN-FIN-004

O pagamento poderá registrar data de quitação.

---

### RN-FIN-005

O status financeiro representa a situação atual da cobrança.

---

# Segurança

As regras deste domínio serão documentadas durante a implementação dos módulos de autenticação, autorização e auditoria.

---

# Controle de Alterações

| Versão | Data | Alteração |
|---------|------|-----------|
| V1.1 | 2026 | Criação do documento |
| V1.1 | 2026 | Consolidação das regras após Auditoria da Modelagem |
| V1.1 | 2026 | Inclusão das regras da Agenda Semanal das Turmas (`tb_turma_dias`) |
| V1.1 | 2026 | Refatoração estrutural do documento |

---

# Observações

Este documento representa a consolidação das Regras de Negócio identificadas durante a Auditoria da Modelagem da versão V1.1.

Alterações futuras deverão ocorrer apenas durante a evolução funcional do sistema e ser registradas conforme o versionamento oficial do projeto.

As Regras de Negócio mantêm rastreabilidade com:

- Auditoria da Modelagem;
- Decisões Arquiteturais (ADR);
- Backlog;
- DER Oficial;
- Documentação Técnica.