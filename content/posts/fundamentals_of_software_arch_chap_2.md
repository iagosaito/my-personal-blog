---
title: "Resumo/Análise do livro: Fundamentals of Software Architecture - Cap. 2"
date: 2023-07-01T00:41:22-03:00
draft: false
tags: [fundamentals of software architecture, software architecture, book resume]
categories: [Book Resume, Architecture]
---

> O capítulo dois introduz a primeira parte do livro: __Foundations__

# Capítulo 2 - Pensamento arquitetural

Neste capítulo, o autor cita quatro aspectos necessários para desenvolver um pensamento arquitetural: 

- 1. Entender a diferença entre arquitetura vs design

- 2. Abrangência vs profundidade de conhecimento

- 3. Entender e analisar trade-offs 

- 4. Entender os _business drivers_ e traduzi-los para a arquitetura

Cada aspecto será explorado em mais detalhes abaixo. 

## Arquitetura vs Design

Veja as diferenças entre as responsabilidades do arquiteto - a arquitetura, com as responsabilidades do desenvolvedor - o design do código da aplicação.

O arquiteto tem como responsabilidade: 

> - Analisar os requisitos de negócio e, a partir deles, definir as características arquiteturais ("illities"). 
>
> - Definir o padrão arquitetural e os princípios de design.
>
> - Criar componentes ou blocos do sistema.

Enquanto o desenvolvedor tem como responsabilidade: 

> - Criar interfaces (ou as telas) das aplicação.
>
> - Desenvolver e testar o código fonte.
>
> - Criar diagrama de classes (considero isso uma responsabilidade BEM QUESTIONÁVEL, mas é como o autor exemplifica).

O autor argumenta que a grande questão é que nos modelos de desenvolvimento tradicionais, a comunicação entre o arquiteto e o time de desenvolvimento acontecia de maneira **unilateral**, criando uma desconexão. Algumas decisões que o arquiteto tomava não eram aplicadas pelo time de desenvolvimento, enquanto decisões que o time de desenvolvimento tomava e que alteravam a arquitetura não eram repassadas para o arquiteto.

A solução, portanto, é ter um feedback constante e uma comunicação **bilateral**, aberta e receptiva entre o arquiteto e o time de desenvolvimento. Isso permite que o arquiteto saia do seu trono superior (cof...) e passe a fazer parte do time, mentorando os desenvolvedores.

Perceba que há uma relação nítida entre as duas abordagens. Uma estática, parecida com o modelo de desenvolvimento em cascata; e outra iterativa, adepta as mudanças, ágil, como deve ser.

O autor conclui com a seguinte pergunta: 

> _Quando então a arquitetura acaba e o design de sofware começa?_
>
> R: Não acaba. Ambos fazem parte do ciclo de desenvolvimento e devem estar em sintonia.

## Technical Breadth (Abrangência técnica)

O conhecimento técnico pode ser divido numa pirâmide de três níveis, da base para o topo: 

- Coisas que você que não sabe que não sabe.

- Coisas que você sabe que não sabe.

- Coisas que você sabe. 

Quando inicia-se na carreira de desenvolvimento, o ideal é tentar expandir o topo da pirâmide (coisas que você sabe). Dessa forma, o programador ganha experiência e conhecimento, ou seja: _Technical Depth_ (profundidade técnica). 

Com o passar do tempo, conforme o desenvolvedor evolua e atinja o cargo o arquiteto, o seu foco deve mudar. Agora, ele deve buscar um equilibrio entre o topo e o meio da tabela. **Para um arquiteto, a abrangência (Breadth) é mais importante que a profundidade (Depth)**. É melhor que ele saiba os trade-offs de 10 ferramentas de cache diferentes do que ser expert em apenas uma.

Isso significa que o arquiteto talvez abra mão de algumas habilidades que ele havia adquirido durantes os estágios iniciais como desenvolvedor - ficando enferrujado, por assim dizer. Não só o arquiteto, mas todo desenvolvedor deve medir durante a sua carreira o balanço entre expertise e profundidade. É preciso saber quais batalhas lutar.

## Analisando trade-offs

De acordo com o autor, pensar como um arquiteto significa enxergar os trade-offs em cada solução. Ao contrário dos desenvolvedores que tem o costumer de enxergar apenas os benefícios de determinada solução, os arquitetos precisam ver os dois lados da moeda. 

Então, se alguém perguntar, o que é melhor: Tópicos ou Filas? 

A resposta: **Depende**. Eis o porquê.

O autor propõe um exercício relacionado a uma aplicação de leilão com 4 componentes: Bid Producer, Bid Capture, Bid Tracking, Bid Analytics. 

<figure>
    <img src="/img/fundamentals_of_software_arch/chap2/img1.jpg" alt="Representação dos componentes do sistema de leilão">
    <figcaption style="text-align: center;">Imagem 1 - Sistema de leilão</figcaption>
</figure>

Conforme vemos na figura 1, o Bid Producer produz um Bid (lance) que é transmitido para três serviços: Capture, Tracking e Analytics. 

Isso pode ser feito de duas formas, utilizando filas ou tópicos, conforme as imagens a seguir. 

### Tópicos

<figure>
    <img src="/img/fundamentals_of_software_arch/chap2/img2.jpg" alt="Comunicação entre serviços utilizando tópico">
    <figcaption style="text-align: center;">Imagem 2 - Comunicação entre serviços utilizando tópico (pub-sub)</figcaption>
</figure>

#### Vantagens

A vantagem óbvia dos tópicos é a **extensibilidade**. Caso um novo serviço - como por exemplo _Bid History_ - necessite escutar os lances, bastará se inscrever no tópico e nada no sistema precisará ser alterado. Cria-se um desacoplamento entre o serviço que produz com os demais que o escutam.

#### Desvantagens

As desvantagens, no entanto, não são tão óbvias e por isso o trabalho do arquiteto é tão importante. Um ponto a considerar é que qualquer serviço poderá acessar os dados de leilão (Item Bid) sem que o Producer fique sabendo, criando uma brecha na segurança da aplicação. 

Outro ponto, e particularmente o mais interessante, é que um sistema de tópicos utilizando pub/sub, possui um contrato homogêneo. Todos os serviços que se inscrevem no tópico devem aceitar o mesmo contrato da mensagem. Caso um serviço específico necessite de uma informação adicional que os outros não precisam, todos os serviços serão afetados devido a alteração do contrato.  

### Filas

<figure>
    <img src="/img/fundamentals_of_software_arch/chap2/img3.jpg" alt="Comunicação entre serviços utilizando filas">
    <figcaption style="text-align: center;">Imagem 3 - Comunicação entre serviços utilizando filas</figcaption>
</figure>


#### Vantagens

De imediato é possível identificar que, ao contrário do modelo por tópicos (pub/sub), as filas possibilitam contratos heterogênos entre os diferentes serviços que consomem as mensagens. Outro fator é a capacidade de escalar os serviços de maneira independente, através de um Load Balancer associado a cada fila. 

Por fim, as filas possuem menos brechas de segurança, pois dependem da associação específica entre um Producer -> Fila -> Consumidor. 

#### Desvantagens

Alto acoplamento, para cada novo consumidor é necessário uma nova fila e, portanto, não possui uma alta extensibilidade.

---------------------------------------------------------------------------

O exemplo deixou claro que tudo dentro da arquitetura de software são trade-offs. Um arquiteto analisa cada aspecto comentado acima, tendo como parâmetro os requisitos de pensamento arquitetural citados anteriormente.

Se alguém perguntar: qual devo usar, fila ou tópicos? A resposta é: __Depende!__

### Hands-on Coding (mão na massa)

Na última parte do capítulo, o autor analisa as dificuldades para o arquiteto manter o balanço entre arquitetura de software e codificação. 

Perder a prática de escrever código não é saudável. Ao mesmo tempo, cria-se um gargalo terrível caso o arquiteto se torne "dono" do código do time. Muitas vezes isso ocorre quando o arquiteto puxa para si as atividades mais complexas do projeto - que na maioria das vezes são aquelas que vão além do framework utilizado no momento. 

O autor apresenta três maneiras de como o arquiteto pode, continuamente, trabalhar o hands-on sem prejudicar o time: 

- Criar POCs (Provas de conceito).

- Trabalhar em cima de débitos técnicos e deixar o time com as funcionalidades mais críticas.

- Trabalhar em cima de bug fixes.

- Criar ferramentas de linhas de comando para auxiliar o processo de desenvolvimento do time.

- Realizar code reviews frequentemente.

## Próximo artigo da série

*Artigo e leitura ainda em andamento... Em breve o link aparecerá por aqui. Grato*