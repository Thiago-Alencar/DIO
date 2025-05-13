# Microsoft Copilot Studio: Aprofundando a Criação de Copilots

Este guia expande os conceitos básicos e explora funcionalidades mais detalhadas do Microsoft Copilot Studio.

## 1. Criar um Copilot em Branco

Começar com um copilot em branco oferece controle total sobre a estrutura e o comportamento do seu bot.

**Passos:**

1.  No portal do Microsoft Copilot Studio, selecione a opção para criar um "Novo copilot" e escolha a opção "Começar do zero" ou similar.
2.  Defina um nome para o seu copilot e selecione o idioma desejado.
3.  O próximo passo é criar seus próprios **tópicos**. Um tópico representa um fluxo de conversa com um objetivo específico (por exemplo, responder a uma pergunta, coletar informações).
4.  Para criar um tópico, clique em "+ Novo tópico". Dê um nome ao tópico e defina as **frases de gatilho**. Estas são as palavras ou frases que os usuários digitarão para iniciar este tópico.
5.  Construa o **fluxo de conversa** dentro do tópico usando o editor visual. Adicione nós para:
    * **Perguntas:** Solicitar informações do usuário.
    * **Condições:** Criar ramificações lógicas com base nas respostas do usuário.
    * **Ações:** Executar tarefas como pesquisar informações, chamar fluxos do Power Automate ou exibir mensagens.
    * **Mensagens:** Exibir texto, imagens ou vídeos para o usuário.
    * **Encerrar a conversa:** Finalizar o tópico com uma pesquisa de satisfação opcional.

## 2. Customizar um Tópico

A customização de tópicos permite adaptar o fluxo de conversa e a interação do seu copilot para atender às necessidades específicas dos seus usuários.

**Ações de Customização:**

* **Editar Frases de Gatilho:** Adicione, remova ou modifique as frases que iniciam um tópico para garantir que o copilot reconheça as intenções dos usuários de forma precisa.
* **Personalizar Mensagens:** Adapte o texto das mensagens para refletir a voz e o tom da sua marca. Use variáveis para inserir informações dinâmicas coletadas durante a conversa.
* **Adicionar Entidades:** Entidades representam tipos específicos de informações que você deseja extrair das falas dos usuários (por exemplo, nome, e-mail, número do pedido). O Copilot Studio possui entidades pré-construídas e permite criar entidades personalizadas. Ao adicionar uma entidade a uma pergunta, o copilot tentará identificar e extrair essa informação da resposta do usuário.
* **Implementar Lógica Condicional:** Use nós de "Condição" para criar diferentes caminhos de conversa com base nas respostas dos usuários ou em outras variáveis. Isso permite lidar com diferentes cenários e fornecer respostas mais relevantes.
* **Integrar com Power Automate:** Utilize o nó "Chamar uma ação" para conectar seu copilot a fluxos do Power Automate. Isso permite automatizar tarefas complexas, como consultar bancos de dados, enviar e-mails ou interagir com outros sistemas.

## 3. Personalizar uma Mensagem de Erro de Tópico

Quando um copilot não consegue entender a entrada do usuário ou encontrar uma resposta correspondente, ele exibe uma mensagem de erro padrão. Personalizar essa mensagem pode melhorar a experiência do usuário e fornecer orientações mais úteis.

**Passos para Personalizar a Mensagem de Erro:**

1.  No painel de navegação esquerdo, clique em "Configurações".
2.  Selecione "Mensagens do sistema".
3.  Localize a mensagem "Não entendi" ou similar.
4.  Clique em "Editar" para personalizar o texto da mensagem. Você pode:
    * Fornecer alternativas ou exemplos de como o usuário pode reformular sua pergunta.
    * Sugerir tópicos relacionados que o usuário pode tentar.
    * Oferecer a opção de falar com um agente humano (se configurado).
5.  Salve suas alterações.

## 4. Aumentar e Diminuir a Qualidade da Resposta com GenAI (IA Generativa)

O Microsoft Copilot Studio integra recursos de IA Generativa (GenAI) para aprimorar a capacidade do seu copilot de responder a perguntas de forma mais natural e abrangente, mesmo quando não há um tópico específico correspondente. Você pode ajustar a "confiança" ou a "criatividade" da GenAI para controlar a qualidade e a relevância das respostas geradas.

**Como Ajustar a Qualidade da Resposta:**

1.  No painel de navegação esquerdo, clique em "Configurações".
2.  Selecione "IA Generativa".
3.  Você encontrará configurações para ajustar a forma como a GenAI responde quando não há uma correspondência direta com um tópico. Geralmente, haverá um controle deslizante ou opções para definir o nível de "confiança" ou "criatividade":
    * **Aumentar a Confiança (Diminuir a Criatividade):** O copilot será mais conservador e só fornecerá respostas geradas pela IA se tiver alta certeza de sua relevância. Isso pode resultar em menos respostas, mas com maior precisão.
    * **Diminuir a Confiança (Aumentar a Criatividade):** O copilot será mais propenso a gerar respostas com base em seu conhecimento geral, mesmo que a correspondência não seja perfeita. Isso pode levar a respostas mais abrangentes, mas com um risco maior de imprecisão ou irrelevância.

