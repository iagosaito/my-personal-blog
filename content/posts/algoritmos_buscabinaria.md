---
title: "Algoritmos: Busca Binária"
date: 2023-05-22T13:47:39-03:00
draft: false
tags: [algorithms, search_algorithms]
categories: [Algorithms]
---

# Algoritmos: Busca Binária

> Classificação: Algoritmo de busca
>
> Tempo de execução (BigO Notation): O(log n)

Alguns dias atrás, eu me deparei com um programa chamado *A Culpa é do Cabral* na televisão. Nesse programa, havia o quadro *“Jogo do balão”*, cuja ideia principal é que os participantes respondam perguntas de conhecimento geral e, conforme o tempo passa, o balão enche. Cada vez que um participante responde corretamente, ele passa o balão para o próximo participante. O participante que estiver com o balão em mãos no momento em que estourar, perde o jogo. Simples, não?

Caso ainda não tenha ficado claro, veja esse trecho de 15 segundos de um programa de *A Culpa é do Cabral — Jogo do Balão*:

<iframe width="560" height="315" src="https://www.youtube.com/embed/X-TTl-EM2_o?clip=UgkxlStXf8QW3wGEV30ptMk1pNhGAvnFoQJ5&amp;clipt=ENz_Axif9wQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Vamos entender esse diálogo entre o apresentador e o participante.

Apresentador — “Segundo o IBGE, quantas festas de casamento o Brasil celebra por dia?”.

Nesse momento o participante faz a sua primeira tentativa: “20 mil por dia”.

O apresentador, em seguida, dá uma dica para o participante e diz: “Menos!”.

O participante faz uma nova tentativa: “10 mil por dia”. E o Apresentador dá mais uma dica: “Menos!”. Participante: “200”. Apresentador: “Mais!”, e continua… Até o participante acertar o valor de 3 mil.

Depois disso tudo talvez se pergunte: o que isso tem a ver com a busca binária? Pois bem, a busca binária é, fundamentalmente, __uma forma de encontrar um valor alvo por meio de tentativas/dicas dentro de uma lista ordenada!__

## Busca Binária

A busca binária tem por característica estas três palavras chaves: alvo, tentativa e dica.

Pensando no *Jogo do Balão* é possível facilmente definir essas três palavras chave.

Alvo = Número de festas de casamento no Brasil por dia (3 mil)
Tentativa = Os chutes do participante (20 mil, 10 mil, 200…)
Dicas = “Menos!” e “Mais!”.
A diferença entre as tentativas do participante para o algoritmo de busca binária é que o algoritmo sempre verificará a posição do meio da lista. Caso o valor do meio seja menor que o valor alvo, toda a metade antes do meio é eliminada; caso seja maior, toda a metade maior é eliminada. Ficou confuso?

## Exemplo prático

Imagine uma lista de 10 elementos ordenados de maneira crescente. O objetivo é encontrar em qual posição está o número 13 — sendo assim, o número 13 é o alvo.

<figure>
    <img src="/img/algoritmos/buscabinaria/buscabinaria_img1.jpg" alt="Texto alternativo">
    <figcaption>Imagem 1 — Lista de números em ordem crescente</figcaption>
</figure>

A busca binária, primeiro, irá verificar se o elemento do meio da lista é igual ao alvo. Como podemos observar na imagem abaixo, o número 10 (tentativa) é menor que o 13 (alvo).

<figure>
    <img src="/img/algoritmos/buscabinaria/buscabinaria_img2.jpg" alt="Texto alternativo">
    <figcaption>Imagem 2 — Verifica se a tentativa é igual ao alvo</figcaption>
</figure>

O algoritmo, portanto, irá eliminar todos os números antes do meio. A partir disso, podemos identificar duas características importantes da busca binária:

- A ordenação é obrigatória: Isso faz sentido porque se a lista está ordenada de maneira crescente e sabemos que o número do meio (10) é menor que o alvo (13), logicamente todos os números antes do meio também serão menores que o alvo. Se a lista não estivesse ordenada seria impossível chegar a essa conclusão.
- A cada rodada de tentativa, a busca binária __elimina metade dos elementos__.

Depois de eliminar os elementos, chegou a hora de fazer uma nova tentativa. O processo se repete. O algoritmo irá verificar qual é o elemento do meio em relação aos elementos que sobraram, conforme mostra a figura abaixo.

<figure>
    <img src="/img/algoritmos/buscabinaria/buscabinaria_img3.jpg" alt="Texto alternativo">
    <figcaption>Imagem 3 — Elementos ignorados e nova tentativa</figcaption>
</figure>

O elemento 19 (tentativa) é igual a 13 (alvo)? Não. Sendo assim, eliminaremos todos os elementos a direita do meio, porque 19 é maior do que 13.

Depois disso, o processo novamente é realizado. Como só restaram dois elementos, o primeiro é considerado como meio.

<figure>
    <img src="/img/algoritmos/buscabinaria/buscabinaria_img4.jpg" alt="Texto alternativo">
    <figcaption>Imagem 4 — Elementos ignorados a direita do meio e uma nova tentativa sendo feita</figcaption>
</figure>

Opa! A nossa tentativa (13) é igual ao alvo (13)! Parabéns, o algoritmo foi executado com sucesso.

> OBS: Como mencionado no início, esse algoritmo possui um tempo de execução logarítmico. Isso faz com que esse algoritmo seja muito eficiente para buscas.
> 
> Ex: Caso tenhamos uma lista de 4 bilhões de elementos, __o algoritmo encontraria o alvo em, no máximo, 32 tentativas__!

## Código
O código abaixo representa um algoritmo de busca binária criado a partir da linguagem de programação Golang.

```
package main

import "fmt"

func main() {
	fmt.Println("Binary Search...")

	list := []int{2, 3, 5, 7, 10, 13, 15, 19, 23, 30}
	position := binarySearch(list, 13)

	fmt.Println(position)
}

func binarySearch(list []int, target int) int {

	low := 0
	high := len(list) - 1

	for low <= high {
		middle := (high + low) / 2
		attempt := list[middle]

		if attempt == target {
			return middle
		}

		if attempt > target {
			high = middle - 1
		}

		if attempt < target {
			low = middle + 1
		}
	}

	return -1
}
```

Um ponto acerca do código merece consideração:

- Existem duas variáveis que guardam referência ao início da lista (low) e ao final da lista (end). Quando eliminamos os elementos antes do meio, a variável low é atualizada, apontando para o elemento seguinte depois do meio; quando eliminamos os elementos depois do meio, a variável end é atualizada, apontando para o primeiro elemento antes do meio.

## Referências

- https://en.wikipedia.org/wiki/Binary_search_algorithm
- Learning Algorithms, by George Heineiman
- Grokking Algorithms — An illustrated guide for programmers and other curious people, by Aditya Y. Bhargava

