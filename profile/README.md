## FIAP POSTECH SOAT 01 - Tech Challenge 👋

Essa organização foi criada para manter os repositórios usados no projeto Tech Challenge do curso de Arquitetura de Software da Postech da FIAP.

## Fase 5 - Arquitetura

Para a Fase 5, a aplicação anterior (https://github.com/SOAT-01/tech-challenge-app/wiki/Fase-4) foi modificada aplicando o padrão de SAGA coreografada usando o serviço de mensageria SQS da AWS, onde o principal motivador desta escolha foi o fator simplicidade, considerando que existiam poucas comunicações implementadas entre os serviços.

![image](https://github.com/SOAT-01/tech-challenge-app/assets/15642927/487b171a-1375-40a1-b42c-6f1bbcf72a01)

### Fluxo dos Pedidos

O fluxo de vida de um pedido criado no sistema segue o diagrama abaixo:

![fase5-v2-fluxo drawio](https://github.com/SOAT-01/tech-challenge-app/assets/15642927/03bd5b00-d40b-4657-b07a-530b4f4fbd8d)


### :page_with_curl: Documentos do projeto

Usamos o miro para fazer toda a parte de DDD (fase 1) e modelagem do banco de dados (fase 3). A documentação técnica da arquitetura se encontra nas páginas Wiki

- [DDD](https://miro.com/app/board/uXjVMKm6NN0=/?moveToWidget=3458764567529814607&cot=14)
- [Modelagem Banco de dados](https://miro.com/app/board/uXjVMKm6NN0=/?moveToWidget=3458764567529883724&cot=14)
- [Arquitetura Fase 4](https://github.com/SOAT-01/tech-challenge-app/wiki/Fase-4)
- [Arquitetura Fase 3](https://github.com/SOAT-01/tech-challenge-app/wiki/Fase-3)
- [Arquitetura Fase 2](https://github.com/SOAT-01/tech-challenge-app/wiki/Fase-2)

### :file_folder: Estrutura de repositórios:
#### Gerais
- **lambda-authorizer:** serverless contendo a criação da rota para geração de token para o usuário, lambda authorizer e criação do api gateway.
- **lambda-notification:** serverless contendo a criação de função que recebe uma mensagem (SQS) de notificação de status do Pedido e faz um envio de e-mail notificando o cliente.
- **infra-k8s-cluster:** administrar a infra do cluster Kubernetes do projeto.
- **infra-sonarqube:** administrar máquina ec2 para subir o Sonarqube.
#### Clientes
- **clientes-app:** aplicação do serviço em node.js.
- **infra-clientes-postgres:** administrar a infra do banco de dados PostgreSQL.
- **infra-clientes-k8s:** administrar os recursos Kubernetes do serviço.
#### Produtos
- **produtos-app:** aplicação do serviço em node.js.
- **infra-produtos-postgres:** administrar a infra do banco de dados PostgreSQL.
- **infra-produtos-k8s:** administrar os recursos Kubernetes do serviço.
#### Pedidos
- **pedidos-app:** aplicação do serviço em node.js.
- **infra-pedidos-mongo:** administrar a infra do banco de dados MongoDB.
- **infra-pedidos-k8s:** administrar os recursos Kubernetes do serviço.
#### Pagamentos
- **pagamentos-app:** aplicação do serviço em node.js.
- **infra-pagamentos-mongo:** administrar a infra do banco de dados MongoDB.
- **infra-pagamentos-k8s:** administrar os recursos Kubernetes do serviço.

### Repositórios Deprecated (Fase 3):
- **infra-k8s-resources:** administrar os recursos Kubernetes do projeto Tech Challenge.
- **tech-challenge-app:** aplicação da lanchonete em node.js
- **infra-mongo:** administrar a infra do banco de dados MongoDB.
- **infra-postgres:** administrar a infra do banco de dados PostgreSQL.

### :minidisc: Justificativa e modelagem dos bancos de dados (Fase 3)

#### Clientes e Produtos

Escolhemos o banco de dados relacional (Postgres) pois são dados cadastrais onde não haverá mudanças estruturais de schema e também podem se relacionar com outras tabelas/sistemas futuramente como por exemplo análises promocionais para clientes ou um sistema de estoque para os produtos.

#### Pedidos

Já para os pedidos, vamos usar o banco de dados não relacional de documentos (MongoDB) porque precisamos de flexibilidade no schema, uma vez que a parte de pagamento pode vir de diferentes providers. Outro motivo muito relevante, é que a parte de pedidos é basicamente o coração do sistema, onde terá um volume muito grande de dados e que deve ser possível escalar horizontalmente para que proporcione uma experiência melhor para os clientes, sem problemas de lentidão para fazer os pedidos e consultar o status do mesmo.

![image](https://github.com/SOAT-01/.github/assets/23150778/a5e5f352-52c5-4c27-89fd-4efe4237ecde)

