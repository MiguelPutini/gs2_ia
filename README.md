# Citizen Assist AI — Assistente Digital de Orientação ao Cidadão
**Global Solutions — Prompt and Artificial Intelligence**

**Integrantes do Grupo:**
- Miguel Putini — RM 571624
- Alexandre Rizzi — RM 569621
- Lucas Klein de Veiga — RM 570029

---

## 1. Visão Geral dos Entregáveis

Este repositório contém o pacote completo de entrega do projeto **Citizen Assist AI**, conforme exigido pelo enunciado da Global Solution:

| Arquivo / Pasta | Descrição |
| --- | --- |
| `citizen_assist_ai.ipynb` | Notebook executado de ponta a ponta no Google Colab com as fichas oficiais, agente LangGraph (v1 baseline e v2 melhorado), pipeline de LLM as a Judge, resultados empíricos nas 26 mensagens (+6 extras), e cálculo dos indicadores de testes com usuários. |
| `relatorio_citizen_assist_ai.docx` | Relatório executivo completo em formato Word (.docx), contendo arquitetura, justificativas, análise detalhada de erros do v1, comparativo antes x depois, testes com usuários e limitações (100% preenchido e formatado, sem pendências). |
| `arquitetura.png` | Diagrama do fluxo do agente LangGraph (8 nós, guardas determinísticas, sanitização e desvios condicionais). |
| `golden_dataset.csv` | Dataset de avaliação contendo as 26 mensagens obrigatórias do enunciado mais 6 mensagens extras do grupo (32 itens no total). |
| `testes_usuarios.csv` | Registros dos testes de usabilidade com 6 participantes externos (P01 a P06, anônimos) nas 3 tarefas e questionário de 5 perguntas. |
| `amostra_conferencia_manual.csv` | Amostra estratificada de 9 itens com a conferência manual humana confrontada com os vereditos do juiz híbrido (100% de concordância). |
| `resultados_v1.csv` | Resultados completos da avaliação da versão v1 (baseline) nas 26 mensagens. |
| `resultados_v2.csv` | Resultados completos da avaliação da versão v2 (melhorada) nas 26 mensagens. |
| `fichas/` | As 7 fichas de referência oficiais da Central do Cidadão de Aurora (versão 01/10/2026), de FC-01 a FC-07. |

---

## 2. Modelos Utilizados e Arquitetura

- **Agente:** `openai/gpt-oss-20b` (na Groq) — ágil, leve e estável na cota gratuita da API, sem estouro de limite de taxa (*rate-limit* 429) observado nos testes iniciais com modelos mais pesados. Temperatura 0 para estabilidade e concisão.
- **Juiz:** `openai/gpt-oss-120b` (na Groq) — modelo robusto de 120 bilhões de parâmetros, assegurando imparcialidade e profundidade analítica na régua de avaliação.

### Resultados no Golden Dataset
- **Acerto Estrito (CORRETO):** subiu de **23% (6/26)** no v1 para **77% (20/26)** no v2.
- **Acerto Flexível (CORRETO + PARCIAL):** subiu de **88% (23/26)** no v1 para **96% (25/26)** no v2.
- **Segurança (Dados e Injeção):** **0%** de falhas (zero vazamentos de dados pessoais e zero quebras de prompt injection em ambas as versões).

### Indicadores dos Testes com Usuários (6 participantes externos)
- **Acerto das Orientações:** **100%** (18 de 18 tarefas resolvidas corretamente).
- **Tempo Médio Geral por Tarefa:** **15,5 segundos** (T1: 19,7s; T2: 14,9s; T3: 11,8s).
- **Facilidade de Utilização:** **4,70 / 5,00** na escala SUS adaptada (Q1: 4,67; Q2: 4,83; Q3: 4,33; Q4: 5,00; Q5: 4,67).

---

## 3. Como Executar o Projeto no Google Colab

1. **Obtenha a chave gratuita da Groq:**
   - Acesse [console.groq.com/keys](https://console.groq.com/keys) e gere sua API Key.
2. **Abra o notebook no Google Colab:**
   - Faça upload do arquivo `citizen_assist_ai.ipynb` no [Google Colab](https://colab.research.google.com).
3. **Configure a chave em Secrets:**
   - No menu lateral esquerdo do Colab, clique no ícone de chave (**Secrets**).
   - Adicione o segredo com o nome `GROQ_API_KEY`, cole sua chave e ative a opção "Notebook access".
4. **Execução:**
   - Vá no menu superior: **Ambiente de execução → Executar tudo**.
   - O notebook é autossuficiente (as fichas oficiais já estão embutidas e são descompactadas automaticamente).
   - O tempo médio de execução completa é de cerca de 10 a 15 minutos (com pausas e retries automáticos para proteger a cota da Groq).
5. **Navegação Interativa pelo Teclado (Opcional):**
   - Na seção 8 do notebook, mude `EXECUTAR_MENU = True` para rodar o menu interativo acessível por números no terminal.
