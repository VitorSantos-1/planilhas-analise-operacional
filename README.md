# Análises em Excel para Varejo — Precificação, Acordos e Conciliação

Coletânea de análises construídas em Excel para a operação de uma rede de supermercados, cobrindo
precificação e margem, controle de acordos comerciais (verbas e notas de débito), conciliação de NFDs
e desempenho por categoria. Cada análise nasceu de uma necessidade real do dia a dia de compras e
comercial, e é apresentada aqui com a explicação do que resolve e da lógica de cálculo por trás dela.

> **Nota de confidencialidade:** este repositório expõe apenas a estrutura, a lógica e os cálculos das
> análises — nunca os dados reais, que são confidenciais e estão protegidos. Os prints das planilhas,
> quando adicionados, terão os campos sensíveis (empresas, fornecedores e valores) tarjados.

---

## Visão Geral

Boa parte da inteligência de compras e comercial de um supermercado vive em planilhas: é onde o
comprador calcula margem, acompanha acordos com fornecedores, confere notas de débito e mede
categorias. Este repositório reúne essas análises, documentando o raciocínio de negócio e as fórmulas
que as sustentam. O objetivo é mostrar o domínio do problema — precificação, verbas, conciliação e
rentabilidade — que antecede e orienta qualquer dashboard ou pipeline de dados.

## Contexto de Negócio

No varejo alimentar, margem se ganha e se perde nos detalhes: um preço mal calculado, uma verba de
fornecedor não recebida, uma nota de débito que não bate com o sistema. Cada uma das análises a seguir
ataca um desses pontos, transformando um controle manual em um instrumento de decisão — com o
vocabulário que a operação usa: custo, preço de venda, margem, markup, verba, NFD, acordo, giro.

---

## 1. Precificação e Rentabilidade

### 1.1. Calculadora de Preço, Margem e Markup
Planilha que, a partir do preço de custo e do preço de venda de um item, calcula a rentabilidade
completa. É a ferramenta base de precificação do comprador.

- **Entradas:** quantidade, preço de custo (R$), preço de venda (R$).
- **Cálculos:**
  - **Margem (sobre a venda)** = (Preço de Venda − Preço de Custo) / Preço de Venda.
  - **Markup (sobre o custo)** = (Preço de Venda − Preço de Custo) / Preço de Custo.
  - **Lucro Unitário** = Preço de Venda − Preço de Custo.
  - **Lucro Total** = Lucro Unitário × Quantidade.
- **Para que serve:** decidir o preço de venda mirando uma margem-alvo e enxergar, em um olhar, a
  rentabilidade de cada item.

<!-- ![Calculadora de preço, margem e markup](docs/print-01.png) -->

### 1.2. Previsão de Preço de Oferta
Planilha que projeta o preço e a meta de uma oferta a partir do histórico de vendas do ano anterior.

- **Base:** informações das ofertas vendidas no ano passado (preço, volume, resultado).
- **Lógica:** parte do desempenho histórico do item em oferta e aplica o quanto se deseja vender a mais
  para chegar ao preço/meta da nova oferta.
- **Para que serve:** planejar ofertas com base em dado real de sazonalidade e volume, não em achismo.

<!-- ![Previsão de preço de oferta](docs/print-02.png) -->

### 1.3. Precificação e Estatística de Preço
Conjunto de análises de apoio: cálculo de datas futuras (planejamento de campanhas), precificação por
margem e estatística básica de uma lista de preços (mínimo, comparação entre preços praticados).

- **Cálculos:** preço baseado em margem-alvo; estatísticas descritivas (menor preço, dispersão) sobre
  uma lista de itens.
- **Para que serve:** dar base estatística à decisão de preço e ao calendário de ofertas.

<!-- ![Precificação e estatística de preço](docs/print-03.png) -->

---

## 2. Acordos Comerciais, Verbas e Notas de Débito

### 2.1. Acordos em Aberto (Total, Verbas e NFDs)
Controle dos acordos comerciais em aberto com fornecedores, separando **verbas** (bonificações
negociadas) e **NFDs** (notas de débito), com saldo a receber por fornecedor e por loja.

- **Estrutura:** três visões — um **Total** consolidado por loja; a aba de **Verbas** (controle,
  fornecedor, razão social, datas de emissão/vencimento, loja, tipo de verba, valor total, recebido e
  restante); e a aba de **NFDs** (nº da nota, fornecedor, datas, loja, valor, recebido e restante).
- **Cálculo central:** **Valor Restante** = Valor Total − Valor Recebido, por acordo.
- **Para que serve:** enxergar quanto ainda há a receber de fornecedores (verbas e notas), por loja,
  para cobrança e conciliação.

<!-- ![Acordos em aberto — verbas e NFDs](docs/print-04.png) -->

### 2.2. Acordos Vencidos por Empresa (Aging)
Acompanhamento histórico dos acordos vencidos e em aberto, consolidando total por loja e para as 4
lojas, com controle de quitação ao longo do tempo.

- **Cálculos:** **Total por loja** e **Total das 4 lojas**; **valor quitado até o momento**; e o
  **tempo decorrido** ("já se passou") desde a data de início do acordo — um cálculo de *aging* que
  mede há quanto tempo o valor está vencido.
- **Para que serve:** priorizar a cobrança pelos acordos mais antigos e medir a evolução da quitação.

<!-- ![Acordos vencidos por empresa — aging](docs/print-05.png) -->

### 2.3. Conciliação de NFDs (Cliente x Sistema)
Conciliação das notas de débito entre o relatório do cliente e o registro no sistema da empresa,
identificando divergências.

- **Estrutura:** cliente, número da NF do cliente, relatório de NFD do cliente e da empresa, o que
  consta no sistema, valor, data faturada e data compensada, situação.
- **Cálculo central:** cruzamento entre o que o cliente apresenta e o que está no sistema, apontando o
  que **falta compensar** e as divergências de valor/data.
- **Para que serve:** garantir que toda nota de débito seja compensada, evitando perda financeira.

<!-- ![Conciliação de NFDs](docs/print-06.png) -->

### 2.4. Conciliação de Oferta
Conferência entre a oferta negociada/planejada e o que foi efetivamente praticado e faturado,
apontando diferenças a acertar com o fornecedor.

- **Lógica:** comparação entre o previsto da oferta e o realizado, destacando divergências de valor ou
  quantidade a conciliar.
- **Para que serve:** assegurar que o combinado da oferta com o fornecedor seja cumprido e cobrado.

<!-- ![Conciliação de oferta](docs/print-07.png) -->

---

## 3. Desempenho por Categoria

### 3.1. Análise de Açougue e Frios
Análise mensal de desempenho do setor de açougue e frios (referência: fevereiro/2025), com indicadores
da categoria ao longo do período.

- **Estrutura:** matriz de itens/indicadores do setor por período (14 colunas de acompanhamento).
- **Para que serve:** acompanhar o desempenho de uma categoria estratégica e perecível, apoiando
  decisões de compra e redução de perda.

<!-- ![Análise de açougue e frios](docs/print-08.png) -->

---

## Como Este Repositório Está Organizado

```text
README.md    -> Documentação das análises (negócio + cálculos)
docs/        -> Reservado para os prints das planilhas (dados sensíveis tarjados) — a adicionar
.gitignore   -> Impede o versionamento de planilhas com dados reais (.xls/.xlsx/.xlsm/.csv)
```

## Autor

José Vitor Santos Pinheiro — Análise de Dados e Inteligência Comercial (Varejo, Indústria e Distribuição).
Contato: vytorsantt@gmail.com
