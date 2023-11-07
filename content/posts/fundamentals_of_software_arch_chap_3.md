---
title: "Resumo/Análise do livro: Fundamentals of Software Architecture - Cap. 3"
date: 2023-07-25T18:46:55-03:00
draft: true
tags: [fundamentals of software architecture, software architecture, book resume]
categories: [Book Resume, Architecture]
---

# Capítulo 3 - Modularidade

Particularmente, achei este capítulo ligeiramente longo e bem mais denso do que os outros dois.

--------------------------------------------------------------------

O autor inicia com uma citação de _Glenford J. Mayers_, o qual diz que "95% das palavras sobre arquitetura de software são gastos para exaltar os benefícios da 'modularidade', mas praticamente nada é dito sobre como alcançá-la."

Basicamente ele se propõe a fazer duas coisas nesse capítulo: 
 
- 1. Definir o que é modularidade. 
- 2. Como medir os níveis de modularidade de sua aplicação. 

Um ponto importante a se destacar é uma analogia que ele faz com a física. Os sistemas de software tendem a entropia (desordem). É preciso esforço, portanto, para preservar a ordem. 

Alcançar modularidade é um princípio __implícito e organizador__. Implícito porque não haverá nenhum requisito propondo que o sistema seja modular; e organizador, porque a modularidade é a base para uma aplicação consistente. Se um arquiteto cria uma aplicação sem se preocupar em como as coisas devem "encaixar", o caos está instaurado.

## Definição de modularidade

O autor sugere a seguinte definição sobre modularidade: 

> "__Um agrupamento lógico de códigos relacionados entre si__, o que pode ser um conjunto de classes numa linguagem orientada a objeto ou um conjunto de funções em linguagens estruturadas ou funcionais"

Algumas linguagens de programações possuem mecanismos de modularidade, ex: _packages_ no Java e _namespaces_ em .NET.


## Medindo modularidade

Dada a importância de modularidade para desenvolvedores e arquitetos, alguns pesquisadores criaram métricas agnósticas a linguagens de programação para ajudar a entender os níveis de modularidade no sistemas, são essas: __coesão__, __acoplamento__ e __connascence__ (não encontrei uma palavra para traduzir a última). 

### Coesão

Coesão é a medida de quão as partes estão relacionadas entre si. Um módulo coeso é aquele cujas partes devem permanecer juntas, porque caso elas sejas quebradas, são necessárias várias chamadas entre as partes para alcançar o resultado esperado, aumentando o acoplamento 

Pesquisadores classificaram diferentes medidas de coesão dentro de uma aplicação, da melhor pra pior: 

- _Functional Cohesion_
- _Sequential Cohesion_
- _Communicational Cohesion_
- _Procedural Cohesion_
- _Temporal Cohesion_
- _Logical Cohesion_
- _Coincidental Cohesion_

O livro define brevemente cada tipo de coesão, como é um assunto bem extenso, segue o link de duas referências para quem quiser se aprofundar nos detalhes: [Software Engineering Coupling and Cohesion](https://www.geeksforgeeks.org/software-engineering-coupling-and-cohesion/) e [CS UNC - Intramodule Cohesion](https://www.cs.unc.edu/~stotts/COMP145/cohesion.html)

Cientistas da computação desenvolveram uma maneira de metrificar a coesão dentro de aplicações,a mais conhecida se chama __Chidamber and Kemerer Object-oriented metrics suite__ ou LCOM.

Como o LCOM funciona?

O LCOM é uma equação que expõe os níveis de acoplamento entre as classes. Considere o seguinte exemplo:

<figure>
    <img src="/img/fundamentals_of_software_arch/chap3/img1.jpg" alt="LCOM - .">
    <figcaption style="text-align: center;">Imagem 1 - Modelo LCOM representado em forma de grafo.</figcaption>
</figure>

Nas duas figuras temos 5 métodos representados pelas letras A até E, e duas variáveis x e y. As setas indicam quais variáveis são utilizadas pelos métodos. 

Na figura a direita é possível observar que todos os métodos e variáveis estão interligados, com isso, a classe recebeu uma pontuação LCOM baixa: 1.

**Quanto menor o valor mais coesa é a classe**

Em contrapartida, a figura da esquerda recebeu a pontuação 2, indicando falta de coesão. Isso acontece porque a classe da esquerda não possui todos os métodos e variáveis interligados. 

Perceba que há dois conjuntos diferentes {A, B, x} e {C, D, E, y}. Não há uma intersecção, portanto, é perfeitamente possível separar esses dois conjuntos em classes separadas.

A fórmula para calcular o LCOM de uma classe é a seguinte. 

    LCOM2 = 1 − sum(mA) / (m * a)

Sendo que:

- m - número de métodos de uma classe.

- a - número de variáveis (atributos) da classe.

- mA - número de métodos que acessam a variável (atributo).


Entretanto, como tudo dentro da Engenharia de Software são trade-offs, o modelo de medida de coesão LCOM não está imune. O LCOM é útil para medir a falta de coesão estrutural, mas ele não consegue determinar de maneira lógica se as peças da classes encaixam. 

Para isso, outro tipo de medida é mais apropriada. 

## Acomplamento

Em 1979, Edward Yourdon e Larry Constantine publicaram __Structure Design: Fundamentals of Discipline of Computer Program and System Design (Prentice-Hall)__. Foi nessa publicação que eles definiram dois conceitos importantes: métricas aferentes e eferentes.

Acoplamento aferente mede o número de conexões de entrada de um determinado artefato, enquanto acomplamento eferente mede o número de conexões de saída para artefatos de código.  

A partir disso, o livro segue com outras métricas derivadas desses conceitos. Essas métricas foram criadas por Robert Martin e são aplicadas para diferentes linguagens de programação. Elas são: **Abstração, instabilidade e distância da sequência principal**.

### Abstração

A abstração envolve a razão entre a abstração vs implementação. Por exemplo, imagine uma classe que contenha mais de 5000 linhas de código tudo dentro de um único método main(). O númerador de abstração seria 1, enquanto o numerador seria 5000, resultando num valor de abstração que estaria beirando 0. 

### Instabilidade

Responsável por medir o acoplamento eferente e aferente dentro de uma aplicação. A instabilidade mede a volatidade. Se uma classe faz chamadas para muitas outras classes, essa classe possui um nível alto de instabilidade, alto acoplamento e por isso é altamente suscetível a quebras caso haja uma alteração em algum método. 



https://www.aivosto.com/project/help/pm-oo-cohesion.html