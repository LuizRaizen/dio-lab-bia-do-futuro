# Base de Conhecimento

## Dados Utilizados

Descreva se usou os arquivos da pasta `data`, por exemplo:

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores do cliente sobre suspeitas de golpes ou contestações |
| `transacoes_pix.json` | JSON | Consultar transações Pix recentes, valores, datas e destinatários mascarados via Gateway de Dados |
| `sinais_antifraude.json` | JSON | Fornecer sinais de risco e alertas produzidos pelos mecanismos oficiais de prevenção a fraude |
| `politicas_bancarias.json` | JSON | Fundamentar orientações oficiais sobre o Mecanismo Especial de Devolução (MED) e fluxos de segurança |

> [!TIP]
> **Quer um dataset mais robusto?** Você pode utilizar datasets públicos do [Hugging Face](https://huggingface.co/datasets) relacionados a finanças, desde que sejam adequados ao contexto do desafio.

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

Os dados mockados foram adaptados para refletir o contexto específico de segurança de pagamentos Pix do projeto Sentinela. Foram incluídos campos simulando status de transações recentes, mascaramento de dados de destinatários para conformidade com a privacidade, flags de indício de golpe e metadados de elegibilidade para o Mecanismo Especial de Devolução (MED).

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

Os dados estruturados de transações e sinais antifraude são consultados de forma controlada por meio de ferramentas e APIs do Gateway de Dados Bancários, enquanto a documentação de procedimentos e políticas (Base de Conhecimento oficial) é carregada e referenciada no contexto do sistema de forma versionada e auditável.

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Os dados transacionais e de risco não vão diretamente hardcoded no system prompt; eles são recuperados dinamicamente e de forma isolada pelas ferramentas autorizadas do orquestrador apenas quando necessários para o atendimento autenticado, garantindo que o LLM receba exclusivamente as informações estritamente necessárias para contextualizar o caso sem acesso direto a bancos de dados financeiros.

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```text
Dados da Sessão Autenticada:
- Cliente: João Silva
- Situação Relatada: Suspeita de golpe envolvendo Pix enviado

Última transação consultada (via Gateway Autorizado):
- ID Transação: TX-9842103
- Data/Hora: 02/06/2026 - 14:35
- Valor: R$ 1.500,00
- Status: Concluído
- Destinatário: M**** S***** (Mascarado)
- Sinais Antifraude: Indicador de risco moderado por engenharia social

Instrução de Fluxo:
- Aplicar regras determinísticas do Mecanismo Especial de Devolução (MED) e orientar os próximos passos oficiais sem prometer recuperação de valores.
