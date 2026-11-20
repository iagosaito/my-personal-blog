---
title: "Resumen/Análisis del libro: Fundamentals of Software Architecture - Cap. 2"
date: 2023-07-01T00:41:22-03:00
draft: false
tags: [fundamentals of software architecture, software architecture, book resume]
categories: [Book Resume, Architecture]
---

> El capítulo dos introduce la primera parte del libro: __Foundations__

# Capítulo 2 - Pensamiento arquitectónico

En este capítulo, el autor menciona cuatro aspectos necesarios para desarrollar un pensamiento arquitectónico:

- 1. Entender la diferencia entre arquitectura y diseño

- 2. Amplitud vs profundidad de conocimiento

- 3. Entender y analizar trade-offs

- 4. Entender los _business drivers_ y traducirlos a la arquitectura

Cada aspecto se explora con más detalle a continuación.

## Arquitectura vs Diseño

Observa las diferencias entre las responsabilidades del arquitecto - la arquitectura - y las responsabilidades del desarrollador - el diseño del código de la aplicación.

El arquitecto tiene como responsabilidad:

> - Analizar los requisitos de negocio y, a partir de ellos, definir las características arquitectónicas ("ilities").
>
> - Definir el patrón arquitectónico y los principios de diseño.
>
> - Crear componentes o bloques del sistema.

Mientras que el desarrollador tiene como responsabilidad:

> - Crear las interfaces (o pantallas) de la aplicación.
>
> - Desarrollar y probar el código fuente.
>
> - Crear diagramas de clases (considero esto una responsabilidad MUY CUESTIONABLE, pero así lo ejemplifica el autor).

El autor argumenta que el gran problema es que, en los modelos de desarrollo tradicionales, la comunicación entre el arquitecto y el equipo de desarrollo ocurría de manera **unilateral**, creando una desconexión. Algunas decisiones que tomaba el arquitecto no eran aplicadas por el equipo de desarrollo, mientras que las decisiones que tomaba el equipo de desarrollo y que alteraban la arquitectura no se le comunicaban al arquitecto.

La solución, por lo tanto, es tener un feedback constante y una comunicación **bilateral**, abierta y receptiva entre el arquitecto y el equipo de desarrollo. Esto permite que el arquitecto baje de su trono (ejem...) y pase a formar parte del equipo, haciendo de mentor de los desarrolladores.

Observa que hay un contraste claro entre los dos enfoques. Uno estático, parecido al modelo de desarrollo en cascada; y otro iterativo, abierto a los cambios, ágil, como debe ser.

El autor concluye con la siguiente pregunta:

> _¿Cuándo termina entonces la arquitectura y empieza el diseño de software?_
>
> R: No termina. Ambos forman parte del ciclo de desarrollo y deben estar en sintonía.

## Technical Breadth (Amplitud técnica)

El conocimiento técnico puede dividirse en una pirámide de tres niveles, de la base a la cima:

- Cosas que no sabes que no sabes.

- Cosas que sabes que no sabes.

- Cosas que sabes.

Al comenzar la carrera de desarrollo, lo ideal es intentar expandir la cima de la pirámide (cosas que sabes). De esta forma, el programador gana experiencia y conocimiento, es decir: _Technical Depth_ (profundidad técnica).

Con el paso del tiempo, a medida que el desarrollador evoluciona y llega al cargo de arquitecto, su enfoque debe cambiar. Ahora debe buscar un equilibrio entre la cima y el medio de la pirámide. **Para un arquitecto, la amplitud (Breadth) es más importante que la profundidad (Depth)**. Es mejor que conozca los trade-offs de 10 herramientas de caché diferentes que ser experto en una sola.

Esto significa que el arquitecto quizás renuncie a algunas habilidades que había adquirido durante las etapas iniciales como desarrollador - quedándose oxidado, por así decirlo. No solo el arquitecto, sino todo desarrollador debe medir a lo largo de su carrera el balance entre expertise y profundidad. Hay que saber qué batallas pelear.

## Analizando trade-offs

Según el autor, pensar como arquitecto significa ver los trade-offs en cada solución. A diferencia de los desarrolladores, que suelen ver solo los beneficios de una solución determinada, los arquitectos necesitan ver las dos caras de la moneda.

Entonces, si alguien pregunta qué es mejor: ¿Tópicos o Colas?

La respuesta: **Depende**. He aquí por qué.

El autor propone un ejercicio relacionado con una aplicación de subastas con 4 componentes: Bid Producer, Bid Capture, Bid Tracking, Bid Analytics.

<figure>
    <img src="/img/fundamentals_of_software_arch/chap2/img1.jpg" alt="Representación de los componentes del sistema de subastas">
    <figcaption style="text-align: center;">Imagen 1 - Sistema de subastas</figcaption>
</figure>

Como vemos en la figura 1, el Bid Producer produce un Bid (puja) que se transmite a tres servicios: Capture, Tracking y Analytics.

Esto puede hacerse de dos formas, usando colas o tópicos, como muestran las siguientes imágenes.

### Tópicos

<figure>
    <img src="/img/fundamentals_of_software_arch/chap2/img2.jpg" alt="Comunicación entre servicios usando un tópico">
    <figcaption style="text-align: center;">Imagen 2 - Comunicación entre servicios usando un tópico (pub-sub)</figcaption>
</figure>

#### Ventajas

La ventaja obvia de los tópicos es la **extensibilidad**. Si un nuevo servicio - como por ejemplo _Bid History_ - necesita escuchar las pujas, bastará con suscribirse al tópico y no habrá que cambiar nada en el sistema. Se crea un desacoplamiento entre el servicio que produce y los demás que lo escuchan.

#### Desventajas

Las desventajas, sin embargo, no son tan obvias, y por eso el trabajo del arquitecto es tan importante. Un punto a considerar es que cualquier servicio podrá acceder a los datos de la subasta (Item Bid) sin que el Producer se entere, creando una brecha de seguridad en la aplicación.

Otro punto, y particularmente el más interesante, es que un sistema de tópicos con pub/sub tiene un contrato homogéneo. Todos los servicios que se suscriben al tópico deben aceptar el mismo contrato de mensaje. Si un servicio específico necesita una información adicional que los demás no necesitan, todos los servicios se verán afectados por el cambio del contrato.

### Colas

<figure>
    <img src="/img/fundamentals_of_software_arch/chap2/img3.jpg" alt="Comunicación entre servicios usando colas">
    <figcaption style="text-align: center;">Imagen 3 - Comunicación entre servicios usando colas</figcaption>
</figure>


#### Ventajas

De inmediato se puede identificar que, a diferencia del modelo de tópicos (pub/sub), las colas permiten contratos heterogéneos entre los distintos servicios que consumen los mensajes. Otro factor es la capacidad de escalar los servicios de manera independiente, mediante un Load Balancer asociado a cada cola.

Por último, las colas tienen menos brechas de seguridad, ya que dependen de la asociación específica entre un Producer -> Cola -> Consumidor.

#### Desventajas

Alto acoplamiento: para cada nuevo consumidor se necesita una nueva cola y, por lo tanto, no tiene una alta extensibilidad.

---------------------------------------------------------------------------

El ejemplo dejó claro que todo en la arquitectura de software son trade-offs. Un arquitecto analiza cada aspecto comentado arriba, tomando como parámetro los requisitos de pensamiento arquitectónico mencionados anteriormente.

Si alguien pregunta: ¿cuál debo usar, colas o tópicos? La respuesta es: __¡Depende!__

### Hands-on Coding (manos a la obra)

En la última parte del capítulo, el autor analiza las dificultades del arquitecto para mantener el equilibrio entre la arquitectura de software y la programación.

Perder la práctica de escribir código no es saludable. Al mismo tiempo, se crea un cuello de botella terrible si el arquitecto se vuelve "dueño" del código del equipo. Muchas veces esto ocurre cuando el arquitecto toma para sí las tareas más complejas del proyecto - que la mayoría de las veces son las que van más allá del framework utilizado en el momento.

El autor presenta cinco maneras en que el arquitecto puede, continuamente, mantenerse hands-on sin perjudicar al equipo:

- Crear POCs (pruebas de concepto).

- Trabajar en la deuda técnica y dejarle al equipo las funcionalidades más críticas.

- Trabajar en bug fixes.

- Crear herramientas de línea de comandos para ayudar al proceso de desarrollo del equipo.

- Hacer code reviews con frecuencia.

## Próximo artículo de la serie

*Artículo y lectura todavía en curso... Pronto el enlace aparecerá por aquí. Gracias*
