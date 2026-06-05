---
page_id: practica_1
layout: page
title: Sistema de Ecuaciones en Diferencia
description: Modelo Depredador-Presa o Lotka-Volterra
img: assets/img/practicas/converge.png
importance: 1
category: Taller de Modelado
related_publications: true
---

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
x_{n+1} = ( \alpha +1) - \alpha {x_{n}}^{2} - \beta x_{n} y_{n} \\
$$ 

$$ 
y_{n+1} = ( 1 - \gamma ) y_{n} + /delta y_{n} x_{n]  
$$

Este sistema es el que nos permite observar los cambios a tiempo discreto utilizando métodos computacionales.

<div class="row">
    <div class="col">
        {% include figure.liquid loading="eager" path="assets/img/practicas/preywin.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col">
        {% include figure.liquid loading="eager" path="assets/img/practicas/converge.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col">
        {% include figure.liquid loading="eager" path="assets/img/practicas/cycle.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images, even citations {% cite einstein1950meaning %}.
Say you wanted to write a bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, _bled_ for your project, and then... you reveal its glory in the next row of images.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
