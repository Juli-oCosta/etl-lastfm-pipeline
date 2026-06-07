# 🎵 Last.fm ETL Data Pipeline

## 📌 Sobre o Projeto
Este projeto é um pipeline completo de Engenharia de Dados (ETL) focado na extração, tratamento e modelagem de dados de consumo musical utilizando a API pública do Last.fm. O objetivo é transformar dados comportamentais brutos (scrobbles, tags da comunidade e popularidade global) em inteligência de negócios através de um modelo relacional (Star Schema) consumido por dashboards interativos no Power BI.

A arquitetura foi desenhada para permitir análises em três camadas:
1. **Macro:** O ecossistema global de gêneros musicais.
2. **Meso:** O domínio do estilo (Top artistas e faixas dentro de nichos como Progressive Rock, Post-Punk, Dark Folk, etc.).
3. **Micro:** Deep dive no perfil do artista e suas redes de similaridade.

## 🛠️ Tecnologias Utilizadas
* **Linguagem:** Python 3
* **Extração (Extract):** `requests`, API REST (Last.fm)
* **Transformação (Transform):** `pandas`, `python-dotenv`
* **Carga (Load):** `sqlite3` (Banco de Dados Relacional Local)
* **Visualização (BI):** Microsoft Power BI
* **Ambiente & Versionamento:** VS Code, Jupyter Notebook, Git & GitHub

## 📂 Arquitetura do Repositório
O projeto segue as melhores práticas de organização de diretórios para pipelines de dados:

```text
├── data/
│   ├── raw/             # Dados brutos extraídos da API (.json) - Não versionado
│   └── processed/       # Dados limpos e modelados (.csv/.parquet) - Não versionado
├── notebooks/           # Cadernos Jupyter para exploração e Prova de Conceito (PoC)
├── src/                 # Scripts de produção do pipeline
│   ├── extract.py       # Conexão com API e coleta de dados
│   ├── transform.py     # Limpeza e achatamento de listas com Pandas
│   ├── load.py          # Ingestão dos dados no SQLite
│   └── main.py          # Gatilho orquestrador do fluxo completo
├── .env.example         # Template seguro para variáveis de ambiente
├── .gitignore           # Regras de segurança de versionamento
├── requirements.txt     # Dependências do projeto
└── README.md            # Documentação oficial
```

## 🚀 Como Executar o Projeto

1. Clone o repositório e acesse a pasta: git clone [https://github.com/Juli-oCosta/etl-lastfm-pipeline.git](https://github.com/Juli-oCosta/etl-lastfm-pipeline.git)
cd etl-lastfm-pipeline

2. Crie e ative seu ambiente virtual (Recomendado)
python -m venv venv

# No Windows:
venv\Scripts\activate

# No Linux/Mac:
source venv/bin/activate

3. Instale as dependências
pip install -r requirements.txt

4. Configure as Variáveis de Ambiente
* Crie uma conta de desenvolvedor no Last.fm API.
* Crie um arquivo .env na raiz do projeto.
* Adicione a sua chave no formato: LASTFM_API_KEY=sua_chave_aqui

5. Execute o Pipeline: python src/main.py

## 📊 Estrutura do Banco de Dados (Star Schema)
Os dados processados são carregados no arquivo banco_musical.db (SQLite), estruturados nas seguintes tabelas para consumo otimizado via Power Query:

dim_artistas: ID, Nome, Ouvintes Totais

dim_tags: ID, Nome da Tag

fato_artista_tag: Relacionamento (N:N) e métricas absolutas (Scrobbles)

Desenvolvido por Julio Cesar