---
layout: seccion
title: Manipulación del DOM
parent:
    url: pages/introduccion-d3.html
    title: Introducción a D3
prev:
    url: pages/introduccion-d3.html
    title: Introducción a D3
next:
    url: pages/data-binding.html
    title: Data Binding
---

D3 permite manipular elementos del DOM usando datos. Para entender cómo funciona D3, necesitamos entender cómo el browser interpreta y pinta el contenido web.


### Qué es el DOM?

<aside>Para una introducción a HTML referimos a la siguiente guía de <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Introduction">MDN</a> _Mozilla Developer Network_.</aside>

El contenido de una página web está organizado como una serie de elementos que contienen otros elementos. Por ejemplo, el `<body>` contiene a todos los elementos visibles, el contenedor `<div>` se usa para crear bloques de contenido relacionado (barras de navegación, pie de página, columnas, etc). Esta organización se conoce como el DOM, _Document Object Model_.

Por ejemplo, el siguiente código HTML representa una lista no ordenada, que contiene dos ítems de lista. Cada uno contiene un link.

<div class="runnable" id="code-a01">
  <textarea class="form-control" rows="4">
  <ul>
     <li><a href="index.html" id="link-a02">Index</a></li>
     <li><a href="page1.html">Página 1</a></li>
  </ul>
  </textarea>
</div>

<ul>
   <li><a href="index.html">Index</a></li>
   <li><a href="page1.html">Página 1</a></li>
</ul>

<aside>Para una lista de elementos de HTML y sus respectivos atributos, consultar la <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element">documentación en el sitio MDN</a>.

<a href="https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_started">Introducción a CSS</a> en el sitio MDN.</aside>

Un elemento en el DOM puede tener cero o más atributos. Por ejemplo, un link normalmente tiene el atributo `href`, cuyo valor es la URL de la página a la que apunta el link. Además de los atributos del elemento, hay atributos de estilo, que se pueden asignar directamente, o a través de una hoja de estilo CSS

Usualmente, los browsers incluyen una consola que permite ver y manipular elementos del DOM en cualquier página. Las modificaciones al DOM son locales, sólo afectan a la copia de la página que esta viendo el usuario en ese momento.

### Manipulando el DOM

D3 permite manipular los elementos del DOM muy fácilmente, usando _selectores_ del DOM, que funcionan igual que las reglas de CSS. En el ejemplo anterior, el primer link tiene un ID `id="link-a02"`. Podemos seleccionar este elemento mediante su ID y cambiar, por ejemplo, su color.

<div class="ejemplo">
  <div id="ejemplo-a02">
    <ul>
        <li><a href="index.html" id="link-a02">Index</a></li>
        <li><a href="page1.html">Página 1</a></li>
    </ul>
  </div>
</div>

<aside>Para mayor información acerca de las selecciones, diríjase al artículo <a href="http://bost.ocks.org/mike/selection/">"How Selections Work"</a> del creador de D3, Mike Bostock.</aside>

<div class="runnable" id="code-a02">
d3.select('#link-a02').style('color', 'red');
</div>
<script>codeBlock().editor('#code-a02').init();</script>

Los selectores permiten seleccionar por ID, por clase, por tipo de elemento o incluso usando la estructura del documento. Para seleccionar un elemento de lista, podemos usar:

<div class="ejemplo">
  <div id="ejemplo-a03">
    <ul>
        <li><a href="index.html">Index</a></li>
        <li><a href="page1.html">Página 1</a></li>
    </ul>
  </div>
</div>

<div class="runnable" id="code-a03">
// Selecciona el primer elemento que encuentra bajo ese camino
d3.select('#ejemplo-a03 ul li').style('font-weight', 'bold');
</div>
<script>codeBlock().editor('#code-a03').init();</script>

Los métodos para cambiar atributos se pueden encadenar, por ejemplo, se puede poner `style('font-weight', 'bold').style('color', 'blue')`.

También se puede seleccionar varios elementos simultáneamente:

<div class="ejemplo">
  <div id="ejemplo-a04">
    <ul>
        <li><a href="index.html">Index</a></li>
        <li><a href="page1.html">Página 1</a></li>
    </ul>
  </div>
</div>

<div class="runnable" id="code-a04">
// Selecciona TODOS los elementos que encuentra bajo ese camino
d3.selectAll('#ejemplo-a04 ul li').style('font-weight', 'bold');
</div>
<script>codeBlock().editor('#code-a04').init();</script>

Las selecciones pueden almacenarse en variables:

<div class="ejemplo">
  <div id="ejemplo-a05">
    <ul>
        <li><a href="index.html">Index</a></li>
        <li><a href="page1.html">Página 1</a></li>
    </ul>
  </div>
</div>

<div class="runnable" id="code-a05">
// Almacena la selección el la variable `li`.
var li = d3.selectAll('#ejemplo-a05 li');

// Usa la selección para cambiar los atributos de los elementos
li.style('font-weight', 'bold');
</div>
<script>codeBlock().editor('#code-a05').init();</script>

Se pueden crear subselecciones:

<div class="ejemplo">
  <div id="ejemplo-a06">
    <ul>
        <li><a href="index.html">Index</a></li>
        <li><a href="page1.html">Página 1</a></li>
    </ul>
  </div>
</div>

<div class="runnable" id="code-a06">
// Almacena la selección el la variable `li`.
var div = d3.select('#ejemplo-a06');

// Usa la selección para cambiar los atributos de los elementos
div.selectAll('li').style('font-weight', 'bold');
</div>
<script>codeBlock().editor('#code-a06').init();</script>

### Agregando y Eliminando Elementos

Podemos agregar y eliminar elementos del DOM. Por ejemplo,

<div class="ejemplo">
  <div id="ejemplo-a07">
    <ul>
        <li>Peras</li>
        <li>Manzanas</li>
    </ul>
  </div>
</div>

<div class="runnable" id="code-a07">
// Almacena la selección el la variable `li`.
var ul = d3.select('#ejemplo-a07 ul');

var li = ul.append('li');

li.html('Pitufos').style('color', 'blue');
</div>
<script>codeBlock().editor('#code-a07').init();</script>

Para eliminar este último elemento, sólo necesitamos usar `remove`.

<div class="runnable" id="code-a08">
li.remove();
</div>
<script>codeBlock().editor('#code-a08').init();</script>

La manipulación el DOM constituye la base para crear Visualizaciones de Datos.


### Usando SVG

<aside>Para una introducción a SVG, referimos otra vez al siguiente <a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Introduction">tutorial</a> de MDN.</aside>

El DOM no es suficientemente versátil para crear gráficos complejos. Afortunadamente, la mayoría de los browsers soporta SVG, un formato de imagen vectorial que tiene un modelo de datos similar a HTML, y que, por lo tanto, puede ser manipulado con D3.

Crearemos un SVG dentro del siguiente contenedor:

<div class="ejemplo">
  <div id="ejemplo-b01"></div>
</div>

<div class="runnable" id="code-b01">
var svg = d3.select('#ejemplo-b01').append('svg');

svg.attr('width', '600px').attr('height', '200px');
</div>
<script>codeBlock().editor('#code-b01').init();</script>

Nuestro elemento SVG tiene un tamaño definido pero aún está vacío. Agregaremos un círculo:

<div class="runnable" id="code-b02">
var circle = svg.append('circle');

circle.attr('cx', 50).attr('cy', 100).attr('r', 50).attr('fill', 'blue');
</div>
<script>codeBlock().editor('#code-b02').init();</script>

Podemos cambiar los atributos suavemente, usando transiciones. Las transiciones se realizan interpolando los valores iniciales y finales, cambiando los atributos progresivamente durante la duración de la transición. Las transiciones ayudan a seguir los elementos visualmente y agregan un componente estético a la visualización.


<div class="runnable" id="code-b03">
circle.transition().duration(2000)
    .attr('cx', 500).attr('r', 100).attr('fill', 'red');
</div>
<script>codeBlock().editor('#code-b03').init();</script>

Con SVG y D3, podemos crear gráficos atractivos y dinámicos. Pero primero, necesitamos aprender a vincular datos con elementos del DOM, lo que se conoce como data binding.




