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

<table class="table-auto">
  <thead>
    <tr>
      <th>Longitud (cm)</th>
      <td>36.81</td>
      <td>31.77</td>
      <td>43.82</td>
      <td>36.82</td>
      <td>32.07</td>
      <td>45.07</td>
      <td>35.89</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Peso (kg)</th>
      <td>0.78</td>
      <td>0.47</td>
      <td>1.16</td>
      <td>0.74</td>
      <td>0.44</td>
      <td>1.40</td>
      <td>0.64</td>
    </tr>
  </tbody>
</table>

Como la densidad de los pescados es constante y son geometricamente similares, podemos concluir que $$W \propto V$$. Al graficar esta relación usando los
datos anteriores tenemos: 

<div class="row">
    <div class="col">
        {% include figure.liquid loading="eager" path="assets/img/practicas/pesovolumen.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
