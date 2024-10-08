# Sistema Semântico

## Visão Geral

A classe `SistemaSemantico` é responsável por realizar o processamento semântico de textos, permitindo a análise de similaridade entre diferentes textos utilizando vetores de palavras. Esta classe é útil para aplicações que exigem a comparação semântica de conteúdo textual, como no sistemas de recomendação.

---

## Classe `SistemaSemantico`

### Estrutura da Classe

A classe `SistemaSemantico` implementa métodos para pré-processamento de texto, obtenção de representações vetoriais e cálculo de similaridade entre textos. Ela depende de um modelo de vetores de palavras (por exemplo, Word2Vec, GloVe) para gerar essas representações.

### Assinatura da Classe

```python
class SistemaSemantico:
    def __init__(self, modelo):
```

#### Parâmetros

- `modelo`: Um modelo de vetores de palavras que será utilizado para gerar representações vetoriais dos textos. Pode ser um modelo treinado previamente, como o Word2Vec ou outro do tipo embedding.

---

### Métodos

#### `preprocessamento_de_texto(text)`

Este método realiza o pré-processamento do texto de entrada, removendo pontuações, convertendo todas as letras para minúsculas e separando o texto em tokens (palavras). O objetivo é deixar o texto em uma forma padrão para facilitar a análise semântica posterior.

**Parâmetros**:
- `text` (str): O texto a ser pré-processado.

**Retorno**:
- `list`: Uma lista de tokens resultante do texto pré-processado.

**Exemplo de uso**:

```python
sistema_semantico = SistemaSemantico(modelo)
tokens = sistema_semantico.preprocessamento_de_texto("Este é um exemplo de texto.")
print(tokens)  # Saída: ['este', 'é', 'um', 'exemplo', 'de', 'texto']
```

---

#### `obter_vetor_medio(modelo, texto)`

Este método gera um vetor médio a partir dos vetores de palavras presentes no texto. Ele utiliza o modelo de vetores de palavras fornecido na inicialização da classe. Se uma palavra do texto não estiver presente no modelo, ela é ignorada. O vetor resultante é a média dos vetores de todas as palavras encontradas.

**Parâmetros**:
- `modelo` (obj): O modelo de vetores de palavras utilizado para gerar os vetores das palavras.
- `texto` (str): Texto de entrada para ser convertido em vetor médio.

**Retorno**:
- `numpy.ndarray`: Um vetor médio que representa o texto de entrada.

**Exemplo de uso**:

```python
vetor_medio = sistema_semantico.obter_vetor_medio(modelo, "Este é um exemplo de texto.")
print(vetor_medio)  # Saída: array([0.123, -0.234, ..., 0.456])
```

---

#### `similaridade_cosseno_textos(texto1, texto2)`

Este método calcula a similaridade de cosseno entre dois textos, utilizando os vetores médios gerados a partir de cada texto. A similaridade de cosseno é uma métrica que indica o quão semelhantes são dois textos em termos de seus vetores de palavras.

**Parâmetros**:
- `texto1` (str): O primeiro texto a ser comparado.
- `texto2` (str): O segundo texto a ser comparado.

**Retorno**:
- `float`: Um valor entre -1 e 1 que indica a similaridade entre os dois textos. Quanto mais próximo de 1, maior a similaridade.

**Exemplo de uso**:

```python
similaridade = sistema_semantico.similaridade_cosseno_textos("Texto um", "Texto dois")
print(similaridade)  # Saída: 0.87 (alta similaridade)
```

---

### Exemplo de Uso Completo

```python
from gensim.models import Word2Vec

# Exemplo de criação e uso da classe SistemaSemantico
modelo = Word2Vec.load("modelo_vetores.bin")  # Carrega um modelo de vetores de palavras previamente treinado

sistema_semantico = SistemaSemantico(modelo)

texto1 = "O carro é rápido e confortável."
texto2 = "O automóvel é veloz e confortável."

# Pré-processamento dos textos
tokens1 = sistema_semantico.preprocessamento_de_texto(texto1)
tokens2 = sistema_semantico.preprocessamento_de_texto(texto2)

# Obtenção dos vetores médios
vetor1 = sistema_semantico.obter_vetor_medio(modelo, texto1)
vetor2 = sistema_semantico.obter_vetor_medio(modelo, texto2)

# Cálculo da similaridade
similaridade = sistema_semantico.similaridade_cosseno_textos(texto1, texto2)

print(f"Similaridade entre os textos: {similaridade}")
```
