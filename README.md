# Previsão de Vendas - Rossmann 
![rossmann-logo](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8e/Rossmann_Logo.svg/1024px-Rossmann_Logo.svg.png)
 
 # 1. Problema de Negócio
 
 A Rossman é uma empresa europeia que atua com uma rede de drograrias possuindo mais de 4.000 lojas, tornando assim uma das maiores redes de drogarias do mundo.
 
 O diretor financeiro precisa reformar as lojas, mas para a criação do orçamento, ele precisa de uma previsão de vendas para cada uma das lojas nas próximas 6 semanas.
 
 Como forma de resolução do problema, foi desenvolvido um modelo de machine learning, indicando assim o faturamento de cada loja gerando insights para equipe financeira e possam decidir como melhor desenvolver um orçamento.
 
 # 2. Premissas de Negócio
 
 Para melhor análise foram necessárias algumas considerações:
 
 - Apenas consideradas lojas com vendas superior a 0.
 - Dias com lojas fechadas foram ignorados.
 - Lojas sem dados de competidores próximos foi considerado uma distânca de 200.000 metros

## Atributos
|Atributos | Descrição |
|----------|-----------|
|Id | Um identificador único que representa a loja e data. |
|Store | Id único de cada loja. |
|Date | Data em que ocorreu o evento. |
|DayOfWeek | Variável numérica que representa o dia da semana. |
|Sales | Quantidade de vendas do dia. |
|Customers | O número de clientes na loja no dia. Open - Indicador para loja aberta = 1 ou fechada = 0. |
|StateHoliday | Indica um feriado de estado. Tipicamente as lojas fecham nesses dias. a = Feriado público, b = Feriado de páscoa, c = Natal, 0 = Não há feriado. |
|SchoolHoliday | Feriado escolar, indica se a loja naquele dia fechou. |
|StoreType | Tipos de lojas, possuem variações a, b, c, d. |
|Assortment | Nível de variedade de produtos: a = básico, b = extra, c = estendido. |
|CompetitionDistance | Distância em metros para o competidos mais próximo. |
|CompetitionOpenSince[Month/Year] | Disponibiliza o ano e mês em quem o competidor mais próximo abriu. |
|Promo | Indica se a loja está com uma promoção naquele dia. |
|Promo2 | Indica uma continua e consecutiva promoção da loja: 0 = loja não está participando, 1 = loja participando. |
|Promo2Since[Year/Week] | Descreve o ano e semana de quando a loja começa a promo2. |
|PromoInterval | Descreve os meses em que a loja iniciou a promo2, ex.: "Feb,May,Aug,Nov" significa que a loja iniciou as promoções estendidas em cada um desses meses. |


# 3. Solução

A resolução do problema seguiu os passos da metodologia CRISP-DM, que consiste em uma abordagem cíclica, onde podemos agilizar os processos e entregar resultados mais rápido.

![CRISP-DM](https://miro.medium.com/max/1400/1*z0U0taZoignUB7aQ4ZsOtg.png)

## Coleta de Dados e Entendimento
O primeiro passo foi coletar e entender os dados do Kaggle. Logo após foi feita a limpeza dos dados e o tratamento dos dados faltantes e exclusão da coluna de clientes, já que devemos prever as vendas, não podemos conhecer o número de clientes.

## Exploração dos Dados
Para uma melhor exploração dos dados, foi criado um mapa mental de hipoteses, onde vai ser o guia para criação das hipóteses e assim será possivel explorar os dados com mais eficiência entendendo quais os atributos mais importantes.

![mind-map](https://github.com/carlosandradeds/store_sales_predict/blob/main/img/mindmap.png)

Após a criação do mapa foram criadas diversas hipóteses e selecionada as melhores para melhor exploração dos dados:

1. Lojas com maior sortimentos deveriam vender mais.

2. Lojas com competidores mais próximos deveriam vender menos.

3. Lojas com competidores à mais tempo deveriam vendem mais.

4. Lojas com promoções ativas por mais tempo deveriam vender mais.

5. Lojas com mais dias de promoção deveriam vender mais.

7. Lojas com mais promoções consecutivas deveriam vender mais.

8. Lojas abertas durante o feriado de Natal deveriam vender mais.

9. Lojas deveriam vender mais ao longo dos anos.

10. Lojas deveriam vender mais no segundo semestre do ano.

11. Lojas deveriam vender mais depois do dia 10 de cada mês.

12. Lojas deveriam vender menos aos finais de semana.

13. Lojas deveriam vender menos durante os feriados escolares.

A análise detalhada das hipóteses encontra-se na pasta de notebooks nesse repositório.

Abaixo a análise de alguns insights gerados:

### 1. H1. Lojas com maior sortimento deveiram vender mais
***Verdadeiro***

Quando análisamos as vendas médias de cada tipo de loja, podemos perceber que lojas com mais sortimento, tendem a vender mais. É possivel observar com o gráfico de vendas médias por tipo sortimento:

![h1](https://github.com/carlosandradeds/store_sales_predict/blob/main/img/h1m.png)

Ainda é possivel perceber a tendência de crescimento ao longo do tempo para lojas com maior sortimento:

![h1e](https://github.com/carlosandradeds/store_sales_predict/blob/main/img/h1e.png)

### 2. H7. Lojas deveriam vender mais ao longo dos anos
***Verdadeira***

A partir dá análise dessa hipótese pode-se perceber uma tendência no aumento de vendas ao longo dos anos, é possivel o entendimento já que a cada ano passado o número de vendas foi maior:

![h7](https://github.com/carlosandradeds/store_sales_predict/blob/main/img/h7.png)

### 3. H10. Lojas deveriam vender menos aos finais de semana
***Verdadeira***

Com base na análise da hipotese é possivel notar que as vendas nos finais de semana apresentam um numero de vendas baixissimo se comparado com as vendas no meio da semana:

![h10](https://github.com/carlosandradeds/store_sales_predict/blob/main/img/h101.png)

## Preparação dos Dados

Nessa etapa os dados foram re-escalonados os dados para que os dados ficassem adequados para uma boa previsão gerando numeros mais fáceis de serem compreendidos, assim como a transformação das varáveis categóricas em variáveis numéricas.

## Seleção de features

Foram selecionadas as melhores features para utilização no modelo usando o algortimo do Boruta, com um olhar análitico é possivel avaliar as escolhas do algortimo e assim escolher as melhores features para desenvolvimento do modelo.

## Machine learning modeling

Quatro diferentes tipos de modelos foram testados (linear regression, regularized linear regression - lasso, random forest and XGBoost) e foram avaliadas utilizando o método de cross validation.

Começou com uma parcela reduzida do banco de dados, onde foram utilizadas as ultimas 6 semanas para teste dos modelos. Dessa forma foram feitas algumas iterações os modelos foram comparados a partir da média. Então chegamos ao seguintes dados comparativos:

|Model|MAE|MAPE|RMSE|
|-----------------------------|------------------|-------------|------------------|
|Random forest regressor      |837.94 +/- 218.82 |0.12 +/- 0.02|1257.19 +/- 319.82|
|XGBoost regressor            |1063.51 +/- 178.21|0.15 +/- 0.02|1518.89 +/- 241.61|
|Linear regression            |2081.73 +/- 295.63|0.3 +/- 0.02 |2952.52 +/- 468.37|
|Regularized linear regression|2116.38 +/- 341.50|0.29 +/- 0.01|2952.52 +/- 241.61|

A partir dos dados gerados é possivel análisar que os dados da Random Forest apresentam melhores condições, mas como o XGBoost apresentou dados também satisfátorios e tem uma melhor otimização dos recursos consumindo menos espaço em disco foi escolhido esse modelo para desenvolvimento do projeto.

Utilizando o procedimento de busca aleatória, com valores diferentes para os parâmetros "n_estimators", "eta", "max_depth", "subsample", "colsample_bytree" e "min_child_weight", foram realizadas 5 iterações diferentes do XGBoost, todas avaliadas por cross validation. Os valores de MAE, MAPE e RMSE estão detalhados nos notebooks para todas as iterações.
O desempenho do modelo escolhido, considerando desempenho e tamanho (tendo em conta a operacionalidade em produção), foi:

|Parameter | Value |
|----------|-------|
| n_estimators | 500 |
| eta | 0.3 |
| max_depth | 9 |
| subsample	| 0.1 |
| colsample_bytree | 0.7 |
| min_child_weight |15 |

|Model|MAE|MAPE|RMSE|
|----------------|----------------|-------------|-----------------|
XGBoost regressor|793.01 |0.11|1128.65|


# 4. Business Perfomance

Agora com o modelo treinado, é possivel traduzir a solução para o negócio trazendo os dados com o seu erro médio para buscar o melhor e o pior cenário com base nos dados:

| store	| predictions | worst_scenario | best_scenario | MAE | MAPE |
|-------|-------------|----------------|---------------|-----|------|
|337|	200223.234375|	199906.411324|	200540.057426|	316.823051|	0.057442|
|464	|384747.281250	|384094.960014	|385399.602486	|652.321236|	0.059325|
|1|	159690.593750|	159419.219641|	159961.967859|	271.374109|	0.060676|
|667	|321662.656250	|321126.230442	|322199.082058	|536.425808	|0.062828|
|929|	216773.125000	|216398.962020|	217147.287980	|374.162980	|0.064222|

Importante análisar que existem lojas com um grau de erro muito alto e que não podem ser utilizados como modelo para tomada de decisão no momento, dessa forma ficando para o próximo ciclo do CRISP, análisar o que ser feito com lojas com um alto grau de incerteza:

| store	| predictions | worst_scenario | best_scenario | MAE | MAPE |
|-------|-------------|----------------|---------------|-----|------|
|292|	108202.250000	|104740.518979	|111663.981021|	3461.731021|	0.599689|
|909|	227634.453125|	219581.676312	|235687.229938|	8052.776813|	0.543349|
|876|	203944.828125|	200224.689772	|207664.966478|	3720.138353|	0.308157|
|649|	160538.250000|	159669.154716	|161407.345284|	869.095284	|0.294179|
|286|	161908.843750|	161153.949720	|162663.737780|	754.894030	|0.272756|

O desempenho geral do modelo pode ser representado nos gráficos abaixo, onde:

error_rate = predictions/sales

error = sales - predictions


![error](https://github.com/carlosandradeds/store_sales_predict/blob/main/img/error.png)

O modelo teve um bom desempenho, mas é sempre possível melhorá-lo. Como estamos utilizando a metódologia CRISP, é possível uma nova rodada de análise e desempenho e observar as lojas que precisam de um tratamento diferenciado para um melhor retorno de informações a cerca de cada loja.
Como a análise e aplicação demanda muito tempo e muitos detalhes é preciso uma entrega de resultados o mais rapido possivel, então a primeira rodada foi realizada e assim nos próximos ciclos é possivel adaptar determinados parametros e melhorar assim a entrega dos próximos resultados.

# 5. Modelo em produção

O modelo foi então colocado em produção por meio de um chat_bot do Telegram. Para o funcionamento foi necessário além do modelo a criação de uma classe em Python com todo pipeline de processamento de dados um manipulador de API e um aplicativo para gerenciar as mensagens. Todos os arquivos foram hospedados no Heroku. É possivel entender com o esquema a seguir:

![app](https://github.com/carlosandradeds/store_sales_predict/blob/main/img/app.png)


Chat bot em funcionamento: <br>

![bot](https://github.com/carlosandradeds/store_sales_predict/blob/main/img/app.gif) <br />


QR Code para acesso ao app:


![qr](https://github.com/carlosandradeds/store_sales_predict/blob/main/img/qr.jpg)

@rosmmann_kaka_bot
