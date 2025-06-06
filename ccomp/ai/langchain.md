[[AI]]

https://www.youtube.com/watch?v=qU3fmidNbJE&ab_channel=TinaHuang

O **LangChain** é um framework de código aberto projetado para **construir aplicações com modelos de linguagem (LLMs)**, como o ChatGPT, de forma **modular, estruturada e conectada a fontes externas de dados**. Ele é especialmente útil para desenvolvedores que querem criar **aplicações de IA mais complexas e contextuais**, como **chatbots inteligentes, assistentes com memória, RAGs (retrieval-augmented generation)**, e até agentes autônomos.

---

### 🌐 **Explicando de forma simples:**

O LangChain é como uma "ferramenta LEGO" para você montar aplicações com IA, conectando blocos como:

- Modelos de linguagem (OpenAI, Anthropic, Hugging Face etc.)
    
- Fontes de dados (bancos de dados, PDFs, APIs, websites, etc.)
    
- Memória (lembrar de interações anteriores)
    
- Ferramentas externas (busca na web, calculadora, scripts customizados)
    

---

### 🧩 Principais Componentes:

1. **LLMs (Modelos de Linguagem):** conecta com modelos como o GPT.
    
2. **Prompts:** estrutura e customiza os prompts enviados ao LLM.
    
3. **Memory:** permite que o modelo "lembre" de conversas ou interações passadas.
    
4. **Tools:** integra o modelo com ferramentas externas (como bancos de dados, API, Google Search).
    
5. **Agents:** cria "agentes inteligentes" que decidem qual ferramenta usar, baseado na tarefa.
    
6. **Chains:** encadeia múltiplas etapas (ex: pegar info de um banco de dados → montar resposta → enviar para o modelo).
    

---

### 🧠 Exemplo prático:

Você quer criar um assistente de atendimento ao cliente que:

1. Recebe perguntas dos usuários.
    
2. Busca informações em documentos PDF da empresa.
    
3. Gera uma resposta personalizada.
    
4. Lembra do histórico de cada usuário.
    

O LangChain te ajuda a **conectar todos esses pontos de forma organizada e com menos código do que fazer tudo do zero**.

---

### 💼 Tecnologias relacionadas:

- **Python e JavaScript (TypeScript):** LangChain suporta ambos.
    
- **OpenAI API / Hugging Face / Cohere:** modelos compatíveis.
    
- **Vector stores (Pinecone, FAISS, Chroma):** para armazenar embeddings e fazer buscas semânticas.
    
- **Streamlit / Gradio / FastAPI:** para criar a interface do usuário.
    

---

### ⚡ Quando usar LangChain?

Use se você quer:

- Construir um sistema de IA que **conversa com seus dados** (RAG).
    
- Ter **memória contextual** nas interações.
    
- Integrar **LLMs com ferramentas do mundo real** (navegadores, banco de dados, APIs).
    
- Criar **agentes autônomos** (ex: um que decide se deve consultar um site ou responder direto).
    

---

Se quiser, posso te mostrar um exemplo de código simples usando LangChain com OpenAI + busca em documentos. Quer?