---
title: "Apache Kafka - O Básico"
date: 2023-05-21T13:27:19-03:00
draft: false
tags: [kafka, distributed systems]
---

# Apache Kafka — O básico

## Introdução

A ideia deste artigo é cobrir toda a teoria básica do Kafka desde a produção até o consumo de mensagens de maneira objetiva e direta, sem abrir mão de alguns detalhes importantes.

### O que este artigo não cobre? 

Perguntas como:
- Quando eu devo utilizar o Kafka?
- Como eu configuro o Kafka? 
- Quantos brokers eu devo utilizar?
- Como eu crio uma classe Producer no Java?

### O que este artigo cobre?

- Tópicos e partições
- Brokers e Clusters
- Fator de replicação
- Producers (acknowledgment, definições de partição por key)
- Consumers (consumer groups, delivery semantics, rebalanceamento)
- ZooKeeper

Espero que gostem!

## Tópicos e Partições

O principal elemento e a base de tudo dentro do ecossistema do Kafka. Tópicos são uma maneira de categorizar mensagens.

Algumas características dos tópicos são:

- Similar a uma tabela de um banco de dados relacional, porém sem nenhuma constraint;
- Assim como num banco de dados é permitido ter infinitas tabelas, é possível ter infinitos tópicos Kafka;
- Cada tópico é identificado pelo seu nome, portanto, não é possível que dois tópicos tenham o mesmo nome.

 > Os tópicos Kafka são divididos entre partições. Cada partição é uma divisão independente uma da outra dentro do tópico e são ordenadas entre si.

A imagem 1, a seguir, ilustra o funcionamento de um tópico Kafka com três partições. A partição 0 possui oito mensagens, a partição 1 possui três e a partição 2 possui quatro.

Conforme as mensagens chegam as partições, elas recebem um ID numérico incremental chamado offset e são lidas do começo para o fim.

![Representação de um tópico Kafka com 3 partições](/img/apachekafka/apachekafka_img1.jpg)

> Não há garantia de que a leitura ordenada de mensagens funcionará dentro do mesmo tópico, visto que __essa garantia existe apenas para mensagens dentro da mesma partição.__
>
> __Exemplo__: É impossível que na Partição 0, a mensagem de ID 2 seja lida antes da mensagem de ID 1. Porém, essa garantia não se aplica entre as partições.

Uma outra característica das mensagens é a imutabilidade. Isso significa que uma vez que a mensagem é anexada a uma partição, o seu valor nunca poderá ser atualizado ou excluído; ou seja, a mensagem permanecerá ali até o tempo de retenção configurado.

Mas onde os tópicos ficam armazenados?

## Brokers e Clusters

Kafka pode rodar em um ou mais Clusters, que podem estar situados em diferentes datacenters ou clouds. Um Cluster Kafka é composto por um conjunto de brokers.

É possível pensar como:

- Cluster = Máquinas
- Brokers = Servidores.

Cada broker é identificado por um ID numérico e contém partições de tópicos Kafka. A imagem 2 exemplifica como seria um Cluster com dois tópicos — A e B, contendo duas e três partições, respectivamente.

<figure>
    <img src="/img/apachekafka/apachekafka_img2.jpg" alt="Texto alternativo">
    <figcaption>Imagem 2 — Representação de um cluster Kafka com 2 tópicos — A e B distribuídas entre os três brokers
    </figcaption>
</figure>

Mas e se o número de partições for maior que o número de brokers?

Nesse cenário alguns brokers poderão conter mais de uma partição de um mesmo tópico. Por exemplo, imagine que um novo tópico (Tópico C) foi criado dentro do cluster da imagem 2 com 4 partições. A divisão dentro do cluster ficaria assim:

__Tópico C__
- Partição 0 -> Broker 100
- Partição 1 -> Broker 101
- Partição 2 e 3 -> Broker 102 (duas partições no mesmo broker)

> As partições são completamente independentes do broker. Não existe uma sequência e nem é possível prever para qual broker uma partição será atribuída.

### Replicação de Tópicos

Como vimos, o Kafka distribui as partições dos tópicos nos brokers, mas apenas distribuir as partições não é suficiente.

- Se um broker cair, o acontecerá com as mensagens nos tópicos que não foram lidas?
- Os tópicos ficarão com menos partições?

O Kafka foi criado para ser distribuído e tolerante a falhas. Num universo de computação distribuída é necessário existir redundância de dados. O Kafka, por sua vez, resolve esses problemas por meio de um processo chamado fator de __replicação de tópicos.__

E como isso funciona?

Para cada tópico Kafka deve-se definir o número do fator de replicação. Esse número deve ser maior que 1, mas geralmente fica entre 2 e 3 — sendo 3 o mais recomendado. Com um fator de replicação 2, por exemplo, um tópico terá as suas mensagens sincronizadas de forma passiva em dois brokers diferentes (imagem 3).

Além do fator de replicação, existe o conceito de Leader e Replicas (em alguns lugares o nome dado é followers).

>O Leader é a partição responsável por receber os dados e enviar para as réplicas; ou seja, o Leader representa a partição ativa recebendo e servindo dados. As réplicas ficam situadas nos demais brokers diferente do Leader e apenas sincronizam os dados a cada ação do Leader.

Na imagem 3 é possível identificar quem é o Leader e quem são as replicas (followers) de cada partição:

<figure>
    <img src="/img/apachekafka/apachekafka_img3.jpg" alt="Texto alternativo">
    <figcaption>Imagem 3 — Representação do fator de replicação 2 nos tópicos A, B e C dentro de um cluster Kafka
    </figcaption>
</figure>

> OBS: Apenas um único broker pode ser o líder de determinada partição. 
>
> Ex: Não é possível que exista, ao mesmo tempo, um líder para a partição 0 no broker 100 e no broker 101.
> Portanto, uma partição possui um Leader e múltiplas Replicas (ISR — In sync replica).

Segue a lista dos Leaders e Replicas de cada partição tendo como base a Imagem 3:

__Tópico A (Partição 0)__

- Leader -> Broker 100;
- Replica -> Broker 101

__Tópico B (Partição 0)__

- Leader -> Broker 101;
- Replica -> Broker 100

__Tópico C (Partição 0)__

- Leader -> Broker 102;
- Replica -> Broker 101

Mas o que aconteceria caso o Broker 100 morresse?

O Tópico A (Partição 0) teria o seu líder deslocado para o Broker 101 e uma réplica seria criada no Broker 102. O Tópico B (Partição 0) que possuía uma réplica no Broker 100 terá uma nova réplica criada no Broker 102. A imagem 4 demonstra esse deslocamento.

<figure>
    <img src="/img/apachekafka/apachekafka_img4.jpg" alt="Texto alternativo">
    <figcaption>Imagem 4 — Demonstração de como o fator de replicação funciona quando um broker morre
    </figcaption>
</figure>

Caso o Broker 100 volte a operar, o Tópico A (partição 0) poderá voltar a ser Leader.

É dessa maneira que o Kafka garante a integridade e a disponibilidade dos dados!

## Producers

A responsabilidade de um Producer é __escrever ou publicar mensagens__ (dados) nos tópicos Kafka — como os tópicos são constituídos de partições, logicamente, os dados ficam armazenados em partições.

Sempre é preciso informar para qual tópico o Producer escreverá as mensagens. Ao fazer isso, o Kafka automaticamente irá definir a partição que a mensagem será enviada (Imagem 5).

<figure>
    <img src="/img/apachekafka/apachekafka_img5.jpg" alt="Texto alternativo">
    <figcaption>Imagem 5 — Producer Kafka enviando mensagens para as três partições do tópico
    </figcaption>
</figure>

Quando uma mensagem é enviada pelo Producer, __não é possível saber qual será a partição que irá reter a mensagem__. Entretanto, existem dois casos básicos que irão definir o caminho de uma determinada mensagem.

__Caso 1: key != null__

Uma key pode ser literalmente qualquer coisa — uma string, um inteiro, um timestamp. Quando uma mensagem é enviada com uma mesma key é garantido que a mensagem sempre cairá na mesma partição. Não é possível saber qual, mas será sempre a mesma.

__Caso 2: key == null__

Caso nenhuma key seja informada ao produzir mensagens, o Kafka irá distribuir as mensagens entre as partições utilizando o algoritmo de [Round-Robin](https://pt.wikipedia.org/wiki/Round-robin).

### Ack (Acknowledgment)
Quando os Producers escrevem mensagens nos tópicos eles recebem uma confirmação (em ingles, acknowledgment) de que as mensagens foram sincronizadas pelas partições e réplicas. O nível de confirmação pode variar dependendo do nível de ack configurado. São três níveis principais de ack:

- __acks = 0__

Nesse nível o Producer __não espera por nenhuma confirmação__ do broker e irá sempre assumir que as mensagens chegaram com sucesso. Se acontecer da mensagem não chegar no broker ela será perdida.

Embora essa abordagem pareça perigosa — e é mesmo, ela garante um alto throughput.

- __acks = 1 (Padrão)__

O Producer irá assumir que a mensagem chegou com sucesso __quando o broker que contém a partição Leader receber a mensagem.__ Se a mensagem não chegar ao Leader, um erro será gerado e o Producer poderá dar retry na mensagem posteriormente.

Entretanto, a mensagem ainda poderá ser perdida caso o Leader morra e as mensagens não tenham chegado as replicas.

- __acks = all__

O Producer irá assumir que a mensagem chegou com sucesso __quando o Leader e todas as replicas (in-sync replicas) da partição receberem a mensagem__. Esse é o modo mais seguro, mas, ao mesmo tempo, é o modo de maior latência.

## Consumers

Consumers são responsáveis pelo __leitura de mensagens em um tópico__. Um Consumer pode ser uma aplicação Java, por exemplo.

Da mesma forma que os Producers publicam (publish) as mensagens em um tópico, os Consumers se inscrevem (subscribe) nos tópicos para consumir/ler as mensagens. É possível pensar numa analogia com o padrão publish/subscribe.

A leitura é sempre feita na ordem em que as mensagens são produzidas, caso a leitura ocorra dentro da mesma partição.

> Assim como é possível que vários Producers escrevam/publiquem mensagens para uma determinada partição, vários Consumers podem ler mensagens de uma determinada partição.

Geralmente os Consumers consomem as mensagens em grupos. Para coordenar este consumo existe um conceito chamado Consumer Groups.

### Consumer Groups

Consumer Groups representam um conjunto de Consumers.

Quando vários Consumers de um mesmo Consumer Group se inscrevem num tópico, cada Consumer irá ler as mensagens de um subconjunto específico de partições.

A imagem 6 apresenta um modelo de consumo de mensagens através de dois Consumers Groups diferentes.

A quantidade de partições que cada Consumer Group consome está diretamente relacionado a quantidade de consumidores. O Kafka faz o possível para balancear a distribuição entre cada consumidor.

A regra é a seguinte (Veja a imagem 6 como referência):

- __Se número de consumidores = número de partições__: Cada consumidor consome de uma partição diferente. Ex: O Consumer Group 2 da imagem 6

- __Se número de consumidores < número de partições__: O kafka irá balancear, mas alguns consumidores lerão os dados de mais de uma partição. Ex: O Consumer Group 1 possui dois consumers para ler mensagens de três partições, portanto, o Consumer 2 ficou responsável por ler as mensagens da partição 1 e 2./

- __Se número de consumidores > número de partições__: Cada consumidor irá ler os dados de apenas uma partição, os que sobrarem ficarão em estado inativo (IDLE).

> A estratégia de criar mais consumidores do que partições é valida, mesmo com o efeito colateral de alguns consumidores ficarem inativos, pois pode acontecer de algum broker cair/morrer. Dessa forma os consumidores inativos tomam o lugar dos que caíram e a frequência de consumo não diminui.

<figure>
    <img src="/img/apachekafka/apachekafka_img6.jpg" alt="Texto alternativo">
    <figcaption>Imagem 6 — Representação do consumo do tópico qualquer por meio de dois Consumers Group diferentes
    </figcaption>
</figure>

De acordo com a imagem 6 temos dois Consumers Groups. Imagine que o Consumer Group 1 seja uma aplicação Java, e o Consumer Group 2 seja uma outra aplicação feita em Python para trabalhos de análise de dados.

> Ambos os Consumers Groups irão consumir todas as mensagens do tópico. Isso significa que todas as mensagens que forem consumidas pelo Consumer Group 1 também serão pelo Consumer Group 2

Essa estratégia de utilizar grupos de consumidores permite com que os dados produzidos nesse tópicos estejam disponíveis para vários casos dentro da mesma organização.

E se caso uma nova aplicação necessite consumir os dados desse tal *Tópico Qualquer*? Nesse caso, basta que essa nova aplicação crie um novo Consumer Group e se inscreva no tópico.

### Rebalanceamento

Imagine um cenário cujo determinado tópico Kafka possua três partições e dois consumidores.

A Imagem 7 demonstra como possivelmente ficaria a distribuição entre Consumers/Partições para este tópico.

<figure>
    <img src="/img/apachekafka/apachekafka_img7.jpg" alt="Texto alternativo">
    <figcaption>Imagem 7 — Distribuição antes do rebalanceamento
    </figcaption>
</figure>

O *Consumer 1* está associado a Partição 0, enquanto o Consumer 2 está associado a Partição 1 e 2.

Mas o que aconteceria se um novo consumidor fosse incluído no Consumer Group? E se *o Consumer 2* morresse, as partições associadas a ele ficariam sem consumidor?

Nesses dois casos citados acima, o Kafka irá acionar o sistema de __rebalanceamento__ de tópicos.

> Rebalanceamento implica associar o conjunto de consumidores ativos a um novo sub-conjunto de partições

A imagem 8 simula, de maneira bem simples, o rebalanceamento na hipótese do Consumer Group receber mais um Consumidor. Nesse contexto, agora cada consumidor está associado a uma única partição.

<figure>
    <img src="/img/apachekafka/apachekafka_img8.jpg" alt="Texto alternativo">
    <figcaption>Imagem 8 — Distribuição após o rebalanceamento</figcaption>
</figure>

Note que antes o Consumer 2 fazia associação com a Partição 1 e 2, porém, depois do rebalanceamento, o Consumer 3 passou a ter associação com a Partição 2.

Com essa situação surge uma questão interessante.

Imagine que a Partição 2 tenha dez mensagens e, antes do rebalanceamento, o Consumer 2 consumiu cinco mensagens. Após o rebalanceamento, como que o novo Consumer 3 sabe que ele deverá consumir a partir da sexta mensagem?

A resposta para isso se chama Consumer Offsets.

### Consumer Offsets

Consumer offsets é uma maneira de rastrear qual foi o offset da última mensagem consumida por um determinado Consumer Group.

> O mecanismo de Consumer Offsets permite ao Kafka continuar o consumo de mensagens a partir do último offset comitado, sem a necessidade de consumir todas as mensagens desde o início.

A imagem 9 demonstra o mecanismo de Consumer Offsets. Conforme as mensagens são lidas pelo Consumer 1, o Broker Kafka, periodicamente, envia uma mensagem para um tópico especial chamado __consumer_offsets informando o último offset da partição lida.

<figure>
    <img src="/img/apachekafka/apachekafka_img9.jpg" alt="Texto alternativo">
    <figcaption>Imagem 9— Representação do mecanismo de Consumer Offset</figcaption>
</figure>

Dessa maneira, mesmo que haja o rebalanceamento, os novos consumidores associados aos tópicos saberão exatamente a partir de qual offset deverão começar o consumo das mensagens.

### Delivery Semantics

Como foi visto na parte sobre Producers, diferentes níveis de acknowledgments podem ser configurados o envio de mensagens.

Em paralelo a isso, delivery semantics é uma maneira de configurar quando a mensagem será commitada no tópico **__consumer_offsets**, ou seja, é a definição de quando uma mensagem poderá ser classificada como processada.

> O rebalanceamento é um evento que acontece frequentemente no Kafka. Eis o porquê deste assunto de Delivery Semantics ser tão importante.

Existem três estratégias principais de delivery manual (commit manual) dos offsets:

- __At least once (padrão)__
Nessa opção, os offsets são commitados assim que as mensagens forem processadas. Caso aconteça uma falha no processamento a mensagem será lida novamente. Isso garante que nenhuma mensagem será perdida.

Essa opção pode acarretar na duplicação de leitura (at least once). Por isso é importante implementar mecanismos de idempotência.

- __At most once__
Os offsets são commitados assim que as mensagens chegam, mas não garantia de que essas mensagens serão processadas corretamente. Há risco de perda de mensagens.

Com essa configuração a preferência é que não chegue nenhuma mensagem em vez de chegar duplicado.

- __Exactly once__
Garante que todas as mensagens serão processadas corretamente e apenas uma vez. Essa estratégia utiliza um consumidor idempotente mais a Transaction API para funcionar.

> A exactly once é um tópico relativamente novo (e polêmico!) dentro do Kafka e um pouco mais profundo. Não será abordado nesse artigo, mas vale a pena dar uma olhada nesse link caso surja a curiosidade.

### Zookeeper

"Zookeeper é um serviço centralizado que guarda informações a respeito de configurações, nomes, provê sincronização distribuída e grupos de serviço".

Dentro do contexto do Kafka, o software Zookeeper é responsável por guardar metadados a respeito dos brokers, por exemplo:

- O Zookeeper mantém uma lista dos brokers dentro de um cluster.
- Auxilia no processo de eleição de um líder de partição
- Ele envia notificações para o Kafka quando um novo tópico é criado, quando um broker morre, quando um broker sobe, etc…

> O Zookeeper não funcionará junto com o Kafka a partir da versão 4.x. Para mais detalhes, pesquise sobre Kafka Raft (KIP-500).

## Arquitetura Geral
A imagem 10 representa todos os conceitos desse artigo: brokers, clusters, partições, producers, consumers e o Zookeeper. Em conjunto, esses conceitos formam a arquitetura geral do Kafka.


<figure>
    <img src="/img/apachekafka/apachekafka_img10.jpg" alt="Texto alternativo">
    <figcaption>Imagem 10 — Arquitetura geral do Kafka</figcaption>
</figure>

## Referências

- Saphira, Gwen, et al. Kafka: The Definitive Guide 2nd Edition
- [Kafka Docs](https://kafka.apache.org/documentation/).
- [Zookeeper Docs](https://zookeeper.apache.org/).