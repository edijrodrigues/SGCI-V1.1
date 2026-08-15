# Marcos do Projeto SGCI

Este documento registra os principais marcos históricos do desenvolvimento do **SGCI (Sistema de Gestão de Cursos e Instituições)**, apresentando a evolução do projeto desde o MVP inicial até as versões planejadas para o futuro.

Cada marco representa a conclusão de uma etapa estratégica do projeto e serve como referência para o acompanhamento da evolução da arquitetura, documentação e implementação do sistema.

---

# MVP Beta 0

**Data:** Junho/2026

**Status:** ✅ Concluído

## Objetivos alcançados

- Modelagem acadêmica;
- Modelagem pedagógica;
- Calendário letivo;
- Histórico escolar;
- Certificação;
- Controle financeiro;
- Documentação técnica inicial.

## Resultado

Primeira versão funcional do SGCI desenvolvida com foco na validação da arquitetura e das regras de negócio.

Ao término desta fase, o projeto foi oficialmente encerrado e preservado como referência histórica para a reconstrução da versão V1.1.

---

# V1.1 — Fundação do Projeto

**Data:** Julho/2026

**Status:** ✅ Concluído

## Objetivos alcançados

- Criação da nova estrutura de diretórios;
- Organização do projeto em módulos;
- Criação do README;
- Criação do CHANGELOG;
- Configuração do `.gitignore`;
- Inicialização do repositório Git;
- Publicação no GitHub;
- Configuração do acesso SSH;
- Definição das branches `main` e `develop`.

## Resultado

O projeto foi reorganizado e preparado para uma nova etapa de desenvolvimento baseada em Engenharia de Software, documentação e controle de versões.

---

# V1.1 — Auditoria da Modelagem

**Data:** Agosto/2026

**Status:** ✅ Concluído

## Objetivos alcançados

- Auditoria completa das **24 entidades** da modelagem;
- Documentação técnica de todas as entidades;
- Validação dos relacionamentos;
- Revisão das cardinalidades;
- Consolidação das Regras de Negócio;
- Consolidação da documentação da modelagem;
- Criação do Backlog da V1.1;
- Registro das primeiras Decisões Arquiteturais (ADR);
- Padronização da documentação técnica;
- Definição da política de commits da documentação.

## Resultado

A modelagem do SGCI foi completamente auditada, documentada e consolidada.

Ao final desta etapa, a estrutura do banco de dados tornou-se suficientemente estável para servir como base oficial para:

- DER;
- Scripts SQL;
- Migrations;
- Arquitetura MVC;
- Desenvolvimento da aplicação.

---

# Próximo Marco

## V1.1 — DER Oficial

**Status:** 🔄 Em andamento

## Objetivos

- Elaborar o Diagrama Entidade-Relacionamento (DER) oficial do projeto;
- Validar todos os relacionamentos entre as entidades;
- Revisar cardinalidades;
- Revisar chaves primárias e estrangeiras;
- Consolidar a estrutura definitiva da modelagem.

## Resultado Esperado

Disponibilizar o DER oficial da versão V1.1, servindo como referência única para:

- Banco de Dados;
- Scripts SQL;
- Migrations;
- Documentação Técnica;
- Arquitetura MVC.

---

# Próxima Etapa

Após a conclusão do DER Oficial, será encerrada a fase de Engenharia da Modelagem e terá início a fase de Implementação do Sistema.

---

# Marcos Futuros

## V1.1 — Congelamento da Modelagem

**Status:** ⏳ Planejado

### Objetivos

- Congelar oficialmente a estrutura da modelagem da V1.1;
- Formalizar que alterações estruturais passarão a ser controladas por versionamento e backlog;
- Encerrar oficialmente a Engenharia da Modelagem.

---

## V1.1 — Refatoração da Arquitetura MVC

**Status:** ⏳ Planejado

### Objetivos

- Implementar a arquitetura MVC definitiva;
- Desenvolver as classes base;
- Implementar o sistema de rotas;
- Configurar a camada de acesso aos dados (PDO);
- Preparar a estrutura para o desenvolvimento dos módulos.

---

## V1.1 — Release Final

**Status:** ⏳ Planejado

### Objetivos

- Finalizar todos os módulos previstos para a versão V1.1;
- Executar testes funcionais e integrados;
- Publicar oficialmente a primeira versão estável do SGCI.

---

## V2.0 — Expansão Financeira

**Status:** ⏳ Planejado

### Objetivos

- Evoluir o módulo financeiro;
- Implementar contratos financeiros;
- Parcelamentos;
- Descontos;
- Multas;
- Juros;
- Integrações financeiras.

---

## V3.0 — Multiunidade

**Status:** ⏳ Planejado

### Objetivos

- Evoluir o sistema para múltiplas unidades;
- Parametrizações institucionais;
- Expansão administrativa;
- Evolução da gestão organizacional e das permissões.

---

## V5.0 — Planejamento Institucional Inteligente

**Status:** ⏳ Planejado

### Objetivos

- Automatizar o planejamento institucional;
- Gerar automaticamente calendários letivos;
- Planejar turmas;
- Distribuir planos de aula;
- Organizar cronogramas institucionais;
- Automatizar eventos acadêmicos;
- Integrar planejamento pedagógico, calendário e execução acadêmica.

---

# Linha do Tempo

```text
                    ENGENHARIA DO PROJETO

✓ MVP Beta 0

        ↓

✓ Fundação da V1.1

        ↓

✓ Auditoria da Modelagem

        ↓

🔄 DER Oficial V1.1

═══════════════════════════════════════════════

             IMPLEMENTAÇÃO DO SISTEMA

        ↓

⏳ Congelamento da Modelagem

        ↓

⏳ Refatoração da Arquitetura MVC

        ↓

⏳ Release V1.1

        ↓

⏳ V2.0 — Expansão Financeira

        ↓

⏳ V3.0 — Multiunidade

        ↓

⏳ V5.0 — Planejamento Institucional Inteligente
```

---

# Observações

Este documento possui caráter histórico e estratégico.

Os marcos aqui registrados representam as principais etapas da evolução do SGCI e servem como referência para o acompanhamento do projeto.

Ao término da Auditoria da Modelagem, todas as **24 entidades** da versão V1.1 foram auditadas, documentadas e consolidadas, estabelecendo a base oficial para a elaboração do DER e para o início da implementação do sistema.

Cada novo marco deverá ser atualizado ao término de sua respectiva etapa, preservando a rastreabilidade da evolução técnica, arquitetural e funcional do SGCI.