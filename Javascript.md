# Manual de Javascript

En este manual usaremos el siguiente documento "a.html":

```html
<!DOCTYPE html>
<html>
  <head>
	<script src="b.js"></script>
  </head>
</html>
```

E iremos modificando el documento "b.js" para probar cada uno de los ejemplos.

## console.log() y alert()

Las funciones console.log() y alert() se usan para mostrar mensajes por consola y pop-up respectivamente.

|                                 | alert()                     | console.log()                    |
|---------------------------------|-----------------------------|----------------------------------|
| object sin toString()           | "[object Object]"           | `<objeto_desplegable>`           |
| object con toString()           | object.toString()           | `<objeto_desplegable>`           |
| "obj: " + object sin toString() | "obj: [object Object]"      | "obj: [object Object]"           |
| "obj: " + object con toString() | "obj: " + object.toString() | "obj: " + object.toString()      |
| "obj: ", object sin toString()  | "obj: "                     | "obj: " + `<objeto_desplegable>` |
| "obj: ", object con toString()  | "obj: "                     | "obj: " + `<objeto_desplegable>` |

Recomendación:
- Usar alert("obj: " + object) con o sin toString()
- Usar console.log("obj: ", object) con o sin toString()

Ejemplo:

```js
var obj = {
  nombre: "Bruce Wayne",
  edad: 30,
  isMayorEdad: function(){
    return this.edad >= 18;
  }
}

var objToString = {
  nombre: "Bruce Wayne",
  edad: 30,
  isMayorEdad: function(){
    return this.edad >= 18;
  },
  toString: function(){
    return this.nombre + " (" + this.edad + ", " + this.isMayorEdad() + ")";
  }
}

alert(obj);
alert("obj: " + obj);
alert("obj: ", obj);
alert(objToString);
alert("objToString: " + objToString);
alert("objToString: ", objToString);
console.log(obj);
console.log("obj: " + obj);
console.log("obj: ", obj);
console.log(objToString);
console.log("objToString: " + objToString);
console.log("objToString: ", objToString);
```

Resultado:

```txt
Alerts:
[object Object]
obj: [object Object]
obj: 
Bruce Wayne (30, true)
objToString: Bruce Wayne (30, true)
objToString: 

Console logs:
Object { nombre: "Bruce Wayne", edad: 30, isMayorEdad: isMayorEdad() }
obj: [object Object]
obj: Object { nombre: "Bruce Wayne", edad: 30, isMayorEdad: isMayorEdad() }
Object { nombre: "Bruce Wayne", edad: 30, isMayorEdad: isMayorEdad(), toString: toString() }
objToString: Bruce Wayne (30, true)
objToString: Object { nombre: "Bruce Wayne", edad: 30, isMayorEdad: isMayorEdad(), toString: toString() }
```

## Variables y constantes

Si no se les asigna valor tienen el valor `undefined`.

Existen variables de cuatro tipos de variables y constantes:
- con declaración `var`
- con declaración `let`
- sin declaración
- con declaración `const`

Diferencias de los tipos de variables y constantes:

|                   | Con var            | Con let             | Sin declaración     | Con const           |
|-------------------|--------------------|---------------------|---------------------|---------------------|
| Sin inicializar   | var a; //undefined | let a; //undefined  | No es posible       | No es posible       |
| Inicializando     | var a = 2;         | let a = 2;          | a = 2;              | const a = 2;        |
| Ámbito en función | función            | función hacia abajo | función hacia abajo | función hacia abajo |
| Ámbito global     | global             | global hacia abajo  | global hacia abajo  | global hacia abajo  |

Ejemplo de declaración con y sin inicialización dentro de una function:

```js
function printVariables() {
	console.log("a: ", a);
	var a = 1;
	let b = 2;
	console.log("b: ", b);
    c = 3;
	console.log("c: ", c);
	const d = 4;
	console.log("d: ", d);
}
printVariables();
```

Resultado:

```txt
a:  undefined
b:  2
c:  3
d:  4
```

Ejemplo de declaración con y sin inicialización fuera de una function:

```js
function printVariables() {
	console.log("a: ", a);
	console.log("b: ", b);
	console.log("c: ", c);
	console.log("d: ", d);
}
console.log("a: ", a);
var a = 1;
let b = 2;
console.log("b: ", b);
c = 3;
console.log("c: ", c);
const d = 4;
console.log("d: ", d);
printVariables();
```

Resultado:

```txt
a:  undefined
b:  2
c:  3
d:  4
a:  1
b:  2
c:  3
d:  4
```

## Tipos de datos

Existen los tipos primitivos:
- boolean
- string
- number
- undefined
- null

A mayores existe el tipo de dato no primitivo Object.

Los tipos de las variables son dinámicos:

```js
var a = "hello"; //string
a = true;        //boolean
a = 2;           //number
```

## Operadores de comparación

| var1 | var2 | var1 == var2 | var1 != var2 | var1 === var2 | var1 !== var2 |
|------|------|--------------|--------------|---------------|---------------|
| 2    | 2    | true         | false        | true          | false         |
| 2    | 1    | false        | true         | false         | true          |
| 2    | "2"  | true         | false        | false         | true          |
| 2    | "1"  | false        | true         | false         | true          |

## for in y for of

Se usa "for in" para obtener las propiedades de un objeto.

Ejemplo:

```js
var fruta = {nombre:"plátano", origen:"Canarias", precio:1};
for(var prop in fruta) {
  console.log("fruta." + prop + " = " + fruta[prop]);
}
```

Resultado:

```txt
fruta.nombre = plátano
fruta.origen = Canarias
fruta.precio = 1
```

Se usa "for of" para recorrer objetos iterables (como Array, Set y Map).

Ejemplo:

```js
var frutas = ["manzana", "plátano", "pera"];
for(let x in frutas) {
  console.log(x);
}

for(let x of frutas) {
  console.log(x);
}
```

Resultado:

```txt
0
1
2
manzana
plátano
pera
```

## Funciones

Se declaran así:

```js
function <nombreFunción> (<parametrosEntrada>) {
  ...
  return <valorSalida>;
}
```

Son objetos y, por tanto, se pueden asignar a variables e invocar con dichas variables.

Nota: Al asignar una función a una variable, el nombre original de la función sólo puede ser usado desde dentro de la propia función para llamadas recursivas.

Ejemplo:

```js
var func = function myFunction(value1, value2) {
  let value3 = value1 + value2;
  if(value3 > 7) {
	  value3 = myFunction(0, 1);
  } else if(value3 > 5) {
	  value3 = func(0, 0);
  }
  return value3;
}
console.log(func(1,7));
console.log(func(1,5));
console.log(func(1,2));
```

Resultado:

```txt
1
0
3
```

La función anterior también se podría convertir en una función anónima, para usarla sólo con el nombre de la variable.

Ejemplo:

```js
var func = function(value1, value2) {
  let value3 = value1 + value2;
  if(value3 > 7) {
	  value3 = func(0, 1);
  } else if(value3 > 5) {
	  value3 = func(0, 0);
  }
  return value3;
}
console.log(func(1,7));
console.log(func(1,5));
console.log(func(1,2));
```

Resultado:

```txt
1
0
3
```

## Funciones con argumentos variables

Ejemplo:

```js
function sumatorio(x, y) {
  //Sumatorio de los dos primeros parámetros
  var result = x + y;
  
  //Sumatorio del resto de parámetros
  for(var i = 2; i < arguments.length; i++) {
    result = result + arguments[i];
  }
  
  return result;
}
console.log("sum: ", sumatorio(1,2,3,4));
```

Resultado:

```txt
sum:  10
```

## Funciones con argumentos por defecto

Ejemplo:

```js
function sumatorio(x=5, y=10, z=5) {
  var result = x + y + z;
  return result;
}
console.log("sum: ", sumatorio(1,2,3,4));
console.log("sum: ", sumatorio(1,2));
console.log("sum: ", sumatorio(1));
console.log("sum: ", sumatorio());
```

Resultado:

```txt
sum:  6
sum:  8
sum:  16
sum:  20
```

## Funciones con argumentos rest

Ejemplo:

```js
function sumatorio(x, y, ...restValues) {
  //Sumatorio de los dos primeros parámetros
  var result = x + y;
  
  //Sumatorio del resto de parámetros
  for(var i = 0; i < restValues.length; i++) {
    result = result + restValues[i];
  }
  
  return result;
}
console.log("sum: ", sumatorio(1,2,3,4));
```

Resultado:

```txt
sum:  10
```

## Funciones flecha

Como las lambda de Java.

NOTA:
- No usar this, super o arguments en funciones flecha.
- Para devolver un object, se requieren paréntesis alrededor de la expresión.
- Los arrays tienen métodos forEach, reduce, filter y map que hacen uso de funciones flecha.

Ejemplo:

```js
let arrowFunc1 = (alias) => ({name: "Bruce Wayne", price: 1, alias: alias})
console.log(arrowFunc1("Batman"));

var arr = [5, 6, 13, 0, 1, 18, 23];
arr.forEach(arrElement => console.log(arrElement));

var sum = arr.reduce((arrElement1, arrElement2) => arrElement1 + arrElement2);
console.log("sum: ", sum);

var even = arr.filter(arrElement => arrElement % 2 == 0);
console.log("even: ", even);

var double = arr.map(arrElement => arrElement * 2);
console.log("double: ", double);

let arrayDestructuringFunc = ([a, b] = ["10", 20]) => a + b;
console.log("desestructuración array: ", arrayDestructuringFunc());

let objectDestructuringFunc = ({a, b} = {b: "10", a: 20}) => a + b;
console.log("desestructuración objeto: ", objectDestructuringFunc());
```

Resultado:

```txt
Object { name: "Bruce Wayne", price: 1, alias: "Batman" }
5
6
13
0
1
18
23
sum:  66
even:  Array(3) [ 6, 0, 18 ]
double:  Array(7) [ 10, 12, 26, 0, 2, 36, 46 ]
desestructuración array:  1020
desestructuración objeto:  2010
```

## Funciones predefinidas

Ejemplo:

```js
function suma(x, y) {
  console.log("{inputX: " + x + ", inputY: " + y + "}");
  
  let isNaNXResult = isNaN(x);
  let isNaNYResult = isNaN(y);
  
  console.log("{isNaNXResult: " + isNaNXResult + ", isNaNYResult: " + isNaNYResult + "}");
  
  let parseIntXResult = parseInt(x);
  let parseIntYResult = parseInt(y);
  
  console.log("{parseIntXResult: " + parseIntXResult + ", parseIntYResult: " + parseIntYResult + "}");
  
  let parseFloatXResult = parseFloat(x);
  let parseFloatYResult = parseFloat(y);
  
  console.log("{parseFloatXResult: " + parseFloatXResult + ", parseFloatYResult: " + parseFloatYResult + "}");
  
  return {suma: x + y, sumaInt: parseIntXResult + parseIntYResult, sumaFloat: parseFloatXResult + parseFloatYResult};
}

function getSumaResultElements(sumaResult) {
  return "{suma: " + sumaResult.suma + ", sumaInt: " + sumaResult.sumaInt + ", sumaFloat: " + sumaResult.sumaFloat + "}";
}

var evalSumaIntResult = eval("getSumaResultElements(suma(3,2))");
console.log("evalSumaIntResult: ", evalSumaIntResult);

var evalSumaFloatResult = eval("getSumaResultElements(suma(3.5,2))");
console.log("evalSumaFloatResult: ", evalSumaFloatResult);

var evalSumaStringResult = eval("getSumaResultElements(suma(\"3\",2))");
console.log("evalSumaStringResult: ", evalSumaStringResult);

var evalSumaNaNResult = eval("getSumaResultElements(suma(\"a\",2))");
console.log("evalSumaNaNResult: ", evalSumaNaNResult);
```

Resultado:

```txt
{inputX: 3, inputY: 2}
{isNaNXResult: false, isNaNYResult: false}
{parseIntXResult: 3, parseIntYResult: 2}
{parseFloatXResult: 3, parseFloatYResult: 2}
evalSumaIntResult:  {suma: 5, sumaInt: 5, sumaFloat: 5}
{inputX: 3.5, inputY: 2}
{isNaNXResult: false, isNaNYResult: false}
{parseIntXResult: 3, parseIntYResult: 2}
{parseFloatXResult: 3.5, parseFloatYResult: 2}
evalSumaFloatResult:  {suma: 5.5, sumaInt: 5, sumaFloat: 5.5}
{inputX: 3, inputY: 2}
{isNaNXResult: false, isNaNYResult: false}
{parseIntXResult: 3, parseIntYResult: 2}
{parseFloatXResult: 3, parseFloatYResult: 2}
evalSumaStringResult:  {suma: 32, sumaInt: 5, sumaFloat: 5}
{inputX: a, inputY: 2}
{isNaNXResult: true, isNaNYResult: false}
{parseIntXResult: NaN, parseIntYResult: 2}
{parseFloatXResult: NaN, parseFloatYResult: 2}
evalSumaNaNResult:  {suma: a2, sumaInt: NaN, sumaFloat: NaN}
```

## Funciones callback

Una función callback es una función que se pasa como argumento a otra y que luego es ejecutada dentro de dicha función.

Los callbacks son utilizados a menudo en operaciones asíncronas, de forma que son lanzadas en respuesta a la finalización de la misma.

Ejemplo de callback síncrono:

```js
function saludarPersona(saludo) {
  console.log(saludo);
}

function crearSaludo(persona, callback) {
  let saludo = "Hola " + persona.nombre + " " + persona.apellidos;
  callback(saludo);
}

var persona = new Persona("Bruce", "Wayne", 30);
crearSaludo(persona, saludarPersona);
```

## Objetos

Diferencias entre Java y Javascript:
- Java es un lenguaje orientado a objetos basado en clases
- Javascript es un lenguaje orientado a objetos basado en prototipos

En Javascript no existen clases y la reutilización de comportamiento se basa en otros objetos ya existentes.

Podemos crear:

1. Objetos simples

  - Se crean utilizando los caracteres {}.
  - Si una vez creado el objeto le queremos añadir más atributos o métodos se puede hacer.
  - Los objetos creados de esta manera carecen de esquema, por lo que no pueden usarse como prototipos ni soportan herencia.
  
  Ejemplo:
  
  ```js
  var persona = {
    nombre: "Bruce",
    apellidos: "Wayne",
    edad: 30,
    isMayorEdad: function(){
      return this.edad >= 18;
    }
  }
  
  persona.dni = "12345678A";
  persona.nombreCompleto = function(){
    return this.nombre + " " + this.apellidos;
  }
  
  console.log(persona.nombreCompleto() + ": " + persona.dni + " " + persona.isMayorEdad());
  ```

2. Clases (prototipos) y objetos

  - Las clases se crean como una function (constructor) y los objetos utilizando la palabra new.
  - Para poder darle funcionalidad a la clase tenemos que usar la propiedad prototype de la function (constructor).
  - Los objetos creados de esta manera soportan herencia simple.
  
  Ejemplo:
  
  ```js
  function Persona(nombre, apellidos, edad){
    this.nombre = nombre;
    this.apellidos = apellidos;
    this.edad = edad;
  }
  
  Persona.prototype.isMayorEdad = function() {
    return this.edad >= 18;
  }

  Persona.prototype.nombreCompleto = function(){
    return this.nombre + " " + this.apellidos;
  }

  function Trabajador(nombre, apellidos, edad, empresa){
    this.empresa = empresa;
    Persona.call(this, nombre, apellidos, edad);
  }
  
  //Para hacer que Trabajador tenga los métodos definidos en Persona
  Trabajador.prototype = Object.create(Persona.prototype);
  //Para establecer como constructor el de Trabajador en vez del de Persona
  Trabajador.prototype.constructor = Trabajador;
  Trabajador.prototype.fichar = function(){
    console.log("Entro a trabajar en " + this.empresa);
  }
  
  var batman = new Persona("Bruce", "Wayne", 30);
  var luciusFox = new Trabajador("Lucius", "Fox", 50, "Wayne Enterprises");
  
  console.log(batman.nombreCompleto() + ": " + batman.edad + " " + batman.isMayorEdad());
  console.log(luciusFox.nombreCompleto() + ": " + luciusFox.edad + " " + luciusFox.isMayorEdad());
  luciusFox.fichar();
  ```

## Arrays

Acerca de los arrays:
- Son un conjunto de datos ordenados por posición
- Los datos que se almacenan en ellos no tienen por que ser del mismo tipo
- Sus dimensiones no son fijas. Siempre podremos añadir nuevos datos a ellos
- Son objetos, por lo que tienen una serie de métodos para manipularlos fácilmente
- Ejemplos de creación de Arrays:

```js
var frutasEmpty = [];
var cochesEmpty = new Array();
var frutas = ["NARANJA", "MANZANA", "PERA"];
var coches = new Array("BMW", "AUDI", "MERCEDES");
//Con segunda posición vacía
var personas = [{nombre: "Bruce", apellidos: "Wayne"}, , {nombre: "Lucius", apellidos: "Fox"}];
//Con 10 posiciones vacías
var elements = new Array(10);
```

## Maps

Ejemplo:

```js
var mapa = new Map();
mapa.set("clave1", "valor1");
mapa.set("clave2", "valor2");
mapa.set("clave3", "valor3");
console.log(mapa.get("clave2"));
console.log(mapa.size);
mapa.delete("clave2");
console.log(mapa.has("clave2"));
console.log(mapa);
for(var [clave, valor] of mapa){
  console.log(clave, valor);
}
```

Resultado:

```txt
valor2
3
false
Map { clave1 → "valor1", clave3 → "valor3" }
clave1 valor1
clave3 valor3
```

## Sets

Ejemplo:

```js
var set = new Set();
set.add("valor1");
set.add("valor2");
set.add(1);
set.add("valor1");
console.log(set.has("valor3"));
set.delete(1);
console.log(set);
set.forEach((valor) => console.log(valor));
```

Resultado:

```txt
false
Set [ "valor1", "valor2" ]
valor1
valor2
```

## Desestructuración

La desestructuración es una expresión que permite desempacar valores de arrays o propiedades de objetos en distintas variables.

Ejemplo:

```js
let a, b, c, rest;
[a=1, b=2, c=3, ...rest] = [10, 20, undefined, 30, 40, 50];
console.log(a);
console.log(b);
console.log(c);
console.log(rest);

({a=1, b=2, c=3, ...rest} = {d: 10, b: 20, a: 30, e: 40});
console.log(a);
console.log(b);
console.log(c);
console.log(rest);

const batman = {
  name: 'Batman',
  realName: 'Bruce Wayne'
};

function printHero({ name, realName }) {
  console.log(name);
  console.log(realName);
}

printHero(batman);
```

Resultado:

```txt
10
20
3
Array(3) [ 30, 40, 50 ]
30
20
3
Object { d: 10, e: 40 }
Batman
Bruce Wayne
```

## Promesas

Las promesas se suelen usar para operaciones asíncronas.

La creación de una Promise se realiza de la siguiente forma:

```js
var promesa = new Promise(
  function(resolve, reject) {
    ...
  }
);
```

Dentro de la función se realizarán las tareas necesarias y, para indicar si el resultado ha ido bien o mal, llamaremos a:
- la función resolve() pasándole como parámetro la información que queramos
- la función reject() incicando como parámetro el motivo del error

Ejemplo de creación de Promises:

```js
var cuenta = 100;

function comprobarCargo(cargo) {
  return new Promise(
    (resolve, reject) => {
      if((cuenta - cargo) >= 0) {
	    resolve(cargo);
	  } else {
	    reject("SALDO INSUFICIENTE");
	  }
    }
  );
}

function hacerCargo(cargo) {
  return new Promise(
    (resolve, reject) => {
      if((cuenta - cargo) >= 0) {
	    cuenta = cuenta - cargo;
		let restante = cuenta;
	    resolve(restante);
	  } else {
	    reject("SALDO INSUFICIENTE");
	  }
    }
  );
}
```

Cuando finalice la operación la promesa lanzará alguna de las siguientes funciones: 
- En caso de que la operación haya ido bien, la proporcionada en el método then.
- En caso de error, la proporcionada en el método catch.


Ejemplo de uso de las Promises creadas:

```js
comprobarCargo(70)
  .then(
    (cargo) => {
	  console.log("TENGO SALDO");
	  return hacerCargo(cargo);
	}
  ).then(
    (restante) => console.log("Me queda " + restante + " en la cuenta")
  ).catch(
    error => console.log("No he podido realizar el cargo", error)
  );
```

## AJAX

Ejemplo petición GET:

```js
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then(response => response.json())
  .then(json => console.log(json));
```

Ejemplo petición POST:

```js
var mensajeEnvio = {
  title: 'Llamada AJAX',
  body: 'Estoy haciendo una petición POST',
  userId: 1
}

fetch("https://jsonplaceholder.typicode.com/posts",
    {
      method: 'POST',
	  body: JSON.stringify(mensajeEnvio),
	  headers: {
	    "Content-type": "application/json; charset=UTF-8"
	  }
    }
  )
  .then(response => response.json())
  .then(json => console.log("INFORMACIÓN RECIBIDA --> ", json));
```

## Acceso al DOM

Para recuperar un elemento en el DOM podemos usar:
- document.getElementById()

Para recuperar un array de elementos en el DOM podemos usar:
- document.getElementsByTagName()
- document.getElementsByName()
- document.getElementsByClassName()

A modo de ejemplo, si queremos modificar la propiedad href del primer enlace de una página HTML usaríamos:

```js
document.getElementsByTagName("a")[0].href = "https://www.viewnext.com"
```

El DOM tiene una estructura de árbol, de modo que en cada nodo del mismo podemos hacer uso de los atributos:
- parent (para acceder al nodo padre del nodo actual)
- childNodes (para acceder a los nodos hijos del nodo actual)

## Eventos

Podemos indicarle a Javascript que cuando se efectúe una determinada acción sobre un elemento visual concreto se ejecute una función predefinida.

Un ejemplo puede ser validar un formulario al presionar un botón y, según el resultado, enviarlo o mostrar un error.

Los eventos más comunes son:
- click
- change
- focus y blur
- mouseOver y mouseOut
- keyDown y keyUp
- submit
- load

Supongamos que queremos que cuando un select cambie de valor se escriba en la consola la opción seleccionada y su value.

Tenemos dos opciones:

1. Mediante HTML:

  El HTML quedaría así:

  ```html
  <select id="fruta" onchange="avisoFruta(event, this);">
    <option value="NARANJA">naranja</option>
    <option value="MANZANA">manzana</option>
    <option value="FRESA">fresa</option>
    <option value="SANDIA">sandía</option>
  </select>
  ```
  
  El Javascript quedaría así:

  ```js
  function avisoFruta(event, elemento){
    let texto = elemento[elemento.selectedIndex].innerText;
    texto += "(" + elemento.value + ")";
    console.log(texto);
  }
  ```

2. Mediante Javascript:

  El HTML quedaría así:

  ```html
  <body onload="init();">
  
  ...

  <select id="fruta">
    <option value="NARANJA">naranja</option>
    <option value="MANZANA">manzana</option>
    <option value="FRESA">fresa</option>
    <option value="SANDIA">sandía</option>
  </select>
  
  ...

  </body>
  ```

  El Javascript quedaría así:
  
  ```js
  function init(){
    document.getElementById("fruta").onchange=avisoFruta;
  }
  
  function avisoFruta(event){
    let texto = this[this.selectedIndex].innerText;
    texto += "(" + this.value + ")";
    console.log(texto);
  }
  ```

NOTAS:
- Los eventos de Javascript se propagan o burbujean, esto quiere decir que un elemento externo puede capturar un evento producido por un elemento interno.
- Los eventos pueden ser, por tanto, capturados múltiples veces. Para evitar esto, podemos usar el método stopPropagation() del objeto event.
