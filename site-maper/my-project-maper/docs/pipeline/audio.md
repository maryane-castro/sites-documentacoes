# Devolutiva

## Descrição

Este módulo contém a implementação da classe AudioProcessor, que é responsável pelo processamento de áudio. A classe oferece funcionalidades para gerar arquivos de áudio a partir de texto(devolutiva), bem como para combinar esses arquivos, permitindo uma manipulação eficaz de conteúdos sonoros. Com um enfoque em flexibilidade e eficiência, a AudioProcessor facilita a integração de recursos de áudio em aplicações que demandam síntese e edição de som.


## Estrutura do Módulo
    audio/
        audio/TextToSpeechProcessor.py  # Classe para este módulo específico.
        audio/utils.py  # Arquivo com utilidades dedicadas a este módulo.
    TTS/
        Faça o clone do repositório TTS dentro da pasta audio e realize a instalação via pip.
    ...


## Uso

Aqui está um exemplo de utilização do módulo.

### Exemplo

```python
from audio.TextToSpeechProcessor import AudioProcessor
import json

# -> ÁUDIO
processor = AudioProcessor()
path_input = "./artifacts/resultado.json"  # nome do arquivo de entrada
with open(path_input, 'r', encoding='utf-8') as file:
    json_data = json.load(file)
text_devolutiva = json_data["saida"]

output_file = processor.process_text_to_audio(
    text_devolutiva,
    "./artifacts/audio_devolutiva.wav" # nome de saída do arquivo
)

```


## Funções e Classes Principais

### `AudioProcessor`

- **Descrição**: Classe para processamento de áudio, incluindo a geração de arquivos de áudio a partir de texto e a combinação desses arquivos.

- **Atributos**:
  - `model`: Instância do modelo TTS para síntese de fala, configurada com base em arquivos de configuração, vocabulário e ponto de verificação.

- **Parâmetros do Construtor**:
  - `tts_model_path (str)`: Caminho para o modelo TTS.
  - `gpu (bool)`: Se `True`, utiliza GPU para processamento; caso contrário, utiliza CPU.

- **Métodos Principais**:
  - `split_text_by_sentence(text)`: Divide o texto em sentenças, retornando uma lista de sentenças.
  - `process_and_save_audio(split_texts, output_path)`: Processa cada parte do texto em áudio e salva o áudio combinado em um arquivo especificado.
  - `process_text_to_audio(text, combined_output_path)`: Processa o texto em áudio combinado e salva o arquivo resultante.


## Testes

Você pode executar a pipeline completa com o seguinte comando

```bash
# Execute a pipeline completa
python main.py
```