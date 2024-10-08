# Caixa de Ferramentas

## Visão Geral

A classe `CaixaDeFerramentas` fornece utilitários que facilitam operações auxiliares, como manipulação de sequências numéricas e algoritmos de apoio que podem ser úteis para a implementação de sistemas semânticos e de recomendação. A classe também oferece funções matemáticas e de processamento que servem como suporte ao sistema geral.

---

## Classe `CaixaDeFerramentas`

### Estrutura da Classe

A classe `CaixaDeFerramentas` possui métodos que lidam com manipulações de sequências de Fibonacci e escolhas dinâmicas baseadas em parâmetros fornecidos. Ela interage diretamente com outras classes como o `SistemaSemantico`.

### Assinatura da Classe

```python
class CaixaDeFerramentas:
    def __init__(self, modelo_semantico):
```

#### Parâmetros

- `modelo_semantico`: Uma instância da classe `SistemaSemantico` que será utilizada pela caixa de ferramentas para interagir com o modelo semântico, quando necessário.

---

### Métodos

#### `proximo_fibonacci(lista_fib)`

Este método calcula e retorna o próximo número na sequência de Fibonacci com base em uma lista de números Fibonacci fornecida.

**Parâmetros**:
- `lista_fib` (list): Uma lista de inteiros representando a sequência de Fibonacci atual.

**Retorno**:
- `int`: O próximo número da sequência de Fibonacci.

**Exemplo de uso**:

```python
caixa_ferramentas = CaixaDeFerramentas(modelo_semantico)
proximo_numero = caixa_ferramentas.proximo_fibonacci([1, 1, 2, 3, 5])
print(proximo_numero)  # Saída: 8
```
---

#### `probc(c, cartas_visitadas, lista_fibonacci, alfa)`

A função `probc` é responsável por calcular uma probabilidade ajustada associada a uma carta específica, levando em consideração as cartas já visitadas, valores de Fibonacci correspondentes e um fator de ajuste alfa.

**Definição da Função**

```python
def probc(self, c, cartas_visitadas: list, lista_fibonacci: list, alfa: float) -> float:
```

**Parâmetros**

- `self`: Referência à instância da classe. Necessário se a função estiver dentro de um método de classe.
- `c`: (Tipo: qualquer) A carta cuja probabilidade será verificada.
- `cartas_visitadas` (Tipo: `list`): Uma lista contendo as cartas que já foram visitadas.
- `lista_fibonacci` (Tipo: `list`): Uma lista de valores de Fibonacci que estão associados às cartas visitadas.
- `alfa` (Tipo: `float`): Um fator de ajuste que influencia o cálculo da probabilidade.

**Retorno**

- **Tipo**: `float`  
- **Descrição**: Retorna a probabilidade ajustada para a carta `c`, considerando o fator alfa e o valor de Fibonacci associado. Se `c` não estiver presente na lista `cartas_visitadas`, a função retorna 1.

**Lógica da Função**

1. **Verificação de Presença**:
   - A função primeiro verifica se a carta `c` está presente na lista `cartas_visitadas`.
   - Se não estiver, a probabilidade é considerada como `1`, indicando que a carta é nova ou não foi visitada antes.

2. **Cálculo da Probabilidade**:
   - Se `c` já foi visitada, a função encontra a posição da carta na lista `cartas_visitadas` usando `index(c)`.
   - Em seguida, utiliza essa posição para buscar o valor correspondente de Fibonacci na `lista_fibonacci`.
   - A probabilidade é calculada com a fórmula:  
     \[
     \text{probabilidade\_atual} = \frac{1}{1 + \alpha \cdot \text{valor\_fib}}
     \]

3. **Retorno da Probabilidade**:
   - A função retorna o valor calculado de `probabilidade_atual`.

**Exemplo de Uso**

```python
cartas_visitadas = ['A', 'K', 'Q']
lista_fibonacci = [1, 1, 2]
alfa = 0.5
carta = 'K'

probabilidade = self.probc(carta, cartas_visitadas, lista_fibonacci, alfa)
print(probabilidade)  # Saída: 0.3333333333333333
```

#### `f_custo(carta_atual)`

A função `f_custo` é uma parte crítica do sistema de recomendação de cartas. Ela calcula o "custo" ou a relevância de uma carta atual com base em três critérios principais: probabilidade, similaridade com o "Caderno de Ouro" e a similaridade com a justificativa do usuário. Este custo é utilizado para priorizar ou classificar cartas em um sistema de recomendação, ajudando a determinar qual carta deve ser recomendada ao usuário a seguir.

**Assinatura da Função**

```python
def f_custo(self, carta_atual: str, cartas_visitadas: list, valores_fibonacci: list, alfa: float, peso_probabilidade: float, peso_similaridade_exp: float, peso_similaridade_just: float, caderno_de_ouro: str, justificativa_usuario: str) -> float:
```

**Parâmetros**

- **`carta_atual (str)`**: A carta atual que está sendo avaliada.
- **`cartas_visitadas (list)`**: Lista das cartas que já foram visitadas ou interagidas pelo usuário anteriormente.
- **`valores_fibonacci (list)`**: Valores da sequência de Fibonacci associados às cartas visitadas. Estes valores ajudam a modular a probabilidade da próxima carta recomendada.
- **`alfa (float)`**: Parâmetro de ajuste para influenciar o cálculo da probabilidade. Esse valor ajuda a ponderar a importância do histórico de interações passadas do usuário.
- **`peso_probabilidade (float)`**: Peso que define a importância relativa da probabilidade no cálculo do custo final da carta.
- **`peso_similaridade_exp (float)`**: Peso atribuído à similaridade da carta com o "Caderno de Ouro". O "Caderno de Ouro" é uma espécie de referência ou modelo ideal de carta.
- **`peso_similaridade_just (float)`**: Peso atribuído à similaridade da carta com a justificativa fornecida pelo usuário. Este parâmetro ajusta a recomendação com base nos desejos ou preferências explícitas do usuário.
- **`caderno_de_ouro (str)`**: Texto base do Caderno de Ouro, utilizado para comparação de similaridade semântica.
- **`justificativa_usuario (str)`**: Justificativa fornecida pelo usuário, utilizada para ajustar as recomendações com base em suas preferências ou feedback.

**Retorno**

- **`float`**: Retorna o custo calculado da carta atual. Este valor será utilizado para ranquear ou selecionar a carta a ser recomendada ao usuário. A função também retorna a própria carta (`carta_atual`), facilitando a correspondência entre o custo e a carta em si.

**Explicação do Cálculo**

A função calcula o custo da carta com base em três componentes principais:

1. **Probabilidade**:
   - É calculada pela função `self.probc`, que leva em consideração as cartas já visitadas, os valores de Fibonacci associados a elas e o parâmetro `alfa` que ajusta o peso do histórico nas recomendações futuras.
   - Esse valor é multiplicado pelo `peso_probabilidade`, refletindo a importância dessa métrica no custo final.

2. **Similaridade com o Caderno de Ouro**:
   - Utiliza a função `similaridade_cosseno_textos` para calcular a similaridade entre a carta atual e o Caderno de Ouro.
   - Multiplicado pelo `peso_similaridade_exp`, este componente mede o quanto a carta se alinha com o ideal definido pelo sistema.

3. **Similaridade com a Justificativa do Usuário**:
   - Também utilizando `similaridade_cosseno_textos`, esta métrica calcula o quão bem a carta atual reflete os desejos e preferências expressos pelo usuário em sua justificativa.
   - O resultado é ponderado pelo `peso_similaridade_just`.

O custo final é a soma ponderada dessas três componentes, refletindo um balanceamento entre probabilidade, similaridade com o modelo ideal e preferências do usuário.

**Exemplo de Aplicação**

```python
custo = self.f_custo(
    carta_atual="Carta A",
    cartas_visitadas=["Carta B", "Carta C"],
    valores_fibonacci=[1, 2, 3],
    alfa=0.5,
    peso_probabilidade=0.4,
    peso_similaridade_exp=0.3,
    peso_similaridade_just=0.3,
    caderno_de_ouro="Texto ideal de referência",
    justificativa_usuario="Preferência do usuário para esta recomendação"
)

print(f"Custo da Carta A: {custo[1]}")
```