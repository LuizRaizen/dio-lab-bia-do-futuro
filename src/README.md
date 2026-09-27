# 🛡️ Sentinela — Segurança Pix e Prevenção a Fraudes

Assistente inteligente especializado em segurança de pagamentos, triagem de transações Pix suspeitas e orientação para prevenção a fraudes bancárias.

## 📂 Estrutura do Projeto

```text
sentinela_codigo_fonte/
├── data/
│   ├── perfil_investidor.json      # Dados cadastrais e perfil do cliente
│   ├── produtos_financeiros.json   # Catálogo de produtos e investimentos disponíveis
│   ├── historico_atendimento.csv   # Histórico prévio de interações e chamados
│   └── transacoes.csv              # Extrato de transações, receitas e despesas
├── src/
│   ├── app.py                      # Aplicação principal em Streamlit
│   ├── agente.py                   # Lógica central do Agente Sentinela e system prompts
│   └── config.py                   # Gestão de configurações e variáveis de ambiente
├── requirements.txt                # Dependências do projeto
└── README.md
```

---

## 🚀 Como Executar o Projeto

Siga o passo a passo abaixo para clonar, configurar e rodar o Sentinela na sua máquina utilizando o Visual Studio Code (VS Code) e o terminal:

### Passo 1: Clonar ou Baixar o Repositório
Abra o seu terminal (Git Bash, CMD ou PowerShell) e execute o comando de clonagem do Git, ou descompacte o arquivo ZIP do projeto:
```bash
git clone <URL_DO_REPOSITORIO>
cd sentinela_codigo_fonte
```

### Passo 2: Abrir no VS Code
Com a pasta do projeto aberta, inicie o VS Code pelo terminal:
```bash
code .
```
*(Ou abra o VS Code manualmente e vá em **File > Open Folder...** selecionando a pasta `sentinela_codigo_fonte`).*

### Passo 3: Criar e Ativar o Ambiente Virtual
No terminal integrado do VS Code (`Ctrl + ~`), crie e ative um ambiente virtual Python:

* **No Windows (PowerShell/CMD):**
  ```bash
  python -m venv .venv
  .venv\Scripts\activate
  ```
* **No macOS / Linux:**
  ```bash
  python3 -m venv .venv
  source .venv/bin/activate
  ```

### Passo 4: Instalar as Dependências
Com o ambiente virtual ativado, instale as bibliotecas necessárias descritas no arquivo `requirements.txt`:
```bash
pip install -r requirements.txt
```

### Passo 5: Configurar as Variáveis de Ambiente
Crie um arquivo chamado `.env` na raiz do projeto (`sentinela_codigo_fonte/.env`) e insira a sua chave de API (compatível com o Gemini ou OpenAI, conforme configurado no projeto):

```env
GEMINI_API_KEY="sua_chave_da_api_aqui"
MODEL_NAME="gemini-1.5-flash"
```

### Passo 6: Executar a Aplicação
Com tudo configurado, execute o Streamlit apontando para o arquivo principal da aplicação dentro da pasta `src`:
```bash
streamlit run src/app.py
```

O Streamlit iniciará um servidor local e abrirá automaticamente o painel interativo do Sentinela no seu navegador padrão (`http://localhost:8501`).
