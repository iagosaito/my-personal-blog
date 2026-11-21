---
title: "Resumen/Análisis del libro: Fundamentals of Software Architecture - Cap. 1"
date: 2023-06-02T19:52:00-03:00
draft: false
tags: [fundamentals of software architecture, software architecture, book resume]
categories: [Book Resume, Architecture]
---

## Prefacio - Invalidating Axioms

El objetivo del autor es establecer una definición de qué es un axioma y cómo puede aplicarse (o no) dentro del área de *Software Architecture*.

Según el autor, *"un axioma es una afirmación que se considera establecida, aceptada y verdadera en sí misma"*. Un ejemplo
de un axioma famoso en matemáticas es el [__axioma de igualdad de Peano__](https://es.wikipedia.org/wiki/Axiomas_de_Peano), usado en la teoría de conjuntos:

> Sabiendo que A = C y B = C, entonces podemos afirmar que A = B.

Aunque estas reglas son rígidas en matemáticas, el autor cree que
dentro del área de ingeniería de software __esto no debería existir__.

Esto se debe fundamentalmente a la idea de que el desarrollo de software está en constante cambio. A lo largo de las últimas dos décadas, las prácticas de ingeniería de software cambiaron por completo. Pasamos de XP a CI/CD. Después surgieron la revolución DevOps, los microservicios, los contenedores y la Cloud.

El autor caracteriza este cambio frecuente como __Dynamic Equilibrium__. Sería como si el universo del desarrollo de software fuera algo vivo, que siempre intenta encontrar el equilibrio entre las ventajas de las innovaciones y los inevitables trade-offs.

Esta definición me recordó la polémica de la semana pasada, en la que [Amazon Prime Video cambió su sistema de microservicios y serverless por una arquitectura monolítica, reduciendo sus costos en un 90%](https://www.primevideotech.com/video-streaming/scaling-up-the-prime-video-audio-video-monitoring-service-and-reducing-costs-by-90), haciendo que la disputa entre sistemas monolíticos y microservicios pasara a un nuevo round. Otra vez, __Dynamic Equilibrium__.

Este tipo de discusión se menciona en el prefacio, ya que, según el autor, *"es fácil enamorarse de una tecnología o un enfoque específico"*; sin embargo, el papel de un arquitecto es tener una noción exacta de lo que es bueno y malo y entender exactamente los trade-offs de cada elección.

> En resumen, la idea general del libro es repensar los axiomas dentro de la arquitectura de software y entender los trade-offs involucrados, siempre teniendo en cuenta el ecosistema de desarrollo que tenemos actualmente.

## Capítulo 1 - Introducción

### *Roadmap* para un Software Architect

En el primer capítulo, el autor intenta explicar por qué no existe un *path* o *roadmap* específico para la carrera de un *Software Architect*.

El autor destaca cuatro motivos principales:

- 1. La dificultad de definir qué es un *Software Architect*.
- 2. El enorme alcance de responsabilidades y habilidades que se le exigen a un *Software Architect*.
- 3. El cambio constante de los ecosistemas de desarrollo de software.
- 4. La desactualización de los materiales sobre *Software Architecture*.

Se cita una frase muy famosa de *Ralph Johnson*

> *"Architecture is about the important stuff... whatever that is."* (La arquitectura trata sobre lo importante... sea lo que sea) - Ralph Johnson

Él argumenta que es complicado definir qué es un arquitecto de software. La industria no tiene una definición debido al amplio alcance de habilidades que necesita un *Software Architect*, además de que ese alcance cambia constantemente en busca de un equilibrio (de nuevo la idea de *Dynamic Equilibrium*).

Por ejemplo, hasta hace algún tiempo se decía que el *Software Architect* era la persona que se ocupaba de la parte de los sistemas que __era difícil (o costosa $$) de cambiar__.
Aunque parte de esto sigue siendo cierto, estilos arquitectónicos como los microservicios van en contra de esa idea, ya que buscan la construcción incremental del software, de modo que un cambio estructural no se vuelva caro.

### Definición de *Software Architecture*

El autor intenta responder a esta pregunta respondiendo a otra: __¿Qué se analiza cuando un arquitecto de software analiza una arquitectura?__

Para el autor, lo que un arquitecto debe analizar es un conjunto de cuatro cosas:

- 1. La estructura de un sistema.

Se refiere al tipo de estilo arquitectónico, por ejemplo: microservicios, multicapa, microkernel, etc.

- 2. Las características que un sistema debe soportar ("ilities").

Se refieren a los criterios de éxito de un sistema, sin relación con su funcionalidad, pero que son necesarios para que funcione adecuadamente. Por ejemplo: availability (disponibilidad), scalability (escalabilidad), testability (testeabilidad), etc.

- 3. Decisiones arquitectónicas.

Definiciones de las reglas sobre cómo debe construirse el sistema y sus restricciones.

Por ejemplo, el arquitecto puede definir que, en una arquitectura en capas, la capa de presentación (presentation layer) no puede interactuar directamente con la base de datos.

- 4. Principios de diseño.

Orientaciones dadas al equipo de desarrollo, por ejemplo, el uso de comunicación asíncrona entre servicios. Este tipo de orientación guiará al desarrollador a elegir la tecnología más adecuada para ese fin.

La diferencia entre el 3 (decisiones arquitectónicas) y el 4 (principios de diseño) está básicamente en la rigidez. Los principios sirven como guidelines, mientras que las decisiones arquitectónicas establecen restricciones que deben respetarse al máximo.

### Definición de la función de un Software Architect

En esta parte del capítulo, el autor argumenta que definir lo que hace un *Software Architect* también es difícil, ya que la función puede variar de empresa a empresa. Por eso, el autor prefiere enfocarse en las __expectativas__ de la función, y cita ocho como principales.

Él explica cada una de estas funciones en detalle; para que no quede muy largo, intentaré sintetizar los puntos clave.

- 1. *Make architecture decisions.*

> El arquitecto debe definir las decisiones de arquitectura y los design principles que se usan para guiar las elecciones tecnológicas del equipo; por lo tanto, __debe guiar en lugar de imponer__.

Por ejemplo, según el autor, debe guiar al equipo a usar un framework frontend reactivo para el desarrollo web, en lugar de imponer que construyan la aplicación con React.js.

- 2. *Continually analyze the architecture.*

> El arquitecto debe analizar continuamente la arquitectura de las aplicaciones y proponer soluciones para su mejora y vitalidad.

Debe preguntarse: ¿La arquitectura hecha hace cuatro años sigue siendo viable o muestra señales de deterioro? ¿Se siguen cumpliendo las características arquitectónicas (ilities)?

- 3. *Keep current with latest trends.*

> El arquitecto debe mantenerse actualizado con las nuevas tecnologías y las nuevas tendencias de la industria.

- 4. *Ensure compliance with decisions.*

> El arquitecto debe verificar continuamente que el equipo de desarrollo esté siguiendo las decisiones arquitectónicas y los design principles que fueron comunicados y documentados.

- 5. *Diverse exposure and experience.*

> El arquitecto debe exponerse a distintas tecnologías, frameworks, plataformas y entornos.

La idea no es que sea especialista en todas las tecnologías y lenguajes, sino que tenga familiaridad con una variedad de tecnologías. Por ejemplo: es mejor que el arquitecto conozca 10 productos de caching diferentes y sepa los pros y contras de cada uno, que ser especialista en uno solo.

- 6. *Have business domain knowledge.*

> El arquitecto debe tener expertise en el dominio de negocio.

Sin entender cuál es el problema que tu arquitectura debe resolver, es imposible crear una arquitectura que cumpla con los requisitos de negocio.

- 7. *Possess interpersonal skills.*

> El arquitecto debe tener habilidades interpersonales excepcionales, incluyendo trabajo en equipo, capacidad de facilitar y liderazgo.

El autor menciona que al menos el 50% del trabajo de un arquitecto de software implica habilidades relacionadas con el liderazgo.

- 8. *Understand and navigate politics*

> El arquitecto debe entender el clima político de la empresa y saber moverse en él.

La idea es que la mayoría de los cambios arquitectónicos impactarán a más de un sector dentro de la compañía. Por lo tanto, el arquitecto siempre verá sus decisiones cuestionadas. Ya sea por P.O., gerentes o desarrolladores, el arquitecto deberá saber negociar de forma política y luchar para que sus decisiones sean aprobadas.

### Prácticas de ingeniería de software vs Procesos

En las páginas siguientes, el autor se esfuerza por distinguir el concepto de *Proceso vs Prácticas de Ingeniería*.

> Según el autor, el proceso se refiere a cómo se forman y gestionan los equipos, cómo se conducen las reuniones y el flujo de trabajo en la organización.

> Por otro lado, las prácticas de ingeniería de software son agnósticas a los procesos. Por ejemplo, el uso de CI es una práctica de ingeniería que no depende de ningún tipo de proceso en particular.

Esta diferencia se vuelve aún más evidente cuando vemos que, a lo largo de los últimos años, varias prácticas de ingeniería de software (automatización, pruebas, SSOT) fueron adoptadas por metodologías de desarrollo como XP (Extreme Programming), por ejemplo.

Las prácticas de ingeniería son importantes y no deben despreciarse, porque están íntimamente relacionadas con la arquitectura de la aplicación que se está desarrollando. __Así como existen diferentes arquitecturas para diferentes problemas, existen diferentes prácticas de ingeniería para diferentes problemas - aquí la relación es simbiótica.__

### Leyes de la Arquitectura de Software

Por último, el autor describe dos leyes generales que rigen la arquitectura de software y que van a atravesar toda la idea central del libro.

- 1. *"Todo en la arquitectura de software es un trade-off".* (Si un arquitecto cree haber descubierto algo que no tiene un trade-off, lo más probable es que todavía no lo haya identificado)
- 2. *"El porqué es más importante que el cómo".*

## Próximo artículo de la serie

[Resumen/Análisis del libro: Fundamentals of Software Architecture - Cap. 2]({{< ref "posts/fundamentals_of_software_arch_chap_2" >}} "Capítulo 2")
