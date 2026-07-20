# DA-003 — Política de Commits da Documentação

## Objetivo

Definir um padrão para versionamento da documentação do projeto SGCI.

---

# Tipos de Commit

## 1. Criação

Utilizado quando um novo documento é criado.

Exemplo:

docs: criar auditoria da tb_plano_curso

---

## 2. Atualização

Utilizado quando documentos existentes são modificados em decorrência de uma auditoria.

Exemplo:

docs: atualizar documentação do plano de curso

Arquivos envolvidos:

- Auditoria
- Índice
- Regras de Negócio

---

## 3. Conclusão de Bloco

Utilizado quando um conjunto de auditorias é finalizado.

Exemplo:

docs: concluir auditoria do planejamento pedagógico

---

# Fluxo de Trabalho

Para cada auditoria concluída:

1. Atualizar a auditoria da tabela.
2. Registrar Observações de Arquitetura.
3. Atualizar Regras de Negócio.
4. Atualizar o Índice.
5. Realizar o commit correspondente.

---

# Objetivos

- Histórico claro.
- Commits pequenos e coesos.
- Fácil rastreabilidade.
- Padronização do projeto.