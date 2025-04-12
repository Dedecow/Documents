# Projeto Analise de dados Paises a partir da API RestFul Countries

## Introdução

Este projeto utiliza Python 3.11.9 como linguagem principal e tem como objetivo facilitar a manipulação e análise de dados relacionados a países. As principais bibliotecas utilizadas são:

- `pandas` para manipulação de dados
- `numpy` para operações numéricas
- `datetime` para tratamento de datas
- `requests` para consumo de APIs

Os dados são obtidos através da API fornecida por [Restful Countries](https://restfulcountries.com/api/v1/countries). Para utilizar a API, é necessário gerar um token de acesso:

```python
token = "2528|https://restfulcountries.com/request-access-token"
url = "https://restfulcountries.com/api/v1/countries"
```

## Instalação

Para configurar o ambiente e instalar as dependências necessárias, execute:

```bash
pip install pandas numpy requests
```

Após a instalação, configure o token da API no código-fonte do projeto.

## Uso

Aqui está um exemplo básico de como utilizar as bibliotecas para consumir dados da API:

```python
import requests
import pandas as pd

token = "SEU_TOKEN_AQUI"
url = "https://restfulcountries.com/api/v1/countries"

headers = {
    "Authorization": f"Bearer {token}",
    "Accept": "application/json"
}

response = requests.get(url, headers=headers)
data = response.json()

# Convertendo para DataFrame
df = pd.DataFrame(data)
print(df.head())
```

## Contribuição

Contribuições são bem-vindas! Para contribuir com o projeto:

1. Faça um fork do repositório: [https://github.com/Dedecow/Documents/tree/main](https://github.com/Dedecow/Documents/tree/main)
2. Crie uma branch com sua feature (`git checkout -b feature/incrivel`)
3. Faça commit das suas alterações (`git commit -m 'Adicionando feature incrível'`)
4. Push para a branch (`git push origin feature/incrivel`)
5. Abra um Pull Request

## Licença

Este projeto está licenciado sob uma licença pública. Consulte o arquivo [LICENSE](LICENSE) para mais detalhes.

## Contato

- GitHub: [https://github.com/Dedecow](https://github.com/Dedecow)
- Email: [andrehbahia@gmail.com](mailto:andrehbahia@gmail.com)
