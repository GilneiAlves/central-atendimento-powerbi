## Introdução

Este documento está dividido em duas seções principais:  
**Modelagem e Justificativas Técnicas**  
**Geração de Insights Analíticos**

A primeira seção aborda as decisões relacionadas à compreensão, preparação, transformação e modelagem dos dados no Power BI, com foco em boas práticas como o uso do **esquema estrela** e **enriquecimento via Power Query (M)**.  
A segunda seção organiza os principais **insights e respostas** às perguntas de negócio extraídas da modelagem, com interpretações orientadas à tomada de decisão.

---

## Modelagem e Justificativas Técnicas

### 1. Compreensão e Preparação Inicial dos Dados

- **Fontes de Dados**:  
  - `Chamados.xlsx` – detalhes dos chamados  
  - `Detalhes_Chamados.xlsx` – ações por chamado

- **Análise Exploratória**:
  - Identificação de chaves, métricas e dimensões
  - Conexão dos chamados às ações via `IDChamado`

### 2. Modelagem de Dados

- **Tipo de Modelo**: Esquema estrela
- **Tabelas Fato**:
  - `fChamados`: um registro por chamado
  - `fAcoesChamado`: um registro por ação dentro do chamado
- **Tabelas Dimensão**:
  - `dCalendario`: gerada com `CALENDAR`, inclui dias úteis/finais de semana
  - `dAnalistas`, `dCategorias`, `dAcoes`, `dChamados`
- **Relacionamentos**: via `AnalistaID`, `CategoriaID`, `Data`, `AcaoID`

### 3. Transformações no Power Query (M)

- **Limpeza/Padronização**:
  - Correções como "Sisteemas" → "Sistemas"
  - Segurança da Rede → "Segurança Rede
  - Consolidação de nomes duplicados ou com erro de digitação
  - **Recomendação:** reforçar a padronização no preenchimento dos dados na origem para minimizar retrabalho.
- **Enriquecimento**:
  - `HoraAbertura` e `PeriodoAbertura`
  - `FotoURL` para personalização visual

- **Justificativa**: Transformações estáticas foram realizadas no Power Query (linguagem M), por ser mais adequado para enriquecimentos simples e determinísticos. Para cenários mais dinâmicos, complexos ou com alto volume de dados, o ideal seria utilizar ferramentas especializadas de ETL/ELT, como Informatica PowerCenter, Talend Open Studio, Apache Hop, Pentaho ou outras soluções robustas do mercado.

---

## Geração de Insights Analíticos

### Página 1: Visão Geral e Categorias
