---
title: "Resumo/Análise do livro: Fundamentals of Software Architecture - Cap. 3"
date: 2023-07-25T18:46:55-03:00
draft: true
tags: [fundamentals of software architecture, software architecture, book resume]
categories: [Book Resume, Architecture]
---

# Capítulo 3 - Modularidade

Particularmente, achei este capítulo ligeiramente longo e bem mais denso do que os outros dois. Vou tentar resumir de uma forma simples e tentar exemplificar de uma maneira mais hands-on coding. 

--------------------------------------------------------------------

O autor inicia com uma citação de _Glenford J. Mayers_, o qual diz que "95% das palavras sobre arquitetura de software são gastos para exaltar os benefícios da 'modularidade', mas praticamente nada é dito sobre como alcançá-la."

Basicamente ele se propõe a fazer duas coisas nesse capítulo: 
 
- 1. Definir o que é modularidade. 
- 2. Como medir os níveis de modularidade da sua aplicação. 

Um ponto importante a se destacar é uma analogia que ele faz com a física. Basicamente, os sistemas de software tendem a entropia (desordem). É preciso esforço, portanto, para preservar a ordem. 

Alcançar modularidade é um princípio __implícito e organizador__. Implícito porque não haverá nenhum requisito propondo que o sistema seja modular; e organizador, porque a modularidade é a base para uma aplicação consistente. Se um arquiteto cria uma aplicação sem se preocupar em como as coisas devem "encaixar", o caos está instaurado.

## Definição de modularidade

O autor sugere a seguinte definição sobre modularidade: 

> "__Um agrupamento lógico de códigos relacionados entre si__, o que pode ser um conjunto de classes numa linguagem orientada a objeto ou um conjunto de funções em linguagens estruturadas ou funcionais"

Algumas linguagens de programações possuem mecanismos de modularidade, ex: _packages_ no Java e _namespaces_ em .NET.


## Como medir modularidade

Dada a importância de modularidade para desenvolvedores e arquitetos, alguns pesquisadores criaram métricas agnósticas a linguagens de programação para ajudar a entender os níveis de modularidade no sistemas, são essas: __coesão__, __acoplamento__ e __connascence__ (não encontrei uma palavra para traduzir a última). 

### Coesão

Coesão é a medida de quão as partes estão relacionadas entre si. Um módulo coeso é aquele cujas partes devem permanecer juntas, porque caso elas sejas quebradas, são necessárias várias chamads entre as partes para alcançar o resultado esperado, gerando um aumento no acoplamento. 

Pesquisadores classificaram diferentes medidas de coesão dentro de uma aplicação, da melhor pra pior: 

- _Functional Cohesion_
- _Sequential Cohesion_
- _Communicational Cohesion_
- _Procedural Cohesion_
- _Temporal Cohesion_
- _Logical Cohesion_
- _Coincidental Cohesion_

O livro define brevemente cada tipo de coesão, como é um assunto bem extenso, segue o link de duas referências para quem quiser se aprofundar nos detalhes: [Software Engineering Coupling and Cohesion](https://www.geeksforgeeks.org/software-engineering-coupling-and-cohesion/) e [CS UNC - Intramodule Cohesion](https://www.cs.unc.edu/~stotts/COMP145/cohesion.html)


