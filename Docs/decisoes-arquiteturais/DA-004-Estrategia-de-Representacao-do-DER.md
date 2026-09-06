# DA-004 — Estratégia de Representação do DER

## Contexto

O SGCI V1.1 possui 24 entidades e uma quantidade significativa
de relacionamentos entre seus módulos.

Durante a elaboração do DER foram avaliadas diferentes
ferramentas de representação.

## Decisão

O MySQL Workbench será utilizado como representação consolidada
da modelagem física do banco de dados.

O PlantUML será utilizado como documentação técnica versionável
da estrutura do modelo.

Diagramas produzidos em Draw.io poderão ser utilizados para
representações modulares ou apresentações específicas.

## Justificativa

A modelagem física já é mantida no MySQL Workbench desde o início
do projeto e representa diretamente a estrutura do banco.

O PlantUML permite manter uma representação textual versionável
junto ao código-fonte.

A criação de uma representação visual completamente reorganizada
do modelo consolidado não será considerada requisito da V1.1,
por se tratar de uma melhoria predominantemente estética.

## Consequência

A V1.1 não terá como requisito um DER consolidado visualmente
otimizado.

A melhoria da apresentação visual poderá ser realizada
futuramente sem alteração da modelagem.