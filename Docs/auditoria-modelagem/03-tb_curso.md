# 03 - Auditoria da Tabela tb_curso

## Identificação

**Tabela:** tb_curso

**Módulo:** Acadêmico / Pedagógico

**Categoria:** Entidade Estruturante

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_curso` representa os cursos ofertados pela instituição.

Ela funciona como a base organizacional do módulo acadêmico e pedagógico, sendo responsável por definir os cursos que poderão ser ministrados, planejados, executados e certificados.

--- 

# Responsabilidades

A tabela possui as seguintes responsabilidades:

* Cadastrar cursos ofertados;
* Definir carga horária do curso;
* Definir nível do curso;
* Servir como base para criação de turmas;
* Servir como base para planos de curso;
* Servir como referência para histórico escolar;
* Servir como referência para certificados.

---

# Estrutura Atual

| Campo              |Tipo         | Observação                 |
| ------------------ | ----------- | -------------------------- |
| id_curso	         | int	       | Chave Primária             |
| codigo_curso	     | varchar(20) | Código único               |
| nome_curso	     | varchar(150)| Nome do curso              |
| descricao	         | text	       | Descrição                  |
| carga_horaria	     | int	       | CH total                   |
| duracao_meses	     | decimal(4,1)| Duração estimada           |
| nivel	             | enum	       | Nível do curso             |
| ativo	             | tinyint(1)  | Controle lógico            |
| criado_em	         | datetime	   | Auditoria                  |
| atualizado_em	     | datetime	   | Auditoria                  |
| deletado_em	     | datetime	   | Soft Delete                |

---

# Chave Primária

```text
PK: id_curso
```

* Avaliação:

✅ Adequada.

# Chave de Negócio

```text
codigo_curso
```

Implementado por:

```sql
UNIQUE(codigo_curso)
```

Avaliação:

✅ Excelente prática.

Permite identificar cursos sem depender da PK.

# Relacionamentos

## Curso → Turma

```text
Curso
 1:N
Turma
```

Implementado por:

```text
tb_turma.curso_id
```

Justificativa:

Um curso pode possuir diversas turmas.

---

Exemplo:

```text
Curso:
Informática

Turmas:

INFO-2025A
INFO-2025B
INFO-2025C
```

## Curso → Plano de Curso

```text
Curso
 1:N
Plano de Curso
```

Implementado por:

```text
tb_plano_curso.curso_id
```

Avaliação:

✅ Correto.

Permite versionamento dos planos.

## Curso → Histórico

```text
Curso
 1:N
Histórico
```

Implementado por:

```text
tb_historico_aluno.curso_id
```

## Curso → Certificado

```text
Curso
 1:N
Certificado
```

Implementado por:

```text
tb_certificado.curso_id
```

# Cardinalidade

## Atual

```text
Curso
 1:N
Turma

Curso
 1:N
Plano de Curso

Curso
 1:N
Histórico

Curso
 1:N
Certificado
```

Avaliação:

✅ Consistente.

---

# Regras de Negócio

## RN-001

Todo curso deve possuir código único.

Implementado por:

```sql
UNIQUE(codigo_curso)
```

---

## RN-002

Todo curso deve possuir nome.

---

## RN-003

Todo curso deve possuir carga horária.

---

## RN-004

Um curso pode possuir várias turmas.

---

## RN-005

Um curso deve possuir um Plano de Curso.

(Regra documental do projeto)

---

## RN-006

Um curso deve possuir Plano de Aula derivado de seu Plano de Curso.

(Regra documental do projeto)

---

## RN-007

Cursos podem possuir múltiplas versões de plano ao longo do tempo.

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

* Código único;
* Estrutura simples;
* Permite evolução pedagógica;
* Suporta versionamento do plano de curso;
* Boa integração com histórico e certificados;
* Soft delete implementado.

---

# Pontos de Atenção
## Nível

Atualmente:
```text
enum(
'basico',
'intermediario',
'avancado',
'tecnico'
)
```

Atende perfeitamente ao cenário atual.

Porém pode exigir expansão futura.

Exemplo:

```text
Livre
Profissionalizante
Extensão
Graduação
Pós-graduação

Duração
```
Atualmente:

```text
duracao_meses
```

É apenas informativa.  
Não participa de cálculos automáticos.

---

# Melhorias Futuras

## V2

Avaliar:

```text
categoria_curso
```

Exemplo:

```text
Informática

Administração

Eletrônica

Idiomas
```
---

## V3

Avaliar:

```text
tb_categoria_curso
```

---

## V4

Avaliar:

```text
Pré-requisitos

Competências

Certificações vinculadas
```

---

## V5

Possível integração com:

```text
Calendário Institucional

Planejamento Anual

Captação de Alunos

(Ideia já registrada durante as discussões da V1.1)
```
---

# Conclusão

A tabela `tb_curso` representa corretamente a entidade central da estrutura acadêmica e pedagógica do SGCI.

Sua modelagem está consistente, normalizada e alinhada com os objetivos do projeto.

As melhorias identificadas são evolutivas e não justificam alterações estruturais imediatas.

```text
Status Final:
```

```text
APROVADA PARA V1.1
```