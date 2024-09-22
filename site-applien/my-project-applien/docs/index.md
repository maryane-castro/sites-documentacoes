# NUVEN - IA APPLIEN
<p align="center">
    <img src="assets/logo.png" alt="Descrição da Imagem" width="300">
</p>

Bem-vindo à documentação do projeto **IA APPLIEN**.

## 📚 Sobre o Repositório

Este repositório contém o código da Prova de Conceito (POC) do **IA APPLIEN**. Aqui você encontrará todas as informações necessárias para configurar e utilizar o projeto.



## 🎲 Pré-Requisitos

Antes de começar, verifique se você atende aos seguintes pré-requisitos:

- Gerenciador de ambientes Conda instalado.
- CUDA Toolkit 11.8 ou superior instalado (caso o ambiente rode em GPU).
- Gerenciador de pacotes `pip` instalado.

## 💿 Instalação

Siga as etapas abaixo para configurar o ambiente de desenvolvimento:

### 1. Clone o repositório

Clone este repositório para o seu sistema local:

```bash
git clone https://github.com/nuven-applien/applien-ia.git
```

### 2. Crie um ambiente via `conda`

Crie um ambiente Python 3.10.0 com o Conda:

```bash
conda create -n IAPPLIEN python=3.10.0
```

### 3. Instale as dependências do projeto

Ative o ambiente criado e instale as dependências:

```bash
pip install -r requirements.txt
```


## Estrutura do projeto
    ├── artefatos
    │   ├── base-dados-aleatória-alternativas.json
    │   ├── cartas.json
    │   ├── cartas_transformadas_fibonacci.json
    │   ├── df_deteccao_anomalia.json
    │   └── df_subgrupos.json
    ├── artefatos_usuario
    │   └── cartoes_selecionados_usuario.json
    ├── assets
    │   └── logo.png
    ├── help.txt
    ├── main.py
    ├── model
    │   ├── modeloCbow.py
    │   └── __pycache__
    │       └── modeloCbow.cpython-39.pyc
    ├── README.md
    ├── Recomendar_Cartas
    │   ├── analise_Sentimento_LLAMA
    │   │   └── Analise_Sentimento_LLAMA.py
    │   ├── detectar_Anomalia
    │   │   ├── Detectar_Anomalia.py
    │   │   └── __pycache__
    │   │       └── Detectar_Anomalia.cpython-39.pyc
    │   ├── funcao_Recomendar_Cartas.py
    │   ├── mainRecomendar_Cartas.py
    │   └── sistema_Recomendacao
    │       ├── __pycache__
    │       │   ├── Recomendar_Carta.cpython-39.pyc
    │       │   └── Sistema_Recomendacao.cpython-39.pyc
    │       └── Sistema_Recomendacao.py
    ├── requirements.txt
    ├── Selecionar_Cartas_do_Usuario
    │   ├── mainSelecionar_Cartas.py
    │   ├── __pycache__
    │   │   └── Selecionar_Cartas.cpython-39.pyc
    │   └── Selecionar_Cartas.py
    ├── Sugerir_Primeiras_Cartas
    │   ├── mainSugerir_Primeiras_Cartas.py
    │   ├── Pular_Primeiras_Cartas.py
    │   ├── __pycache__
    │   │   ├── Pular_Primeiras_Carta.cpython-39.pyc
    │   │   └── Sugerir_Primeira_Carta.cpython-39.pyc
    │   └── Sugerir_Primeira_Carta.py
    └── utils
        ├── caixaDeFerramentas.py
        ├── carregarJson.py
        ├── preProcessamento.py
        ├── __pycache__
        │   ├── caixaDeFerramentas.cpython-39.pyc
        │   ├── carregarJson.cpython-39.pyc
        │   ├── preProcessamento.cpython-39.pyc
        │   ├── removerAlternativas.cpython-39.pyc
        │   └── sistemaSemantico.cpython-39.pyc
        ├── removerAlternativas.py
        └── sistemaSemantico.py
