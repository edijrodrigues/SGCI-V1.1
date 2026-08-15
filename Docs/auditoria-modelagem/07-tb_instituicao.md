# 06 - Auditoria da Tabela tb_instituicao

## Identificação

**Tabela:** tb_instituicao

**Módulo:** Estrutura Organizacional

**Categoria:** Entidade Institucional

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_instituicao` representa a entidade mantenedora do sistema.

Sua finalidade é armazenar os dados institucionais da organização responsável pela oferta dos cursos e pela gestão das unidades acadêmicas.

Ela funciona como o nível mais alto da estrutura organizacional do SGCI.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

* Armazenar dados institucionais;
* Armazenar dados fiscais da organização;
* Armazenar dados de contato;
* Servir como entidade raiz da estrutura organizacional;
* Servir como base para as unidades vinculadas;
* Fornecer informações para documentos oficiais;
* Fornecer informações para certificados e relatórios.

---

# Estrutura Atual

| Campo | Tipo | Observação |
|---------|---------|---------|
| id_instituicao | int | Chave Primária |
| nome | varchar(150) | Nome fantasia |
| razao_social | varchar(200) | Razão social |
| cnpj | varchar(18) | Cadastro Nacional da Pessoa Jurídica |
| telefone | varchar(20) | Contato |
| email | varchar(150) | E-mail institucional |
| site | varchar(150) | Website |
| endereco | varchar(200) | Endereço |
| ativo | tinyint(1) | Controle lógico |
| criado_em | datetime | Auditoria |
| atualizado_em | datetime | Auditoria |
| deletado_em | datetime | Soft Delete |

---

# Chave Primária

```text
PK: id_instituicao
```

Avaliação:

✅ Adequada.

---

# Relacionamentos

## Unidade

Relacionamento esperado:

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

# Cardinalidade

## Atual

```text
Instituição
 1:N
Unidade
```

Avaliação:

✅ Consistente.

---

# Regras de Negócio

## RN-001

Toda instituição deve possuir nome.

---

## RN-002

Uma instituição pode possuir várias unidades.

---

## RN-003

Os dados institucionais devem estar disponíveis para emissão de documentos oficiais.

---

## RN-004

A instituição pode ser desativada sem remoção física dos registros.

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
* Fácil manutenção;
* Soft delete implementado;
* Campos de auditoria presentes;
* Preparada para expansão organizacional.

---

# Pontos de Atenção

## CNPJ

Atualmente:

```text
cnpj
```

Não possui restrição UNIQUE.

Isso permite o cadastro duplicado da mesma instituição.

---

## Endereço

Atualmente:

```text
endereco
```

Armazenado em um único campo.

Atende ao cenário atual, porém limita consultas futuras.

---

# Melhorias Futuras

## V2

Adicionar:

```text
UNIQUE(cnpj)
```

Caso a regra de negócio exija unicidade.

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

Avaliar criação de:

```text
tb_contato_institucional
```

para múltiplos contatos.

---

## V5

Preparação para cenário multi-institucional:

```text
Instituição
 ↓
Unidades
 ↓
Cursos
 ↓
Turmas
```

Possibilitando administração centralizada de grupos educacionais.

---

# Conclusão

A tabela `tb_instituicao` apresenta modelagem simples, consistente e adequada aos objetivos atuais do projeto.

Sua estrutura atende corretamente às necessidades do MVP Beta 0 e da V1.1, estando preparada para futuras expansões organizacionais.

As melhorias identificadas são evolutivas e não justificam alterações estruturais imediatas.

Status Final:

```text
APROVADA PARA V1.1
```