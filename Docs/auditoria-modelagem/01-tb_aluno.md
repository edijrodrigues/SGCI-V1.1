# 01 - Auditoria da Tabela tb_aluno

## Identificação

**Tabela:** tb_aluno

**Módulo:** Acadêmico

**Categoria:** Entidade Principal

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_aluno` é responsável por armazenar os dados cadastrais dos alunos da instituição.

Representa a entidade central do estudante dentro do sistema e serve como ponto de partida para os processos acadêmicos.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

* Armazenar dados pessoais do aluno;
* Armazenar informações de contato;
* Permitir identificação única do aluno;
* Servir como origem para matrículas;
* Servir como origem para histórico acadêmico;
* Servir como origem para certificados emitidos.

---

# Estrutura Atual

| Campo           | Tipo         | Observação              |
| --------------- | ------------ | ----------------------- |
| id_aluno        | int          | Chave Primária          |
| nome_aluno      | varchar(150) | Nome completo           |
| data_nascimento | date         | Data de nascimento      |
| cpf_aluno       | varchar(14)  | CPF único               |
| rg_aluno        | varchar(20)  | Documento de identidade |
| email_aluno     | varchar(150) | E-mail principal        |
| telefone_aluno  | varchar(20)  | Contato                 |
| endereco_aluno  | varchar(255) | Endereço                |
| cidade_aluno    | varchar(100) | Cidade                  |
| estado_aluno    | char(2)      | UF                      |
| cep_aluno       | varchar(15)  | CEP                     |
| ativo           | tinyint(1)   | Controle lógico         |
| criado_em       | datetime     | Auditoria               |
| atualizado_em   | datetime     | Auditoria               |
| deletado_em     | datetime     | Soft Delete             |

---

# Chave Primária

```text
PK: id_aluno
```

Características:

* Inteiro auto incremento;
* Identificador único do aluno;
* Não possui significado de negócio.

Avaliação:

✅ Adequado.

---

# Relacionamentos

## Matrícula

```text
Aluno
  1:N
Matrícula
```

Implementado por:

```text
tb_matricula.aluno_id
```

Justificativa:

Um aluno pode realizar várias matrículas ao longo da vida acadêmica.

Exemplos:

* Curso de Informática
* Curso de Excel
* Curso de Administração

---

## Certificados

Relacionamento indireto:

```text
Aluno
 ↓
Matrícula
 ↓
Histórico
 ↓
Certificado
```

Avaliação:

✅ Adequado.

---

# Cardinalidade

## Atual

```text
tb_aluno
 1:N
tb_matricula
```

Avaliação:

✅ Correta.

---

# Regras de Negócio

## RN-001

O aluno deve possuir nome.

---

## RN-002

O aluno deve possuir data de nascimento.

---

## RN-003

CPF deve ser único quando informado.

Implementado por:

```sql
UNIQUE(cpf_aluno)
```

---

## RN-004

Um aluno pode possuir várias matrículas.

---

## RN-005

Um aluno não pode possuir duas matrículas na mesma turma.

Regra implementada em:

```sql
tb_matricula

UNIQUE(aluno_id, turma_id)
```

---

# Normalização

## Primeira Forma Normal (1FN)

Atendida.

Todos os campos possuem valores atômicos.

---

## Segunda Forma Normal (2FN)

Atendida.

Todos os atributos dependem da chave primária.

---

## Terceira Forma Normal (3FN)

Atendida.

Não foram identificadas dependências transitivas relevantes.

---

# Pontos Fortes

* Estrutura simples;
* Fácil manutenção;
* CPF único;
* Soft delete implementado;
* Campos de auditoria presentes;
* Relacionamento bem definido com matrícula.

---

# Pontos de Atenção

## Endereço

Atualmente:

```text
endereco_aluno
cidade_aluno
estado_aluno
cep_aluno
```

Funcionam adequadamente para o porte atual do projeto.

Entretanto, podem ser normalizados futuramente.

---

## RG

Atualmente armazenado como texto livre.

Pode exigir validação futura.

---

# Melhorias Futuras

## V2

Adicionar:

```text
nome_social
```

Quando necessário.

---

## V3

Avaliar normalização de endereço.

Possível criação de:

```text
tb_endereco
```

Caso haja necessidade de múltiplos endereços.

---

## V4+

Avaliar integração com:

```text
Responsáveis

Documentação Digital

Portal do Aluno
```

---

# Conclusão

A tabela `tb_aluno` apresenta modelagem consistente, simples e adequada aos objetivos atuais do projeto.

Atende corretamente aos requisitos do MVP Beta 0 e encontra-se preparada para evolução gradual nas próximas versões do SGCI.

Não foram identificados problemas estruturais que justifiquem alterações imediatas.

```text
Status Final:
```

```text
APROVADA PARA V1.1
```