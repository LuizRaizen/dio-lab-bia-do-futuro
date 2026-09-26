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
