# Análise da Pandemia de COVID-19 no Brasil (Dados de SRAG)

> Um projeto de análise de dados de ponta a ponta que investiga o impacto de casos graves (hospitalizados) de COVID-19 no Brasil, desde a coleta e tratamento de dados brutos do DataSUS até a geração de insights geográficos, demográficos e temporais.

Este projeto realiza uma análise exploratória profunda sobre os casos de Síndrome Respiratória Aguda Grave (SRAG) confirmados para COVID-19 no Brasil. O objetivo é transformar um dataset governamental massivo e complexo (com mais de 1.2 milhões de registros e 194 colunas) em um conjunto de dados limpo e estruturado, do qual possamos extrair conclusões e visualizações informativas.

---
## 🎯 Objetivos

As principais perguntas que este projeto buscou responder foram:

1.  **Panorama Geral:** Quais os números totais de hospitalizações e óbitos por COVID-19 no Brasil, e qual a taxa de mortalidade hospitalar geral?
2.  **Análise Geográfica:** Como a pandemia se distribuiu entre os estados e as macro-regiões do Brasil? Quais localidades foram mais impactadas em números absolutos e em termos proporcionais à sua população?
3.  **Análise Demográfica:** Qual o perfil demográfico dos pacientes hospitalizados? Houve diferença no impacto da doença entre sexos e, principalmente, entre diferentes faixas etárias?
4.  **Análise Temporal:** Como os casos graves e os óbitos evoluíram ao longo do tempo? Foi possível identificar as diferentes "ondas" da pandemia?

---
## 📂 Fontes de Dados

-   **Fonte Primária (Casos e Óbitos):**
    -   **Origem:** Portal de Dados Abertos do SUS (OpenDataSUS).
    -   **Dataset:** Síndrome Respiratória Aguda Grave - SRAG.
    -   **Link para o Portal:** [https://opendatasus.saude.gov.br/dataset/srag-2021-e-2022](https://opendatasus.saude.gov.br/dataset/srag-2021-e-2022)

-   **Fonte Secundária (Enriquecimento de Dados):**
    -   **Origem:** Instituto Brasileiro de Geografia e Estatística (IBGE), disponibilizado via repositório público.
    -   **Dataset:** Lista de Municípios Brasileiros com códigos IBGE e UFs.
    -   **Link para o Arquivo:** [https://raw.githubusercontent.com/kelvins/Municipios-Brasileiros/main/csv/municipios.csv](https://raw.githubusercontent.com/kelvins/Municipios-Brasileiros/main/csv/municipios.csv)

    -   **Origem:** Dados de população por estado do IBGE (Estimativa 2021).

---
## 🛠️ Tecnologias e Bibliotecas

-   **Linguagem:** `Python 3`
-   **Ambiente:** `Google Colab`
-   **Bibliotecas Principais:**
    -   `Pandas`: Para toda a manipulação, limpeza, tratamento e estruturação dos dados.
    -   `Matplotlib` & `Seaborn`: Para a criação de visualizações e gráficos estatísticos.
    -   `Glob`: Para a localização e listagem de arquivos de dados no ambiente.

---
## ⚙️ Pipeline do Projeto (Metodologia)

O projeto seguiu um pipeline robusto de ciência de dados, dividido em três macro-etapas:

**1. Coleta e Consolidação:**
-   Os dados brutos, separados em múltiplos arquivos anuais pelo DataSUS, foram carregados e unidos (`pd.concat`) em um único DataFrame com mais de 1.2 milhão de registros.

**2. Limpeza e Pré-processamento (ETL):**
-   **Filtragem Primária:** O dataset original continha todos os tipos de SRAG. Foi aplicado um filtro na coluna `CLASSI_FIN` para isolar apenas os **~720 mil** casos confirmados de COVID-19.
-   **Seleção de Atributos:** De um total de 194 colunas, foram selecionadas as 8 variáveis essenciais para a análise, reduzindo drasticamente a complexidade e o uso de memória.
-   **Tratamento de Dados Faltantes (Avançado):** Para garantir a máxima qualidade dos dados, foram aplicadas duas técnicas avançadas:
    -   **Enriquecimento de Dados:** Para um pequeno número de registros com a UF (estado) faltante, foi utilizada a tabela de municípios do IBGE para preencher a informação com base no código do município, demonstrando a capacidade de enriquecer um dataset com fontes externas.
    -   **Imputação de Dados:** As datas de evolução (óbito/cura) faltantes foram preenchidas (imputadas) utilizando a mediana de tempo entre a notificação e o desfecho, calculada a partir dos dados completos.
-   **Engenharia de Atributos:** Foram criadas novas colunas para enriquecer a análise, como `IDADE` (calculada a partir da data de nascimento), `OBITO` (uma variável binária para óbito), `FAIXA_ETARIA` e `REGIAO`.

**3. Análise Exploratória e Visualização:**
-   Com um DataFrame final limpo e estruturado, foram realizadas agregações e cálculos de taxas para responder às perguntas de negócio, com todos os resultados apresentados em tabelas e gráficos para facilitar a interpretação.

---
## 📊 Principais Descobertas e Visualizações

-   **Impacto Geográfico Desigual:** A análise por estado revelou que **São Paulo** liderou com mais de **230 mil casos graves** e **80 mil óbitos** registrados. No entanto, a análise de **casos por 100 mil habitantes** mostrou que **Distrito Federal** e **Espírito Santo** tiveram um impacto proporcionalmente maior. A **taxa de mortalidade hospitalar** foi mais alta em estados como o **Rio de Janeiro (~52%)**, indicando maior pressão sobre o sistema de saúde.

-   **Fator de Risco Etário:** A idade provou ser o fator de risco mais crítico. A taxa de mortalidade hospitalar saltou de **menos de 5%** para jovens na faixa dos 20 anos para mais de **57%** para pacientes com 80 anos ou mais.

-   **As Ondas da Pandemia:** O gráfico de evolução temporal revelou claramente as diferentes ondas de hospitalizações e óbitos no Brasil. Foi possível identificar o pico da onda da variante **Gamma em meados de 2021**, caracterizada por uma alta mortalidade, e o pico de hospitalizações da **Ômicron no início de 2022**, que, apesar dos números altos, apresentou uma letalidade hospitalar menor.

---
## 🚀 Como Executar este Projeto
1.  **Baixe os arquivos** de dados anuais de SRAG do portal [OpenDataSUS](https://opendatasus.saude.gov.br/dataset/srag-2021-e-2022).
2.  **Faça o upload dos arquivos** para uma pasta no seu Google Drive (ex: `Dados_COVID`).
3.  **Abra o notebook** (`.ipynb`) no Google Colab.
4.  **Ajuste a variável `caminho_da_pasta`** na Célula 2 para apontar para a sua pasta no Google Drive.
5.  **Execute as células** em sequência para replicar todo o processo.

---
## ✍️ Autor
**Luiz Almeida**
* **LinkedIn:** www.linkedin.com/in/luizmarques84
* **GitHub:** https://github.com/LuizAmeida
