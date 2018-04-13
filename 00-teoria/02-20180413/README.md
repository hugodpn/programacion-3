# Web Responsive (web Adaptables)

Debido a la proliferación de smartphones y tablets en el mercado actual, existe más diversidad que nunca de formatos de pantalla. Este panorama obliga a adaptar los formatos web a estos nuevos dispositivos y la estructura de cada uno de ellos, es indiscutible que necesitamos websites inteligentes que se adapten a todos ellos.

A partir de todo esto, el término “responsive web design” se escucha frecuentemente, pero ¿qué es exactamente? El responsive design corresponde a una tendencia de creación de páginas web que pueden ser visualizadas perfectamente en todo tipo de dispositivos, desde ordenadores de escritorio hasta smartphones o tablets. Con este tipo de diseño no necesitas tener una versión para cada dispositivo, una sola web se adapta a todos ellos.

> http://www.maestrosdelweb.com/que-es-responsive-web-design/

# Bootstrap

Bootstrap es un framework desarrollado y liberado por Twitter que tiene como objetivo facilitar el diseño web. Permite crear de forma sencilla webs de diseño responsive (adaptable), es decir, que se ajusten a cualquier dispositivo y tamaño de pantalla y siempre se vean igual de bien. Es Open Source o código abierto, por lo que lo podemos usar de forma gratuita y sin restricciones.

## Ventajas de utilizar Bootstrap

+ diseños elegantes
+ maquetación rápida
+ muchos elementos web (html, css, js)
+ es adaptable a distintas resoluciones de dispositovos - responsive
+ código abierto
+ gratuito

>  https://puntoabierto.net/blog/que-es-bootstrap-y-cuales-son-sus-ventajas

# Javascript

> http://librosweb.es/libro/javascript/
> https://developer.mozilla.org/es/docs/Web/JavaScript/Guide

JavaScript es un lenguaje de programación que se utiliza principalmente para crear páginas web dinámicas.

Una página web dinámica es aquella que incorpora efectos como texto que aparece y desaparece, animaciones, acciones que se activan al pulsar botones y ventanas con mensajes de aviso al usuario.

Técnicamente, JavaScript es un lenguaje de programación interpretado, por lo que no es necesario compilar los programas para ejecutarlos. En otras palabras, los programas escritos con JavaScript se pueden probar directamente en cualquier navegador sin necesidad de procesos intermedios.

El nucleo de JavaScript contiene una librería estándar de objetos, tales como  Array, Date, y Math, y un conjunto central de elementos del lenguaje, tales como operadores, estructuras de control, y sentencias. El núcleo de JavaScript puede extenderse para varios propósitos, complementándolo con objetos adicionales, por ejemplo:

+ **Client-side** (Cliente - Navegador) JavaScript extiende el núcleo del lenguaje proporcionando objetos para controlar un navegador y su modelo de objetos (o DOM, por las iniciales de Document Object Model). Por ejemplo, las extensiones del lado del cliente permiten que una aplicación coloque elementos en un formulario HTML y responda a eventos del usuario, tales como clicks del ratón, ingreso de datos al formulario y navegación de páginas.

+ **Server-side** (Servidor - Nodejs) JavaScript extiende el núcleo del lenguaje proporcionando objetos relevantes a la ejecución de JavaScript en un servidor. Por ejemplo, las extensiones del lado del servidor permiten que una aplicación se comunique con una base de datos, proporcionar continuidad de la información de una invocación de la aplicación a otra, o efectuar manipulación de archivos en un servidor.


## Características

1. Interpretado
2. Debilmente tipado y dinámico, es decir los tipos de datos pueden cambiar durante la ejecución
3. Orientado a Objetos
4. Multiplataforma
5. Ejecuta en el cliente y en el servidor
6. Evaluación en tiempo de ejecución con **eval**


> https://es.wikipedia.org/wiki/JavaScript#Imperativo_y_estructurado

## Imprimir cadena por consola

```javascript
console.info("Imprimir Cadena");
```
## Variables

```javascript
let numero = 4;
numero = numero + 2;
console.info(numero); // 6

let decimal = 3.4;
decimal += 1; 
console.info(decimal); // 4.4

let cadena = "Hola";
let cadena2 = "mi nombre es";
let cadena3 = cadena + " Juan";
console.info(cadena); // Hola
console.info(cadena3);  // Hola Juan
console.info(`Buen día, ${cadena2} Pedro`); // Buen día, mi nombre es Pedro

```

## Tipos de datos

-   Sin definir (`undefined`)
-   Nulo (`null`)
-   Lógicos (`boolean`)
-   Numérico (`number`)
-   Cadena (`string`)
-   Símbolo (`symbol`)
-   Matriz (`array`)
-   Objetos (`object`)
-  Function (`function`)

```javascript
let variable;
console.info(variable); // undefined
variable = null;
console.info(variable); // null
variable = 1;
console.info(typeof variable); // number
variable = "hola";
console.info(typeof variable); // string
varibale = true;
console.info(typeof variable); // boolean
variable = Symbol('nuevo')
console.info(variable); // Symbol(nuevo)

let lista = new Array(3);
console.info(lista.length); // 3
```

```javascript
let variable = [1, 3, 5];
console.info(typeof variable); // array

variable = { 'nombre': 'Juan', 'edad': 32};
console.info(typeof variable); // object

myFunc = function() {};
console.info(typeof myFunc); // function

```

> **undefined**: para **Javascript**, no existe. O bien no ha sido declarada o jamás se le asignó un valor. **null**: para **Javascript**, la variable existe. En algún momento, explícitamente, la variable se estableció a **null**.

> https://msdn.microsoft.com/es-es/library/7wkd9z69(v=vs.94).aspx
> https://www.todojs.com/tipos-datos-javascript-es6/

## Funciones

```javascript
function saludar(nombre) {
	console.info("Hola " + nombre);
}
saludar('Juan'); // Hola Juan

const sumar = function(num1, num2) {
	return num1 + num2;
}
console.info(sumar(3,5)); // 8

const restar = (num1, num2) => {
	return num1 - num2;
};
```

## Bucles

### for

```javascript
const miArray = ['uno', 'dos', 'tres'];

for(let i=0; i < myArray.length; i++) {
    // codigo acá...
    console.info('Index: ', i);
}
```

```javascript
const miArray = ['uno', 'dos', 'tres'];

for(let i in myArray) {
    // codigo acá...
    console.info('Index: ', i);
    console.info('Val: ', myArray[i]);
}
```

```javascript
const miObjeto = {
    'uno': 1, 
    'dos': "dos",
    'tres': [3, 4, 5]
};

for(let i in miObjeto) {
    // codigo acá...
    console.info('Index: ', i);
    console.info('Val: ', myArray[i]);
}
```

### while

```javascript
let i = 0;
while(i < 10) {
    console.info('Código acá: ', i);
    i = i + 1; // i++
}
```

### map

```javascript
const miArray = ['uno', 'dos', 'tres'];

const res = miArray.map((obj) => {
    // codigo acá
    return obj + " + uno";
});

console.info(res); // ["uno + uno", "dos + uno", "tres + uno"]
```
