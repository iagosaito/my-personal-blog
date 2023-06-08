---
title: "Resumo/Análise do livro: Fundamentals of Software Architecture - Cap. 1"
date: 2023-06-02T19:52:00-03:00
draft: true
tags: [fundamentals of software architecture, software architecture, book resume]
categories: [Book Resume, Architecture]
---

## Prefácio - Invalidating Axioms

O objetivo do autor é estabelecer uma definição do que é um axioma e como isso pode ser aplicado (ou não) dentro da área de *Software Archtecture*. 

De acordo com o autor, *"um axioma é uma sentença que é considerada como sendo estabelecida, aceita e tida como verdade em si mesmo"*. Um exemplo
de um axioma famoso na matemática é o [__axioma da igualdade de Peano__](https://pt.wikipedia.org/wiki/Axiomas_de_Peano#:~:text=Para%20todos%20os%20n%C3%BAmeros%20naturais%20x%2C%20y%2C%20e%20z%2C,s%C3%A3o%20fechados%20em%20sua%20igualdade.) usado dentro da teoria dos conjuntos: 

> Sabendo que A = C e B = C, então podemos afirmar que B = C. 

Embora essas regras sejam rígidas na matématica, o autor acredita que 
dentro da área de engenharia de software __isso não deveria existir__.

Isso se dá fundamentalmente pela ideia que o desenvolvimento de software está em constante mudança. Ao longos das últimas duas décadas, as práticas de engenharia de software mudaram completamente. Passamos de XP para CI/CD. Depois, surgiu a revolução DevOps, microserviços, containers e Cloud. 

Essa mudança frequente é caracterizada pelo autor como __Dynamic Equilibrium__. Seria como se o universo de desenvolvimento de software fosse algo vivo, tentando sempre encontrar o equilíbrio entre as vantagens das inovações e os inevitáveis trade-offs. 

Essa definição me lembrou a polêmica na semana passada em que a [Amazon Prime Vídeo trocou o sistema de microsserviços e serveless para uma arquitetura monolítica, reduzindo seus custos em 90%](https://www.primevideotech.com/video-streaming/scaling-up-the-prime-video-audio-video-monitoring-service-and-reducing-costs-by-90), fazendo com que a briga argumentativa entre sistemas monolíticos vs microsserviços fossem para um novo round. Novamente, __Dynamic Equilibrium__.

Esse tipo de discussão é mencionada no prefácio, visto que, de acordo como o autor, *"se apaixonar por uma tecnologia específica ou abordagem é fácil"*, porém, o papel de um arquiteto é ter uma exata noção do que é bom e ruim e entender exatamente os trade-offs dentro de cada escolha. 

> Em resumo, a ideia geral do livro é repensar os axiomas dentro da arquitetura de  software, entender os trade-offs envolvidos, sempre levando em consideração o ecossistema de desenvolvimento que temos atualmente. 

## Capítulo 1 - Introduction

### *Roadmap* para um Software Architect

No primeiro capítulo o autor tenta definir porque não existe um *path* ou *roadmap* específico para a carreira de um *Software Archictect*

O autor destaca quatro motivos principais: 

- 1. Dificuldade em definir o que é um *Software Architect*.
- 2. O tamanho gigantesco do escopo de responsabilidades e habilidades exigidas de um *Software Architect*.
- 3. A mudança constante dos ecossistemas de desenvolvimento de software.
- 4. Defasagem dos materias sobre *Software Architecture*. 

Uma frase bem famosa do *Ralph Johnson* é citada

> *"Archtecture is about the important stuff... whatever that is."* (Arquitetura é sobre a parte importante... seja lá o que seja) - Ralph Johnson

Ele argumenta que definir o que é um arquiteto de software é algo difícil. A industria não tem uma definição em função do amplo escopo de habilidades que um *Software Architect* necessita, além de que o escopo muda constantemente buscando um equilíbrio (novamente a ideia de *Dynamic Equilibrium*). 

Por exemplo, até algum tempo atrás dizia-se que o *Software Architect* era a pessoa que lidava com a parte dos sistemas que __eram difíceis (ou custosas $$) de mudar__.
Embora parte disso ainda seja verdade, estilos arquiteturais como microsserviços vão de encontro a essa ideia, pois visam a construção incremental do Software, de forma que uma mudança estrutural não se torne cara.

### Definição de *Software Architecture*

O autor tenta responder a essa pergunta respondendo a seguinte pergunta: __O que é analisado quando um arquiteto de software analisa uma arquitetura?__ 

Para o autor, o que um arquiteto deve analisar são um conjunto de quatro coisas: 

- 1. Estrutura de um sistema.

Se refere ao tipo de estilo arquitetural, por exemplo: microsserviços, multicamada, microkernel e etc.

- 2. Características que um sistema deve suportar ("ilities").

Referem-se aos critérios de sucesso de um sistema, sem relação com a sua funcionalidade, mas que são necessários para seu funcionamento de maneira adequada. Por exemplo: Availability (disponibilidade), Scalability (escalabilidade), testability testabilidade e etc.  

- 3. Decisões arquiteturais.

Definições das regras de como o sistema deve ser construído e suas restrições. 

Por exemplo, o arquiteto pode definir que numa arquitetura de camadas, a camada de apresentação (presentation layer) não pode interagir diretamente com a base de dados. 

- 4. Princípios de design. 

Orientações fornecidas ao time de desenvolvimento, por exemplo, utilização de comunicação assíncrona entre serviços. Esse tipo de orientação vai guiar o desenvolvedor a escolher a tecnologia mais adequada para aquele fim. 

A diferença entre o 3 (decisões arquiteturais) para o 4 (princípios de design) está basicamente na rigidez. Os princípios servem como guidelines, enquanto as decisões arquiteturais fornecem restrições que devem ser obedecidas ao máximo.  