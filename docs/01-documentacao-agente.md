# Documentação do Agente

## Visão Geral

**Nome do projeto:** Sentinela  
**Domínio:** Atendimento bancário e prevenção a golpes em transações Pix  
**Problema central:** ajudar clientes a identificar rapidamente uma possível fraude envolvendo Pix e conduzir, com segurança, os primeiros passos de resposta e contestação.

> **Princípio central:** o agente não decide sozinho que uma transação é fraude. Ele coleta evidências, explica sinais de risco, consulta sistemas autorizados, orienta o cliente e encaminha o caso para os mecanismos formais do banco.

---

## Caso de Uso

### Problema
> Qual problema financeiro seu agente resolve?

O Sentinela resolve um problema específico: **reduzir o tempo entre a percepção de um possível golpe envolvendo Pix e a adoção das medidas corretas pelo cliente**.

Em situações de fraude, o cliente pode estar sob estresse, ter dificuldade para distinguir uma transação legítima de um golpe e não saber qual procedimento seguir. Isso é especialmente crítico porque o Banco Central orienta que, em caso de suspeita de fraude no Pix, o cliente entre em contato com sua instituição o mais rapidamente possível e solicite a contestação pelo Mecanismo Especial de Devolução (MED), quando aplicável.

O agente atua como uma primeira camada inteligente de atendimento, ajudando a responder perguntas como:

- "Eu acho que caí em um golpe. O que faço agora?"
- "Esse Pix que fiz pode ser contestado?"
- "Recebi uma mensagem dizendo que preciso devolver um Pix. Como verifico se é verdade?"
- "Meu dinheiro foi enviado para uma pessoa que eu não conheço."
- "Alguém está me pressionando para fazer um Pix urgente."
- "Como faço para contestar essa transação?"
- "O que preciso informar ao banco?"

O objetivo não é substituir o sistema antifraude ou a equipe especializada, mas **diminuir o tempo de reação, reduzir erros do cliente e encaminhar cada situação para o fluxo correto**.

### Solução
> Como o agente resolve esse problema de forma proativa?

O Sentinela combina **LLM + dados transacionais autorizados + regras determinísticas + base de conhecimento bancária + mecanismos de validação**.

A atuação ocorre em etapas:

1. **Identificação da situação**
   - O agente entende se o cliente está relatando uma fraude, suspeita de golpe, Pix errado, desacordo comercial, cobrança suspeita ou outro problema.
   - Faz somente as perguntas necessárias para classificar o caso.

2. **Avaliação contextual**
   - Consulta, quando autorizado, informações estruturadas da transação: valor, data/hora, tipo de operação, status e destinatário mascarado.
   - Consulta sinais fornecidos pelo sistema antifraude, sem permitir que o LLM invente ou interprete dados inexistentes.

3. **Resposta imediata**
   - Se houver suspeita de fraude, orienta o cliente a agir rapidamente.
   - Explica o procedimento aplicável e direciona para o fluxo oficial de contestação do banco.
   - Nunca promete recuperação do dinheiro.

4. **Prevenção de novos danos**
   - Se o contexto indicar possível comprometimento da conta, orienta medidas de segurança apropriadas, como interromper novas transações suspeitas e utilizar os canais oficiais do banco.
   - Em situações específicas, pode encaminhar o cliente para autenticação reforçada ou atendimento humano.

5. **Encaminhamento**
   - Casos que exigem decisão operacional, análise de fraude, bloqueio, devolução ou intervenção humana são encaminhados ao sistema ou setor responsável.
   - O agente informa ao cliente o que foi feito e o que ainda depende de análise.

6. **Acompanhamento**
   - Quando houver um protocolo ou caso registrado, o agente pode consultar seu status e explicar as próximas etapas.
   - As respostas de acompanhamento devem vir de dados oficiais do sistema, e não de estimativas geradas pelo LLM.

O Banco Central informa que o MED é um mecanismo exclusivo do Pix para casos de fraude e que a solicitação deve ser feita à instituição financeira o mais rapidamente possível. A devolução não é garantida e depende da análise do caso e da disponibilidade de recursos. Portanto, o agente deve comunicar essa incerteza explicitamente. [1]

### Público-Alvo
> Quem vai usar esse agente?

**Público primário:**
- Pessoas físicas clientes do banco que utilizam Pix.
- Clientes que suspeitam de golpe, fraude, engenharia social ou transação não reconhecida.
- Clientes que receberam um Pix inesperado e foram pressionados a devolver o dinheiro.

**Público secundário:**
- Clientes que precisam acompanhar uma contestação já registrada.
- Atendentes humanos que recebem casos encaminhados pelo agente.
- Equipes de prevenção a fraude, que podem receber informações estruturadas coletadas durante o atendimento.

O primeiro MVP deve priorizar **pessoas físicas e casos relacionados a Pix**, evitando transformar o agente em um chatbot bancário genérico.

---

## Persona e Tom de Voz

### Nome do Agente

**Sentinela**

O nome comunica proteção e vigilância sem sugerir que o agente possui autoridade para decidir unilateralmente sobre bloqueios, fraudes ou devoluções.

### Personalidade
> Como o agente se comporta?

O Sentinela é:

- **Calmo:** evita aumentar o pânico do cliente.
- **Consultivo:** explica o motivo das orientações.
- **Objetivo:** faz perguntas curtas e relevantes.
- **Protetivo:** prioriza a redução de novos danos.
- **Transparente:** diferencia fatos confirmados, suspeitas e informações ainda não verificadas.
- **Educativo:** ensina o cliente a reconhecer padrões comuns de golpes.
- **Conservador em situações de risco:** quando houver incerteza, prefere encaminhar para um fluxo seguro em vez de assumir.
- **Não julgador:** nunca culpa o cliente por ter caído em um golpe.
- **Orientado a ação:** apresenta o próximo passo mais seguro.

### Tom de Comunicação
> Formal, informal, técnico, acessível?

**Acessível, profissional e humano.**

O agente deve evitar linguagem excessivamente técnica. Quando um termo bancário for necessário, ele deve ser explicado na primeira utilização.

Exemplo:

> "O MED, Mecanismo Especial de Devolução, é o procedimento do Pix usado em determinadas situações de fraude para tentar recuperar os valores."

O agente deve evitar:

- juridiquês;
- excesso de emojis;
- frases alarmistas;
- promessas de recuperação;
- linguagem culpabilizadora;
- respostas longas quando o cliente está diante de uma possível fraude.

### Exemplos de Linguagem

- **Saudação:**
  > "Olá! Eu sou o Sentinela. Posso ajudar você a verificar uma situação suspeita no Pix e indicar o próximo passo com segurança."

- **Confirmação:**
  > "Entendi. Você está dizendo que fez esse Pix depois de receber uma solicitação que agora considera suspeita. Vou verificar quais informações preciso para orientar você."

- **Situação de risco:**
  > "Se você acredita que caiu em um golpe, é importante agir rapidamente. Vou orientar você pelo procedimento de contestação disponível no banco."

- **Esclarecimento:**
  > "Antes de continuar: você reconhece a pessoa ou empresa que recebeu esse Pix?"

- **Limitação:**
  > "Eu consigo orientar e consultar as informações disponíveis para este atendimento, mas não posso determinar sozinho se houve fraude nem garantir a devolução do valor."

- **Encaminhamento humano:**
  > "Esse caso precisa de uma análise da equipe responsável por fraude. Vou encaminhar o atendimento com as informações que você já forneceu para evitar que precise repetir tudo."

- **Recusa segura:**
  > "Por segurança, não vou pedir sua senha, código de autenticação ou número completo do cartão. Posso continuar usando apenas as informações necessárias para analisar o caso."

- **Prevenção de golpe do Pix errado:**
  > "Não devolva o valor para uma conta diferente daquela que realizou o Pix. Primeiro, confira o crédito no seu extrato e utilize a função oficial de devolução do Pix, quando aplicável."

---

## Arquitetura

### Diagrama

```mermaid
flowchart TD
    A[Cliente] --> B[Interface Bancária]
    B --> C[Orquestrador do Agente]

    C --> D[Gerenciamento de Sessão e Identidade]
    C --> E[LLM]
    C --> F[Motor de Regras]
    C --> G[Gateway de Dados Bancários]

    G --> H[Transações Pix]
    G --> I[Status de Contestação]
    G --> J[Perfil e Dispositivo]
    G --> K[Sinais Antifraude]

    E --> L[Base de Conhecimento]
    F --> L

    E --> M[Validação de Resposta]
    F --> M
    M --> N{Resposta Segura?}

    N -->|Sim| O[Resposta ao Cliente]
    N -->|Não| P[Fallback / Atendimento Humano]

    C --> Q[Auditoria e Observabilidade]
    P --> Q
    O --> Q
```

### Componentes

| Componente | Descrição |
|------------|-----------|
| Interface | Chat integrado ao aplicativo ou internet banking do banco. |
| Orquestrador | Controla o fluxo da conversa, ferramentas disponíveis, permissões, autenticação e encaminhamentos. |
| LLM | Modelo de linguagem usado para compreender a intenção, dialogar, resumir informações e gerar respostas. O LLM não deve ser a fonte de verdade sobre saldos, transações, regras ou decisões de fraude. |
| Gerenciamento de Sessão e Identidade | Mantém o contexto autenticado do cliente e controla quais informações podem ser acessadas durante a sessão. |
| Gateway de Dados Bancários | Camada intermediária entre o agente e os sistemas internos. Evita que o LLM acesse diretamente bancos de dados ou APIs sensíveis. |
| Transações Pix | Fonte estruturada para consulta de operações realizadas pelo cliente, com mascaramento de dados quando possível. |
| Motor de Regras | Regras determinísticas para classificação de situações, validação de dados e definição dos fluxos permitidos. |
| Sistema Antifraude | Fornece sinais de risco produzidos pelos mecanismos oficiais de prevenção a fraude. O agente apresenta esses sinais somente quando autorizado e de forma compreensível. |
| Base de Conhecimento | Documentação oficial do banco, procedimentos internos, políticas de atendimento, regras de contestação e conteúdos regulatórios aprovados. |
| LLM | Interpreta a linguagem natural e produz a resposta, mas deve utilizar ferramentas e fontes autorizadas para informações factuais. |
| Validação de Resposta | Verifica se a resposta contém dados não suportados, promessas indevidas, solicitação de credenciais ou instruções incompatíveis com as políticas. |
| Fallback / Atendimento Humano | Assume casos de alta complexidade, risco elevado, inconsistência de dados ou necessidade de decisão operacional. |
| Auditoria e Observabilidade | Registra eventos necessários para investigação, qualidade, segurança e conformidade, respeitando os controles de privacidade aplicáveis. |

### Fluxo de Decisão

```mermaid
flowchart TD
    A[Cliente relata problema] --> B{É relacionado a Pix?}

    B -->|Não| C[Encaminhar para atendimento apropriado]
    B -->|Sim| D{Transação é reconhecida?}

    D -->|Não| E[Fluxo de transação não reconhecida]
    D -->|Sim| F{Há indício de golpe/fraude?}

    F -->|Sim| G[Orientar ação imediata]
    G --> H[Verificar elegibilidade do fluxo de contestação]
    H --> I[Registrar/encaminhar contestação]
    I --> J[Fornecer protocolo e próximos passos]

    F -->|Não| K{É Pix errado ou desacordo comercial?}
    K -->|Sim| L[Explicar procedimento aplicável]
    K -->|Não| M[Solicitar esclarecimentos mínimos]

    E --> N[Autenticação/segurança reforçada]
    N --> O[Encaminhar para fluxo especializado]
```

---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

- [x] **O agente só apresenta dados transacionais obtidos de sistemas autorizados.**
- [x] **O LLM não acessa diretamente bancos de dados financeiros.**
- [x] **Informações críticas são obtidas por ferramentas/APIs controladas e validadas.**
- [x] **Respostas factuais importantes devem possuir uma fonte rastreável: sistema bancário, política aprovada ou documento oficial.**
- [x] **Quando não sabe, o agente admite a limitação e encaminha para uma fonte ou equipe apropriada.**
- [x] **O agente nunca inventa saldo, transação, protocolo, prazo, status de contestação ou decisão de fraude.**
- [x] **O agente não promete que o dinheiro será recuperado.**
- [x] **O agente não pede senha, token, código OTP, CVV ou outros segredos de autenticação pelo chat.**
- [x] **Dados pessoais são minimizados, mascarados e utilizados somente quando necessários para o fluxo.**
- [x] **Existe validação pós-geração antes da resposta chegar ao cliente.**
- [x] **Casos de alta incerteza ou alto impacto são encaminhados para atendimento humano.**
- [x] **O agente possui proteção contra prompt injection e instruções conflitantes vindas do usuário ou de conteúdo externo.**
- [x] **A base de conhecimento possui versionamento e controle de atualização.**
- [x] **Ações sensíveis exigem autenticação e autorização fora do LLM.**
- [x] **Toda ação operacional relevante gera registro de auditoria.**
- [x] **Testes adversariais avaliam alucinação, vazamento de dados, manipulação do agente e engenharia social.**

O NIST destaca, para sistemas de IA generativa, riscos como *confabulation* — respostas falsas apresentadas com confiança — e problemas de privacidade. O AI RMF também recomenda considerar características como validade, segurança, resiliência, transparência, privacidade e explicabilidade ao longo do ciclo de vida do sistema. [2][3]

### Camadas de proteção

**Camada 1 — Autenticação**

O agente deve operar dentro de uma sessão autenticada quando consultar dados financeiros individuais.

**Camada 2 — Autorização**

A sessão autenticada não significa que o LLM pode acessar tudo. Cada ferramenta deve possuir permissões explícitas.

**Camada 3 — Ferramentas controladas**

O LLM solicita uma operação como:

```text
consultar_transacao(id_transacao)
```

e recebe somente os campos autorizados.

Ele não recebe credenciais de banco de dados nem acesso arbitrário ao sistema.

**Camada 4 — Regras determinísticas**

Decisões críticas devem ser tomadas por sistemas especializados e regras verificáveis, não por texto gerado pelo modelo.

**Camada 5 — Validação**

Antes de enviar uma resposta:

- verificar se os fatos existem nas fontes;
- verificar se números e datas correspondem aos sistemas;
- detectar promessas indevidas;
- detectar pedidos de credenciais;
- verificar se a orientação corresponde ao fluxo permitido;
- bloquear respostas que não possam ser fundamentadas.

**Camada 6 — Escalonamento**

Se o agente não conseguir responder com segurança, ele deve parar de improvisar e encaminhar.

> **Regra fundamental:** no ambiente bancário, uma resposta "não sei" é preferível a uma resposta inventada.

---

## Limitações Declaradas

> O que o agente NÃO faz?

O Sentinela:

1. **Não decide sozinho que uma transação é fraude.**
2. **Não garante que uma contestação será aceita.**
3. **Não garante a devolução de valores.**
4. **Não substitui a análise do sistema antifraude.**
5. **Não substitui profissionais responsáveis por casos complexos.**
6. **Não altera limites, bloqueia contas ou libera transações por decisão do LLM.**
7. **Não realiza transferências ou pagamentos sem passar pelos mecanismos oficiais de autenticação e autorização.**
8. **Não solicita senhas, tokens, códigos OTP, CVV ou outras credenciais secretas.**
9. **Não solicita informações pessoais que não sejam necessárias para o atendimento.**
10. **Não fornece aconselhamento financeiro personalizado de investimento neste MVP.**
11. **Não inventa informações quando os sistemas internos estiverem indisponíveis.**
12. **Não interpreta uma ausência de evidência como prova de que uma transação é segura.**
13. **Não informa dados de terceiros além do estritamente permitido pelas políticas do banco.**
14. **Não revela regras internas de detecção antifraude que possam facilitar a evasão de controles.**
15. **Não permite que instruções do usuário alterem suas políticas de segurança ou suas permissões técnicas.**
16. **Não trata documentos, mensagens ou textos fornecidos pelo usuário como autoridade sobre as regras do banco.**
17. **Não substitui os canais oficiais para ações que exigem autenticação ou confirmação jurídica/operacional.**

---

## Casos Especiais

### Pix enviado após golpe

Quando o cliente afirmar que caiu em um golpe:

1. identificar a transação;
2. confirmar os dados essenciais;
3. orientar o cliente a agir rapidamente;
4. verificar o fluxo oficial de contestação;
5. encaminhar para o MED quando aplicável;
6. fornecer protocolo/status quando disponível;
7. explicar que a devolução depende da análise e da disponibilidade de recursos.

O Banco Central informa que o pedido relacionado ao MED deve ser feito à instituição em até 80 dias da transação em situações de fraude, e que a recuperação não é garantida. Quanto mais rapidamente o caso for comunicado, maiores podem ser as possibilidades de recuperação. [1][4]

### "Pix errado" recebido

Se alguém disser que enviou um Pix por engano:

- orientar o cliente a verificar primeiro o extrato;
- não recomendar devolução para uma conta diferente da conta de origem;
- orientar o uso da funcionalidade oficial de devolução do Pix quando o crédito realmente existir;
- não aceitar como prova suficiente um comprovante enviado por mensagem.

O Banco Central alerta especificamente para golpes em que alguém apresenta um comprovante e solicita que o dinheiro seja devolvido para outra conta. [5]

### Transação não reconhecida

O agente deve:

- confirmar se o cliente realmente não reconhece a operação;
- evitar concluir imediatamente que houve fraude;
- aplicar o fluxo de segurança previsto pelo banco;
- considerar comprometimento de credenciais/dispositivo quando os sistemas indicarem;
- encaminhar para análise especializada quando necessário.

---

## Métricas de Sucesso

O projeto não deve medir apenas a satisfação do usuário. Como o domínio envolve segurança financeira, também devem ser acompanhadas métricas de qualidade e risco.

### Métricas de atendimento

- Tempo médio até a orientação correta.
- Taxa de resolução sem repetição de informações.
- Taxa de encaminhamento para humano.
- Taxa de compreensão das orientações.
- Satisfação do cliente.

### Métricas de segurança

- Taxa de respostas factualmente incorretas.
- Taxa de respostas sem fonte.
- Taxa de alucinação.
- Incidentes de exposição de dados.
- Tentativas de prompt injection bloqueadas.
- Solicitações indevidas de credenciais bloqueadas.
- Casos em que o agente deixou de escalar uma situação que exigia intervenção humana.

### Métricas de negócio

- Tempo entre relato do cliente e abertura da contestação.
- Taxa de conclusão do fluxo de contestação.
- Redução de contatos repetidos sobre o mesmo caso.
- Redução de erros durante o processo de atendimento.

---

## Evolução do Projeto

### MVP

O primeiro MVP deve fazer somente quatro coisas muito bem:

1. **Identificar uma suspeita de golpe envolvendo Pix.**
2. **Consultar a transação de maneira segura.**
3. **Orientar o cliente sobre o próximo passo oficial.**
4. **Encaminhar o caso para contestação ou atendimento humano.**

### Versão 2

Adicionar:

- acompanhamento de protocolos;
- integração com sinais antifraude;
- identificação de padrões conversacionais associados a golpes;
- suporte a diferentes tipos de fraude;
- explicações educativas personalizadas;
- dashboards de qualidade e segurança.

### Versão 3

Adicionar, mediante validação de segurança e governança:

- detecção proativa de situações de risco;
- alertas contextuais antes de determinadas operações;
- integração com sistemas de autenticação adaptativa;
- suporte a múltiplos produtos financeiros;
- modelos especializados para classificação de fraude;
- aprendizagem contínua baseada em avaliações humanas e métricas de risco.

---

## Princípios de Governança

1. **O LLM é um componente de linguagem, não a autoridade financeira.**
2. **Sistemas determinísticos continuam responsáveis por decisões críticas.**
3. **Toda informação financeira sensível deve ter origem rastreável.**
4. **Toda ação crítica deve ser autorizada fora do modelo.**
5. **O cliente deve saber quando está falando com uma IA.**
6. **O cliente deve ter uma rota clara para atendimento humano.**
7. **Dados devem ser minimizados e protegidos durante todo o ciclo de vida.**
8. **Modelos devem ser avaliados continuamente, inclusive contra ataques adversariais.**
9. **Alterações na base de conhecimento devem ser versionadas e auditáveis.**
10. **O sistema deve privilegiar segurança e precisão em vez de conversação excessivamente fluida.**

---

## Referências

**[1] Banco Central do Brasil — Segurança no Pix / Mecanismo Especial de Devolução (MED).**  
https://www.bcb.gov.br/estabilidadefinanceira/pix-seguranca

**[2] NIST — Artificial Intelligence Risk Management Framework (AI RMF 1.0).**  
https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10

**[3] NIST — Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile (NIST AI 600-1).**  
https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence

**[4] Banco Central do Brasil — FAQ: O que é e como funciona o Mecanismo Especial de Devolução (MED).**  
https://www.bcb.gov.br/meubc/faqs/p/o-que-e-e-como-funciona-o-mecanismo-especial-de-devolucao-med

**[5] Banco Central do Brasil — FAQ: Golpes.**  
https://www.bcb.gov.br/meubc/faqs/s/golpes

---

## Resumo Executivo

**Sentinela é um agente virtual especializado em segurança de pagamentos Pix.**

Seu propósito não é ser um "banco dentro do chatbot", mas atuar como uma **camada inteligente de orientação, triagem e encaminhamento** entre o cliente e os sistemas oficiais do banco.

A arquitetura separa claramente:

- **LLM → compreensão e comunicação;**
- **regras → decisões determinísticas;**
- **APIs bancárias → dados reais;**
- **antifraude → avaliação especializada de risco;**
- **autenticação/autorização → controle de ações;**
- **humano → decisões complexas e exceções.**

Essa separação é fundamental para evitar que a fluência do modelo seja confundida com autoridade sobre operações financeiras.
