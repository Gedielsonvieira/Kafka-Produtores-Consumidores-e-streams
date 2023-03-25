# Introdução

## Apache Kafka

### O que é?

> "É uma plataforma distribuida de streaming", a ideia do kafka é mover e armazenar dados.

### Caracteristicas

- Plataforma: ele tem um ecossistemas em torno dele
- Trabalha de forma distribuida
- BD: Ele também é um Banco de dados (Todas as mensagens que trafegam pelo Kafka, temos a possibilidade de armazená-las e consultá-las e processá-las posteriormente)
- Utiliza o disco ao invés da memória para processar os dados

Obs: Kafka NÃO é apenas um sistema tradicional de filas como RabbitMQ.

### Conceito Básico

- Produtor: Produz a mensagem, envia a mensagem para um sistema
- Consumidor: Consome a mensagem

> Explicação:
> Ao invés de um sistema A enviar uma msg direto para o sistema B, o sistema A ele passa a enviar uma mensagem para o kafka e o kafka mantem essa msg no Tópico e o outro sistema lê desse tópico. (Basicamente o dado passa por dentro de um tópico)

### O que é um "Tópico"?

- O Tópico é um Stream de dados que atua como um BD.

  > Explicação: Ao mandar mensagens para esse tópico, esse tópico vai ficar o tempo inteiro encaminhando essas mensagens para quem esta querendo ler.

- Todos os dados ficam armazenados, ou seja, cada Tópico tem seu "local" para armazenar seus dados.

- Tópico possui diversas partições
  - Cada partição é definida por um número. Ex: 0,1,2
  - Ao criar um Tópico somos obrigado a definir a quantidade de partições

### Kafka Cluster

- Cluster é um conjunto de Brokers
- Cada Broker é um servidor
- Cada Broker é responsável por armazenar os dados de uma partição

Mensageria tem um broker que recebe mensagem e a apartir dessa mensagem outros serviços fazem o que tem que ser feito levando em consideração a mensagem recebida

captura analisa e responde em tempo real

comunicação entre sistemas

"Mensageria é um conceito que define que sistemas distribuidos possam se comunicar por meio de troca de mensagens (evento) sendo estas mensagens 'gerenciadas' por um Message Broker (servidor/módulo de mensagens)."

## Produtores e consumidores

### Instalando o Kafka localmente

- Como instalar e rodar o Kafka:

  - Algumas informações básicas, o Kafka tem que armazenar em algum lugar e o lugar onde o Kafka armazena isso, por padrão, se chama zookeeper, ou seja, precisamos rodar o zookeeper antes do kafka

  - Rodar zookeeper: **zookeeper-server-start.bat ../../config/zookeeper.properties**

  - Rodar kafka: **kafka-server-start.bat ../../config/server.properties**

---

- Criação de tópicos manualmente:

  - Criar tópico: **kafka-topics.bat --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic LOJA_NOVO_PEDIDO**

  - Ver se foi criado o tópico: **kafka-topics.bat --list --bootstrap-server localhost:9092**

  - Obtendo a descrição de um tópico: **kafka-topics.bat --bootstrap-server localhost:9092 --describe**

---

- O que são produtores:

  > Produtor é quem produz mensagens

  - Criar um produtor de mensagens: **.\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic LOJA_NOVO_PEDIDO**

---

- O que são consumidores:
  - Criar um consumidor: **.\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic LOJA_NOVO_PEDIDO**

### Criando Produtores em Java

> Produzir mensagens se resume a criar um produtor, criar a mensagem, enviar e colocar algum listener

### Criando Consumidores em Java

- Cada serviço vai ter uma tarefa, um serviço em epecifico, por isso não é comum um consumidor ficar escutando mais de um tópico, porque como ele tem um objetivo em específico vai ficar escutando somente um tópico.

- Ao criar um consumer precisamos informar qual é o GROUP_ID_CONFIG
