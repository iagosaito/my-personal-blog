---
title: "Book Summary/Analysis: Fundamentals of Software Architecture - Ch. 1"
date: 2023-06-02T19:52:00-03:00
draft: false
tags: [fundamentals of software architecture, software architecture, book resume]
categories: [Book Resume, Architecture]
---

## Preface - Invalidating Axioms

The author's goal is to establish a definition of what an axiom is and how it can (or cannot) be applied within the field of *Software Architecture*.

According to the author, *"an axiom is a statement or proposition which is regarded as being established, accepted, or self-evidently true"*. An example
of a famous axiom in mathematics is the [__Peano equality axiom__](https://en.wikipedia.org/wiki/Peano_axioms) used in set theory:

> Knowing that A = C and B = C, we can state that A = B.

Although these rules are rigid in mathematics, the author believes that
in the field of software engineering __this should not exist__.

This is fundamentally because software development is constantly changing. Over the last two decades, software engineering practices have changed completely. We went from XP to CI/CD. Then came the DevOps revolution, microservices, containers and the Cloud.

The author describes this frequent change as __Dynamic Equilibrium__. It is as if the software development universe were something alive, always trying to find the balance between the advantages of innovations and the inevitable trade-offs.

This definition reminded me of last week's controversy in which [Amazon Prime Video swapped its microservices and serverless system for a monolithic architecture, cutting its costs by 90%](https://www.primevideotech.com/video-streaming/scaling-up-the-prime-video-audio-video-monitoring-service-and-reducing-costs-by-90), sending the monolith vs microservices debate into a new round. Once again, __Dynamic Equilibrium__.

This kind of discussion is mentioned in the preface since, according to the author, *"it's easy to become enamored with a particular technology or approach"*; however, an architect's role is to have an exact sense of what is good and bad and to understand exactly the trade-offs within each choice.

> In short, the general idea of the book is to rethink the axioms within software architecture and understand the trade-offs involved, always taking into account the development ecosystem we have today.

## Chapter 1 - Introduction

### *Roadmap* for a Software Architect

In the first chapter the author tries to explain why there is no specific *path* or *roadmap* for a *Software Architect* career.

The author highlights four main reasons:

- 1. The difficulty of defining what a *Software Architect* is.
- 2. The enormous scope of responsibilities and skills required of a *Software Architect*.
- 3. The constant change of software development ecosystems.
- 4. Outdated material about *Software Architecture*.

A well-known quote by *Ralph Johnson* is cited

> *"Architecture is about the important stuff... whatever that is."* - Ralph Johnson

He argues that it is hard to define what a software architect is. The industry has no definition because of the broad range of skills a *Software Architect* needs, and also because that scope constantly changes in search of balance (again the idea of *Dynamic Equilibrium*).

For example, until some time ago it was said that the *Software Architect* was the person who dealt with the parts of systems that __were hard (or expensive $$) to change__.
Although part of that is still true, architectural styles such as microservices go against this idea, since they aim at building software incrementally, so that a structural change does not become expensive.

### Defining *Software Architecture*

The author tries to answer this question by answering another one: __What is analyzed when a software architect analyzes an architecture?__

For the author, what an architect must analyze is a set of four things:

- 1. The structure of a system.

This refers to the type of architectural style, for example: microservices, layered, microkernel, etc.

- 2. The characteristics a system must support ("ilities").

These refer to a system's success criteria, unrelated to its functionality but necessary for it to work properly. For example: availability, scalability, testability, etc.

- 3. Architecture decisions.

Definitions of the rules for how the system should be built and its constraints.

For example, the architect can decide that, in a layered architecture, the presentation layer cannot interact directly with the database.

- 4. Design principles.

Guidance given to the development team, for example, using asynchronous communication between services. This kind of guidance will lead the developer to choose the most suitable technology for that purpose.

The difference between 3 (architecture decisions) and 4 (design principles) is basically rigidity. Principles serve as guidelines, while architecture decisions provide constraints that should be followed as closely as possible.

### Defining the role of a Software Architect

In this part of the chapter the author argues that defining what a *Software Architect* does is also hard, since the role can vary from company to company. For that reason, the author prefers to focus on the __expectations__ of the role, citing eight main ones.

He explains each of these in detail; to keep this from getting too long, I will try to summarize the key points.

- 1. *Make architecture decisions.*

> The architect should define the architecture decisions and design principles used to guide the team's technology choices; therefore, __they should guide rather than dictate__.

For example, according to the author, they should guide the team to use a reactive frontend framework for web development instead of dictating that the application must be built with React.js.

- 2. *Continually analyze the architecture.*

> The architect should continually analyze the architecture of the applications and propose solutions for their improvement and vitality.

They should ask themselves: Is the architecture built four years ago still viable, or does it show signs of decay? Are the architectural characteristics (ilities) still being met?

- 3. *Keep current with latest trends.*

> The architect should keep up to date with new technologies and new industry trends.

- 4. *Ensure compliance with decisions.*

> The architect should continually verify that the development team is following the architecture decisions and design principles that were communicated and documented.

- 5. *Diverse exposure and experience.*

> The architect should be exposed to different technologies, frameworks, platforms and environments.

The idea is not for them to be an expert in every technology and language, but to be familiar with a variety of technologies. For example: it is better for an architect to know 10 different caching products and the pros and cons of each than to be an expert in just one.

- 6. *Have business domain knowledge.*

> The architect should have expertise in the business domain.

Without understanding the problem your architecture is meant to solve, it is impossible to create an architecture that meets the business requirements.

- 7. *Possess interpersonal skills.*

> The architect should have exceptional interpersonal skills, including teamwork, facilitation and leadership.

The author mentions that at least 50% of a software architect's job involves leadership-related skills.

- 8. *Understand and navigate politics*

> The architect should understand the company's political climate and know how to navigate it.

The idea is that most architectural changes will impact more than one area within the company. So the architect will always have their decisions challenged. Whether by POs, managers or developers, the architect must know how to negotiate politically and fight to get their decisions approved.

### Software engineering practices vs Processes

In the following pages, the author makes an effort to distinguish the concept of *Process vs Engineering Practices*.

> According to the author, process refers to how teams are formed and managed, how meetings are conducted, and the workflow within the organization.

> On the other hand, software engineering practices are process-agnostic. For example, using CI is an engineering practice that does not depend on any particular kind of process.

This difference becomes even more evident when we see that, over the last few years, several software engineering practices (automation, testing, SSOT) have been adopted by development methodologies, such as XP (Extreme Programming), for example.

Engineering practices are important and should not be overlooked, because they are closely related to the architecture of the application being developed. __Just as there are different architectures for different problems, there are different engineering practices for different problems - the relationship here is symbiotic.__

### Laws of Software Architecture

Finally, the author describes two general laws that govern software architecture and that will run through the book's central idea.

- 1. *"Everything in software architecture is a trade-off".* (If an architect thinks they have discovered something that isn't a trade-off, more likely they just haven't identified the trade-off yet)
- 2. *"Why is more important than how".*

## Next article in the series

[Book Summary/Analysis: Fundamentals of Software Architecture - Ch. 2]({{< ref "posts/fundamentals_of_software_arch_chap_2" >}} "Chapter 2")
