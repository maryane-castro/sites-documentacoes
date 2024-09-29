# Analisador de Sentimentos

## Descrição

O módulo `SentimentAnalyzer` é uma ferramenta projetada para analisar sentimentos em respostas de usuários, utilizando um modelo de linguagem (LLM) para processar o texto e gerar uma análise de sentimento. Este módulo é capaz de interpretar respostas textuais, converter a análise em um formato estruturado (JSON) e visualizar a intensidade do sentimento ao longo do tempo através de um gráfico.

## Estrutura do Módulo

```
- `sentiment_analyzer.py`: Contém a implementação da classe SentimentAnalyzer.
```

## Uso

Para utilizar o módulo, é necessário instanciar a classe `SentimentAnalyzer` e chamar o método `main` com as respostas do usuário e o número de dias de inatividade.

### Exemplo

```python
from sentiment_analyzer import SentimentAnalyzer

analyzer = SentimentAnalyzer()

resposta1 = "Estou me sentindo bem hoje."
resposta2 = "O trabalho tem sido desafiador, mas gratificante."
resposta3 = "Estou ansioso para as férias do próximo mês."
dias_inatividade = 5

temp_file_name, json_result = analyzer.main(resposta1, resposta2, resposta3, dias_inatividade)

print(f"Arquivo do gráfico: {temp_file_name}")
print(f"Resultado JSON:\n{json_result}")
```

## Funções e Classes Principais

### `SentimentAnalyzer`

#### `__init__(model_name="llama3.1", temperature=0.001)`

- **Descrição**: Inicializa a classe SentimentAnalyzer com um modelo de linguagem específico.
- **Parâmetros**:
  - `model_name`: Nome do modelo Ollama a ser utilizado (padrão: "llama3.1").
  - `temperature`: Temperatura para geração de texto (padrão: 0.001).

#### `process_json(resposta)`

- **Descrição**: Processa a resposta do modelo LLM e converte em um dicionário JSON estruturado.
- **Parâmetros**:
  - `resposta`: String contendo a resposta do modelo LLM.
- **Retorno**: Uma tupla contendo o dicionário JSON processado e sua representação em string.

#### `gerar_resposta(user_input, prompt)`

- **Descrição**: Gera uma resposta usando o modelo LLM com base nas entradas do usuário.
- **Parâmetros**:
  - `user_input`: Tupla contendo as respostas do usuário e dias de inatividade.
  - `prompt`: Template de prompt para o modelo LLM.
- **Retorno**: A resposta gerada pelo modelo LLM.

#### `gerar_grafico(data)`

- **Descrição**: Gera um gráfico de linha suave mostrando a intensidade do sentimento ao longo do tempo.
- **Parâmetros**:
  - `data`: Dicionário contendo os dados de sentimento.
- **Retorno**: Nome do arquivo temporário onde o gráfico foi salvo.

#### `main(resposta1, resposta2, resposta3, dias_inatividade)`

- **Descrição**: Método principal que orquestra o processo de análise de sentimento.
- **Parâmetros**:
  - `resposta1`, `resposta2`, `resposta3`: Strings contendo as respostas do usuário.
  - `dias_inatividade`: Número de dias de inatividade.
- **Retorno**: Uma tupla contendo o nome do arquivo do gráfico e a representação JSON do resultado.

## Dependências

O módulo requer as seguintes bibliotecas:

- langchain_community
- matplotlib
- sklearn
- scipy
- numpy

Certifique-se de instalá-las antes de usar o módulo.

## Notas Adicionais

- O módulo utiliza o Ollama como modelo de linguagem, assegure-se de que ele esteja corretamente configurado em seu ambiente.
- O gráfico gerado é salvo temporariamente e o caminho do arquivo é retornado. Lembre-se de gerenciar adequadamente esses arquivos temporários em sua aplicação.
- A análise de sentimento considera valores negativos para sentimentos negativos, o que é refletido no gráfico gerado.