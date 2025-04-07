# Documentação

## Funções Disponíveis

---

### `obter_dados_da_api(url)`
Faz uma requisição GET para a URL especificada e retorna os dados JSON.

**Parâmetros**:
- `url` (str): A URL para fazer a requisição.

**Retorno**:
- `list`: Uma lista de dicionários contendo os dados JSON da resposta, ou `None` em caso de erro na requisição.

**Exemplo de uso**:
```python
dados = obter_dados_da_api("https://restcountries.com/v3.1/all")

criar_dataframe(data)

Cria um DataFrame pandas com informações básicas dos países.

Parâmetros:

    data (list): Uma lista de dicionários contendo os dados dos países.

Retorno:

    pandas.DataFrame: Um DataFrame contendo os dados básicos, ou None se os dados forem inválidos.

Exemplo de uso:
dataframe_paises = criar_dataframe(dados)

Campos incluídos no DataFrame:

    Nome Comum

    Nome Oficial

    Código Alpha-2

    Região

    Latitude

    Longitude

    Capital


criar_dataframe_populacao(data)

Cria um DataFrame pandas com informações demográficas e geográficas dos países.

Parâmetros:

    data (list): Uma lista de dicionários contendo os dados dos países.

Retorno:

    pandas.DataFrame: Um DataFrame contendo os dados demográficos e geográficos, ou None se os dados forem inválidos.

Exemplo de uso:
dataframe_populacao = criar_dataframe_populacao(dados)

Campos incluídos no DataFrame:

    Nome Comum

    População

    Área

    Continente

    País sem litoral

criar_dataframe_membro_da_onu(data)

Cria um DataFrame pandas com informações sobre a independência e afiliação à ONU dos países.

Parâmetros:

    data (list): Uma lista de dicionários contendo os dados dos países.

Retorno:

    pandas.DataFrame: Um DataFrame contendo os dados de status e afiliação, ou None se os dados forem inválidos.

Exemplo de uso:
dataframe_membro_onu = criar_dataframe_membro_da_onu(dados)

Campos incluídos no DataFrame:

    Nome Comum

    Independente

    Membro da ONU

    Status

Observações:

    Este script implementa funcionalidades para facilitar a interação com a API REST Countries.

    As funções criar_dataframe, criar_dataframe_populacao e criar_dataframe_membro_da_onu permitem criar DataFrames com diferentes conjuntos de informações.

    Os nomes das colunas do DataFrame foram adaptados para maior compatibilidade, substituindo '.' por '_'.

    Este é um exemplo básico e pode ser expandido para incluir mais funcionalidades e tratamento de erros.