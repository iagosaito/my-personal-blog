---
title: "Resumo/Análise do livro: Fundamentals of Software Architecture - Cap. 2"
date: 2023-06-23T14:51:22-03:00
draft: true
tags: [fundamentals of software architecture, software architecture, book resume]
categories: [Book Resume, Architecture]
---

> O capítulo dois introduz a primeira parte do livro: __Foundations__

## Capítulo 2 - Pensamento arquitetural

Neste capítulo, o autor cita quatro aspectos necessários para desenvolver um pensamento arquitetural: 

- 1. Entender a diferença entre arquitetura vs design

- 2. Abrangência vs profundidade de conhecimento

- 3. Entender e analisar trade-offs 

- 4. Entender os _business drivers_ e traduzi-los para a arquitetura

Cada aspecto será explorado em mais detalhes abaixo. 

### Arquitetura vs Design

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

### Technical Breadth (Abrangência técnica)

O conhecimento técnico pode ser divido numa pirâmide de três níveis, da base para o topo: 

- Coisas que você que não sabe que não sabe.

- Coisas que você sabe que não sabe.

- Coisas que você sabe. 

Quando inicia-se na carreira de desenvolvimento, o ideal é tentar expandir o topo da pirâmide (coisas que você sabe). Dessa forma, o programador ganha experiência e conhecimento, ou seja: _Technical Depth_ (profundidade técnica). 

Com o passar do tempo, conforme o desenvolvedor evolua e atinja o cargo o arquiteto, o seu foco deve mudar. Agora, ele deve buscar um equilibrio entre o topo e o meio da tabela. **Para um arquiteto, a abrangência (Breadth) é mais importante que a profundidade (Depth)**. É melhor que ele saiba os trade-offs de 10 ferramentas de cache diferentes do que ser expert em apenas uma.

Isso significa que o arquiteto talvez abra mão de algumas habilidades que ele havia adquirido durantes os estágios iniciais como desenvolvedor - ficando enferrujado, por assim dizer. Não só o arquiteto, mas todo desenvolvedor deve medir durante a sua carreira o balanço entre expertise e profundidade. É preciso saber quais batalhas lutar.

### Analisando trade-offs

De acordo com o autor, pensar como um arquiteto significa enxergar os trade-offs em cada solução. Ao contrário dos desenvolvedores que tem o costumer de enxergar apenas os benefícios de determinada solução, os arquitetos precisam ver os dois lados da moeda. 

Então, se alguém perguntar, o que é melhor: Tópicos ou Filas? 

A resposta: **Depende**. Eis o porquê.

O autor propõe um exercício relacionado a uma aplicação de leilão com 4 componentes: Bid Producer, Bid Capture, Bid Tracking, Bid Analytics. 

<figure>
    <img src="/img/fundamentals_of_software_arch/img1.jpg" alt="Representação dos componentes do sistema de leilão">
    <figcaption style="text-align: center;">Imagem 1 - Sistema de leilão</figcaption>
</figure>