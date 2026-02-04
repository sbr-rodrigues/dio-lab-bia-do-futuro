# 💰 Bayan — Agente Inteligente de Finanças

Bayan é um agente virtual especializado em **análise de perfil de investidor (Suitability)**, desenvolvido para simular interações financeiras inteligentes com base em dados estruturados de clientes.

O projeto demonstra, de forma prática, a construção de um chatbot financeiro utilizando **Python + Streamlit + Integração com LLM (Ollama)**, com foco em orientação de investimentos, liquidez e classificação de risco.

---

## 🎯 Objetivo do Projeto

Criar um agente capaz de:

* Analisar perfil do investidor
* Classificar risco (Conservador, Moderado ou Arrojado)
* Avaliar liquidez e adequação de produtos
* Simular recomendações financeiras
* Alertar sobre riscos e desenquadramento de perfil

---

## 🧠 Conceitos Aplicados

* Suitability (Análise de Perfil do Investidor)
* Educação financeira
* Liquidez vs Rentabilidade
* Risco de mercado
* Conformidade regulatória

---

## 🛠️ Tecnologias Utilizadas

* **Python**
* **Streamlit** — Interface conversacional
* **Pandas** — Manipulação de dados
* **JSON / CSV** — Base de conhecimento
* **Requests** — Integração API
* **Ollama (LLM local)** — Inteligência generativa

---

## 📂 Estrutura de Documentação

* **Documentação do Agente

* **Base de Conhecimento

* **Prompts

* **Métricas de Avaliação

* **Pitch do Projeto

---

## 📂 Estrutura do Projeto

```
📁 data/
 ├─ perfil_investidor.json
 ├─ transacoes.csv
 ├─ historico_atendimento.csv
 └─ produtos_financeiros.json

📁 src/
 └─ app.py

README.md
requirements.txt
```
## 🧠 Arquitetura da Solução

O projeto foi estruturado de forma modular, contendo:

- Interface em Streamlit

- Base de conhecimento financeira

- Documentação do agente

- Prompts estruturados

- Métricas de avaliação

- Simulação de respostas via LLM / fallback

Isso permite trocar o modelo de linguagem conforme a capacidade da máquina.

---

## ▶️ Como Executar

1️⃣ Clone o repositório

```bash
git clone https://github.com/sbr-rodrigues/dio-lab-bia-do-futuro.git
```

2️⃣ Acesse a pasta

```bash
cd dio-lab-bia-do-futuro
```

3️⃣ Instale as dependências

```bash
pip install -r requirements.txt
```

4️⃣ Execute o Streamlit

```bash
streamlit run src/app.py
```

---

## 🤖 Integração com LLM

O projeto suporta execução com modelos locais via **Ollama**.

Exemplo de modelos compatíveis:

* mistral
* llama3
* phi

> Observação: Para demonstrações em máquinas com pouca RAM, foi implementado **modo simulado (demo)** para garantir funcionamento da interface.

---

## 💬 Exemplos de Interação

**Pergunta:**
Tenho perfil conservador e preciso de liquidez. Qual investimento recomenda?

**Resposta esperada:**
Tesouro Selic e CDB com liquidez diária, priorizando segurança e resgate rápido.

---

**Pergunta fora do escopo:**
Qual a melhor receita de bolo de chocolate?

**Resposta:**
O agente informa que responde apenas temas financeiros.

---

## 📸 Demonstração

O sistema opera em formato de chat, permitindo perguntas sobre:

* Investimentos
* Liquidez
* Perfil de risco
* Gastos financeiros

---
## 📊 Resultados Esperados

Maior adequação entre perfil e investimento

Redução de recomendações incompatíveis

Educação financeira para o investidor

Transparência no processo de decisão

---

## 🚀 Evoluções Futuras

* Memória conversacional
* Upload de extratos
* Dashboards financeiros
* Integração com APIs bancárias
* Recomendação automática de carteira

---

## 👩‍💻 Autoria

Desenvolvido por **Sabrina Rodrigues**
Projeto educacional — DIO Lab BIA do Futuro

---

## 📜 Licença

Uso educacional e demonstrativo.

 ---

 ## 🎥 Demonstração da Solução

Assista ao vídeo do pitch e demonstração do Bayan funcionando:

👉 https://youtu.be/Z2uW5sPgg9Y
