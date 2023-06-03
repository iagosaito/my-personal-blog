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