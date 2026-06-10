---
page_id: practica_3
layout: page
title: Modelos De Similitud Geométrica
description: El Problema del Campeonato de Pesca De Róbalo
img: assets/img/practicas/fishe.jpg
importance: 3
category: Taller de Modelado
related_publications: true
pretty_table: true
---

<span style="font-size: 12px;">_En colaboración con Galeana Morán Miguel Ángel y Chalche Julio César_</span>


Queremos saber el peso de un Róbalo conociendo únicamente mediciones hechas con una cinta metrica. Para el modelo supondremos varias cosas.

- Todos los pescados son de la misma especie
- La densidad de los pescados es constante
- Los Róbalos son geometricamente similares 

Los datos que tenemos sobre los peces son los siguientes: 

| Longitud (cm) | 36.81 | 31.77 | 43.82 | 36.82 | 32.07 | 45.07 | 35.89 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Peso (kg)** | 0.78 | 0.47 | 1.16 | 0.74 | 0.44 | 1.40 | 0.64 |

Como la densidad de los pescados es constante y son geometricamente similares, podemos concluir que $$W \propto V$$. Al graficar esta relación usando los
datos anteriores tenemos: 

<div class="row">
    <div class="col">
        {% include figure.liquid loading="eager" path="assets/img/practicas/pesovolumen.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Usando los datos anteriores, queremos obtener un modelo que al darle una longitud nos devuelva una buena aproximación del peso. Es decir, un modelo de la forma $$W = k l^3$$ para algún $$k$$. 


En este caso, una buena manera de aproximar una $$k$$ es mediante la regresion lineal simple. Sabemos esto debido a que, al calcular el coeficiente de pearson de los volumenes y pesos, obtenemos que $$r \approx 0.99$$ por lo que hay una correlación lineal directa. Ya que solo contamos con una variable independiente de volumen, supongamos que para nuestras observaciones $$\{x_i, y_i\}^{n}_{i=1}$$ se tiene el siguiente modelo:

$$
\begin{align*}
& y_i = k x_i + \epsilon _i \\
\iff & \epsilon _i  = y_i - k x_i
\end{align*}
$$ 

En donde $$\epsilon _i$$ es el error o diferencia entre nuestro modelo y los datos reales. Así, definimos una funcion de error $E$:

$$
\begin{align*}
E(k) &= \sum_{i=1}^n \epsilon _{i}^{2} \\
     &= \sum_{i=1}^n (y_i - k x_i)^2
\end{align*}
$$

Para encontrar la mejor aproximación posible de k queremos minimizar el error, para ello tenemos que encontrar el minimo de la función anterior. Derivando con respectdo a k:

$$
\begin{align*}
\frac{d}{dk} E(k) &= \frac{d}{dk} \sum_{i=1}^n \epsilon _{i}^{2} \\
                  &= -2 \sum_{i=1}^n x_i y_i - k x_i^2 \\
\end{align*}
$$

Igualamos la derivada a 0 

$$
\begin{align*}
& -2 \sum_{i=1}^n x_i y_i - k x_i^2 = 0 \\
\iff & \sum_{i=1}^n x_i y_i - k \sum_{i=1}^n x_i^2 = 0 \\
\iff & k = \frac{\sum_{i=1}^n x_i y_i}{\sum_{i=1}^n x_i^2}
\end{align*}
$$

El cual es el valor deseado de $$k$$. Programamos una función en Python que nos permite obtener el valor de $$k$$ dada una lista de longitudes (variable independiente) y pesos (variable dependiente)

```python
def rls(x, y):
    xy = [xi * yi for xi, yi in zip(x, y)]
    x2 = [xi**2 for xi in x]

    suma_xy = sum(xy)
    suma_x2 = sum(x2)

    k = suma_xy / sum_x2

    return k
```

Al ejecutar la función con los volumenes y los pesos de los Róbalos, nos regresa el siguiente valor para k:

```bash
## 1.4610241788737212e-05
```
Al graficar la función $$W=k l^3$$ en la gráfica de comparación de nuestros valores, obtenemos lo siguiente:

<div class="row">
    <div class="col">
        {% include figure.liquid loading="eager" path="assets/img/practicas/aproximacion_lineal.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


Como se puede observar, el valor de k obtenido nos da una buena aproximación lineal.


Ahora supongamos que además de la longitud del pez, también tenemos los datos de su circunferencia máxima. 

| **Longitud (cm)** | 36.81 | 31.77 | 43.82 | 36.82 | 32.07 | 45.07 | 35.89 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Peso (kg)** | 0.78 | 0.47 | 1.16 | 0.74 | 0.44 | 1.40 | 0.64 |
| **Circunferencia_Max** | 24.77 | 21.29 | 27.94 | 24.77 | 21.59 | 31.75 | 22.86 |

Con lo anterior, podemos hacer dos nuevas suposiciones para nuestro modelo: 

- Solo la sección transversal de los peces es geometricamente similar
- La dimensión característica de los peces es su circunferencia máxima

$$
\begin{align*}
\implies & V \propto l_e ( A_{prom} ) \\
\iff     & V \propto l C_{max}^2
\end{align*}
$$ 

Entonces, ahora tenemos observaciones de la forma $$\{x_{i1}, x_{i2}, y_i\}^{n}_{i=1}$$:

$$
\begin{align*}
& y_i = \beta _0 x_{i1} + \beta _1 x_{i2} + \epsilon _i \\
\iff & \epsilon _i  = y_i - \beta _0 x_{i1} - \beta _1 x_{i2}
\end{align*}
$$ 

Nuevamente definimos nuestra función de error: 

$$
\begin{align*}
E(\beta _0, \beta _1) &= \sum_{i=1}^n \epsilon _{i}^{2} \\
                      &= \sum_{i=1}^n (y_i - \beta _0 x_{i1} - \beta _1 x_{i2})^2
\end{align*}
$$

Tomamos las derivada parciales con respecto a $$\beta _0$$ y $$\beta _1$$:


$$
\begin{align*}
\frac{\partial}{\partial \beta _0} E(\beta _0, \beta _1) &= \frac{\partial}{\partial \beta _0} \sum_{i=1}^n (y_i - \beta _0 x_{i1} - \beta _1 x_{i2})^2 \\
                      &= -2 ( \sum_{i=1}^n y_i x_{i1} - \beta _0 \sum_{i=1}^n x_{i1}^2 - \beta _1 \sum_{i=1}^n x_{i2}x_{i1} )
\end{align*}
$$

$$
\begin{align*}
\frac{\partial}{\partial \beta _1} E(\beta _0, \beta _1) &= \frac{\partial}{\partial \beta _1} \sum_{i=1}^n (y_i - \beta _0 x_{i1} - \beta _1 x_{i2})^2 \\
                      &= -2 ( \sum_{i=1}^n y_i x_{i2} - \beta _0 \sum_{i=1}^n x_{i1}x_{i2} - \beta _1 \sum_{i=1}^n x_{i2}^2 )
\end{align*}
$$

Igualando ambos a cero, obtenemos el siguiente sistema de ecuaciones en forma matricial:

$$
\begin{bmatrix}
\sum_{i=1}^n x_{i1}^2 & \sum_{i=1}^n x_{i2}x_{i1} \\
\sum_{i=1}^n x_{i1}x_{i2} & \sum_{i=1}^n x_{i2}^2
\end{bmatrix}
\begin{bmatrix}
\beta_0 \\
\beta_1
\end{bmatrix} =
\begin{bmatrix}
\sum_{i=1}^n y_i x_{i1} \\
\sum_{i=1}^n y_i x_{i2}
\end{bmatrix}
$$

Definimos otra función en python que resuelva el sistema de ecuaciones utilizando numpy:

```python
def rlm(x1, x2, y):
    x1sq = [xi ** 2 for xi in x1]
    x2sq = [xi ** 2 for xi in x2]
    x1x2 = [xi1 * xi2 for xi1, xi2 in zip(x1, x2)]

    suma_x1x2 = sum(x1x2)
    suma_x1sq = sum(x1sq)
    suma_x2sq = sum(x2sq)

    yx1 = [y * xi for y, xi in zip(y, x1)]
    yx2 = [y * xi for y, xi in zip(y, x2)]

    suma_yx1 = sum(yx1)
    suma_yx2 = sum(yx2)

    A = np.array([[suma_x1sq, suma_x1x2],[suma_x1x2, suma_x2sq]])
    
    B = np.array([[suma_yx1],[suma_yx2]])
    
    solucion = np.linalg.solve(A, B)

    return solucion
```

Como queremos una aproximación de la forma $$W=\beta_0 l^3 + \beta_1 l C_{max}^2$$. Al ingresar la lista de las longitudes y las circunferencias máximas nos regresa los siguientes valores de $$\beta_0$$ y $$\beta_1$$:

```bash
## -0.012237, 0.001990
```

Y al graficarlos obtenemos la siguiente gráfica: 

<div class="row">
    <div class="col">
        {% include figure.liquid loading="eager" path="assets/img/practicas/aproximacion_multilineal.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>





