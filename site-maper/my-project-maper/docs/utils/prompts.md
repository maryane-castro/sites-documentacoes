
# Módulo Prompts

O módulo `prompts.py` é responsável por gerar prompts e feedbacks personalizados para o sistema de avaliação de desempenho e desenvolvimento pessoal, em conformidade com as diretrizes do teste MAPER. Este módulo integra funcionalidades de leitura de arquivos JSON, cálculo de índices e geração de textos para relatórios, proporcionando uma experiência de feedback clara e adaptada às necessidades do usuário.

## Estrutura do Módulo

O módulo contém as seguintes classes e funções:

### Classes

#### `GetPromptsFeedbackAndGraphics`

Esta classe é projetada para gerar prompts que fornecem feedbacks e descrições de gráficos baseados nos resultados de um teste, levando em conta as notas do usuário e seus dados pessoais.

**Construtor:**
- `__init__(self, nome: str, notas: dict, data_nascimento: str)`
    - **Parâmetros:**
        - `nome` (str): Nome do paciente.
        - `notas` (dict): Dicionário que contém as notas do paciente por competência.
        - `data_nascimento` (str): Data de nascimento do paciente.
    - **Descrição:** Inicializa a classe, carregando feedbacks de um arquivo JSON e calculando o índice geral do usuário.

**Métodos:**
- `_open_feedback_json()`
    - **Descrição:** Carrega os feedbacks e competências de arquivos JSON e retorna os dados.

- `_generate_feedbacks()`
    - **Descrição:** Gera feedbacks relevantes com base nas notas do paciente, filtrando os resultados do teste.

- `_gererate_general_index()`
    - **Descrição:** Calcula o índice geral do paciente com base nas notas médias.

- `_generate_score_mapertest_style()`
    - **Descrição:** Gera uma nota para cada estilo do teste MAPER com base nas competências do usuário.

- `get_graphics_and_score_prompt()`
    - **Descrição:** Cria um prompt detalhado que resume os resultados do teste, incluindo gráficos e análises de desempenho.

- `get_feedbacks_prompt()`
    - **Descrição:** Retorna um prompt contendo feedbacks personalizados sobre as competências avaliadas.


### Funções

#### `get_merge_prompt(sections, profession, sex, birthday)`

Esta função cria um prompt que une diferentes seções de feedback em um texto contínuo, utilizando conectivos para garantir fluidez e coerência.

- **Parâmetros:**
    - `sections` (list): Lista contendo as seções de feedback.
    - `profession` (str): Profissão do usuário.
    - `sex` (str): Gênero do usuário.
    - `birthday` (str): Data de nascimento do usuário.
- **Retorno:**
    - Um prompt que combina as seções e adapta o texto para manter um tom conversacional, sem repetições.

## Uso do Módulo

Para utilizar o módulo, você deve importá-lo em seu script Python e instanciar a classe `GetPromptsFeedbackAndGraphics`. Você pode então chamar os métodos para gerar feedbacks e gráficos personalizados. A função `get_merge_prompt` pode ser usada para combinar os feedbacks em um texto único, garantindo uma apresentação clara e coerente das informações.

### Exemplo de Uso

```python
from utils import save_json_file
from utils.prompts import GetPromptsFeedbackAndGraphics, get_merge_prompt

# Criar uma instância da classe
feedback_generator = GetPromptsFeedbackAndGraphics(nome="João", notas={"competencia_1": {"nota": 8, "status": "ideal"}}, data_nascimento="01/01/1990")

# Gerar o prompt de gráficos e notas
graphics_prompt = feedback_generator.get_graphics_and_score_prompt()

# Gerar feedbacks
feedback_prompt = feedback_generator.get_feedbacks_prompt()

# Unir feedbacks em um único texto
merged_prompt, additional_section = get_merge_prompt(feedback_prompt, profession="Engenheiro", sex="Masculino", birthday="01/01/1990")
```

## Conclusão

O módulo `prompts.py` é uma ferramenta essencial para a personalização de feedbacks no contexto do teste MAPER, permitindo que usuários recebam informações detalhadas e adaptadas ao seu desempenho. A integração com arquivos JSON facilita a atualização e manutenção dos dados utilizados nos feedbacks.


