# bridge-perl-pandas: Migração de dados legados Perl para Python (nfe, log e pessoa)
Este projeto é uma demonstração prática e enxuta da migração de scripts ETL legados em Perl para Python utilizando Pandas e NumPy com aplicação de práticas de DataOps.  
> Meu objetivo é transformar os scripts legados (`.pl`) em um pipeline moderno e escalável. Os dados são gerados com a biblioteca Faker, processados em memória e organizados em uma estrutura que simula um Lakehouse local com camadas Bronze, Silver e Gold.
---

## Escopo
1. Tradução dos códigos legados  
   Migração dos scripts Perl (`nfe.pl`, `log.pl`, `pessoa.pl`) para Python, usando Pandas para leitura e transformação dos dados.
3. Pipeline ETL em módulos  
   Organização do código em módulos (`extract → transform → load`) para facilitar a manutenção, os testes e a escalabilidade.
3. Simulação do Lakehouse - Os dados são processados em memória e organizados em camadas para simular um ambiente profissional
   * raw → Bronze (dados brutos)
   * processed → Silver (dados limpos e transformados)
   * curated → Gold (dados finais para análise)
4. DataOps e containerização  
   * Docker é usado para garantir que o ambiente possa ser reproduzido, independente do sistema operacional utilizado.
   * Planejado para integração futura com Kubernetes.
---

## Estrutura do Projeto
```text
bridge-perl-pandas/
├── src/                         ← Código Python
│   └── bridge/
│       ├── extract/             ← Leitura/Extração (Aplicação ETL)
│       │   ├── nfe_reader.py
│       │   ├── log_reader.py
│       │   └── pessoa_reader.py
│       │
│       ├── transform/           ← Limpeza e transformação (Aplicação ETL)
│       │   ├── nfe_transform.py
│       │   ├── log_transform.py
│       │   └── pessoa_transform.py
│       │
│       ├── load/                ← Carregamento (Aplicação ETL)
│       │   └── lakehouse_loader.py
│       │
│       ├── mock/                ← Gerador de dados
│       │   ├── nfe_mock.py
│       │   ├── log_mock.py
│       │   └── pessoa_mock.py
│       │
│       ├── utils/               
│       │   └── validators.py
│       │
│       └── pipeline.py          
│
├── data/                        ← Lakehouse local
│   ├── raw/                     ← Bronze (dados gerados pelos mocks)
│   ├── processed/               ← Silver (dados transformados)
│   └── curated/                 ← Gold (dados para análise)
│
├── tests/                        ← Testes unitários
│   ├── extract/
│   ├── transform/
│   └── load/
│
├── legacy_code/                  ← Scripts legados (Perl)
│   ├── nfe.pl
│   ├── log.pl
│   └── pessoa.pl
│
├── Dockerfile                    ← Ambiente containerizado
├── requirements.txt              ← Dependências Python
├── README.md
└── .gitignore
```
---

## Stack Utilizada
- Python 3.12.2 - Via [Pyenv](https://github.com/pyenv/pyenv) (gerenciador de versões do Python em ambiente isolado)
- Pandas & NumPy – manipulação e transformação de dados
- Faker – geração de dados mock
- Docker – containerização do ambiente
- Kubernetes (planejado) – orquestração de containers
- Delta Lakehouse (simulado localmente) – persistência estruturada em camadas
- Perl – scripts legados
- Pytest – testes unitários
---

## Como rodar o projeto?
1. **Configurando o ambiente**
   1. Antes de tudo, instale o Pyenv ([Doc Oficial](https://github.com/pyenv/pyenv))
   ```bash
    # Exemplo: macOS          # Exemplo:Linux (Ubuntu/Debian)
    → brew install pyenv      → curl https://pyenv.run | bash

    # Instale a versão
    → pyenv install 3.12.2
    
    # Defina a versão do Python local
    → pyenv local 3.12.2
    
    # Crie o ambiente virtual
    → python -m venv .venv
    
    # Ative o ambiente virtual (.venv)
    → source .venv/bin/activate
    
    # Instale as dependências
    → pip install -r requirements.txt
    ``` 
2. **Executando o pipeline**
    ```bash
    # Rode o pipeline
        → python src/bridge/pipeline.py

    # Rode os testes unitários
        → pytest tests/
    ```