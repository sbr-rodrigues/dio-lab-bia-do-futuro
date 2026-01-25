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
Para simplificar, podermos "injetar" os dados no prompt, garantindo o melhor contexto possível. O ideal que estas informações sejam carregadas dinamicamente para obter flexibilidade.

```text
PERFIL DO CLIENTE (data/perfil_investidor.json):
{
  "nome": "Dominic Ferreira",
  "idade": 32,
  "profissao": "Analista de Sistemas",
  "renda_mensal": 5000.00,
  "perfil_investidor": "moderado",
  "objetivo_principal": "Construir reserva de emergência",
  "patrimonio_total": 15000.00,
  "reserva_emergencia_atual": 10000.00,
  "aceita_risco": false,
  "metas": [
    {
      "meta": "Completar reserva de emergência",
      "valor_necessario": 15000.00,
      "prazo": "2026-06"
    },
    {
      "meta": "Entrada do apartamento",
      "valor_necessario": 50000.00,
      "prazo": "2027-12"
    }
  ]
}

HISTORICO DO CLIENTE (data/historico_atendimento.csv):
data,canal,tema,resumo,resolvido
2025-09-15,chat,CDB,Cliente perguntou sobre rentabilidade e prazos,sim
2025-09-22,telefone,Problema no app,Erro ao visualizar extrato foi corrigido,sim
2025-10-01,chat,Tesouro Selic,Cliente pediu explicação sobre o funcionamento do Tesouro Direto,sim
2025-10-12,chat,Metas financeiras,Cliente acompanhou o progresso da reserva de emergência,sim
2025-10-25,email,Atualização cadastral,Cliente atualizou e-mail e telefone,sim

TRANSACOES DO CLIENTE (data/transacoes.csv):
data,descricao,categoria,valor,tipo
2025-10-01,Salário,receita,5000.00,entrada
2025-10-02,Aluguel,moradia,1200.00,saida
2025-10-03,Supermercado,alimentacao,450.00,saida
2025-10-05,Netflix,lazer,55.90,saida
2025-10-07,Farmácia,saude,89.00,saida
2025-10-10,Restaurante,alimentacao,120.00,saida
2025-10-12,Uber,transporte,45.00,saida
2025-10-15,Conta de Luz,moradia,180.00,saida
2025-10-20,Academia,saude,99.00,saida
2025-10-25,Combustível,transporte,250.00,saida

PRODUTOS FINANCEIROS (data/produtos_financeiros.json):
[
  {
    "nome": "Tesouro Selic",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "100% da Selic",
    "aporte_minimo": 30.00,
    "indicado_para": "Reserva de emergência e iniciantes"
  },
  {
    "nome": "CDB Liquidez Diária",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "102% do CDI",
    "aporte_minimo": 100.00,
    "indicado_para": "Quem busca segurança com rendimento diário"
  },
  {
    "nome": "LCI/LCA",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "95% do CDI",
    "aporte_minimo": 1000.00,
    "indicado_para": "Quem pode esperar 90 dias (isento de IR)"
  },
  {
    "nome": "Fundo Multimercado",
    "categoria": "fundo",
    "risco": "medio",
    "rentabilidade": "CDI + 2%",
    "aporte_minimo": 500.00,
    "indicado_para": "Perfil moderado que busca diversificação"
  },
  {
    "nome": "Tesouro IPCA+",
    "categoria": "renda_fixa",
    "risco": "medio",
    "rentabilidade": "IPCA + Taxa Fixa",
    "aporte_minimo": 40.00,
    "indicado_para": "Proteção contra a inflação no longo prazo"
  },
  {
    "nome": "Fundos Imobiliários (FIIs)",
    "categoria": "renda_variavel",
    "risco": "medio_alto",
    "rentabilidade": "Dividendos + Valorização",
    "aporte_minimo": 10.00,
    "indicado_para": "Geração de renda mensal e diversificação imobiliária"
  },
   {
    "nome": "ETFs (Ex: IVVB11 ou BOVA11)",
    "categoria": "renda_variavel",
    "risco": "alto",
    "rentabilidade": "Variação do Índice",
    "aporte_minimo": 100.00,
    "indicado_para": "Diversificação em índices de ações com baixo custo"
  },
    {
    "nome": "Criptoativos (Bitcoin/Ethereum)",
    "categoria": "renda_variavel",
    "risco": "muito_alto",
    "rentabilidade": "Alta Volatilidade",
    "aporte_minimo": 1.00,
    "indicado_para": "Perfil agressivo buscando ganhos exponenciais"
  },
  {
    "nome": "Fundo de Ações",
    "categoria": "fundo",
    "risco": "alto",
    "rentabilidade": "Variável",
    "aporte_minimo": 100.00,
    "indicado_para": "Perfil arrojado com foco no longo prazo"
  }
]
```

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.
O exemplo abaixo encontra se na base de conhecimento, sintetizados com isso otimizando o consumo de tokens. Ressaltando todas as informações relevantes.
```
Dados do Cliente:
- Nome: Dominic Ferreira
- Perfil: Moderado
- Saldo disponível: R$ 100.000,00 (meta: R$ 500.000,00)
- Objetivo: Casa própria

Últimas transações:
- 01/11: Supermercado - R$ 450,00
- 03/11: Streaming - R$ 55,00
- 10/11: Gamaboy - R$ 39,99
- 10/11: Farmácia - R$ 164,99
- 15/11: Internet - R& 130,00
- 15/11: Viagem - R$ 210,00
- 20/11: Aluguel - R& 1.300,00
- 25/11: Roupas e acessórios: R$ 66,00
- 27/11: Combustível: R$ 120,00

Produtos financeiros:
- Tesouro Selic: Risco baixo
- CDB (Certificado de Depósito Bancário): Risco baixo
- LCI e LCA: Risco baixo
- Tesouro IPCA+: Risco médio
-  Fundos Multimercado: Risco médio
- Debêntures: Risco médio
- Fundos Imobiliários (FIIs): Risco médio a alto
- Ações: Risco alto
- ETFs (Índices): Risco alto
- COE (Certificado de Operações Estruturadas): Risco alto/complexo
- Criptoativos (Bitcoin/Ethereum): Risco muito alto
- Derivativos (Opções e Futuros): Risco muito alto

...
```
