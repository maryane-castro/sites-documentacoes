# Devolutiva

## Descrição

Este script Python foi projetado para gerar devolutivas completas e personalizadas, utilizando dados de pacientes e notas de competências. Com o suporte de um modelo de linguagem avançado da família LLAMA/GROQ, o sistema é capaz de processar e interpretar informações complexas, resultando em relatórios detalhados que atendem às necessidades individuais de cada paciente.

A ferramenta visa facilitar o acompanhamento e a avaliação do desempenho, oferecendo feedbacks construtivos e direcionados. Com isso, busca-se contribuir para o desenvolvimento contínuo das competências, promovendo uma abordagem mais eficaz no gerenciamento de informações e no suporte aos pacientes.


## Estrutura do Módulo
    model/
        llm_models.py  # Contém as classes responsáveis pela criação e instanciação dos modelos de linguagem (LLM).
        
    utils/
        prompts.py  # Armazena os prompts e alguns métodos para gerar a devolutiva.
        save_json_file.py  # Salva o resultado da devolutiva em um arquivo JSON.
    ...


## Uso

Aqui está um exemplo de utilização do módulo.

### Exemplo

```python
from pipeline.DevolutivaGenerator import DevolutivaGenerator
from utils.calcular_resutado_maper import calc_resul_maper


groq_key = "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"

respostas_usuario = {
    "nome_usuario": "Jessyca",
    "respostas": ["b","b","a","b","b","a","b","b","b","a","a","b","a","b","a","a","b","a","a","a","a","b","a","a","a","a","b","b","a","a","b","a","b","a","a","b","a","a","b","b","b","a","b","b","b","a","b","b","b","a","b","b","b","a","a","a","a","a","a","a","b","b","b","b","b","b","b","b","a","b","b","b","b","a","a","a","a","b","b","b","a","b","a","b","b","a","a","a","a","a","a","a","a","b","b","a","a","b","a","b"
    ],
    "sexo": "feminino",
    "data_nascimento": "12/05/1990",
    "profissao": "professora"
}

# -> CALCULAR MAPPER TESTE
resultado, grades_notas_maper = calc_resul_maper(
            respostas_usuario['nome_usuario'],
            respostas_usuario['data_nascimento'],
            respostas_usuario["respostas"],
        )


# -> DEVOLUTIVA
print(grades_notas_maper)
devolutiva_generator = DevolutivaGenerator(respostas_usuario["nome_usuario"], 
                                           respostas_usuario["data_nascimento"],
                                           respostas_usuario["profissao"],
                                           respostas_usuario["sexo"],
                                           grades_notas_maper,
                                           groq_key)

resultado = devolutiva_generator.generate_devolutiva()
print(resultado)
```


## Funções e Classes Principais

### `DevolutivaGenerator`

- **Descrição**: Classe para a geração de devolutivas completas a partir de dados de pacientes.
- **Parâmetros do Construtor**:
  - `name (str)`: Nome do paciente.
  - `birthday (str)`: Data de aniversário do paciente.
  - `profession (str)`: Profissão do paciente.
  - `sex (str)`: Gênero do paciente.
  - `grades (dict)`: Dicionário contendo as notas de cada competência.
  - `groq_key (str)`: Chave de acesso ao modelo IA Groq.

- **Métodos Principais**:
  - `generate_devolutiva()`: Método que executa o pipeline completo de geração da devolutiva, retornando um texto consolidado.

- **Métodos Privados**:
  - `__generate_presentation_section()`: Gera a seção de apresentação da devolutiva.
  - `__generate_competence_section()`: Gera a seção que aborda comentários sobre as notas de cada competência.
  - `__generate_graphs_section()`: Gera a seção que aborda comentários sobre os gráficos apresentados no PDI.
  - `__generate_ending_section()`: Gera a seção de encerramento da devolutiva.
  - `__merge_sections(sections)`: Une o texto de cada seção da devolutiva em um só.


## Testes

Você pode executar a pipeline completa com o seguinte comando

```bash
# Execute a pipeline completa
python main.py
```