# Detecção Anomalia

## Descrição

O módulo `DeteccaoAnomaliaSentimento` é projetado para detectar anomalias em sentimentos baseados em cartas, utilizando palavras-chave e um modelo CBOW (Continuous Bag of Words) para calcular a similaridade entre palavras. A motivação para a criação deste módulo surge da necessidade de analisar feedbacks e sentimentos expressos por meio de cartas, ajudando a identificar padrões de sentimento e recomendações apropriadas com base em sentimentos anteriores. O módulo resolve o problema de entender e gerenciar respostas emocionais, permitindo que as cartas sejam ajustadas para melhor atender as expectativas dos usuários.

## Estrutura do Módulo

A estrutura do módulo é organizada da seguinte forma:

```
- `deteccao_anomalia_sentimento.py`: Implementação da classe DeteccaoAnomaliaSentimento, incluindo métodos para armazenar sentimentos, detectar erros, e recomendar cartas.
```

## Uso

Para usar o módulo, é necessário importar a classe e instanciá-la com um modelo CBOW e um DataFrame contendo as cartas e suas palavras-chave. A seguir estão exemplos de uso:

### Exemplo

```python
import pandas as pd
from deteccao_anomalia_sentimento import DeteccaoAnomaliaSentimento

# Exemplo de DataFrame com cartas e palavras-chave
data = {
    'Descricao': ['Carta 1', 'Carta 2', 'Carta 3'],
    'PalavrasChave': ['feliz, alegre', 'triste, decepcionado', 'neutro, comum']
}
dataFrame = pd.DataFrame(data)

# Exemplo de modelo CBOW (substitua pela implementação real)
modelo_cbow = {'feliz': np.random.rand(300), 'alegre': np.random.rand(300),
               'triste': np.random.rand(300), 'decepcionado': np.random.rand(300),
               'neutro': np.random.rand(300), 'comum': np.random.rand(300)}

detector = DeteccaoAnomaliaSentimento(modelo_cbow, dataFrame)

# Armazenando uma carta e detectando anomalias
resultado = detector.armazenar_cartas_positivas_e_negativas('Carta 1', 0.5, dataFrame, ['Carta 1', 'Carta 2'])
print(resultado)
```

## Funções e Classes Principais

### `DeteccaoAnomaliaSentimento`

#### `__init__(modelo_cbow, dataFrame)`

- **Descrição**: Inicializa a classe `DeteccaoAnomaliaSentimento` com um modelo CBOW e um DataFrame de cartas.
- **Parâmetros**:
  - `modelo_cbow`: Objeto do modelo CBOW utilizado para converter palavras em vetores.
  - `dataFrame`: DataFrame contendo as descrições das cartas e suas palavras-chave.

#### `armazenar_cartas_positivas_e_negativas(cartaAtual, intensidadeSentimento, listaCartasComPalavrasChaves, cartas_subgrupo)`

- **Descrição**: Armazena palavras-chave positivas ou negativas de uma carta, de acordo com a intensidade do sentimento, e verifica a detecção de anomalias.
- **Parâmetros**:
  - `cartaAtual`: A descrição da carta atual.
  - `intensidadeSentimento`: A intensidade do sentimento gerado pela carta.
  - `listaCartasComPalavrasChaves`: DataFrame contendo cartas e suas palavras-chave.
  - `cartas_subgrupo`: Lista de cartas pertencentes a um subgrupo específico.
- **Retorno**: Carta recomendada se houver detecção de anomalia, caso contrário, `None`.

#### `detectar_erro(ultimaIntensidade, intensidadeSentimento, cartas_subgrupo)`

- **Descrição**: Detecta se há repetição de sentimentos positivos ou negativos consecutivos.
- **Parâmetros**:
  - `ultimaIntensidade`: A última intensidade do sentimento armazenada.
  - `intensidadeSentimento`: A nova intensidade do sentimento a ser verificada.
  - `cartas_subgrupo`: Lista de cartas pertencentes a um subgrupo específico.
- **Retorno**: Carta recomendada se uma anomalia for detectada, caso contrário, `None`.

#### `get_vector(palavra)`

- **Descrição**: Obtém o vetor associado a uma palavra do modelo CBOW.
- **Parâmetros**:
  - `palavra`: A palavra a ser convertida em vetor.
- **Retorno**: O vetor da palavra, ou um vetor de zeros se a palavra não estiver no modelo.

#### `get_mean_vector(palavras)`

- **Descrição**: Calcula o vetor médio de uma lista de palavras.
- **Parâmetros**:
  - `palavras`: Lista de palavras para calcular o vetor médio.
- **Retorno**: O vetor médio das palavras, ou um vetor de zeros se não houver vetores.

#### `calcular_similaridade(vetor1, vetor2)`

- **Descrição**: Calcula a similaridade de cosseno entre dois vetores.
- **Parâmetros**:
  - `vetor1`: O primeiro vetor.
  - `vetor2`: O segundo vetor.
- **Retorno**: A similaridade de cosseno entre os dois vetores.

#### `recomendar_cartas(usuario_palavras, cartas_subgrupo)`

- **Descrição**: Recomenda cartas com base na similaridade das palavras-chave do usuário e das cartas do subgrupo.
- **Parâmetros**:
  - `usuario_palavras`: Lista de palavras-chave do usuário.
  - `cartas_subgrupo`: Lista de cartas pertencentes a um subgrupo específico.
- **Retorno**: Carta recomendada com base na similaridade, ou `None` se não houver similaridades.

## Testes

Para executar a pipeline completa, utilize o seguinte comando:

```bash
# Execute a pipeline completa
python Recomendar_Cartas/mainRecomendar_Cartas.py
```

