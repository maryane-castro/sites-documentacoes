# Seleciona Cartas Para o Usuário

## Descrição

Este módulo é responsável por sugerir cartas de Fibonacci com base nas respostas do usuário, utilizando técnicas de vetorização de texto e similaridade. O propósito do módulo é proporcionar recomendações personalizadas que ajudam os usuários a refletir sobre suas respostas e a explorar diferentes aspectos de suas experiências. A motivação para sua criação vem da necessidade de uma abordagem dinâmica e interativa para feedback e autoconhecimento, resolvendo problemas relacionados à falta de personalização nas recomendações de cartas.

## Estrutura do Módulo

O módulo é composto pelos seguintes arquivos e pastas:

```
- `main.py`: Arquivo principal que executa a pipeline de recomendação de cartas.
- `vetorizacao.py`: Contém funções para vetorização das respostas do usuário e similaridade entre vetores.
- `cartas.py`: Inclui funções para extrair e manipular cartas.
- `utils/removerAlternativas.py`: Implementa a classe `RetirarCartNegacao`, que filtra respostas negativas.
```

## Uso

Para utilizar o módulo, importe as funções desejadas e execute-as com as entradas apropriadas. Veja o exemplo abaixo:

### Exemplo

```python
from vetorizacao import selecionar_cartas_para_usuario

usuario = {
    'respostas': {
        'pergunta1': 'resposta1',
        'pergunta2': None,
        'pergunta3': 'resposta3'
    }
}

cartas_recomendadas = selecionar_cartas_para_usuario(usuario)
print(cartas_recomendadas)
```

## Funções e Classes Principais

### `vetorizar_respostas_usuario(respostas_usuario, max_features=7)`

- **Descrição**: Vetoriza as respostas do usuário usando o método TF-IDF.
- **Parâmetros**:
  - `respostas_usuario`: Lista de respostas do usuário.
  - `max_features`: Número máximo de features para o vetorizador TF-IDF.
- **Retorno**: Retorna uma matriz esparsa TF-IDF das respostas do usuário.
- **Exceções**: Lança `ValueError` se a lista de respostas estiver vazia ou contiver apenas valores `None`.

### `extrair_cartas(lista)`

- **Descrição**: Extrai apenas as cartas de uma lista de objetos de cartas.
- **Parâmetros**:
  - `lista`: Lista de objetos de carta com campos 'carta'.
- **Retorno**: Retorna uma lista de cartas extraídas.

### `ajustar_dimensoes(vetor, tamanho_desejado)`

- **Descrição**: Ajusta as dimensões dos vetores para que todos tenham o mesmo número de características.
- **Parâmetros**:
  - `vetor`: Matriz de vetores a serem ajustados.
  - `tamanho_desejado`: Número desejado de características para todos os vetores.
- **Retorno**: Retorna a matriz de vetores ajustada.

### `selecionar_cartas_para_usuario(user, cartoes_filtrados_pular_carta=None)`

- **Descrição**: Sugere as principais cartas de Fibonacci para cada usuário com base em suas respostas.
- **Parâmetros**:
  - `user`: Dicionário contendo informações do usuário e suas respostas.
  - `cartoes_filtrados_pular_carta`: Cartas que devem ser puladas na recomendação (opcional).
- **Retorno**: Lista das principais cartas de Fibonacci sugeridas ao usuário.

## Testes

Você pode executar a pipeline completa com o seguinte comando:

```bash
# Execute a pipeline completa
python main.py
```
