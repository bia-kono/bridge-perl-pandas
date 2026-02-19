# Bridge Perl-Pandas: Migração NFe

Projeto focado na migração de lógica ETL legada em Perl para o ecossistema moderno de Dados em Python.

### Objetivos do Projeto
1. **Tradução de Código:** Converter `nfe_entrada.pl` para Python utilizando Pandas.
2. **Transformação SQL:** Implementar lógicas complexas com CTEs e Window Functions.
3. **Containerização:** Dockerizar o ambiente para garantir reprodutibilidade (DataOps).

### Tecnologias
* Python 3.12.2 (pyenv)
* Pandas
* Perl
* Docker

### Como rodar o ambiente
1. Ative o ambiente virtual: `source .venv/bin/activate`
2. Instale as dependências: `pip install -r requirements.txt`
