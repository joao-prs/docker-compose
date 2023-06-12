# docker-compose
Uma piscina de exemplos e até estruturas prontas para subir um compose rapidamente. Boa leitura deste README e os composes 👻

## Docker Compose

O Docker Compose é uma ferramenta que permite definir e executar aplicativos de vários contêineres. Com ele, você pode descrever a infraestrutura de um aplicativo usando um arquivo YAML (Compose file). É útil para simplificar o processo de configuração de aplicativos que dependem de vários serviços, como um aplicativo web com um banco de dados e um servidor de cache.

Com o Docker Compose, você pode definir os serviços necessários, especificar as imagens Docker a serem usadas, configurar as redes e volumes compartilhados, além de definir variáveis de ambiente e outras opções de configuração. Em seguida, pode-se usar o comando ```docker-compose up``` para criar e iniciar todos os contêineres definidos no arquivo Compose. É uma ferramenta muito útil para desenvolvimento local e ambientes de teste.

## Docker Swarm

Já o Docker Swarm é uma ferramenta que permite orquestrar e gerenciar clusters de contêineres Docker em um ambiente de produção. Com o Docker Swarm, você pode criar um cluster de vários hosts Docker e distribuir automaticamente os contêineres em vários nós para garantir alta disponibilidade e escalabilidade. O Swarm utiliza o conceito de "serviços", que são grupos de contêineres que executam uma determinada tarefa.

Com o Docker Swarm, você pode implantar aplicativos em um cluster de maneira fácil e escalável. Ele oferece recursos de balanceamento de carga, recuperação automática em caso de falhas e escalabilidade horizontal. Ao usar o Swarm, você pode implantar aplicativos distribuídos em várias máquinas e aproveitar a capacidade de processamento e armazenamento de recursos do cluster como um todo.

