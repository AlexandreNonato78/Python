# Python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

import scipy.stats as stats

from uszipcode import SearchEngine

# Comandos iniciais para importar o arquivo .csv
df = pd.read_csv('/content/sample_data/kc_house_data.csv', sep = ',')
df.info()

search = SearchEngine()

#Encontrando cada cidade e iniciando criação de nova coluna "Cidade"
def zco(x):
  return search.by_zipcode(int(x)).city
  
df['Cidade'] = df['zipcode'].fillna(0).astype(int).apply(zco)
df.info()

#Conferindo a criação da coluna "Cidade"
df.head()

#Conferindo quantas cidades únicas foram encontradas
print(df['Cidade'].unique())
print(type(df['Cidade'].unique()))

#Quantidade de imóveis por cidade
df.groupby('Cidade').size().reset_index()

#Removendo 'id's duplicados
df.drop_duplicates(subset='id', keep='first', inplace=True)
#Deletando colunas que não irão ser utilizadas
df = df.drop(['sqft_living15', 'sqft_lot15'], axis=1)
df.head()

#Removendo 'id's duplicados
df.drop_duplicates(subset='id', keep='first', inplace=True)
#Deletando colunas que não irão ser utilizadas
df = df.drop(['sqft_living15', 'sqft_lot15'], axis=1)
df.head()

#Criando coluna para indicar se o preço está acima do preço mediano da região
for i in range(len(df)):
  if df2.loc[i, 'price'] > df2.loc[i, 'median_price']:
        df2.loc[i, 'is_higher'] = 'yes'
  else:
        df2.loc[i, 'is_higher'] = 'no'
df2.head()  

#Quão acima os preços estão acima do preço mediano da região? (Em %)
for i in range(len(df2)):
  if (df2.loc[i, 'price'] > df2.loc[i, 'median_price']):
    df2.loc[i, 'difference'] = (df2.loc[i, 'price'] * 100) / df2.loc[i, 'median_price'] - 100
  else:
    df2.loc[i, 'difference'] = 'NA'
df2.head()

#Adicionando a percentagem mediana como recomendação de preço de venda e calculando o lucro
for i in range(len(df2)):
  if df2.loc[i, 'recommendation'] == 'Comprar':
    df2.loc[i, 'sell_price'] = df2.loc[i, 'price'] + (df2.loc[i, 'price'] * 24.5 / 100)
  else:
    df2.loc[i, 'sell_price'] = 'NA'
for i in range(len(df2)):
  if df2.loc[i, 'recommendation'] == 'Comprar':
    df2.loc[i, 'profit'] = df2.loc[i, 'sell_price'] - df2.loc[i, 'price']
  else:
    df2.loc[i, 'profit'] = 'NA'
df2.head() 

#Delimitando as melhores casas pelos parâmetros condition e grade
df3 = df2.loc[(df2['condition']>= 5) & (df2['grade']>= 8)]
df3

#Delimitando as melhores casas pelos parâmetros recommendation e profit
df4 = df3.loc[(df3['recommendation'] == 'Comprar') & (df3['profit'] != 'NA')]
df4

#Delimitando as melhores casas pelos parâmetros bedrooms e bathrooms
df5 = df4.loc[(df4['bedrooms'] >= 3) & (df4['bathrooms'] >= 2)]
df5

#Delimitando as melhores casas pelos parâmetros bedrooms e bathrooms
df5 = df4.loc[(df4['bedrooms'] >= 3) & (df4['bathrooms'] >= 2)]
df5

#As 5 casas recomendadas são:
df_casasrecomendadas = df6.drop(columns=["date", "sqft_lot", "zipcode", "lat", "long", "sqft_above", "sqft_basement", "is_higher", "difference", "sell_price", "profit"])
df_casasrecomendadas

#Delimitando as piores casas pelos parâmetros condition e grade
df3N = df2.loc[(df2['condition'] < 3) & (df2['grade'] < 5)]
df3N

#Delimitando as piores casas pelo parâmetro bathrooms
df4N = df3N.loc[(df3N['bathrooms'] < 1)]
df4N

#As 5 casas NÃO recomendadas são:
df_casasNÃOrecomendadas = df4N.drop(columns=["date", "sqft_lot", "zipcode", "lat", "long", "sqft_above", "sqft_basement", "is_higher", "difference", "sell_price", "profit"])
df_casasNÃOrecomendadas
