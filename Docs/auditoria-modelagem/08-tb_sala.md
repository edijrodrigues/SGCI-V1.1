# 08 - Auditoria da Tabela tb_sala

## Identificação

**Tabela:** tb_sala

**Módulo:** Estrutura Organizacional

**Categoria:** Entidade Física

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_sala` representa os ambientes físicos disponíveis para realização das atividades acadêmicas.

Ela organiza os espaços pertencentes às unidades da instituição e serve como base para alocação das turmas, permitindo controlar capacidade, tipo de ambiente e utilização dos recursos físicos.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

* Representar os ambientes físicos da instituição;
* Organizar as salas por unidade;
* Definir a capacidade máxima de alunos;
* Classificar o tipo da sala;
* Servir como base para alocação das turmas;
* Permitir indicadores de ocupação;
* Permitir planejamento da infraestrutura.

---

# Estrutura Atual

| Campo | Tipo | Observação |
|---------|---------|---------|
| id_sala | int | Chave Primária |
| unidade_id | int | FK Unidade |
| nome_sala | varchar(...) | Identificação da sala |
| capacidade | int | Capacidade máxima |
| tipo_sala | enum(...) | Tipo do ambiente |
| observacao | text | Informações complementares |
| ativo | tinyint(1) | Controle lógico |
| criado_em | datetime | Auditoria |
| atualizado_em | datetime | Auditoria |
| deletado_em | datetime | Soft Delete |

---

# Chave Primária

```text
PK: id_sala
```

Avaliação:

✅ Adequada.

---

# Relacionamentos

## Unidade

```text
Unidade
 1:N
Sala
```

Implementado por:

```text
tb_sala.unidade_id
```

Avaliação:

✅ Correto.

Cada unidade pode possuir diversas salas.

---

## Turma

```text
Sala
 1:N
Turma
```

Implementado por:

```text
tb_turma.sala_id
```

Avaliação:

✅ Correto.

Uma sala pode receber diversas turmas ao longo do tempo.

---

# Cardinalidade

## Atual

```text
Unidade
 1:N
Sala

Sala
 1:N
Turma
```

Avaliação:

✅ Consistente.

---

# Regras de Negócio

## RN-001

Toda sala deve pertencer a uma unidade.

---

## RN-002

Toda sala deve possuir nome e numero.

---

## RN-003

Toda sala deve possuir capacidade definida.

---

## RN-004

Uma sala pode atender diversas turmas em períodos distintos.

---

## RN-005

A capacidade da sala determina a lotação máxima da turma.

Esta é uma regra derivada da modelagem.

---

## RN-006

A sala pode ser desativada sem remoção física do cadastro.

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
* Boa separação da estrutura física;
* Capacidade armazenada corretamente;
* Base para indicadores operacionais;
* Soft delete implementado;
* Campos de auditoria presentes.

---

# Pontos de Atenção

## Tipo da Sala

Atualmente:

```text
tipo_sala
```

Atende às necessidades atuais.

Entretanto, novos tipos poderão surgir futuramente.

---

## Ocupação

A tabela armazena apenas a capacidade máxima.

Não existe controle da ocupação em tempo real.

---

# Melhorias Futuras

## V2

Avaliar:

```text
patrimonio

bloco

andar
```

---

## V3

Avaliar:

```text
recursos_disponiveis

projetor

ar_condicionado

computadores

acessibilidade
```

---

## V4

Criar indicadores automáticos:

```text
Taxa de ocupação

Utilização anual

Disponibilidade

Horas utilizadas
```

---

## V5

Integração com:

```text
Reserva de salas

Calendário Institucional

Planejamento Acadêmico

Conflito de horários
```

---

# Observações de Arquitetura

## OA-001 — Lotação da Turma

### Situação Atual

A capacidade máxima de alunos está armazenada na entidade `tb_sala`.

As turmas utilizam essa informação de forma indireta.

---

### Observação

Durante a auditoria foi discutida a possibilidade de armazenar a lotação diretamente na turma.

Após análise, concluiu-se que essa informação pertence à sala, pois representa uma característica física do ambiente.

A quantidade de alunos matriculados deve ser obtida através da tabela `tb_matricula`, permitindo calcular automaticamente indicadores de ocupação.

---

### Impacto

Baixo.

A modelagem atual já atende corretamente à regra de negócio.

---

### Classificação

Nível 1 — Registro

---

### Versão Prevista

Sem alteração prevista.

---

### Justificativa

A estrutura atual está corretamente normalizada.

A ocupação da turma deve ser calculada por meio dos relacionamentos existentes, evitando redundância de dados.

---

### Decisão da Auditoria

A modelagem permanece inalterada.

A lotação continuará sendo derivada da capacidade da sala e da quantidade de matrículas da turma.

---

# Conclusão

A tabela `tb_sala` apresenta modelagem consistente e bem normalizada.

Sua estrutura representa corretamente os ambientes físicos da instituição e fornece suporte às regras de negócio relacionadas à infraestrutura acadêmica.

As melhorias identificadas são evolutivas e não justificam alterações estruturais para a V1.1.

Status Final:

```text
APROVADA PARA V1.1
```