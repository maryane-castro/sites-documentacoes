# Fluxo de Usuário no Aplicativo

## Descrição

O fluxo de usuário no aplicativo envolve a navegação entre **subgrupos** e a recomendação de **cartas**. O sistema calcula para qual subgrupo o usuário será direcionado após realizar atividades em um subgrupo atual. Cada subgrupo tem um conjunto de cartas recomendadas com características específicas, baseadas nos pilares aos quais o subgrupo está mais próximo.

### Subgrupos e Pilares

Existem **6 subgrupos** principais no sistema: **1, 2, 4, 5, 7 e 8**. Estes subgrupos são posicionados em um círculo numerado de **1 a 9**, mas os números **3, 6 e 9** não fazem parte dos subgrupos ativos, pois são considerados **pilares principais**, cada um associado a um aspecto diferente das cartas:

- **Pilar 9: Emocional**
- **Pilar 3: Social**
- **Pilar 6: Cognitivo**

Cada subgrupo é posicionado em relação a esses pilares, de modo que suas cartas têm características que refletem o pilar mais próximo e o segundo pilar mais próximo. Por exemplo:
- O **subgrupo 1** está mais próximo do **Pilar 9 (Emocional)**, seguido pelo **Pilar 3 (Social)**. Assim, as cartas do subgrupo 1 são predominantemente **+EMOCIONAL** (mais características emocionais) e **-SOCIAL** (menos características sociais).

Esse esquema permite que as recomendações de cartas sejam altamente personalizadas com base na posição do subgrupo e nos pilares que o influenciam.

## Função `configura_indice_proximo_subgrupo`

A função `configura_indice_proximo_subgrupo` é responsável por calcular o próximo subgrupo para o qual o usuário deve ser direcionado após realizar uma atividade no subgrupo atual. Ela utiliza uma lógica baseada na "Regra dos Vortex", que envolve dobrar o valor do subgrupo atual e somar os dígitos resultantes.

### Estrutura da Função

```python
def configura_indice_proximo_subgrupo(self, ponto: int) -> int:
    """Calcula o próximo subgrupo de um ponto utilizando a regra dos Vortex.

    Args:
        ponto (int): Ponto inicial (subgrupo atual) para o cálculo do próximo subgrupo.

    Returns:
        int: Próximo subgrupo calculado.
    """
    ponto = 2 * ponto
    proximo_ponto = sum(int(digito) for digito in str(ponto))
    return proximo_ponto
```

### Parâmetros
- **ponto (int)**: Representa o **subgrupo atual** onde o usuário está no momento. É um número inteiro entre os subgrupos disponíveis (**1, 2, 4, 5, 7 ou 8**).

### Retorno
- **int**: O próximo subgrupo calculado, que será o novo destino do usuário. Ele é determinado pela soma dos dígitos do valor dobrado do subgrupo atual.

### Lógica da Função

1. O valor do **subgrupo atual** (parâmetro `ponto`) é multiplicado por 2.
2. Os dígitos do resultado são somados para obter o **próximo subgrupo**.
   - Por exemplo, se o usuário está no subgrupo 1, o cálculo será:
     - `1 * 2 = 2`
     - Próximo subgrupo: **2**
   - Se o usuário está no subgrupo 8:
     - `8 * 2 = 16`, então `1 + 6 = 7`
     - Próximo subgrupo: **7**

## Fluxo de Navegação

- O usuário inicia em um subgrupo (por exemplo, **1**).
- Após realizar a atividade proposta, o sistema calcula o próximo subgrupo utilizando a função `configura_indice_proximo_subgrupo`.
- O usuário então avança para o próximo subgrupo determinado e recebe um novo conjunto de cartas relacionadas a esse subgrupo.

### Exemplo de Navegação

1. O usuário está no **subgrupo 1**, realiza a atividade.
   - O sistema calcula: `1 * 2 = 2`, então o próximo subgrupo é o **subgrupo 2**.
   
2. No **subgrupo 2**, o usuário realiza uma nova atividade.
   - O sistema calcula: `2 * 2 = 4`, então o próximo subgrupo é o **subgrupo 4**.

Este ciclo continua até que o usuário percorra todos os subgrupos disponíveis.

## Características das Cartas

As cartas recomendadas em cada subgrupo são influenciadas pelos pilares mais próximos. Por exemplo:
- **Subgrupo 1**: +EMOCIONAL, -SOCIAL (cartas que enfatizam atividades emocionais com uma influência menor do pilar social).
- **Subgrupo 2**: -EMOCIONAL, +SOCIAL
- **Subgrupo 4**: +SOCIAL, -COGNITIVO
- **Subgrupo 5**: -SOCIAL, +COGNITIVO
- **Subgrupo 7**: +COGNITIVO, -EMOCIONAL
- **Subgrupo 8**: -COGNITIVO, +EMOCIONAL