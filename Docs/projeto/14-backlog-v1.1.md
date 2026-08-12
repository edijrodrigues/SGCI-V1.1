Arquitetura

□ Criar documentação das linguagens

□ Documentar servidor

□ Documentar MVC

□ Documentar estrutura de pastas

□ Documentar banco de dados

□ Documentar padrões utilizados

□ Documentar autenticação

□ Documentar controle de sessão

Planejamento Pedagógico

□ Avaliar criação da restrição
  UNIQUE(plano_curso_id, numero_item)
  para impedir duplicidade da numeração dos itens do Plano de Curso.

□ Avaliar criação da restrição
  UNIQUE(turma_id, data_prevista, plano_aula_id)
  para impedir agendamentos duplicados para a mesma turma, mesma data e mesmo plano de aula.

# Revisão da Modelagem (V2)

## HIST-001 — Garantir um único Histórico Escolar por Matrícula

**Situação Atual**

A tabela `tb_historico_aluno` permite, tecnicamente, que uma mesma matrícula possua mais de um registro de histórico, pois não existe uma restrição `UNIQUE` sobre o campo `matricula_id`.

**Justificativa**

Pela regra de negócio atual do SGCI, uma matrícula representa a participação de um aluno em uma única turma e, ao término desse processo, deve gerar um único Histórico Escolar consolidado.

A inclusão de uma restrição de unicidade reforçaria essa regra diretamente no banco de dados, reduzindo a possibilidade de inconsistências.

**Alteração Proposta**

Adicionar a seguinte restrição:

```sql
UNIQUE (matricula_id)
```

**Impacto**

- Reforça a integridade referencial.
- Garante um único Histórico Escolar por matrícula.
- Simplifica consultas e emissão de certificados.
- Alinha a modelagem à regra de negócio.

**Prioridade**

🟡 Média

**Versão Prevista**

V2

**Status**

Backlog

> **Observação**
>
> Esta melhoria foi identificada durante a auditoria da modelagem da V1.1.
> A alteração não será implementada nesta versão para preservar a compatibilidade com o banco de dados do MVP Beta 0.
> Sua adoção dependerá da confirmação de que o processo acadêmico do SGCI continuará prevendo apenas um Histórico Escolar por Matrícula.

## HIST-002 — Garantir um único Certificado por Histórico Escolar

**Situação Atual**

A tabela `tb_certificado` permite, tecnicamente, múltiplos certificados para o mesmo Histórico Escolar, pois não existe uma restrição `UNIQUE(historico_id)`.

**Justificativa**

Pela regra de negócio atual do SGCI, um Histórico Escolar consolidado deve originar apenas um Certificado oficial.

**Alteração Proposta**

```sql
UNIQUE (historico_id)