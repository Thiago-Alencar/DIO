Delivery utilizando AWS Step Functions e Amazon Bedrock

###### DESCRIÇÃO

Neste desafio prático, você será responsável por criar um Assistente de Delivery utilizando AWS Step Functions e Amazon Bedrock. O projeto consiste em orquestrar diferentes serviços AWS para automatizar e gerenciar um fluxo de pedidos de delivery, desde a recepção do pedido até a entrega final. Utilizando Step Functions, você irá coordenar tarefas como validação de pedidos, integração com serviços de pagamento e atualização de status. O Amazon Bedrock será empregado para aprimorar a personalização e a eficiência do assistente, proporcionando uma experiência otimizada ao cliente.


## Links Úteis

**AWS Step Functions:** [https://aws.amazon.com/pt/step-functions/](https://aws.amazon.com/pt/step-functions/)

**AWS Step Functions Examples:** [https://github.com/aws-samples/aws-stepfunctions-examples](https://github.com/aws-samples/aws-stepfunctions-examples)

**Serverless e Amazon Bedrock:** [https://aws.amazon.com/pt/blogs/aws-brasil/como-criar-um-assistente-virtual-de-baixa-latencia-com-multiplos-modelos-usando-serverless-e-amazon-bedrock/](https://aws.amazon.com/pt/blogs/aws-brasil/como-criar-um-assistente-virtual-de-baixa-latencia-com-multiplos-modelos-usando-serverless-e-amazon-bedrock/)




Arquitetura Proposta
Recepção do Pedido:

API Gateway: Criar uma API REST para receber os pedidos.
Lambda: Função Lambda para validar os dados do pedido e armazená-los em um banco de dados (DynamoDB).
Orquestração com Step Functions:

Máquina de Estado: Definir a lógica de negócio do fluxo do pedido utilizando o Amazon States Language (ASL).
Tarefas:
Validação: Chamar uma Lambda para validar o endereço de entrega, disponibilidade do produto, etc.
Pagamento: Integrar com um serviço de pagamento (Stripe, PayPal) e aguardar a confirmação.
Preparo do Pedido: Notificar a cozinha sobre o novo pedido.
Entrega: Integrar com um serviço de entrega (Uber Eats API, por exemplo) e acompanhar o status da entrega.
Atualização de Status: Atualizar o status do pedido no banco de dados a cada etapa.
Personalização com Amazon Bedrock:

Modelo de Linguagem: Utilizar um modelo de linguagem do Amazon Bedrock para gerar mensagens personalizadas para o cliente (confirmação do pedido, status da entrega, etc.).
Lambda: Chamar o modelo de linguagem para gerar as mensagens e enviá-las para o cliente (e-mail, SMS).
Passo a Passo da Implementação
Configurar o Ambiente:

Criar uma nova aplicação no AWS Management Console.
Configurar as permissões necessárias para os serviços a serem utilizados (Lambda, DynamoDB, API Gateway, Step Functions, Bedrock).
Criar o Banco de Dados:

Utilizar o DynamoDB para armazenar os dados dos pedidos.
Definir um esquema com atributos como ID do pedido, status, informações do cliente, itens do pedido, etc.
Desenvolver a API:

Criar uma API REST utilizando o API Gateway.
Definir as rotas e métodos HTTP para receber os pedidos.
Integrar a API com a função Lambda de validação e armazenamento.
Definir a Máquina de Estado:

Utilizar o AWS Step Functions Console ou a AWS CLI para definir a máquina de estado.
Modelar o fluxo do pedido como uma série de estados e transições.
Configurar as tarefas para chamar as funções Lambda, serviços de pagamento e entrega.
Criar as Funções Lambda:

Validação: Validar os dados do pedido, verificar a disponibilidade de produtos, etc.
Interação com Bedrock: Chamar o modelo de linguagem para gerar mensagens personalizadas.
Integração com Serviços Externos: Chamar as APIs dos serviços de pagamento e entrega.
Configurar o Amazon Bedrock:

Criar um endpoint do Amazon Bedrock.
Configurar o modelo de linguagem desejado.
Implementar a lógica para chamar o endpoint e processar a resposta.
Testar e Depurar:

Utilizar a API para enviar pedidos de teste.
Monitorar o fluxo do pedido no Step Functions Console.
Verificar se as mensagens personalizadas estão sendo geradas corretamente.
