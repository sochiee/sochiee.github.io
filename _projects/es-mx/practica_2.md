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

{% highlight python linenos %}
def eigenvals(A: list[list[float]], n: int = 100) -> list[float]:
    

    Ak = A  # A^0 = A original

    for _ in range(n):
        Q, R = qr(Ak)  # paso 1: factorizar
        Ak = matmul(R, Q)  # paso 2: recombinar al revés

    # Los eigenvalores están en la diagonal de Ak
    return [Ak[i][i] for i in range(len(Ak))]
{% endhighlight %}
