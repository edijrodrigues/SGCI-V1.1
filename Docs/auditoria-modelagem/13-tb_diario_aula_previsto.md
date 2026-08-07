# Auditoria da Tabela: tb_diario_aula_previsto

## Identificação

**Tabela:** `tb_diario_aula_previsto`

**Módulo:** Planejamento Pedagógico

**Responsabilidade:** Planejamento da execução das aulas

---

# Objetivo

Armazenar o cronograma previsto das aulas que serão ministradas para uma determinada turma, vinculando um Plano de Aula a uma data específica.

A tabela representa o planejamento operacional da execução pedagógica.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- associar um Plano de Aula a uma Turma;
- definir a data prevista da aula;
- informar o período do dia;
- indicar se a data é letiva;
- controlar o status do planejamento;
- registrar observações do agendamento.

Não é responsabilidade desta tabela registrar o que realmente ocorreu durante a aula.

---

# Estrutura

## Chave Primária

- id_previsto

## Chaves Estrangeiras

### Turma

```text
turma_id
→ tb_turma
```

ON DELETE CASCADE

---

### Plano de Aula

```text
plano_aula_id
→ tb_plano_aula
```

ON DELETE RESTRICT

---

# Relacionamentos

## tb_turma

Uma Turma possui vários registros previstos.

Cardinalidade

```text
Turma (1)
      │
      └──────< Diário Previsto (N)
```

---

## tb_plano_aula

Um Plano de Aula pode ser previsto diversas vezes.

Cardinalidade

```text
Plano de Aula (1)
          │
          └──────< Diário Previsto (N)
```

Isso permite reutilizar o mesmo Plano de Aula em diferentes Turmas ou diferentes ofertas.

---

# Campos Importantes

## data_prevista

Define a data planejada para realização da aula.

---

## periodo_do_dia

Controla em qual período a aula ocorrerá.

Valores:

- dia_inteiro
- manha
- tarde
- noite

---

## eh_letivo

Indica se a data faz parte do calendário letivo.

---

## status

Controla a situação do planejamento.

Valores atuais:

- prevista
- cancelada

---

# Índices

## idx_previsto_turma_data

```text
(turma_id, data_prevista)
```

Excelente escolha.

Facilita consultas como:

- cronograma da turma;
- calendário acadêmico;
- agenda diária;
- planejamento semanal.

---

# Normalização

A tabela encontra-se adequadamente normalizada.

Não há redundância significativa.

Os dados pedagógicos permanecem na tabela `tb_plano_aula`, enquanto esta tabela registra apenas o planejamento temporal.

---

# Pontos Fortes

- clara separação entre planejamento e execução;
- reutilização dos Planos de Aula;
- excelente índice para consultas por calendário;
- estrutura simples e objetiva;
- bom uso das chaves estrangeiras.

---

# Pontos de Atenção

## ON DELETE CASCADE na Turma

Ao excluir uma Turma, todo o planejamento previsto será removido.

Essa decisão parece coerente, pois um cronograma previsto perde sentido quando a oferta deixa de existir.

---

## ON DELETE RESTRICT no Plano de Aula

Também é uma excelente escolha.

Impede que um Plano de Aula seja removido enquanto ainda existir planejamento associado.

Preserva a integridade pedagógica.

---

# Observações Arquiteturais

Esta tabela representa a transição entre o planejamento pedagógico e a execução das atividades acadêmicas.

Enquanto `tb_plano_aula` descreve **como** uma aula deve ser ministrada, `tb_diario_aula_previsto` define **quando** e **para qual turma** essa aula está planejada.

Essa separação reforça a arquitetura baseada na distinção entre planejamento pedagógico e programação da execução.

---

# Melhorias Futuras

## UNIQUE (turma_id, data_prevista, plano_aula_id)

Evitaria que o mesmo Plano de Aula fosse programado duas vezes para a mesma Turma na mesma data.

Classificação:

Evolução futura.

---

## Avaliar novos status

Caso o sistema evolua, poderão ser considerados novos estados, por exemplo:

- realizada
- adiada
- remarcada

Atualmente esses estados provavelmente pertencem ao Diário de Aula e não ao planejamento.

---

# Regras de Negócio

## RN-PED-DP-001

Todo Diário Previsto pertence a uma Turma.

---

## RN-PED-DP-002

Todo Diário Previsto referencia um Plano de Aula.

---

## RN-PED-DP-003

Todo Diário Previsto deve possuir uma data planejada.

---

## RN-PED-DP-004

O mesmo Plano de Aula pode ser planejado para diferentes Turmas.

---

## RN-PED-DP-005

Um Plano de Aula pode ser planejado diversas vezes.

---

## RN-PED-DP-006

Uma Turma possui diversos registros de Diário Previsto.

---

## RN-PED-DP-007

Um Diário Previsto pode ser cancelado sem remover o planejamento.

---

# Conclusão

A modelagem apresenta boa separação de responsabilidades e mantém a coerência arquitetural estabelecida no módulo pedagógico.

A tabela atua como elo entre o planejamento pedagógico e a futura execução das aulas, preservando a reutilização dos Planos de Aula e permitindo o gerenciamento do cronograma acadêmico de forma consistente.