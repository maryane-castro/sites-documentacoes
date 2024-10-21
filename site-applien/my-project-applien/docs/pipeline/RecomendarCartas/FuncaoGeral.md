# Função Geral

## Descrição
Este conjunto de instruções busca unificar os elementos desenvolvidos do projeto desde o carregamento dos dados a utilização do sistema de recomendação.

### `recomendacaoOuPulo(app_recomendacao, caderno_de_ouro, justificativa_do_usuario, intensidade_do_sentimento, carta_atual)`
Atualiza o fluxo do sistema para o próximo subgrupo, caso a permissão seja concedida. Nesse sistema, a recomendação de carta é baseada em critério como o sentimento de usuário.

**Parâmetros:**
- `app_recomendacao`: `SistemaRecomendacao` - Instância da classe do Sistema de Recomendação utilizada para recomendar a carta.
- `caderno_de_ouro`: `list` - Uma lista de três elementos de string onde cada elemento é uma resposta do usuário.
- `justificativa_do_usuario`: `list` - Uma lista de três elementos de string contendo as justificativas do usuário para cada uma das respostas do `caderno_de_ouro`.
- `intensidade_do_sentimento`: `list` - Intensidade do sentimento gerado pela carta indicada.
- `carta_atual`: `string` - Uma string contendo a carta com a atividade.

**Retorna:**
- `(carta, string)`:`tuple` - Uma tupla contendo a carta indica para o usuário e uma string contendo informações do nome do subgrupo atual e o seu ID (tanto o nome como o ID estão na mesma string).

### `main(app_recomendacao, resposta1, resposta2, resposta3, justificativa1)`
Função responsável por agrupar todos os componentes do projeto.

**Parâmetros:**
- `app_recomendacao`: `SistemaRecomendacao` - Instância da classe do Sistema de Recomendação utilizada para recomendar a carta.
- `resposta1`: `string` - String contendo a primeira resposta dada pelo usuário.
- `resposta2`: `string` - String contendo a segunda resposta dada pelo usuário.
- `resposta3`: `string` - String contendo a terceira resposta dada pelo usuário.
- `justificativa1`: `string` - Uma string contendo a justificativa da `resposta1'` indicada pelo usuário.
**Retorna:**
- `recomendacao_carta_result`:`string` - A string contendo a carta indicada pelo sistema.
