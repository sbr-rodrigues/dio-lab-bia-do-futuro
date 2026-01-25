# Base de Conhecimento

## Dados Utilizados

Descreva se usou os arquivos da pasta `data`, por exemplo:

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Mantém o contexto de conversas passadas, evitando que o cliente precise repetir informações e garantindo fluidez.|
| `perfil_investidor.json` | JSON | Define os parâmetros e pesos das respostas do quiz para classificar o cliente (Conservador, Moderado ou Arrojado). |
| `produtos_financeiros.json` | JSON | Catálogo técnico de investimentos (risco, rentabilidade e carência) para cruzamento com o perfil do cliente. |
| `transacoes.csv` | CSV | Analisa o fluxo de caixa e padrões de consumo para validar se a capacidade de investimento é compatível com o perfil declarado. |

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

Pesquisa de perfil de investidor a inclusão de novos produtos financeiros baseados nas fontes, como títulos de inflação, renda variável e ativos internacionais afim de enriquecer o teste.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.
Existem duas possibilidades: injetar diretamente no prompt (Ctrl + C, Ctrl + V) ou carregar via código, como no exemplo abaixo:
 
```python
import pandas as pd
import json

# CSVs
histórico = pd.read_csv('data/historico_atendimento.csv')
transações = pd.read_csv('data/transacoes.csv')

# JSONs
with open('data/perfil investidor.json', 'r', encoding='utf-8') as f:
	perfil = json.load(f)
with open('data/produtos financeiros.json', 'r', encoding='utf-8') as f:
	produtos = json.load(f)

```

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

```text
PERFIL DO CLIENTE:

HISTORICO DO CLIENTE:

TRANSACOES DO CLIENTE:

PRODUTOS FINANCEIROS:
```

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Dados do Cliente:
- Nome: João Silva
- Perfil: Moderado
- Saldo disponível: R$ 5.000

Últimas transações:
- 01/11: Supermercado - R$ 450
- 03/11: Streaming - R$ 55
...
```
