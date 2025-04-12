
# Documentação do Projeto

## Introdução
Este projeto utiliza APIs RESTful para obter informações sobre países, populações e membros da ONU. Os dados são processados e salvos em arquivos CSV para análise posterior.

## Funções Disponíveis

### `obter_dados_da_api(url, token)`
Faz uma requisição GET para a URL especificada e retorna os dados JSON.

**Parâmetros**:
- `url` (str): A URL para fazer a requisição.
- `token` (str): O token de autenticação para a API.

**Retorno**:
- `dict`: Um dicionário contendo os dados JSON da resposta, ou `None` em caso de erro.

**Exemplo de uso**:
```python
url = "https://restfulcountries.com/api/v1/countries"
token = "Tokem gerado ao colocar apenas o email no endereço: https://restfulcountries.com/request-access-token"
dados = obter_dados_da_api(url, token)
```

### `criar_dataframe(data)`
Cria um DataFrame pandas com informações básicas dos países.

**Parâmetros**:
- `data` (dict): Um dicionário contendo os dados dos países.

**Retorno**:
- `pandas.DataFrame`: Um DataFrame contendo os dados básicos, ou `None` se os dados forem inválidos.

**Campos incluídos no DataFrame**:
- Nome Comum
- Nome Oficial
- Código Alpha-2
- Capital

**Exemplo de uso**:
```python
dataframe_paises = criar_dataframe(dados)
```

### `criar_dataframe_populacao(data)`
Cria um DataFrame pandas com informações demográficas e geográficas dos países.

**Parâmetros**:
- `data` (dict): Um dicionário contendo os dados dos países.

**Retorno**:
- `pandas.DataFrame`: Um DataFrame contendo os dados demográficos e geográficos, ou `None` se os dados forem inválidos.

**Campos incluídos no DataFrame**:
- Nome Comum
- População
- Área
- Continente

**Exemplo de uso**:
```python
dataframe_populacao = criar_dataframe_populacao(dados)
```

### `criar_dataframe_membro_da_onu(data)`
Cria um DataFrame pandas com informações sobre a independência e afiliação à ONU dos países.

**Parâmetros**:
- `data` (dict): Um dicionário contendo os dados dos países.

**Retorno**:
- `pandas.DataFrame`: Um DataFrame contendo os dados de status e afiliação, ou `None` se os dados forem inválidos.

**Campos incluídos no DataFrame**:
- Nome Comum
- Nome Oficial
- Código Alpha-2
- Capital
- População
- Área
- Continente
- Independente
- Membro da ONU
- Status

**Exemplo de uso**:
```python
dataframe_membro_onu = criar_dataframe_membro_da_onu(dados)
```

## Fluxo do Código
1. Requisição à API para obter dados.
2. Criação de DataFrames com diferentes informações.
3. Salvamento dos DataFrames em arquivos CSV.
4. Leitura e manipulação dos arquivos CSV para análise.


