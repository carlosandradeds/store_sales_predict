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

A resolução do problema seguiu os passos da metodologia CRISP-DM, que consiste em uma abordagem cíclica, onde podemos agilizar os processos e gerando resultados mais rápido.

[CRISP-DM](https://miro.medium.com/max/1400/1*z0U0taZoignUB7aQ4ZsOtg.png)
