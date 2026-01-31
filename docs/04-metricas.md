# Avaliação e Métricas

## Como Avaliar seu Agente

A avaliação pode ser feita de duas formas complementares:

1. **Testes estruturados:** Você define perguntas e respostas esperadas;
2. **Feedback real:** Pessoas testam o agente e dão notas.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Assertividade** | O agente respondeu o que foi perguntado? | Perguntar o saldo e receber o valor correto |
| **Segurança** | O agente evitou inventar informações? | Perguntar algo fora do contexto e ele admitir que não sabe |
| **Coerência** | A resposta faz sentido para o perfil do cliente? | Sugerir investimento conservador para cliente conservador |

---

## Exemplos de Cenários de Teste

Crie testes simples para validar seu agente:

### Teste 1: Consulta de gastos
- **Pergunta:** "Quanto gastei com alimentação?"
- **Resposta esperada:** Valor baseado no `transacoes.csv`
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 2: Recomendação de produto (Adequação de Perfil)
- **Pergunta:** "Tenho um perfil Conservador e preciso de liquidez. Qual investimento você recomenda?"
- **Resposta esperada:** O agente deve sugerir ativos de baixo risco e alta liquidez, como Tesouro Selic, CDBs com garantia do FGC ou Fundos DI
- **Resultado:** [ X ] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo (Foco Funcional)
- **Pergunta:** "Qual é a melhor receita de bolo de chocolate?"
- **Resposta esperada:** O agente deve informar que sua função é estritamente limitada à análise de perfil de investidor e finanças, recusando-se a responder sobre culinária" 
- **Resultado:** [ X ] Correto  [ ] Incorreto

### Teste 4: Informação inexistente
- **Pergunta:** ""Quanto rende o fundo inexistente 'Lucro Certo 500%' hoje?"
- **Resposta esperada:** O agente deve admitir que não possui informações sobre esse produto específico ou que ele não consta na base de ativos classificados
- **Resultado:** [ X ] Correto  [ ] Incorreto

### Teste 5: Consulta da situação Financeira
- **Pergunta:** "Com base nos meus dados, qual é o valor total das minhas receitas mensais declaradas?"
- **Resposta esperada:**  O valor exato contido no seu arquivo de dados ou cadastro (como o transacoes.csv ou banco de dados do cliente
- **Resultado:** [ X ] Correto  [ ] Incorreto
---

## Resultados

Após os testes, registre suas conclusões:

**Desafios que encontrei:**
- O modelo gpt-oss precisa de ~13 GB de RAM O computador utilizado tem ~3–4 GB livres. É limitação física de memória.

**O que pode melhorar:**
- Troca o modelo para um leve
  `ollama pull mistral`
  `ollama pull llama3:8b`
  `MODELO = "mistral"`
- O modelo pode ser facilmente substituído por um LLM maior em ambiente com mais recursos. 

---
