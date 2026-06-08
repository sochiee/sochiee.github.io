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

Sea

$$
A = 
\begin{pmatrix}
5 & -2\\
-2 & 8
\end{pmatrix}
$$

Podemos usar el metodo del polinomio caracteristico para calcular sus eigenvalores.

$$
\begin{align*}
& Det( A - I \lambda ) = 0 \\
\iff & \lambda ^{2} - 13 \lambda + 36 = 0 \\
\iff & \lambda _{1} = 4 \quad \lambda _{2} = 9
\end{align*}
$$ 

Sin embargo, calcular el determinante de este modo para matrices más grandes es computacionalmente impractico. Así, usaremos el método QR para calcular los eigenvalores de A.


Dada una función que calcula la factorización QR de una matriz A, definimos la siguiente función.

'''python

def eigenvals(A: list[list[float]], n: int = 100) -> list[float]:

    Ak = A 

    for _ in range(n):
        Q, R = qr(Ak)
        Ak = matmul(R, Q)
        
    return Ak
'''

