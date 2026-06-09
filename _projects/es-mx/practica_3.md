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


En este caso, una buena manera de aproximar una $$k$$ es mediante la regresion lineal simple, ya que solo contamos con una variable independiente de volumen.
Supongamos que para nuestras observaciones $$\{x_i, y_i\}^{n}_{i=1}$$ se tiene el siguiente modelo:

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
                  &= -2 \sum_{i=1}^n x_i y_i - k x_i^2 
\end{align*}
$$



