# 02 - Auditoria da Tabela tb_instrutor

## Identificação

**Tabela:** tb_instrutor

**Módulo:** Acadêmico

**Categoria:** Entidade Principal

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_instrutor` é responsável pelo cadastro dos profissionais responsáveis pela condução das atividades pedagógicas da instituição.

Representa o docente, instrutor ou facilitador vinculado aos cursos ofertados.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

* Armazenar dados cadastrais do instrutor;
* Armazenar dados de contato;
* Registrar especialidade profissional;
* Servir como responsável por turmas;
* Servir como responsável por planos de aula;
* Servir como responsável por avaliações;
* Servir como responsável pelos registros acadêmicos.

---

# Estrutura Atual

| Campo              | Tipo         | Observação                 |
| ------------------ | ------------ | -------------------------- |
| id_instrutor       | int          | Chave Primária             |
| nome_instrutor     | varchar(150) | Nome completo              |
| cpf_instrutor      | varchar(14)  | CPF único                  |
| email_instrutor    | varchar(150) | E-mail                     |
| telefone_instrutor | varchar(20)  | Contato                    |
| especialidade      | varchar(150) | Área de atuação            |
| endereco_instrutor | varchar(255) | Endereço                   |
| cidade_instrutor   | varchar(100) | Cidade                     |
| estado_instrutor   | char(2)      | UF                         |
| cep_instrutor      | varchar(15)  | CEP                        |
| data_admissao      | date         | Data de ingresso           |
| observacao         | text         | Informações complementares |
| ativo              | tinyint(1)   | Controle lógico            |
| criado_em          | datetime     | Auditoria                  |
| atualizado_em      | datetime     | Auditoria                  |
| deletado_em        | datetime     | Soft Delete                |

---

# Chave Primária

```text
PK: id_instrutor
```

Características:

* Inteiro auto incremento;
* Identificador interno;
* Sem significado de negócio.

Avaliação:

✅ Adequado.

---

# Relacionamentos

## Turma

```text
Instrutor
   1:N
Turma
```

Implementado por:

```text
tb_turma.instrutor_id
```

Justificativa:

Um instrutor pode ministrar diversas turmas.

---

## Plano de Aula

```text
Instrutor
   1:N
Plano de Aula
```

Implementado por:

```text
tb_plano_aula.instrutor_id
```

Avaliação:

✅ Correto.

---

## Diário de Aula

```text
Instrutor
   1:N
Diário de Aula
```

Implementado por:

```text
tb_diario_aula.instrutor_id
```

Avaliação:

✅ Correto.

---

## Frequência

```text
Instrutor
   1:N
Frequência
```

Implementado por:

```text
tb_frequencia_aluno.instrutor_id
```

Avaliação:

✅ Correto.

---

## Avaliação

```text
Instrutor
   1:N
Avaliação
```

Implementado por:

```text
tb_avaliacao_aluno.instrutor_id
```

Avaliação:

✅ Correto.

---

## Histórico Escolar

```text
Instrutor
   1:N
Histórico
```

Implementado por:

```text
tb_historico_aluno.instrutor_id
```

Avaliação:

✅ Correto.

---

## Certificado

```text
Instrutor
   1:N
Certificado
```

Implementado por:

```text
tb_certificado.instrutor_id
```

Avaliação:

✅ Correto.

---

# Cardinalidade

## Atual

```text
Instrutor
 1:N
Turma

Instrutor
 1:N
Plano de Aula

Instrutor
 1:N
Diário

Instrutor
 1:N
Avaliação

Instrutor
 1:N
Histórico

Instrutor
 1:N
Certificado
```

Avaliação:

✅ Consistente.

---

# Regras de Negócio

## RN-001

O instrutor deve possuir nome.

---

## RN-002

O instrutor deve possuir e-mail.

---

## RN-003

CPF deve ser único quando informado.

Implementado por:

```sql
UNIQUE(cpf_instrutor)
```

---

## RN-004

Um instrutor pode atuar em várias turmas.

---

## RN-005

Um instrutor pode participar de vários cursos ao longo do tempo.

---

## RN-006

Todos os registros pedagógicos devem possuir rastreabilidade do instrutor responsável.

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
* Boa rastreabilidade pedagógica;
* Soft delete implementado;
* CPF único;
* Campos de auditoria presentes;
* Centralização da responsabilidade acadêmica.

---

# Pontos de Atenção

## Especialidade

Atualmente:

```text
especialidade
```

armazenada em texto livre.

Exemplos:

```text
Informática

Redes

Programação

Eletrônica
```

No cenário atual atende plenamente.

---

# Melhorias Futuras

## V2

Avaliar:

```text
tb_especialidade
```

caso seja necessário vincular múltiplas especialidades por instrutor.

---

## V3

Avaliar:

```text
Registro profissional

Currículo

Titulação
```

---

## V4+

Avaliar:

```text
Portal do Instrutor

Controle de disponibilidade

Agenda de aulas
```

---

# Conclusão

A tabela `tb_instrutor` apresenta modelagem consistente e adequada aos objetivos atuais do projeto.

Sua estrutura atende corretamente às necessidades pedagógicas do SGCI e permite rastrear todas as atividades acadêmicas executadas pelos instrutores.

Não foram identificadas necessidades de alteração estrutural para a V1.1.

```text
Status Final:
```

```text
APROVADA PARA V1.1
```