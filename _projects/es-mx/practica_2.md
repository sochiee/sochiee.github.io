---
page_id: practica_2
layout: page
title: Método QR
description: Para calculo de eigenvalores 
img: assets/img/practicas/converge.png
importance: 2
category: Taller de Modelado
related_publications: true
---

El método QR para el calculo de eigenvalores consiste en calcular la factorización QR de una matriz.

$$
A = QR
$$

De aquí, podemos reordenar las matrices de tal manera que:

$$
RQ = ( Q^{T} A ) Q
$$

Además, como Q es una matriz ortonormal, sabemos que $$ Q^{-1} = Q^{T} $$. Por lo que RQ es una matriz simétrica a A y, en consequencia, tiene los mismos eigenvalores.
Así, definimos a $$ A_{n+1} $$ como RQ y repetimos el proceso. Cuando n tiende a infinito, si A es simetrica, el proceso convergera a una matriz diagonal con los eigenvalores
de A.

