# 15 - Auditoria da Tabela `tb_diario_anexo`

## Identificação

**Tabela:** `tb_diario_anexo`

**Módulo:** Planejamento Pedagógico

**Responsabilidade:** Evidências documentais da execução pedagógica

**Status da Auditoria:** Concluída

---

# Objetivo

A tabela `tb_diario_anexo` é responsável por armazenar os arquivos vinculados ao Diário de Aula.

Esses arquivos representam evidências documentais da execução da atividade pedagógica, permitindo anexar materiais complementares, registros fotográficos, documentos e demais arquivos relacionados à aula realizada.

A separação dos anexos em uma entidade própria preserva a integridade do Diário de Aula e mantém a modelagem desacoplada do mecanismo de armazenamento de arquivos.

---

# Responsabilidades

A tabela possui as seguintes responsabilidades:

- armazenar a referência dos arquivos anexados ao Diário de Aula;
- preservar o nome original do arquivo;
- permitir múltiplos anexos por Diário;
- manter rastreabilidade documental da execução pedagógica.

---

# Estrutura Atual

| Campo | Tipo | Obrigatório | Observação |
|---------|------|------------|------------|
| id_anexo | INT | Sim | Chave primária |
| diario_id | INT | Sim | Diário de Aula |
| caminho_arquivo | VARCHAR(255) | Sim | Caminho físico ou lógico do arquivo |
| nome_original | VARCHAR(255) | Não | Nome informado pelo usuário |
| criado_em | DATETIME | Sim | Auditoria |
| atualizado_em | DATETIME | Sim | Auditoria |

---

# Chave Primária

```text
PK

id_anexo
```

---

# Relacionamentos

## Diário de Aula

```text
Diário de Aula

1:N

Anexos
```

Relacionamento implementado por:

```text
diario_id
```

Integridade referencial:

```text
ON DELETE CASCADE

ON UPDATE CASCADE
```

Caso um Diário de Aula seja removido, seus anexos também serão removidos.

---

# Cardinalidade

```text
Diário de Aula

1:N

Anexos
```

Um Diário pode possuir nenhum, um ou diversos anexos.

Cada anexo pertence exclusivamente a um Diário de Aula.

---

# Regras de Negócio

### RN-PED-ANX-001

Todo Anexo deve pertencer a um Diário de Aula.

---

### RN-PED-ANX-002

Um Diário de Aula pode possuir vários anexos.

---

### RN-PED-ANX-003

Todo Anexo deve possuir um caminho de armazenamento válido.

---

### RN-PED-ANX-004

O nome original do arquivo poderá ser preservado para fins de identificação.

---

# Normalização

A tabela atende à Terceira Forma Normal (3FN).

O armazenamento dos anexos em uma entidade independente elimina redundâncias e mantém o Diário de Aula livre de informações relacionadas ao mecanismo de armazenamento dos arquivos.

---

# Pontos Fortes

- Excelente desacoplamento entre dados pedagógicos e arquivos.
- Permite qualquer quantidade de anexos.
- Estrutura simples.
- Boa integridade referencial.
- Facilita futuras integrações com sistemas de armazenamento.

---

# Pontos de Atenção

Atualmente a tabela armazena apenas o caminho do arquivo.

Informações como:

- tipo MIME;
- tamanho;
- hash do arquivo;
- usuário responsável pelo upload;

não são registradas.

Essa simplificação é adequada para a V1.1.

---

# Observações de Arquitetura

A modelagem separa corretamente os registros pedagógicos das evidências documentais.

O Diário de Aula representa o registro oficial da atividade executada.

Os anexos representam documentos complementares que comprovam ou enriquecem esse registro.

Essa separação reduz o acoplamento e favorece a manutenção do sistema.

> **Nota:** A estratégia de armazenamento de arquivos será documentada futuramente na seção **Decisões Arquiteturais (ADR)**.

---

# Melhorias Futuras

## V2

Avaliar inclusão de:

```text
tipo_arquivo

tamanho

mime_type

usuario_upload
```

---

## V3

Avaliar integração com armazenamento em nuvem.

---

## V4

Avaliar controle de versões dos anexos.

---

## V5

Avaliar assinatura digital e integridade documental utilizando hash criptográfico.

---

# Conclusão

A tabela `tb_diario_anexo` apresenta modelagem simples, objetiva e bem desacoplada.

Sua responsabilidade está claramente delimitada, atuando como repositório das evidências documentais vinculadas ao Diário de Aula.

A auditoria considera a estrutura consistente e plenamente adequada para os objetivos da versão V1.1.

Status Final:

```text
APROVADA PARA V1.1
```

> **Nota:** A estratégia de armazenamento de arquivos será documentada futuramente na seção **Decisões Arquiteturais (ADR)**.