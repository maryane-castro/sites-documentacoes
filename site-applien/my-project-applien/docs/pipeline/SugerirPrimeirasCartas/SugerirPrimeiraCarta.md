# Sugerir Primeira Carta

## Descrição

O módulo `sugerir_carta` é projetado para sugerir cartas com base nas respostas do usuário. Ele utiliza técnicas de processamento de texto, como vetorização TF-IDF e cálculo de similaridade de cosseno, para identificar as cartas mais relevantes de um conjunto disponível. A motivação para sua criação é proporcionar um sistema que ajude os usuários a receber recomendações personalizadas, melhorando a interação e a satisfação com o serviço. O módulo resolve o problema de encontrar sugestões adequadas a partir de um conjunto limitado de respostas, considerando também a história de recomendações anteriores.

## Estrutura do Módulo

```
- sugerir_carta.py: Classe SugerirCarta que contém métodos para vetorizar respostas e sugerir cartas com base na similaridade.
```

## Uso

Para usar o módulo, você deve instanciar a classe `SugerirCarta` e chamar seus métodos com os dados apropriados.

### Exemplo

```python
from sugerir_carta import SugerirCarta

sugeridor = SugerirCarta()

# Exemplo de respostas do usuário
respostas_usuario = {
    'respostas': {
        'resposta1': 'texto da resposta 1',
        'resposta2': 'texto da resposta 2'
    }
}

cartas_selecionadas = ['Carta A', 'Carta B', 'Carta C', 'Carta D', 'Carta E']
cartas_recomendadas, cartas_atualizadas = sugeridor.sugerir_carta(cartas_selecionadas, respostas_usuario)
print(cartas_recomendadas)
```

## Funções e Classes Principais

### `SugerirCarta`

- **Descrição**: Classe para sugerir cartas com base nas respostas do usuário, utilizando vetorização de texto TF-IDF e cálculo de similaridade de cosseno.

#### `__init__(self)`

- **Descrição**: Inicializa uma instância da classe SugerirCarta.

#### `vetorizar_respostas_usuario(self, respostas_usuario, max_features=7)`

- **Descrição**: Vetoriza as respostas do usuário usando TF-IDF (Term Frequency-Inverse Document Frequency).
- **Parâmetros**:
  - `respostas_usuario (list)`: Lista de respostas do usuário.
  - `max_features (int)`: Número máximo de features para o vetorizador TF-IDF.
- **Retorno**: `scipy.sparse.csr_matrix`: Matriz esparsa TF-IDF das respostas do usuário.

#### `sugerir_carta(self, cartas_selecionadas, respostas_usuario, cartas_ja_recomendadas=None)`

- **Descrição**: Sugere cartas com base nas respostas do usuário. Utiliza posições de Fibonacci e cálculo de similaridade de cosseno para selecionar as cartas mais relevantes.
- **Parâmetros**:
  - `cartas_selecionadas (list)`: Lista de cartas disponíveis para seleção.
  - `respostas_usuario (dict)`: Dicionário contendo as respostas do usuário.
  - `cartas_ja_recomendadas (list, optional)`: Lista de cartas que já foram recomendadas previamente.
- **Retorno**: `tuple`: Lista de cartas sugeridas e a lista de cartas já recomendadas atualizada.

## Testes

Você pode executar a pipeline completa com o seguinte comando:

```bash
# Execute a pipeline completa
python Sugerir_Primeiras_Cartas/mainSugerir_Primeiras_Cartas.py
```
