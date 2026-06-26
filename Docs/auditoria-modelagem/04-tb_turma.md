# 04 - Auditoria da Tabela tb_turma

## Identificação

**Tabela:** tb_turma

**Módulo:** Acadêmico / Pedagógico

**Categoria:** Entidade Operacional

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_turma` representa a execução de um curso em um período específico.

Ela conecta os recursos acadêmicos e pedagógicos necessários para a realização das aulas, vinculando curso, instrutor, unidade, sala e turno.

A turma é o elemento central da operação acadêmica, pois é através dela que os alunos participam efetivamente dos cursos.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

* Vincular um curso à sua execução prática;
* Definir período de realização;
* Definir local de realização;
* Definir instrutor responsável;
* Definir turno de funcionamento;
* Servir de base para matrículas;
* Servir de base para frequência;
* Servir de base para avaliações;
* Servir de base para históricos escolares;
* Servir de base para certificados.

---

# Estrutura Atual

| Campo         | Tipo         | Observação                 |
|---------------|--------------|----------------------------|
| id_turma      | int          | Chave Primária             |
| curso_id      | int          | FK Curso                   |
| unidade_id    | int          | FK Unidade                 |
| sala_id       | int          | FK Sala                    |
| turno_id      | int          | FK Turno                   |
| instrutor_id  | int          | FK Instrutor               |
| nome_turma    | varchar(100) | Identificação da turma     |
| data_inicio   | date         | Início das aulas           |
| data_fim      | date         | Encerramento previsto      |
| observacao    | text         | Informações complementares |
| ativo         | tinyint(1)   | Controle lógico            |
| criado_em     | datetime     | Auditoria                  |
| atualizado_em | datetime     | Auditoria                  | 
| deletado_em   | datetime     | Soft Delete                |

---

# Chave Primária

```text
PK: id_turma
```

Avaliação:

✅ Adequada.

---

# Relacionamentos

## Curso

```text
Curso
 1:N
Turma
```

Implementado por:

```text
tb_turma.curso_id
```

Avaliação:

✅ Correto.

Um curso pode possuir diversas turmas ao longo do tempo.

---

## Unidade

```text
Unidade
 1:N
Turma
```

Implementado por:

```text
tb_turma.unidade_id
```

Avaliação:

✅ Correto.

Uma unidade pode ofertar várias turmas.

---

## Sala

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

Uma sala pode receber diversas turmas em períodos distintos.

---

## Turno

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

---

## Instrutor

```text
Instrutor
 1:N
Turma
```

Implementado por:

```text
tb_turma.instrutor_id
```

Avaliação:

✅ Correto.

---

## Matrícula

```text
Turma
 1:N
Matrícula
```

Implementado por:

```text
tb_matricula.turma_id
```

Avaliação:

✅ Correto.

---

# Cardinalidade

## Atual

```text
Curso
 1:N
Turma

Unidade
 1:N
Turma

Sala
 1:N
Turma

Turno
 1:N
Turma

Instrutor
 1:N
Turma

Turma
 1:N
Matrícula
```

Avaliação:

✅ Consistente.

---

# Regras de Negócio

## RN-001

Toda turma deve estar vinculada a um curso.

---

## RN-002

Toda turma deve possuir unidade responsável.

---

## RN-003

Toda turma deve possuir sala definida.

---

## RN-004

Toda turma deve possuir turno definido.

---

## RN-005

Toda turma deve possuir instrutor responsável.

---

## RN-006

Uma turma pode possuir várias matrículas.

---

## RN-007

Uma matrícula pertence a apenas uma turma.

---

## RN-008

A lotação da turma é determinada pela capacidade da sala.

Regra derivada de:

```text
tb_sala.capacidade
```

Observação:

Durante a auditoria foi discutida a possibilidade de armazenar matrículas diretamente na entidade turma.

A análise concluiu que a modelagem atual está correta, sendo a tabela `tb_matricula` a responsável pela relação entre aluno e turma.

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
* Excelente centralização acadêmica;
* Boa separação de responsabilidades;
* Relacionamentos claros;
* Permite rastrear toda a vida acadêmica da turma;
* Compatível com indicadores de ocupação e evasão.

---

# Pontos de Atenção

## Nome da Turma

Atualmente:

```text
nome_turma
```

Não existe regra de padronização.

Exemplos possíveis:

```text
INFO-2025A

INFO-2025B

ADMIN-2025A
```

Recomenda-se definir padrão institucional futuramente.

---

## Encerramento da Turma

Atualmente:

```text
data_fim
```

é apenas informativa.

Não existem regras automáticas para encerramento acadêmico.

---

# Melhorias Futuras

## V2

Avaliar:

```text
status_turma
```

Exemplo:

```text
planejada

em_andamento

encerrada

cancelada
```

---

## V3

Avaliar indicadores automáticos:

```text
Quantidade de matriculados

Vagas disponíveis

Percentual de ocupação

Percentual de evasão
```

---

## V4

Integração com:

```text
Calendário Institucional

Planejamento Acadêmico

Captação de Alunos
```

---

## V5

Possível geração automática de:

```text
Turmas

Cronogramas

Calendários

Planejamento anual
```

A partir dos parâmetros institucionais.

---

# Conclusão

A tabela `tb_turma` representa corretamente a entidade operacional central do SGCI.

Sua modelagem está consistente, normalizada e alinhada com as regras de negócio definidas para o projeto.

As melhorias identificadas são evolutivas e não justificam alterações estruturais imediatas.

Status Final:

```text
APROVADA PARA V1.1
```