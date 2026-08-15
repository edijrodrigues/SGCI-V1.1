# 21 - Auditoria da Tabela `tb_historico_aluno`

## Identificação

**Tabela:** `tb_historico_aluno`

**Módulo:** Histórico

**Categoria:** Histórico Escolar

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_historico_aluno` consolida o resultado acadêmico obtido pelo aluno ao final de sua participação em uma Turma.

Ela representa o registro oficial da vida acadêmica do aluno dentro do curso, reunindo os principais indicadores de desempenho utilizados pela instituição para emissão do Histórico Escolar e posterior certificação.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- consolidar os resultados acadêmicos da matrícula;
- registrar média final;
- registrar frequência final;
- registrar situação final do aluno;
- registrar carga horária cumprida;
- registrar data de conclusão;
- registrar observações acadêmicas;
- servir como base para emissão do Certificado.

---

# Estrutura Atual

| Campo | Tipo | Obrigatório | Observação |
|--------|------|-------------|------------|
| id_historico | INT | Sim | Chave primária |
| matricula_id | INT | Sim | Matrícula |
| curso_id | INT | Sim | Curso |
| turma_id | INT | Sim | Turma |
| media_final | DECIMAL(5,2) | Não | Média final |
| frequencia_final | DECIMAL(5,2) | Não | Frequência final |
| resultado_final | ENUM | Sim | Situação final |
| carga_horaria_cumprida | INT | Não | CH cumprida |
| data_conclusao | DATE | Não | Conclusão |
| instrutor_id | INT | Sim | Responsável |
| observacao | TEXT | Não | Observações |
| ativo | BOOLEAN | Sim | Controle lógico |
| criado_em | DATETIME | Sim | Auditoria |
| atualizado_em | DATETIME | Sim | Auditoria |
| deletado_em | DATETIME | Não | Soft Delete |

---

# Chave Primária

```text
PK

id_historico
```

---

# Relacionamentos

## Matrícula

```text
Matrícula

1:1

Histórico Escolar
```

> **Observação:** Conceitualmente espera-se um único Histórico por Matrícula. Atualmente essa restrição não é garantida por uma chave `UNIQUE`, devendo ser controlada pela aplicação ou considerada para evolução futura.

---

## Curso

```text
Curso

1:N

Histórico
```

---

## Turma

```text
Turma

1:N

Histórico
```

---

## Instrutor

```text
Instrutor

1:N

Histórico
```

---

# Cardinalidade

```text
Aluno

↓

Matrícula

↓

Histórico Escolar

↓

Certificado
```

O Histórico representa a consolidação da trajetória acadêmica da matrícula.

---

# Regras de Negócio

### RN-HIS-001

Todo Histórico pertence a uma Matrícula.

---

### RN-HIS-002

Todo Histórico pertence a um Curso.

---

### RN-HIS-003

Todo Histórico pertence a uma Turma.

---

### RN-HIS-004

O Histórico registra a média final obtida pelo aluno.

---

### RN-HIS-005

O Histórico registra a frequência final consolidada.

---

### RN-HIS-006

O Histórico registra o resultado acadêmico final.

---

### RN-HIS-007

A carga horária cumprida corresponde à carga efetivamente realizada pelo aluno.

---

### RN-HIS-008

O Histórico servirá de base para emissão do Certificado.

---

# Normalização

A tabela atende à Terceira Forma Normal (3FN).

Sua responsabilidade é exclusivamente consolidar os resultados acadêmicos, sem duplicar os registros detalhados de frequência, avaliações ou diários.

---

# Pontos Fortes

- excelente separação entre dados operacionais e dados consolidados;
- estrutura preparada para certificação;
- reduz consultas complexas ao concentrar os indicadores finais;
- boa integração com Matrícula, Curso e Turma.

---

# Pontos de Atenção

## Histórico único por Matrícula

Conceitualmente, uma Matrícula deveria gerar apenas um Histórico Escolar.

Atualmente essa regra não é reforçada por uma restrição:

```text
UNIQUE(matricula_id)
```

Para a V1.1 a modelagem permanece adequada, mas recomenda-se avaliar essa restrição em uma evolução futura.

---

## Instrutor responsável

O campo:

```text
instrutor_id
```

merece uma definição de negócio mais precisa.

É importante esclarecer se representa:

- o instrutor da turma;
- o coordenador responsável pela homologação;
- ou o responsável pela consolidação do histórico.

Essa definição deve constar nas regras de negócio.

---

# Observações Arquiteturais

O Histórico Escolar foi modelado como uma entidade de consolidação.

Em vez de recalcular constantemente médias, frequências e resultados a partir das tabelas operacionais, o sistema mantém um registro consolidado da trajetória acadêmica da matrícula.

Essa decisão melhora o desempenho das consultas e preserva um retrato histórico do encerramento do curso.

> **Nota:** A justificativa completa desta estratégia poderá ser registrada futuramente na seção **Decisões Arquiteturais (ADR)**.

---

# Melhorias Futuras

## V2

Avaliar:

```text
UNIQUE(matricula_id)
```

---

## V3

Avaliar assinatura eletrônica da homologação do Histórico.

---

## V4

Avaliar versionamento do Histórico Escolar.

---

## V5

Avaliar geração automática do Histórico ao término da Turma, consolidando médias, frequência e carga horária.

---

# Conclusão

A tabela `tb_historico_aluno` apresenta uma modelagem consistente e alinhada ao objetivo de consolidar a trajetória acadêmica do aluno.

Sua responsabilidade está claramente delimitada, atuando como ponto de transição entre os registros operacionais do módulo pedagógico e a emissão do Certificado.

**Status Final:**

```text
APROVADA PARA V1.1
```