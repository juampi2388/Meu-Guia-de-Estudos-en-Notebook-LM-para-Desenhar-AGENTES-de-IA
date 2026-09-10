# Implementação de Agentes de IA e Automações para Negócios

Este repositório documenta o design, desenvolvimento e implementação de Agentes de Inteligência Artificial e Automações aplicados à otimização de processos de negócios e atendimento ao cliente, com foco em ambientes comerciais e PMEs. 

O projeto utiliza ferramentas low-code/no-code como **n8n**, **Claude** e fluxos conectados a bancos de dados ou CRMs.

---

## 1. Objetivos do Projeto

- **Compreensão Arquitetônica:** Diferenciar os fundamentos dos agentes inteligentes em relação aos chatbots tradicionais e workflows determinísticos.
- **Domínio Técnico:** Aprofundar o conhecimento em engenharia de prompts, system prompts, alocação de ferramentas (tool use / function calling) e gerenciamento de memória em plataformas de automação.
- **Modelo de Negócios:** Estruturar um plano de produtização e empacotamento comercial (pricing, retainers e modelos de entrega) focado na consultoria tecnológica para pequenos e médios negócios.

---

## 2. Curadoria de Fontes e Referências

O desenvolvimento deste projeto foi embasado nos seguintes materiais e pesquisas:

* **[Documento]** `Plan_Automatizacion_IA_Claude.pdf`: Guia metodológico fase a fase orientado à adoção técnica e comercial.
* **[Documento]** `Manual_Estudio_Vocabulario_IA.pdf`: Glossário técnico transversal e definições-chave sobre LLMs, agentes e protocolos.
* **[Documento]** `Calendario_Contenido_Instagram.pdf`: Estratégia de comunicação e peças de divulgação sobre automação com IA.
* **[Curso/Vídeo]** *Curso Completo De N8N: Como Criar e Vender Agentes IA*: Recurso audiovisual sobre a construção prática de um agente de vendas conectado a estoques e webhooks.
* **[Artigo/Web]** *10 agentes de IA gratuitos para simplificar seu fluxo de trabalho*: Pesquisa aberta sobre ferramentas e plataformas de agentes do mercado atual.

---

## 3. Engenharia de Prompts e Troubleshooting (Cicatrizes)

Documentar o raciocínio por trás dos resultados é fundamental para validar o processo técnico. Abaixo estão os testes realizados ao configurar um agente conversacional para um ambiente comercial (ex: uma loja de veículos no n8n).

### Instrução Estratégica Inicial

> "Você é um assistente da loja. Você tem estes carros disponíveis: BMW X1, Gol 1.0. Diga-me os carros disponíveis."

### Variações e Testes (Prompting Iterativo)

1. **Teste 1 (Básico sem contexto de papel):** 
   O modelo retornou respostas genéricas e inclusive começou a alucinar estoques devido à falta de restrições rigorosas no system prompt.
   
2. **Teste 2 (Estrutura de System Prompt Profissional):** 
   Estruturou-se um prompt dividido em:
   * **Contexto:** Vendedor humano especialista em atendimento pelo WhatsApp.
   * **Objetivo:** Entender a intenção, consultar o estoque real através de ferramentas e listar opções de forma clara, limitando a um máximo de 3 resultados.
   * **Guardrails (Restrições):** Proibir a invenção de dados de estoque e proteger contra prompt injections.

### Dificuldades Encontradas (Troubleshooting)

* **Alucinação de dados:** Inicialmente, se o usuário perguntasse por um modelo inexistente (ex. BMW X6), o LLM tentava inventar características. Solução: vincular uma ferramenta rigorosa de filtragem e uma regra de negação direta nas instruções do sistema.
* **Mapeamento de Ferramentas (Tools):** Conectar as tools de busca por marcas/anos específicos exigiu separar os nós de consulta. Passar um volume massivo de dados de estoque direto para o contexto degrada a precisão da resposta do modelo (*context overload*).

---

## 4. Arquitetura e Conceitos (Mini-guia)

### Anatomia de um Agente vs. Chatbot

* **Chatbot / Workflow:** Opera sob árvores de decisão rígidas, respostas isoladas por turno ou executa tarefas sequenciais fixas.
* **Agente de IA:** Opera através de um ciclo de decisão-ação-avaliação (*agent loop*). Utiliza um LLM como "cérebro" para determinar de forma autônoma quais ferramentas invocar (consultar uma planilha, CRM ou API externa) para cumprir um objetivo com mínima intervenção humana.

### Estrutura de Automação Robusta

Uma arquitetura profissional no n8n ou plataformas similares combina:
1. **Trigger:** Evento de entrada (ex. mensagem de WhatsApp ou Webhook).
2. **Buffer:** Sistema de controle de tempo para acumular ou pausar consultas repetidas.
3. **Nó de IA:** Motor cognitivo dotado de memória e ferramentas conectadas.
4. **Ações Secundárias:** Tarefas automatizadas de background (ex. salvar leads qualificados em bancos de dados).

---

## 5. Glossário Técnico

| Termo | Definição |
| :--- | :--- |
| **Agent Loop** | Ciclo contínuo onde o agente analisa o objetivo, decide qual ação tomar, executa uma ferramenta e avalia o resultado obtido. |
| **System Prompt** | Instrução fundamental que define a personalidade, o papel, as regras operacionais e os limites (guardrails) do modelo antes da interação. |
| **Tool Use / Function Calling** | Mecanismo pelo qual o LLM reconhece a necessidade de invocar uma função externa estruturada em vez de apenas gerar texto. |
| **MCP (Model Context Protocol)** | Padrão aberto projetado para conectar de maneira segura e padronizada os modelos de linguagem a fontes de dados e ferramentas externas. |
| **MRR (Monthly Recurring Revenue)** | Receita recorrente mensal, métrica-chave no modelo de negócios de prestação de serviços de automação por meio de retainers de manutenção. |
