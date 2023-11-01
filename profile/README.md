## FIAP POSTECH SOAT 01 - Tech Challenge 👋

Essa organização foi criada para manter os repositórios usados no projeto Tech Challenge do curso de Arquitetura de Software da Postech da FIAP.

### :page_with_curl: Documentos do projeto

Usamos o miro para fazer toda a parte de DDD (fase 1) e modelagem do banco de dados (fase 3). A documentação técnica da arquitetura se encontra nas páginas Wiki

- [DDD](https://miro.com/app/board/uXjVMKm6NN0=/?moveToWidget=3458764567529814607&cot=14)
- [Modelagem Banco de dados](https://miro.com/app/board/uXjVMKm6NN0=/?moveToWidget=3458764567529883724&cot=14)
- [Desenho da Arquitetura](https://github.com/SOAT-01/tech-challenge-app/wiki/Fase-3)

### :file_folder: Estrutura de repositórios:

- **tech-challenge-app:** aplicação da lanchonete em node.js
- **lambda-authorizer:** serverless contendo a criação da rota para geração de token para o usuário, lambda authorizer e criação do api gateway.
- **infra-k8s-resources:** administrar os recursos Kubernetes do projeto Tech Challenge.
- **infra-k8s-cluster:** administrar a infra do cluster Kubernetes do projeto.
- **infra-mongo:** administrar a infra do banco de dados MongoDB.
- **infra-postgres:** administrar a infra do banco de dados PostgreSQL.

### :minidisc: Justificativa e modelagem dos bancos de dados

#### Clientes e Produtos

Escolhemos o banco de dados relacional (Postgres) pois são dados cadastrais onde não haverá mudanças estruturais de schema e também podem se relacionar com outras tabelas/sistemas futuramente como por exemplo análises promocionais para clientes ou um sistema de estoque para os produtos.

#### Pedidos

Já para os pedidos, vamos usar o banco de dados não relacional de documentos (MongoDB) porque precisamos de flexibilidade no schema, uma vez que a parte de pagamento pode vir de diferentes providers. Outro motivo muito relevante, é que a parte de pedidos é basicamente o coração do sistema, onde terá um volume muito grande de dados e que deve ser possível escalar horizontalmente para que proporcione uma experiência melhor para os clientes, sem problemas de lentidão para fazer os pedidos e consultar o status do mesmo.

![image](https://github.com/SOAT-01/.github/assets/23150778/a5e5f352-52c5-4c27-89fd-4efe4237ecde)

