# 07 - Auditoria da Tabela tb_unidade

## Identificação

**Tabela:** tb_unidade

**Módulo:** Estrutura Organizacional

**Categoria:** Entidade Operacional

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_unidade` representa as unidades operacionais vinculadas à instituição.

Seu objetivo é permitir a organização física e administrativa da instituição, possibilitando a distribuição de cursos, salas, turmas e recursos entre diferentes locais de atendimento.

A unidade é o elo entre a estrutura institucional e a operação acadêmica.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

* Representar uma unidade física da instituição;
* Armazenar dados básicos de contato;
* Permitir segmentação organizacional;
* Servir como base para salas;
* Servir como base para turmas;
* Possibilitar expansão multiunidade;
* Permitir planejamento acadêmico descentralizado.

---

# Estrutura Atual

| Campo | Tipo | Observação |
|---------|---------|---------|
| id_unidade | int | Chave Primária |
| instituicao_id | int | FK Instituição |
| nome | varchar(150) | Nome da unidade |
| endereco | varchar(200) | Endereço |
| telefone | varchar(20) | Contato |
| email | varchar(150) | E-mail |
| ativo | tinyint(1) | Controle lógico |
| criado_em | datetime | Auditoria |
| atualizado_em | datetime | Auditoria |
| deletado_em | datetime | Soft Delete |

---

# Chave Primária

```text
PK: id_unidade
```

Avaliação:

✅ Adequada.

---

# Relacionamentos

## Instituição

```text
Instituição
 1:N
Unidade
```

Implementado por:

```text
tb_unidade.instituicao_id
```

Avaliação:

✅ Correto.

Uma instituição pode possuir diversas unidades.

---

## Turma

Relacionamento esperado:

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

Uma unidade pode ofertar diversas turmas.

---

## Sala

Relacionamento esperado:

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

Uma unidade pode possuir diversas salas.

---

# Cardinalidade

## Atual

```text
Instituição
 1:N
Unidade

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

Toda unidade deve pertencer a uma instituição.

---

## RN-002

Uma instituição pode possuir várias unidades.

---

## RN-003

Toda turma deve estar vinculada a uma unidade.

---

## RN-004

Toda sala deve estar vinculada a uma unidade.

---

## RN-005

A unidade pode ser desativada sem exclusão física dos registros.

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
* Relacionamento bem definido com instituição;
* Permite expansão organizacional;
* Suporte nativo para múltiplas unidades;
* Soft delete implementado;
* Campos de auditoria presentes.

---

# Pontos de Atenção

## Nome da Unidade

Atualmente:

```text
nom
e
```

Não possui restrição de unicidade.

Dependendo do cenário futuro, pode permitir nomes repetidos.

---

## Endereço

Atualmente:

```text
endereco
```

Armazenado em campo único.

Atende ao cenário atual.

---

# Melhorias Futuras

## V2

Avaliar:

```text
UNIQUE(instituicao_id, nome)
```

Evitar duplicidade de nomes dentro da mesma instituição.

---

## V3

Avaliar separação de endereço:

```text
logradouro

numero

bairro

cidade

estado

cep
```

---

## V4

Avaliar:

```text
responsavel_unidade

telefone_secundario

horario_funcionamento
```

---

## V5

Integração com:

```text
Calendário Institucional

Planejamento Acadêmico

Captação de Alunos

Indicadores Operacionais
```

Permitir gestão descentralizada das unidades sob coordenação institucional central.

---

# Observações de Arquitetura

## OA-001 — Relacionamento Unidade × Turma

### Situação Atual

A entidade `tb_turma` possui relacionamento direto com:

```text
tb_turma.unidade_id
tb_turma.sala_id
```

Ao mesmo tempo, a entidade `tb_sala` também pertence a uma unidade.

```text
Instituição
    ↓
Unidade
    ↓
Sala
```

---

### Observação

Foi identificada uma possível redundância entre os relacionamentos.

Conceitualmente, a unidade da turma poderia ser obtida por derivação através da sala.

Modelo possível:

```text
Instituição
    ↓
Unidade
    ↓
Sala
    ↓
Turma
```

---

### Impacto

Alto.

A alteração exigiria revisão de diversas entidades, consultas SQL, controllers, models, views e regras de negócio.

---

### Classificação

Nível 3 — Refatoração Estrutural

---

### Versão Prevista

Indefinida.

(Reavaliar a partir da V3.)

---

### Justificativa

A modelagem atual funciona corretamente e atende aos requisitos da V1.1.

A melhoria identificada representa uma simplificação da modelagem e redução de redundâncias, porém seu custo de implementação é elevado para a fase atual do projeto.

---

### Decisão da Auditoria

Nenhuma alteração será realizada na V1.1.

A observação fica registrada para futura avaliação durante uma refatoração estrutural.

---

# Conclusão

A tabela `tb_unidade` apresenta modelagem consistente, simples e adequada aos objetivos atuais do SGCI.

Sua estrutura permite expansão organizacional futura e atende plenamente aos requisitos do MVP Beta 0 e da V1.1.

As melhorias identificadas são evolutivas e não justificam alterações estruturais imediatas.

Status Final:

```text
APROVADA PARA V1.1
```