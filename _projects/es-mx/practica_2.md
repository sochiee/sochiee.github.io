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
def eigenvals(A, n):
    
    Ak = A 

    for _ in range(n):
        Q, R = qr(Ak)
        Ak = matmul(R, Q) 

    return Ak
{% endhighlight %}

Esta función es una implementación del método QR. Dada una una matriz A y un numero n de iteraciones, corre un ciclo en donde define matrices simétricas a A usando su factorización QR, ya que: 

$$
\begin{align*}
& A = QR \\
\iff & Q^{T} A = R \\
\iff & Q^{T} A Q = R Q
\end{align*}
$$ 

Por lo cual, para cada iteracion, la matriz $$A_{k}$$ es una matriz simétrica a A. 


Al correr la función con la matriz A anteriormente definida y 100 iteraciones:

```bash
## [[8.999998191246124, -0.003007285510328984], [-0.003007285510328903, 4.000001808753881]]
```

La cual es una matriz cuyos valores de su diagonal se aproximan a los eigenvalores de la matriz original. Si necesitamos una precisión especíca, podemos agregar una validación a la función

{% highlight python linenos %}
def eigenvals(A, epsilon, n):
    
    Ak = A 

    for i in range(n):
        Q, R = qr(Ak)
        Ak = matmul(R, Q) 

        if epsilon_check(Ak, epsilon):
            print(i)
            return Ak

    return Ak

def epsilon_check(A, epsilon):
    n = len(A)

    for i in range(n):
        for j in range(n):
            if abs(A[i][j]) >= epsilon and i != j:
                return False

    return True
{% endhighlight %}

Dada un $$\epsilon$$, la función epsilon_check revisa si hay algún elemento fuera de la diagonal mayor a el, si no lo hay, significa que alcanzamos la precisión deseada y regresa la
matriz. Si nunca cumple esa condición, continua hasta terminar el número máximo de iteraciones n.


Al correr la nueva función con una tolerancia $$\epsilon = 1 \times 10^{-10}$$ y un número máximo de iteraciones 1000: 

```bash
