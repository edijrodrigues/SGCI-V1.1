# 23 - Auditoria da Tabela `tb_pagamento`

## Identificação

**Tabela:** `tb_pagamento`

**Módulo:** Financeiro

**Categoria:** Controle Financeiro

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_pagamento` registra as obrigações financeiras relacionadas às matrículas realizadas na instituição.

Cada registro representa um compromisso financeiro vinculado a uma matrícula, permitindo controlar vencimentos, pagamentos, formas de pagamento e situação financeira do aluno.

A tabela constitui a base do módulo financeiro do SGCI.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- registrar cobranças da matrícula;
- controlar vencimentos;
- registrar pagamentos realizados;
- controlar situação financeira;
- registrar forma de pagamento;
- registrar observações financeiras.

---

# Estrutura Atual

| Campo | Tipo | Obrigatório | Observação |
|--------|------|-------------|------------|
| id_pagamento | INT | Sim | Chave primária |
| matricula_id | INT | Sim | Matrícula |
| tipo_pagamento | ENUM | Não | Tipo da cobrança |
| valor | DECIMAL(10,2) | Sim | Valor financeiro |
| data_vencimento | DATE | Sim | Vencimento |
| data_pagamento | DATE | Não | Pagamento |
| status_pagamento | ENUM | Não | Situação |
| forma_pagamento | ENUM | Não | Meio de pagamento |
| descricao | TEXT | Não | Observações |
| criado_em | DATETIME | Sim | Auditoria |
| atualizado_em | DATETIME | Sim | Auditoria |

---

# Chave Primária

```text
PK

id_pagamento
```

---

# Relacionamentos

## Matrícula

```text
Matrícula

1:N

Pagamento
```

Uma matrícula pode possuir diversos registros financeiros.

---

# Cardinalidade

```text
Aluno

↓

Matrícula

↓

Pagamento
```

A matrícula representa a origem da obrigação financeira.

---

# Regras de Negócio

### RN-FIN-001

Todo Pagamento pertence a uma Matrícula.

---

### RN-FIN-002

Todo Pagamento deve possuir um valor.

---

### RN-FIN-003

Todo Pagamento deve possuir uma data de vencimento.

---

### RN-FIN-004

Um Pagamento poderá possuir data de pagamento.

---

### RN-FIN-005

O status financeiro poderá assumir:

- pendente;
- pago;
- atrasado;
- cancelado.

---

### RN-FIN-006

A forma de pagamento será registrada quando houver efetivação da cobrança.

---

# Normalização

A tabela atende à Terceira Forma Normal (3FN).

Sua responsabilidade está limitada ao controle financeiro da matrícula, mantendo independência dos demais módulos do sistema.

---

# Pontos Fortes

- excelente desacoplamento do módulo financeiro;
- relacionamento simples;
- boa rastreabilidade da cobrança;
- preparada para múltiplos pagamentos por matrícula;
- estrutura objetiva.

---

# Pontos de Atenção

Atualmente o sistema registra apenas o pagamento.

Não existe uma entidade específica para:

- títulos financeiros;
- negociação;
- descontos;
- multas;
- juros.

Essa simplificação é adequada para os objetivos da V1.1.

---

# Observações Arquiteturais

O módulo financeiro foi modelado de forma independente do fluxo pedagógico.

Sua única dependência funcional é a Matrícula, que representa o vínculo contratual entre aluno e instituição.

Essa decisão reduz o acoplamento entre os módulos acadêmico e financeiro, permitindo evolução independente de ambos.

> **Nota:** Futuras decisões relacionadas à expansão do módulo financeiro poderão ser documentadas na seção **Decisões Arquiteturais (ADR)**.

---

# Melhorias Futuras

## V2

Avaliar inclusão de:

- desconto;
- multa;
- juros;
- valor pago.

---

## V3

Avaliar parcelamentos vinculados a um contrato financeiro.

---

## V4

Avaliar geração automática das mensalidades a partir da matrícula.

---

## V5

Avaliar integração com:

- PIX dinâmico;
- boleto registrado;
- gateways de pagamento;
- conciliação bancária.

---

# Conclusão

A tabela `tb_pagamento` apresenta uma modelagem consistente, simples e alinhada aos objetivos da versão V1.1.

Sua dependência exclusiva da Matrícula demonstra uma boa separação entre o domínio financeiro e o domínio acadêmico, permitindo que ambos evoluam de forma independente.

**Status Final:**

```text
APROVADA PARA V1.1
```