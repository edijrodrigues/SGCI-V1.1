# 22 - Auditoria da Tabela `tb_certificado`

## Identificação

**Tabela:** `tb_certificado`

**Módulo:** Histórico

**Categoria:** Certificação Acadêmica

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_certificado` registra a emissão oficial dos certificados acadêmicos emitidos pela instituição.

Cada registro representa um certificado emitido com base em um Histórico Escolar consolidado, garantindo rastreabilidade, autenticidade e possibilidade de validação futura.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- registrar a emissão do certificado;
- associar o certificado ao Histórico Escolar;
- identificar o aluno certificado;
- identificar o curso concluído;
- identificar a turma;
- registrar o responsável pela emissão;
- armazenar o código único de autenticação;
- registrar validade, quando aplicável.

---

# Estrutura Atual

| Campo | Tipo | Obrigatório | Observação |
|--------|------|-------------|------------|
| id_certificado | INT | Sim | Chave primária |
| historico_id | INT | Sim | Histórico Escolar |
| aluno_id | INT | Sim | Aluno |
| curso_id | INT | Sim | Curso |
| turma_id | INT | Sim | Turma |
| instrutor_id | INT | Sim | Responsável |
| codigo_certificado | VARCHAR(50) | Sim | Código único |
| data_emissao | DATE | Sim | Emissão |
| validade | DATE | Não | Quando aplicável |
| observacao | TEXT | Não | Observações |
| ativo | BOOLEAN | Sim | Controle lógico |
| criado_em | DATETIME | Sim | Auditoria |
| atualizado_em | DATETIME | Sim | Auditoria |
| deletado_em | DATETIME | Não | Soft Delete |

---

# Chave Primária

```text
PK

id_certificado
```

---

# Chave de Negócio

```text
UNIQUE

codigo_certificado
```

Avaliação:

Excelente.

Permite validação pública do certificado.

---

# Relacionamentos

## Histórico Escolar

```text
Histórico Escolar

1:1

Certificado
```

> **Observação:** Conceitualmente espera-se um único Certificado para cada Histórico Escolar. Atualmente essa regra não é garantida por uma restrição `UNIQUE(historico_id)`.

---

## Aluno

```text
Aluno

1:N

Certificado
```

Um aluno poderá possuir diversos certificados ao longo da vida acadêmica.

---

## Curso

```text
Curso

1:N

Certificado
```

---

## Turma

```text
Turma

1:N

Certificado
```

---

## Instrutor

```text
Instrutor

1:N

Certificado
```

---

# Cardinalidade

```text
Aluno

↓

Histórico Escolar

↓

Certificado
```

O Certificado representa a formalização oficial do Histórico Escolar.

---

# Regras de Negócio

### RN-CER-001

Todo Certificado deve estar vinculado a um Histórico Escolar.

---

### RN-CER-002

Todo Certificado pertence a um Aluno.

---

### RN-CER-003

Todo Certificado pertence a um Curso.

---

### RN-CER-004

Todo Certificado deve possuir um código único.

---

### RN-CER-005

Todo Certificado deve possuir uma data de emissão.

---

### RN-CER-006

A validade do certificado é opcional e depende da política da instituição.

---

### RN-CER-007

O Certificado somente poderá ser emitido para um Histórico Escolar concluído e apto para certificação.

(Regra implementada na camada de negócio.)

---

# Normalização

A tabela atende à Terceira Forma Normal (3FN).

Sua responsabilidade limita-se ao registro da certificação, mantendo separados os dados operacionais e os dados consolidados do Histórico Escolar.

---

# Pontos Fortes

- excelente chave de negócio (`codigo_certificado`);
- boa rastreabilidade da certificação;
- preparada para validação externa;
- estrutura simples e objetiva;
- integra naturalmente o módulo Histórico.

---

# Pontos de Atenção

## Certificado único por Histórico

Conceitualmente, cada Histórico Escolar deveria originar apenas um Certificado.

Atualmente essa regra não é reforçada por uma restrição:

```sql
UNIQUE(historico_id)
```

Recomenda-se avaliar essa melhoria em versões futuras.

---

## Dados redundantes

A tabela armazena:

- aluno_id;
- curso_id;
- turma_id;

Essas informações já podem ser obtidas por meio do Histórico Escolar.

Na V1.1 essa redundância é aceitável por facilitar consultas e emissão de certificados.

Em versões futuras poderá ser reavaliada.

---

# Observações Arquiteturais

A modelagem posiciona o Certificado como uma entidade derivada do Histórico Escolar.

Essa decisão preserva a rastreabilidade acadêmica, garantindo que toda certificação possua um histórico consolidado como fundamento.

Além disso, o código único do certificado prepara o sistema para mecanismos de validação pública e autenticação documental.

> **Nota:** As decisões relacionadas à emissão e validação de certificados poderão ser detalhadas futuramente na seção **Decisões Arquiteturais (ADR)**.

---

# Melhorias Futuras

## V2

Avaliar:

```text
UNIQUE(historico_id)
```

---

## V3

Avaliar:

- assinatura eletrônica;
- QR Code;
- URL pública de validação.

---

## V4

Avaliar:

- emissão em lote;
- revogação de certificados;
- segunda via.

---

## V5

Avaliar integração com certificação digital e mecanismos oficiais de autenticação.

---

# Conclusão

A tabela `tb_certificado` apresenta uma modelagem consistente, simples e alinhada ao objetivo de formalizar a conclusão acadêmica do aluno.

Sua integração com o Histórico Escolar encerra de forma coerente o fluxo acadêmico do SGCI, permitindo rastreabilidade, autenticidade e futuras evoluções relacionadas à certificação digital.

**Status Final:**

```text
APROVADA PARA V1.1
```