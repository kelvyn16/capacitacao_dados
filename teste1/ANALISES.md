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
    

3 - Execução passo a passo - Técnicas e algoritimos utilizadas

   Primeiramente importei as bibliotecas Pandas, Numpy e Matplotlib. Em seguida importei os arquivos Csv, atribuindo uma variável para cada um deles. Posteriormente realizei uma limpeza dos missing values para evitar erros e problemas na execução dos dados, conforme seguem abaixo: conforme seguem os códigos abaixo:
   
 
`import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

airport = pd.read_csv(r"C:\Users\augus\Desktop\airports.csv")
user = pd.read_csv(r"C:\Users\augus\Desktop\users.csv")

airport.dropna(subset = ["country"], inplace = True)
airport.shape[0]
airport.head(10)

airport.dropna(subset = ["continent"], inplace = True)`

5 - Deploy
    [Descreva como você colocaria e manteria a sua solução em produção no AWS]

6 -Benchmark e Melhorias
    Relacionar o preço médio das buscas de voos internacionais por intervalo de data, destino 


#### Análise 2 - Super combo:  

#### Análise 3 - Férias imprevisíveis: 
