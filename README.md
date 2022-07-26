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

![h10](https://github.com/carlosandradeds/store_sales_predict/blob/main/img/h10.png)


