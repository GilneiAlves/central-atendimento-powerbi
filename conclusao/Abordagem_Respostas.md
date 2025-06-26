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

#### Pergunta 1:
**Qual categoria apresenta o maior tempo médio de atendimento (dias úteis vs não úteis)?**

- **Resposta**: Categoria **Conectividade** com média de 180,44 minutos.
  - Dias úteis: 179 min | Dias não úteis: 195 min
- **Visuais**:
  - Gráficos de barras (tempo médio por categoria)
  - Gráfico de linhas (picos de abertura ao longo do dia)
  - Barras com número de chamados por categoria pai

**Insights**:
- Conectividade tem gargalos mesmo com menor volume em finais de semana
- Indica necessidade de reforço ou reestruturação de processos
- Auxilia no planejamento de capacidade da equipe

---

### Página 2: Desempenho dos Analistas

#### Pergunta 2:
**Qual analista atendeu ao maior número de chamados?**

- **Resposta**: 
  - 1º Jon (16 chamados)
  - 2º Tyrion (9)
  - 3º Daenerys (5)

#### Pergunta 3:
**Qual analista possui o menor tempo médio de atendimento?**

- **Resposta**: Tyrion, com média de **138 minutos**

**Insights**:
- Jon tem alto volume, Tyrion é o mais eficiente
- Visualização com formatação condicional destaca o melhor desempenho
- Ranking pode guiar redistribuição de carga e estratégias de capacitação

---

### Página 3: Ações e Complexidade

#### Pergunta 4:
**Qual tipo de ação acumulou o maior total de minutos de execução?**

- **Resposta**: **Intervenção técnica**, com 1.215 minutos

**Insights**:
- Foco de melhorias deve estar nessa ação
- Sugere revisão de processos e automações

#### Pergunta 5:
**Como varia o tempo total de atendimento conforme o número de ações registradas?**

- **Resposta**: Observa-se uma relação direta entre o número de ações registradas e o tempo total de atendimento de um chamado. Chamados com maior número de ações tendem, em média, a apresentar maior tempo total de atendimento.

**Exemplos**:
- 4 ações → Chamado ID 22 (302 min), ID 6 (237 min), Chamado ID 11 (233 minutos) ou Chamado ID 9 (215 minutos)
- 2 ações → Chamado ID 13 (76 min), ID 4 (82 min) ou Chamado ID 17 (99 minutos)

**Insights**:
- Correlação visual mostra crescimento do tempo com mais ações
- Identifica outliers (muitas ações com pouco tempo e vice-versa)
- Suporte à revisão de processos com base na complexidade
- Processos mais enxutos ou melhor integração entre analistas podem ajudar a reduzir o tempo médio de atendimento, mesmo em chamados mais complexos.

---

## Conclusão

Este projeto demonstra como uma modelagem de dados bem estruturada, aliada ao uso eficaz do Power Query, DAX e boas práticas de visualização, pode transformar dados operacionais em insights acionáveis de alto valor para a tomada de decisão.

Ao longo da análise, foi possível identificar gargalos operacionais, mapear padrões de desempenho entre analistas e entender como a complexidade das ações influencia diretamente o tempo de atendimento. Esses achados reforçam a importância de utilizar dados como base para decisões estratégicas, como a alocação de recursos, revisão de processos e melhoria contínua no atendimento.

### Recomendações Gerais:

- **Revisar a atuação em finais de semana** para categorias com maior tempo médio de atendimento.
- **Monitorar ações com alta duração**, como "Intervenção técnica", buscando oportunidades de automação ou simplificação de processos.
- **Valorizar e replicar boas práticas** de analistas com maior eficiência, como observado no desempenho de Tyrion.
- **Investir na padronização dos dados na origem**, reduzindo o retrabalho durante o tratamento e enriquecimento.
- **Expandir o uso de ferramentas de ETL/ELT** para escalabilidade futura, conforme o crescimento do volume ou da complexidade dos dados.

Este case evidencia não apenas a importância de ferramentas como o Power BI, mas também o papel estratégico do analista de dados na construção de soluções que apoiam decisões orientadas por evidência.

---