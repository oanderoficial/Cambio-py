# Cambio-py

Fazendo uma requisição à API ExchangeRate para obter dados de taxa de câmbio de moedas para o Real Brasileiro (BRL). Extraindo os dados de taxa de câmbio da resposta e criando um DataFrame usando a biblioteca Pandas.

```Python
import requests
import pandas as pd

# Faz a requisição à API para obter os dados de moedas
response = requests.get('https://api.exchangerate-api.com/v4/latest/BRL')
if response.status_code == 200:
    data = response.json()

    # Extrai todos os dados do dicionário rates
    dados = data['rates']
    
    # Cria um DataFrame com os dados
    
    dataframe = pd.DataFrame.from_dict(dados, orient='index', columns=['Taxa de Câmbio'])
    dataframe.index.name = 'Moeda'


 # Exibe o DataFrame completo
    with pd.option_context('display.max_rows', None, 'display.max_columns', None):
        print(dataframe)

else:
    print('Falha na requisição:', response.status_code)
