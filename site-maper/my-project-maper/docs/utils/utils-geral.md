# Utils Geral

Este módulo contém diversas funções utilitárias para o projeto MAPER. Essas funções são projetadas para facilitar o processamento de dados, a geração de saídas e a manipulação de arquivos. Os arquivos contendo funções mais complexas terão um documento especifíco.

## Estrutura do Módulo

O módulo `utils` é composto pelos seguintes arquivos:

- **calcular_resutado_maper.py**: Funções para calcular resultados do teste MAPER.
- **devolutive_plus_connection.py**: Conexões e manipulação de dados para devolutivas.
- **gerar_pdf_saida_pdi.py**: Geração de arquivos PDF a partir de Planos de Desenvolvimento Individual (PDI).
- **global_dict.py**: Dicionários globais e variáveis de configuração.
- **prompts.py**: Geração de prompts para feedbacks e gráficos baseados em dados de testes.
- **save_json_file.py**: Funções para salvar e abrir arquivos JSON.

## Uso

Cada arquivo no módulo `utils` contém funções específicas que podem ser importadas e utilizadas conforme necessário. Por exemplo:

```python
from utils.calcular_resutado_maper import calcular_resultado
from utils.save_json_file import save_json

# Exemplo de uso
resultado = calcular_resultado(dados)
save_json("resultado.json", resultado)
```