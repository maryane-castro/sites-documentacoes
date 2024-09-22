# Pular Primeira Carta

## Descrição

O módulo `PularPrimeirasCarta` gerencia a lógica de recomendação e seleção de cartas durante um processo de interação com o usuário. Utiliza a classe `SugerirCarta` para sugerir novas cartas quando necessário e permite que o usuário pule cartas com base em suas respostas e motivos de escolha. A motivação para a criação deste módulo é fornecer uma experiência de recomendação mais dinâmica e adaptativa, ajudando os usuários a encontrarem as cartas mais relevantes de acordo com suas preferências e interações anteriores.

## Estrutura do Módulo

```
- `PularPrimeirasCarta.py`: Implementa a classe PularPrimeirasCarta, que contém métodos para gerenciar a lógica de pular cartas, integrando-se à classe SugerirCarta para recomendações.
- `SugerirCarta.py`: Contém a classe SugerirCarta, que utiliza TF-IDF e similaridade de cosseno para sugerir cartas com base nas respostas do usuário.
- `artefatos_usuario/`:
  - `cartoes_selecionados_usuario.json`: Arquivo JSON que armazena as cartas selecionadas e as respostas do usuário, utilizado para a lógica de recomendação.
```

## Uso

Para utilizar o módulo, você deve instanciar a classe `PularPrimeirasCarta` e chamar o método `pular_carta` com os parâmetros adequados. O método gerencia a lógica de recomendação e retorna a carta atual, o índice e as listas de cartas.

### Exemplo

```python
from PularPrimeirasCarta import PularPrimeirasCarta

# Instanciar a classe
pular_cartas = PularPrimeirasCarta()

# Definir parâmetros
carta_atual = "Carta Exemplo"
indice_atual = 0
cinco_cartas = []
cartas_ja_recomendadas = []
porque_da_escolha = '1'
todas_as_respostas_do_usuario_sao_nulas = False

# Chamar o método para pular a carta
carta_atual, indice_atual, cinco_cartas, cartas_ja_recomendadas = pular_cartas.pular_carta(
    carta_atual, indice_atual, cinco_cartas, cartas_ja_recomendadas, porque_da_escolha, todas_as_respostas_do_usuario_sao_nulas
)

print(carta_atual)
```

## Funções e Classes Principais

### `pular_carta(self, carta_atual, indice_atual, cinco_cartas, cartas_ja_recomendadas, porque_da_escolha, todas_as_respostas_do_usuario_sao_nulas)`

- **Descrição**: Gerencia o processo de pular uma carta com base nas escolhas e respostas do usuário, retornando a carta atual e atualizando as listas de cartas.
- **Parâmetros**:
  - `carta_atual` (str): Carta que está atualmente em exibição.
  - `indice_atual` (int): Índice da carta atual na lista de cartas selecionadas.
  - `cinco_cartas` (list): Lista de até cinco cartas selecionadas para recomendação.
  - `cartas_ja_recomendadas` (list): Lista de cartas que já foram recomendadas anteriormente.
  - `porque_da_escolha` (str): Motivo da escolha do usuário (valores possíveis: '1', '2', '3', '4').
  - `todas_as_respostas_do_usuario_sao_nulas` (bool): Indica se todas as respostas do usuário são nulas.
- **Retorno**: Um tuple contendo a carta atual, o índice da carta, a lista de cinco cartas selecionadas e a lista de cartas já recomendadas.
- **Exceções**: Se o motivo da escolha não for reconhecido, uma mensagem é impressa no console.

## Testes

Você pode executar a lógica de recomendação e pular cartas com o seguinte comando:

```bash
# Execute a lógica de recomendação
python Sugerir_Primeiras_Cartas/mainSugerir_Primeiras_Cartas.py
``` 

