# python-restcountries-example
# Um exemplo simples de como usar um wrapper Python para a API do http://restcountries.com.
# Este projeto se inspira na ideia de fornecer uma interface Python fácil de usar para acessar os dados de países.

# Instalação:
# pip install requests pandas  # As bibliotecas que usamos diretamente

# Uso:
import requests
import pandas as pd

# URL base da API REST Countries v3.1 (conforme a documentação original)
BASE_URL = "https://restcountries.com/v3.1"
ALL_COUNTRIES_ENDPOINT = f"{BASE_URL}/all"

def obter_dados_da_api(url):
    """
    Faz uma requisição GET para a URL especificada e retorna os dados JSON.

    Args:
        url (str): A URL para fazer a requisição.

    Returns:
        list: Uma lista de dicionários contendo os dados JSON da resposta,
              ou None em caso de erro na requisição.
    """
    try:
        response = requests.get(url)
        response.raise_for_status()  # Levanta uma exceção para códigos de status de erro (4xx ou 5xx)
        return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Erro ao acessar a API: {e}")
        return None

def criar_dataframe(data, campos):
    """
    Cria um DataFrame pandas a partir dos dados da API, filtrando pelos campos especificados.

    Args:
        data (list): Uma lista de dicionários contendo os dados dos países.
        campos (list): Uma lista de strings representando os campos a serem incluídos no DataFrame.

    Returns:
        pandas.DataFrame: Um DataFrame contendo os dados filtrados, ou um DataFrame vazio se os dados forem None.
    """
    if data is None:
        return pd.DataFrame()

    data_filtrada = []
    for country in data:
        row = {}
        for campo in campos:
            # Adaptação para acessar campos aninhados como name, currencies, etc.
            partes = campo.split('.')
            valor = country
            try:
                for parte in partes:
                    if isinstance(valor, list) and parte.isdigit():
                        valor = valor[int(parte)]
                    elif isinstance(valor, dict) and parte in valor:
                        valor = valor[parte]
                    else:
                        valor = None
                        break
                row[campo.replace('.', '_')] = valor # Substitui '.' por '_' para nomes de coluna válidos
            except (KeyError, IndexError, TypeError):
                row[campo.replace('.', '_')] = None
        data_filtrada.append(row)
    return pd.DataFrame(data_filtrada)

if __name__ == "__main__":
    dados_paises = obter_dados_da_api(ALL_COUNTRIES_ENDPOINT)

    if dados_paises:
        print("Dados dos países obtidos com sucesso.")

        # Exemplo de filtragem de campos (similar ao parâmetro 'filters' do wrapper python-restcountries)
        campos_basicos = ["name.common", "name.official", "cca2", "region", "latlng.0", "latlng.1", "capital.0"]
        df_basico = criar_dataframe(dados_paises, campos_basicos)
        print("\nDataFrame de Informações Básicas:")
        print(df_basico.head())

        campos_demograficos = ["name.common", "population", "area", "continents.0", "landlocked"]
        df_demografico = criar_dataframe(dados_paises, campos_demograficos)
        print("\nDataFrame de Informações Demográficas e Geográficas:")
        print(df_demografico.head())

        campos_status = ["name.common", "independent", "unMember", "status"]
        df_status = criar_dataframe(dados_paises, campos_status)
        print("\nDataFrame de Informações de Status e Afiliação:")
        print(df_status.head())
    else:
        print("Falha ao obter os dados dos países.")

# Observações:
# - Este script implementa uma funcionalidade similar à de um wrapper de API,
#   facilitando a interação com a API REST Countries.
# - A função `criar_dataframe` demonstra como filtrar os dados da resposta da API
#   selecionando campos específicos, análogo ao parâmetro 'filters' do 'python-restcountries'.
# - Os nomes dos campos aninhados (ex: name.common) são acessados percorrendo a estrutura do dicionário.
# - Os nomes das colunas do DataFrame são adaptados para substituir '.' por '_' para maior compatibilidade.
# - Este é um exemplo básico e pode ser expandido para incluir mais funcionalidades
#   e tratamento de erros.