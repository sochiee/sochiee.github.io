---
page_id: practica_1
layout: page
title: Sistema de Ecuaciones en Diferencia
description: Modelo Lotka-Volterra
img: assets/img/practicas/converge.png
importance: 1
category: Taller de Modelado
related_publications: true
---

<span style="font-size: 6px;">_En colaboración con Galeana Morán Miguel Ángel y Chalche Julio César_</span>


El modelo Lotka-volterra es una representación de un sistema biológico en el que dos especies interactuan, una como presa y la otra como depredador.
Consiste en las siguientes ecuaciones diferenciales, las cuales describen las dinámicas entre las dos poblaciones.

$$
\frac{dx}{dt} = \alpha x - \beta xy
$$

$$
\frac{dy}{dt} = - \gamma y + \delta xy
$$

En donde las variables $$x$$ y $$y$$ representan la densidad de las poblaciones de presa y depredador respectivamente. Mientras que $$\alpha$$ es el crecimiento per capita de
las presas, $$\beta$$ el efecto de los depredadores sobre la mortalidad en población de presas, $$\gamma$$ la tasa de mortalidad de los depredadores y $$\delta$$ el efecto de la
población de presas sobre el crecimiento de los depredadores.


Lo anterior es equivalente al siguiente sistema de ecuaciones en diferencias finitas.

$$
\begin{cases}
x_{n+1} = ( \alpha +1) - \alpha {x_{n}}^{2} - \beta x_{n} y_{n} \\
y_{n+1} = ( 1 - \gamma ) y_{n} + \delta y_{n} x_{n}
\end{cases}
$$

Este sistema es el que nos permite observar los cambios a tiempo discreto utilizando métodos computacionales.

<div class="row">
    <div class="col">
        {% include figure.liquid loading="eager" path="assets/img/practicas/preywin.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Gráfica del modelo con parámetros: alpha=0.08, beta=0.01, gamma=0.1, delta = 0.15
</div>

Podemos observar que, con el tiempo, la problación de depredadores disminuye hasta desaparecer, lo cual deja a la población de presa como la única restante.
Lo anteríor podría ser debido a un muy bajo efecto de los depredadores en la población de las presas y a una tasa de mortalidad de depredadores mayor a la tasa de crecimiento de las presas.
    
<div class="row">
    <div class="col">
        {% include figure.liquid loading="eager" path="assets/img/practicas/converge.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Gráfica del modelo con parámetros: alpha=0.25, beta=0.91, gamma=0.6, delta=1.8
</div>

En este caso se tiene que, dado un tiempo suficiente, ambas poblaciones encuentran un punto de equilibrio despues de un periodo de oscilación. Este punto $$P$$ de convergencia depende de las constantes de las ecuaciones.

$$
P = ( \frac{ \gamma }{ \delta } , \frac{ \alpha ( \delta - \gamma ) }{ \beta \gamma } )
$$

La abscisa del punto anterior es una solucion al sistema de ecuaciones diferenciales cuando ambas son igualadas a cero, es decir, cuando no hay ningun cambio en las poblaciones.


La población de depredadores posiblemente alcanza un punto de equilibrio debido a que la tasa de mortalidad es menor al efecto de presas sobre la población de depredadores.
Mientras que, a pesar de el limite en la población de depredadores, la población de presa llega a un equilibrio debido a su baja trasa de crecimiento y un alto efecto por parte de la población de depredadores.

<div class="row">
    <div class="col">
        {% include figure.liquid loading="eager" path="assets/img/practicas/cycle.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Gráfica del modelo con parámetros: alpha=0.25, beta=0.95, gamma=0.55, delta = 1.1
</div>

En el último caso, podemos ver que, aunque todas las constantes cumples las condiciones del caso anterior, dentro del lapso de tiempo dado nunca llegan a un punto de equilibrio. Esto se podría deber a que la diferencia entre algunas de las constantes es menor que en el casos anterior, especificamente en la tasa de mortalidad y el efecto de presas sobre la población de depredadores. Sin embargo, en la tercera gráfica se puede observar que las poblaciones sí se acercan lentamente a un punto de equilibrio. Es decir, dada una cierta cantidad de tiempo, las poblaciones encontraran llegaran a un equilibrio. Esta cantidad de tiempo depende de las poblaciones iniciales del modelo.

Las ecuaciónes en diferencia nos permiten analizar el comportamiento de modelos basados en ecuaciones diferenciales sin necesidad de resolver las mismas por metodos analíticos, lo cual puede llegar a ser increiblemente complicado e incluso imposible en algunos casos. Para las ecuaciones de Lotka-Volterra en especifico, nos permiten dar un análisis de los comportamientos de ambas poblaciones dadas diferentes constantes y poblaciones iniciales de una manera sencilla utilizando métodos computacionales. 
