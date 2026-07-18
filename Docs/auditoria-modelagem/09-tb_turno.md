# 09 - Auditoria da Tabela tb_turno

## Identificação

**Tabela:** tb_turno

**Módulo:** Estrutura Organizacional

**Categoria:** Entidade Paramétrica

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_turno` representa os períodos de funcionamento da instituição.

Seu objetivo é padronizar os horários de início e término das atividades acadêmicas, permitindo que turmas sejam organizadas em turnos previamente definidos.

A utilização de uma entidade própria evita redundância de informações e garante padronização dos horários em todo o sistema.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

* Definir os turnos de funcionamento da instituição;
* Padronizar horários de início e término;
* Servir como referência para as turmas;
* Permitir organização da grade acadêmica;
* Facilitar o planejamento das atividades.

---

# Estrutura Atual

| Campo | Tipo | Observação |
|---------|---------|---------|
| id_turno | int | Chave Primária |
| nome_turno | varchar(50) | Nome do turno |
| hora_inicio | time | Horário inicial |
| hora_fim | time | Horário final |
| observacao | text | Informações complementares |
| ativo | tinyint(1) | Controle lógico |
| criado_em | datetime | Auditoria |
| atualizado_em | datetime | Auditoria |
| deletado_em | datetime | Soft Delete |

---

# Chave Primária

```text
PK: id_turno
```

Avaliação:

✅ Adequada.

---

# Relacionamentos

## Turma

```text
Turno
 1:N
Turma
```

Implementado por:

```text
tb_turma.turno_id
```

Avaliação:

✅ Correto.

Um turno pode ser utilizado por diversas turmas.

---

# Cardinalidade

## Atual

```text
Turno
 1:N
Turma
```

Avaliação:

✅ Consistente.

---

# Regras de Negócio

## RN-001

Todo turno deve possuir um nome.

---

## RN-002

Todo turno deve possuir horário de início.

---

## RN-003

Todo turno deve possuir horário de término.

---

## RN-004

Uma turma deve estar vinculada a um turno.

---

## RN-005

Os horários devem ser padronizados para toda a instituição.

---

## RN-006

O turno pode ser desativado sem exclusão física dos registros.

Implementado por:

```text
ativo
deletado_em
```

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

* Estrutura simples;
* Evita duplicação de horários nas turmas;
* Facilita manutenção;
* Permite padronização institucional;
* Soft delete implementado;
* Campos de auditoria presentes.

---

# Pontos de Atenção

## Horários

Atualmente são definidos apenas por:

```text
hora_inicio

hora_fim
```

O sistema não valida conflitos entre turnos.

---

## Sobreposição

Não existem regras para impedir horários sobrepostos.

Exemplo:

```text
Manhã
07:30 às 11:30

Manhã Especial
08:00 às 12:00
```

Essa validação depende da regra de negócio da instituição.

---

# Melhorias Futuras

## V2

Avaliar:

```text
cor_turno
```

Para utilização em calendários.

---

## V3

Avaliar:

```text
tipo_turno

regular

intensivo

especial
```

---

## V4

Integração com:

```text
Calendário Institucional

Agenda Acadêmica

Reserva de Salas
```

---

## V5

Permitir configuração de:

```text
Intervalos

Horários de almoço

Aulas consecutivas

Blocos de horários
```

---

# Observações de Arquitetura

## OA-001 — Turno como Entidade Paramétrica

### Situação Atual

O turno é utilizado apenas como referência para as turmas.

Seu papel é padronizar os horários institucionais.

---

### Observação

Durante a auditoria foi discutida a possibilidade de o turno participar diretamente da estrutura física da instituição.

Exemplo:

```text
Instituição
    ↓
Unidade
    ↓
Sala
    ↓
Turno
    ↓
Turma
```

Após análise, concluiu-se que essa alteração aumentaria significativamente a complexidade da modelagem sem trazer benefícios proporcionais para a V1.1.

Atualmente, o turno representa uma característica operacional da turma e não da sala.

---

### Impacto

Alto.

A alteração afetaria a modelagem acadêmica, o calendário, a alocação de salas e diversas consultas do sistema.

---

### Classificação

Nível 3 — Refatoração Estrutural

---

### Versão Prevista

Indefinida.

(Reavaliar a partir da V4 ou V5.)

---
0
### Justificativa

A modelagem atual atende corretamente às necessidades do projeto.

Caso futuramente seja implementado um sistema completo de gestão de ocupação de salas e conflitos de horários, essa arquitetura poderá ser reavaliada.

---

### Decisão da Auditoria

Nenhuma alteração será realizada na V1.1.

O relacionamento atual permanece adequado para os objetivos do projeto.

---

# Conclusão

A tabela `tb_turno` apresenta modelagem simples, consistente e adequada aos objetivos atuais do SGCI.

Sua utilização como entidade paramétrica reduz redundâncias e facilita a padronização dos horários acadêmicos.

As melhorias identificadas são evolutivas e não justificam alterações estruturais para a V1.1.

Status Final:

```text
APROVADA PARA V1.1
```