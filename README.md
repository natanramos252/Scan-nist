# 🔍 CVE Scanner

Scanner automatizado de vulnerabilidades (CVEs) para ativos de infraestrutura, utilizando a API pública do [NVD (National Vulnerability Database)](https://nvd.nist.gov/) via `nvdlib`.

## 📋 Funcionalidades

- Consulta CVEs por CPE (Common Platform Enumeration) para ativos cadastrados
- Busca adicional por keyword (ex: Chromium)
- Cache inteligente: rebusca dados apenas a cada 3 dias
- Na primeira execução, carrega todo o histórico disponível
- Nas execuções seguintes, busca apenas CVEs novos desde o último scan
- Exporta resultados em `.csv` e `.xlsx` com data

## 🖥️ Ativos monitorados (padrão)

| CPE | Ativo |
|-----|-------|
| `cpe:2.3:o:canonical:ubuntu_linux:24.04` | Ubuntu Linux 24.04 LTS |
| `cpe:2.3:o:redhat:enterprise_linux:7.0` | Red Hat Enterprise Linux 7 |
| `cpe:2.3:a:clickhouse:clickhouse:24.3.3.102` | ClickHouse 24.3.3 |
| `cpe:2.3:h:cisco:meraki_mx` | Cisco Meraki MX |
| `chromium` (keyword) | Chromium |

## 🚀 Como usar

### 1. Clone o repositório

```bash
git clone https://github.com/seu-usuario/cve-scanner.git
cd cve-scanner
```

### 2. Instale as dependências

```bash
pip install -r requirements.txt
```

### 3. Execute o scanner

```bash
python scan_cvesServer.py
```

### Saída gerada

| Arquivo | Descrição |
|---------|-----------|
| `cve.csv` | Base de dados acumulada de CVEs |
| `cves_YYYYMMDD.xlsx` | Relatório do dia em Excel |
| `ultima_atualizacao.txt` | Controle de cache |

## ⚙️ Configuração

Para monitorar outros ativos, edite a lista `ativos` no início do script com os CPEs desejados:

```python
ativos = [
    "cpe:2.3:o:canonical:ubuntu_linux:24.04:*:*:*:lts:*:*:*",
    # adicione seus CPEs aqui
]
```

> 💡 Você pode buscar CPEs válidos em: https://nvd.nist.gov/products/cpe/search

## 📦 Dependências

- [nvdlib](https://github.com/vehemont/nvdlib)
- [pandas](https://pandas.pydata.org/)
- [openpyxl](https://openpyxl.readthedocs.io/)

## ⚠️ Limites da API

A API pública do NVD tem limite de **5 requisições por 30 segundos** sem chave de API. Para uso intensivo, [solicite uma API Key](https://nvd.nist.gov/developers/request-an-api-key) gratuita e configure-a no `nvdlib`.

## 📄 Licença

MIT
