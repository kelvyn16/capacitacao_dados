# Projeto Capacitação em Dados

## Introdução

A MaxMilhas é um Marketplace que está no mercado desde 2013, responsável por conectar pessoas que desejam voar com economia, com um outro perfil de cliente, que por sua vez possui milhas oriundas de programas de fidelidade e desejam ganhar um  dinheirinho extra. 

Para que isso seja possível a empresa capta os clientes detentores das milhas e utiliza tal pontuação para emitir passagens aéreas com valores incrivelmente menores para os clientes que compram passagens aéreas, isso sem que os mesmos não tenham contato, o que se torna um desafio e tanto.

Entretanto tal complexidade de negócio, requer uma destreza elevada, assim como a criação de diferenciais de mercado, já que atualmente um segmento de mercado satura com extrema facilidade. Desta forma há a necessidade de inovação constante para agradar tanto clientes compradores como clientes negociadores de milhas(que na MaxMilhas são chamados de ofertantes), agregando produtos e serviços novos.

Surge então o presente projeto, que por meio de análise de bases de dados de compradores, buscará melhorias para processos internos.

### Descrição do projeto 

O projeto em questão visa propor melhorias para o processo de compra dos nossos usuários, com diferenciais de serviços e produtos, se baseando em informações coletadas dos usuários da plataforma. 

As bases utilizadas serão a airports.csv e users.csv, com a primeira base relacionando os aeroportos que estão presentes no site, e a segunda base que contém o tráfego dos usuários durante uma busca por passagens aéreas.

Entretanto, pelo fato de lidarmos com a base airports.csv que possui missing values(dados nulos), necessitamos realizar uma limpeza dos dados(Data Wrangling), a fim de evitar erros e problemas durante a execução dos códigos. Outro fator de extrema relevância é devido a base de usuários do site(users.csv) possuir 6.757.377 de linhas, além de 8 colunas, desta forma, para melhorar o desempenho e qualidade das análises, trabalharemos com amostra do dataset em questão.

### Análises realizadas

Para o estudo, foram propostas três análises, a fim de desenvolver soluções e melhorias no processo de compra  dos clientes, foram elas:

#### Análise 1 - Flying abroad:
1 - Qual é a análise:
    Filtrar dentro da base de dados, os destinos internacionais com voos partindo do Brasil para o exterior e mapear a relação entre os destinos mais procurados e que são inseridos em uma etapa de compra(inserida no carrinho) e a quantidade de compras finalizadas pelo conjunto de usuários.
    
   A ideia principal é listar em ordem crescente de compras de voos internacionais e oferecer novas possibilidades dentro do nosso site, aumentando assim a taxa de conversão para cada destino.

2 - Motivação da análise
    Recentemente realizei buscas em nossos sites, a fim de encontrar uma passagem com preço acessível para diminuir os custos do meu intercâmbio. 
    Me deparei com uma situação que chamou a atenção, a possibilidade de utilizar milhas internacionais de Cias aéreas estrangeiras para emissão dos voos com um custo de cerca de 40% menor que os comprados convencionalmente, sejam passagens tarifadas ou até mesmo por milhas em companhias nacionais.
    Entretanto mesmo com esses fatores que possibilitam ganhos consideráveis para empresa, as emissões são realizadas manualmente, além do cliente ter que enviar um e-mail para orçamento das passagens em questão. Processo no qual, demanda muito tempo dos analistas e acarreta em uma experiência ruim para os clientes, pela demora no procedimento.

3 - Execução passo a passo e análises realizadas - Técnicas e algoritimos

   Primeiramente importei as bibliotecas Pandas, Numpy e Matplotlib. Em seguida importei os arquivos Csv, atribuindo uma variável para cada um deles. Posteriormente realizei uma limpeza dos missing values para evitar erros e problemas na execução dos dados, conforme seguem abaixo: conforme seguem os códigos abaixo:
   
 
~~~
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

airport = pd.read_csv(r"C:\Users\augus\Desktop\airports.csv")
user = pd.read_csv(r"C:\Users\augus\Desktop\users.csv")

airport.dropna(subset = ["country"], inplace = True)
airport.shape[0]
airport.head(10)

airport.dropna(subset = ["continent"], inplace = True)
~~~
Após a importação e limpeza dos dados, inicie as querys para mapeamento dos dados de procura e compra de passagens aéreas para destinos internacionais. Para primeira análise, vamos agrupar e somar a quantidade de voos comprados para os destinos internacionais saindo do Brasil Com a criação de query, vamos determinar a conversão das buscas realizadas em compras em nosso site. A partir deste momento, buscar soluções para aumentar as vendas. Para tanto, foi utilizado o código abaixo:

~~~
inter = combine.query('country != "BR"').groupby("airport_to").sum().sort_values(by = "comprou", ascending=False).head(10)
inter

inter.plot(kind = "bar")
~~~
            
        
airport|buscou|colocou_no_carrinho    |comprou
-------|------|-----------------------|---------------			
EZE	   |23458 |       37350           |	5137
SCL	   |103230|       32097           |	4931
LIS	   |103552|       25369           |	2656
MIA	   |89557 |       20999           |	2484
MCO	   |58404 |       16101           |	1604
LHR	   |9260  |       8514            |	1474
ASU	   |24686 |       5990            |	1219
JFK	   |13248 |       10520           |	1192
MVD	   |25788 |       6541            |	1120
CDG	   |6725  |       7083            |	945

Foi possível observar que temos mais procura para o destino de Lisboa do que para Santiago, porém a taxa de conversão em compras para o Santiago é quase o dobro 4,7% contra 2,5% de taxa de conversão.

Outro fator relevante foi a taxa de conversão de compra dos bilhetes para Londres(Heathrow) cerca de 15,91%, fator este que deve ser analisado profundamente para desenvolver ações de maior procura pelo destino, como promoções, matérias no blog e até mesmo proporcionar um roteiro acessível, com parcerias com hostels, uma vez que a moeda local é elevada em comparação ao real. Paris possui um caso semelhante com taxa de conversão de 14,05%.

4 - Propostas baseadas na análise amostral realizada:

* Ações para captação de ofertantes com milhas internacionais, a fim de aumentar o banco de milhas disponíveis;
* Registro dos principais trechos procurados diretamente no site(são eles os 10 registrados na tabela anterior), tendo em vista uma maior visibilidade para os clientes e um aumento de receita para a empresa;
* Automatização das emissões por milhas internacionas, visando assim o ganho de performance da equipe, assim como é atualmente as emissões nacionais.

5 -Benchmark e Melhorias
    
   Relacionar o preço médio das buscas de voos internacionais por intervalo de data e destino. Para tanto será necessário um dataset que traga tais informações de registro de transações que hoje são criadas manualmente para emissão que ocorre da mesma forma, diretamente no site da Cia aérea.  


#### Análise 2 - Super combo:  

1 - Qual é a análise:
 
A presente análise visa comparar dentro de um mesmo estado, aeroportos próximos, nos quais desejamos entender se é viável oferecer pacotes que incluem, passagem aérea e serviço de taxi. 
 

2 - Motivação da análise:

Grande procura de voos  para região de São Paulo, devido a importância do estado e principalmente da capital e o município de Campinas. 

Desta forma, em diversas situações os clientes necessitam ir à um dos locais, seja mais próximo do centro de São Paulo, no qual o aeroporto de Congonhas é a melhor opção, porém com um preço elevado ou se deslocar diretamente para campinas, porém os voos para o aeroporto de Viracopos ocorrem em menor número e muitas vezes com um preço bem salgado. 

Sendo assim o aeroporto de Guarulhos em muitos casos acaba se tornando a melhor opção em relação à preço, entretanto fica distante do centro da cidade e a distância é maior ainda quando pensamos em Campinas. A ideia é determinar por meio da análise da taxa de conversão de busca em compra, se o resultado de desistência de compras é significativa em CGH e VCP em relação à GRU. 

3 - Execução passo a passo e análises realizadas - Técnicas e algoritimos

A análise em  questão seguiu a mesma metodologia descrita anteriormente, com importação das bibliotecas, aproveitando o data wrangling realizado no início do projeto.

Em seguida definiu-se uma variável para inserir uma query que agrupasse os aeroportos citados anteriormente e em seguida somar as colunas de buscou, colocou_no_carrinho e comprou. Além disso, ainda realizou-se uma plotagem de um gráfico de barras para visualização.

Para tanto, o código ficou da seguinte maneira:

~~~
region = combine.query('airports_group == "SAO"').groupby("airport_to").sum().sort_values(by = "comprou", ascending=False).head(10)
region

region.plot(kind = "bar")
~~~

4 - Propostas baseadas na análise amostral realizada:

* Buscar parcerias para o translado de passageiros que necessitam ir em direção ao centro de São Paulo e demais regiões em direção oposta de Guarulhos ou até mesmo partindo de Guarulhos em direção à Campinas, quando os voos disponíveis neste aeroporto(GRU) estão com preços baixos;

*  Fornecer ao comprador uma cotação antecipada, ressaltando se a economia na passagem em questão compensará o gasto com o translado.


5 -Benchmark e Melhorias
    
* Comparar preços durante o ano para determinar se o combo é viável, levando em conta a demanda de serviço gerada;
* Encontrar bases de períodos de maior procura dos bilhetes, a fim de sugerir ao cliente a melhor época para compra.


#### Análise 3 - Férias imprevisíveis: 
