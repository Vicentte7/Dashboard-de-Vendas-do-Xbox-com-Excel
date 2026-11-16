# Dashboard Executivo de Vendas e Assinaturas — Xbox Game Pass

## Sobre o Projeto

Este projeto foi desenvolvido como parte do desafio prático da **DIO (Digital Innovation One)** com foco na **organização, modelagem e visualização de dados no Microsoft Excel**. O objetivo central consiste em transformar registros brutos de vendas e assinaturas do ecossistema **Xbox Game Pass** (incluindo pacotes adicionais do *EA Play Season Pass* e *Minecraft Season Pass*) em um **Dashboard Executivo interativo**, permitindo a análise clara de indicadores financeiros, performance de planos, sazonalidade e retenção para tomada de decisão orientada a dados.

---

## Estrutura do Repositório

* `base.xlsx`: Arquivo original disponibilizado no desafio contendo a base bruta (`B̳ases`), paleta de cores e logotipos (`A̳ssets`).
* `dashboard_xbox_finalizado.xlsx`: Arquivo Excel completo contendo toda a memória de cálculo dinâmica (`C̳álculos`) e o painel executivo interativo (`D̳ashboard`).
* `README.md`: Documentação técnica do projeto, dicionário de dados, principais insights analíticos e instruções de reprodução.

---

## Dados Utilizados (Aba `B̳ases` — `Tabela1`)

A base de dados contempla **295 registros de assinantes** distribuídos ao longo do ano de **2024** (`01/01/2024` a `16/12/2024`), estruturados em 13 colunas:

| Coluna | Tipo de Dado | Descrição |
| :--- | :---: | :--- |
| `Subscriber ID` | Inteiro | Identificador único do assinante (`3231` a `3525`). |
| `Name` | Texto | Nome completo do titular da assinatura. |
| `Plan` | Categórico | Nível do plano contratado: `Core` (R$ 5,00), `Standard` (R$ 10,00) ou `Ultimate` (R$ 15,00). |
| `Start Date` | Data | Data de início da assinatura (`mm-dd-yy`). |
| `Auto Renewal` | Booleano (`Yes`/`No`) | Indica se a renovação automática está ativa. |
| `Subscription Price` | Moeda (R$) | Valor base do plano de assinatura contratado. |
| `Subscription Type` | Categórico | Periodicidade de cobrança: `Monthly` (Mensal), `Quarterly` (Trimestral) ou `Annual` (Anual). |
| `EA Play Season Pass` | Booleano (`Yes`/`No`) | Adesão ao passe de temporada adicional EA Play. |
| `EA Play Season Pass Price` | Moeda (R$) | Valor do add-on EA Play (`R$ 30,00` quando contratado). |
| `Minecraft Season Pass` | Booleano (`Yes`/`No`) | Adesão ao passe de temporada adicional Minecraft. |
| `Minecraft Season Pass Price` | Moeda (R$) | Valor do add-on Minecraft (`R$ 20,00` quando contratado). |
| `Coupon Value` | Moeda (R$) | Desconto promocional aplicado via cupom (`R$ 0,00` a `R$ 20,00`). |
| `Total Value` | Moeda (R$) | Faturamento líquido pago pelo assinante (`Plano + Add-ons - Cupom`). |

---

## Principais Resultados e Insights Analíticos

1. **Indicadores Consolidados (Safra 2024):**
   * **Total de Assinantes:** `295`
   * **Receita Bruta Total (Antes de Cupons):** `R$ 9.755,00`
   * **Total em Descontos (Cupons):** `-R$ 2.122,00` (`21,8%` da receita bruta)
   * **Faturamento Líquido Total:** `R$ 7.633,00`
   * **Ticket Médio Líquido:** `R$ 25,87` por assinante (Mediana: `R$ 20,00` | Desvio Padrão: `R$ 21,80`)

2. **Performance por Plano (`Core`, `Standard`, `Ultimate`):**
   * **Ultimate (`98` assinantes | `33,2%` da base):** Gera **R$ 5.388,00 (`70,6%` do faturamento líquido)** e possui ticket médio de **R$ 54,98**, impulsionado pela adesão integral aos dois passes adicionais (*EA Play* + *Minecraft*).
   * **Standard (`96` assinantes | `32,5%` da base):** Gera **R$ 1.801,00 (`23,6%` do faturamento líquido)** e ticket médio de **R$ 18,76**, com 100% de adesão ao *Minecraft Season Pass*, mas forte impacto de cupons promocionais (`R$ 1.079,00`).
   * **Core (`101` assinantes | `34,2%` da base):** Gera **R$ 444,00 (`5,8%` do faturamento líquido)** e ticket médio de **R$ 4,40**, sem contratação de add-ons.

3. **Ciclo de Cobrança e Retenção:**
   * A modalidade **Monthly** lidera em volume e receita (**139 assinantes | R$ 3.571,00 | 46,8%**), seguida por **Quarterly** (**85 assinantes | R$ 2.308,00 | 30,2%**, ostentando o maior ticket médio por ciclo: `R$ 27,15`) e **Annual** (**71 assinantes | R$ 1.754,00 | 23,0%**).
   * **50,2% da base (`148` assinantes)** mantém a renovação automática (`Auto Renewal = Yes`) ativa, respondendo por `R$ 3.786,00` em receita recorrente.

---

## Arquitetura da Solução no Excel

O arquivo `dashboard_xbox_finalizado.xlsx` foi estruturado em 4 abas integradas:

1. **`A̳ssets`**: Paleta de cores oficial Xbox (`#9BC848`, `#22C55E`, `#2AE6B1`, `#5BF6A8`, `#E8E6E9`) e ativos visuais (logos Xbox, EA Play e Minecraft).
2. **`B̳ases`**: Tabela estruturada (`Tabela1`) com os dados brutos padronizados e painéis congelados.
3. **`C̳álculos`**: Camada de modelagem analítica construída 100% com fórmulas dinâmicas (`SUM`, `AVERAGE`, `MEDIAN`, `MIN`, `MAX`, `STDEV.S`, `COUNTIF`, `SUMIF`, `COUNTIFS`, `SUMIFS`), dividida em 6 blocos:
   * Estatísticas Descritivas e Resumo Executivo;
   * Consolidação por Plano (`Core`, `Standard`, `Ultimate`);
   * Consolidação por Ciclo de Cobrança (`Monthly`, `Quarterly`, `Annual`);
   * Matrizes Cruzadas (`Plano x Ciclo`) de Receita e Assinantes;
   * Conversão de *Season Passes* e Status de *Auto Renewal*;
   * Série Histórica Mensal (`Jan/2024` a `Dez/2024`).
4. **`D̳ashboard`**: Painel visual executivo sem linhas de grade com:
   * **Simulador Interativo com Dropdowns (`DataValidation`)**: Permite filtrar combinadamente por *Plano*, *Ciclo* e *Auto-Renovação* nas células `B6`, `D6` e `F6`.
   * **7 KPI Cards Executivos** vinculados dinamicamente à aba `C̳álculos`.
   * **4 Gráficos Nativos e 2 Tabelas Resumo** com formatação condicional em escala de cores.

---

## Instruções para Reprodução
