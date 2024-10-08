# SistemaRecomendacao

Classe responsável por gerenciar um sistema de recomendação utilizando um dataset inicial. A classe permite a atualização do dataset, a seleção de cartas e a recomendação de melhores opções com base em critérios definidos.

## Atributos

- **dataset_inicial**: `list` - Conjunto de dados inicial para o sistema de recomendação.
- **dataset_atual**: `list` - Cópia profunda do dataset inicial, usada para armazenar o estado atual.
- **subgrupo_atual**: `dict` ou `None` - O subgrupo atualmente selecionado.
- **tupla_melhor_carta_atual**: `tuple` ou `None` - A melhor carta atualmente selecionada e seu custo associado.
- **lista_cartas_e_custos_atual**: `list` - Lista de cartas e seus respectivos custos atualizados.
- **pulo_permitido**: `bool` - Indica se o pulo entre cartas é permitido.
- **indice_grupo_atual**: `int` ou `None` - Índice do grupo/subgrupo atual.
- **indice_proximo_grupo**: `int` ou `None` - Índice do próximo grupo/subgrupo a ser considerado.
- **classe_Atualiza_Cartas**: `RetirarCartasNegacao` - Instância da classe responsável por atualizar as cartas.
- **classe_caixa_de_Ferramentas**: `CaixaDeFerramentas` - Instância da classe de ferramentas auxiliares.

## Métodos

### `__init__(self, dataset_inicial: list) -> None`
Inicializa a classe `SistemaRecomendacao` com um dataset inicial.

**Parâmetros:**
- `dataset_inicial`: `list` - A lista de dados que será utilizada para iniciar o sistema de recomendação.

### `funcaoDEBUG(self)`
Exibe informações de depuração sobre o estado atual do sistema, incluindo o dataset, subgrupo atual, melhor carta e índices de grupos.

### `atualiza_dataset(self, opcoes_usuario: list) -> None`
Atualiza o dataset atual removendo cartas com base nas opções fornecidas pelo usuário.

**Parâmetros:**
- `opcoes_usuario`: `list` - Lista de opções fornecidas pelo usuário para remoção de cartas.

### `atualizaFluxo(self, permissao_para_proximo_subgrupo: bool) -> bool`
Atualiza o fluxo do sistema para o próximo subgrupo, caso a permissão seja concedida.

**Parâmetros:**
- `permissao_para_proximo_subgrupo`: `bool` - Indica se a transição para o próximo subgrupo é permitida.

**Retorna:**
- `bool` - `True` se a transição foi bem-sucedida; caso contrário, `False`.

### `atualiza_subgrupoAtual(self, id_subgrupo) -> dict or None`
Retorna o subgrupo correspondente ao ID fornecido.

**Parâmetros:**
- `id_subgrupo`: `int` - Identificador único do subgrupo a ser encontrado.

**Retorna:**
- `dict or None` - O subgrupo correspondente ou `None` se não encontrado.

### `inicio_PrimeiraCarta(self, carta_escolhida: str)`
Inicia o processo com a primeira carta escolhida, atualizando o estado do subgrupo e das cartas.

**Parâmetros:**
- `carta_escolhida`: `str` - Nome da carta escolhida para iniciar o processo.

### `atualiza_informacoes_subgrupo(self, carta: tuple) -> bool`
Atualiza as informações do subgrupo com base na carta fornecida, incluindo listas de cartas visitadas e números de Fibonacci.

**Parâmetros:**
- `carta`: `tuple` - Tupla contendo a carta a ser atualizada.

**Retorna:**
- `bool` - `True` se a atualização foi bem-sucedida; caso contrário, `False`.

### `configura_indice_proximo_subgrupo(self, ponto: int) -> int`
Calcula o índice do próximo subgrupo com base em um ponto inicial, utilizando a regra dos Vortex.

**Parâmetros:**
- `ponto`: `int` - Ponto inicial para o cálculo do próximo subgrupo.

**Retorna:**
- `int` - O índice do próximo subgrupo calculado.

### `atualiza_lista_cartas_recomendadas(self, alfa, peso_probabilidade, peso_similaridade_exp, peso_similaridade_just, caderno_de_ouro, justificativa_usuario)`
Atualiza a lista de cartas recomendadas com base nos parâmetros fornecidos.

**Parâmetros:**
- `alfa`: `float` - Parâmetro para o cálculo de custo.
- `peso_probabilidade`: `float` - Peso atribuído à probabilidade.
- `peso_similaridade_exp`: `float` - Peso atribuído à similaridade esperada.
- `peso_similaridade_just`: `float` - Peso atribuído à similaridade justificada.
- `caderno_de_ouro`: `list` - Informações adicionais para a recomendação.
- `justificativa_usuario`: `str` - Justificativa fornecida pelo usuário.

### `retorna_melhor_carta(self, permissao_para_pular_Carta: bool = False) -> tuple`
Retorna a melhor carta atual e seu subgrupo associado, com a opção de pular a carta.

**Parâmetros:**
- `permissao_para_pular_Carta`: `bool` - Indica se a carta atual pode ser pulada.

**Retorna:**
- `tuple` - A tupla contendo a melhor carta atual e seu subgrupo.

### `escolher_carta(self, carta_atual=None)`
Seleciona a carta atual a ser atualizada no subgrupo, com base na melhor carta ou na carta fornecida.

**Parâmetros:**
- `carta_atual`: `tuple` ou `None` - A carta atual a ser escolhida; se `None`, usa a melhor carta.