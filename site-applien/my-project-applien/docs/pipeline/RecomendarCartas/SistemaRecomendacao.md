# README - Função `f_custo`

## Visão Geral

A função `f_custo` é uma parte crítica do sistema de recomendação de cartas. Ela calcula o "custo" ou a relevância de uma carta atual com base em três critérios principais: probabilidade, similaridade com o "Caderno de Ouro" e a similaridade com a justificativa do usuário. Este custo é utilizado para priorizar ou classificar cartas em um sistema de recomendação, ajudando a determinar qual carta deve ser recomendada ao usuário a seguir.

## Estrutura da Função

A função recebe diversos parâmetros que influenciam o cálculo do custo da carta, levando em consideração o histórico de interações do usuário (cartas visitadas), a sequência de Fibonacci (valores Fibonacci associados às cartas visitadas) e a semântica do conteúdo da carta, do caderno de ouro, e da justificativa fornecida pelo usuário.

### Assinatura da Função

```python
def f_custo(self, carta_atual: str, cartas_visitadas: list, valores_fibonacci: list, alfa: float, peso_probabilidade: float, peso_similaridade_exp: float, peso_similaridade_just: float, caderno_de_ouro: str, justificativa_usuario: str) -> float:
```

### Parâmetros

- **`carta_atual (str)`**: A carta atual que está sendo avaliada.
- **`cartas_visitadas (list)`**: Lista das cartas que já foram visitadas ou interagidas pelo usuário anteriormente.
- **`valores_fibonacci (list)`**: Valores da sequência de Fibonacci associados às cartas visitadas. Estes valores ajudam a modular a probabilidade da próxima carta recomendada.
- **`alfa (float)`**: Parâmetro de ajuste para influenciar o cálculo da probabilidade. Esse valor ajuda a ponderar a importância do histórico de interações passadas do usuário.
- **`peso_probabilidade (float)`**: Peso que define a importância relativa da probabilidade no cálculo do custo final da carta.
- **`peso_similaridade_exp (float)`**: Peso atribuído à similaridade da carta com o "Caderno de Ouro". O "Caderno de Ouro" é uma espécie de referência ou modelo ideal de carta.
- **`peso_similaridade_just (float)`**: Peso atribuído à similaridade da carta com a justificativa fornecida pelo usuário. Este parâmetro ajusta a recomendação com base nos desejos ou preferências explícitas do usuário.
- **`caderno_de_ouro (str)`**: Texto base do Caderno de Ouro, utilizado para comparação de similaridade semântica.
- **`justificativa_usuario (str)`**: Justificativa fornecida pelo usuário, utilizada para ajustar as recomendações com base em suas preferências ou feedback.

### Retorno

- **`float`**: Retorna o custo calculado da carta atual. Este valor será utilizado para ranquear ou selecionar a carta a ser recomendada ao usuário. A função também retorna a própria carta (`carta_atual`), facilitando a correspondência entre o custo e a carta em si.

## Explicação do Cálculo

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

### Fórmula do Custo:

\[
\text{Custo da Carta} = (\text{peso\_probabilidade} \times \text{probabilidade}) + (\text{peso\_similaridade\_exp} \times \text{similaridade\_caderno}) + (\text{peso\_similaridade\_just} \times \text{similaridade\_justificativa})
\]

## Dependências

A função faz uso das seguintes dependências:

1. **`self.probc`**: Função que calcula a probabilidade de uma carta ser recomendada com base no histórico do usuário e na sequência de Fibonacci.
2. **`self.classe_sistema_Semantico.similaridade_cosseno_textos`**: Função que calcula a similaridade entre dois textos utilizando o cosseno de seus vetores de palavras. Esse método pertence a uma classe do sistema responsável pelo processamento semântico.

## Uso

A função é utilizada dentro do sistema de recomendação de cartas para calcular o custo de cada carta disponível. Com base nesse custo, o sistema pode classificar as cartas e sugerir ao usuário a próxima carta que melhor equilibra as recomendações automáticas com as preferências expressas pelo próprio usuário.

## Exemplo de Aplicação

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

Neste exemplo, o sistema avalia a "Carta A" com base em seu histórico de cartas visitadas, seu alinhamento com o Caderno de Ouro, e as preferências do usuário, retornando o custo associado.

## Considerações Finais

A função `f_custo` é altamente configurável, permitindo ajustar os pesos das variáveis probabilísticas, de similaridade com o modelo ideal e com as preferências do usuário, oferecendo um controle fino sobre o comportamento do sistema de recomendação.
