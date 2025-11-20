# Capítulo 8: Cadenas de Texto

Las cadenas de texto son una de las estructuras de datos más fundamentales en programación. En este capítulo, exploraremos cómo crear, manipular y trabajar con strings en JavaScript.

### 8.1. Creación de Cadenas: Comillas y _`Template Strings`_

Las cadenas pueden crearse de múltiples formas:

```javascript
// Comillas simples
let cadena1 = 'Hola mundo';

// Comillas dobles
let cadena2 = "Hola mundo";

// Template strings (backticks) - ES6+
let cadena3 = `Hola mundo`;

// No hay diferencia funcional entre los tres tipos
console.log(cadena1 === cadena2); // true
```

#### _**`Template Strings`**_**: Interpolación y Expresiones**

Los template strings permiten incrustar expresiones usando `${}`.

```javascript
let nombre = "Juan";
let edad = 30;

// Interpolación
console.log(`Mi nombre es ${nombre} y tengo ${edad} años`);

// Expresiones dentro de ${}
console.log(`Próximo año tendré ${edad + 1} años`);

// Llamadas a funciones
function obtenerHora() {
    return new Date().getHours();
}
console.log(`Son las ${obtenerHora()} horas`);

// Ternario
console.log(`Eres ${edad >= 18 ? 'mayor' : 'menor'} de edad`);
```

#### **Saltos de línea con Template Strings**

```javascript
// Sin template string: necesita \n
let parrafo1 = "Primera línea\nSegunda línea\nTercera línea";

// Con template string: saltos reales
let parrafo2 = `Primera línea
Segunda línea
Tercera línea`;

console.log(parrafo1);
console.log(parrafo2);
// Ambas producen el mismo resultado
```

***

### 8.2. Propiedades: `length`

Accede a la longitud de una cadena:

```javascript
let texto = "JavaScript";
console.log(texto.length);      // 10

// Acceder a caracteres individuales
console.log(texto[0]);          // "J"
console.log(texto[9]);          // "t"
console.log(texto[-1]);         // undefined (no soporta índices negativos)
```

### 8.3. Métodos de Lectura

#### **`charAt(indice)`**

Retorna el carácter en el índice especificado.

```javascript
let palabra = "Hola";
console.log(palabra.charAt(0)); // "H"
console.log(palabra.charAt(3)); // "a"
console.log(palabra.charAt(10)); // "" (fuera de rango)
```

#### **`charCodeAt(indice)`**

Retorna el código Unicode del carácter:

```javascript
let letra = "A";
console.log(letra.charCodeAt(0)); // 65
```

#### **`indexOf(búsqueda)`**

Encuentra la primera posición de una subcadena:

```javascript
let texto = "Hola Mundo";
console.log(texto.indexOf("Mundo")); // 5
console.log(texto.indexOf("xyz"));   // -1 (no encontrado)
console.log(texto.indexOf("o"));     // 4 (primer "o")
```

***

### 8.4. Métodos de Transformación

#### **`toUpperCase()` y `toLowerCase()`**

```javascript
let texto = "JavaScript";
console.log(texto.toUpperCase()); // "JAVASCRIPT"
console.log(texto.toLowerCase()); // "javascript"
```

#### **`trim()`**

Elimina espacios en blanco al inicio y final:

```javascript
let texto = "  Hola mundo  ";
console.log(texto.trim());      // "Hola mundo"
console.log(texto.trimStart()); // "Hola mundo  "
console.log(texto.trimEnd());   // "  Hola mundo"
```

***

### 8.5. Métodos de Búsqueda

#### **`includes(búsqueda)`**

Verifica si contiene una subcadena:

```javascript
let email = "usuario@ejemplo.com";
console.log(email.includes("@"));       // true
console.log(email.includes(".com"));    // true
console.log(email.includes("xyz"));     // false
```

#### **`startsWith(búsqueda)`**

Verifica si comienza con una subcadena:

```javascript
let url = "https://www.google.com";
console.log(url.startsWith("https")); // true
console.log(url.startsWith("http"));  // false
```

#### **`endsWith(búsqueda)`**

Verifica si termina con una subcadena:

```javascript
let archivo = "documento.pdf";
console.log(archivo.endsWith(".pdf")); // true
console.log(archivo.endsWith(".txt")); // false
```

***

### 8.6. Métodos de Extracción

#### **`slice(inicio, fin)`**

Extrae una parte de la cadena (fin no incluido):

```javascript
let texto = "JavaScript";
console.log(texto.slice(0, 4));   // "Java"
console.log(texto.slice(4));      // "Script"
console.log(texto.slice(-6));     // "Script" (último 6)
console.log(texto.slice(0, -2));  // "JavaScri" (todos menos los 2 últimos)
```

#### **`substring(inicio, fin)`**

Similar a slice, pero no acepta índices negativos:

```javascript
let texto = "JavaScript";
console.log(texto.substring(0, 4));  // "Java"
console.log(texto.substring(4));     // "Script"
console.log(texto.substring(-3, 4)); // "Java" (trata negativos como 0)
```

#### **`substr(inicio, longitud)` ⚠️**

{% hint style="danger" %}
**Deprecado** (no usar en código nuevo, pero puede aparecer en _legacy_):
{% endhint %}

```javascript
let texto = "JavaScript";
console.log(texto.substr(0, 4));     // "Java"
console.log(texto.substr(4, 6));     // "Script"
```

### 8.7. Métodos de Reemplazo

#### **`replace(búsqueda, remplazo)`**

Reemplaza la **primera** ocurrencia:

```javascript
let texto = "gato gato gato";
console.log(texto.replace("gato", "perro")); // "perro gato gato"
```

#### **`replaceAll(búsqueda, reemplazo)`**

Reemplaza **todas** las ocurrencias (ES2021+):

```javascript
let texto = "gato gato gato";
console.log(texto.replaceAll("gato", "perro")); // "perro perro perro"
```

***

### 8.8. _`Template Strings`_ Avanzados

#### **Expresiones en&#x20;**_**`template strings`**_

```javascript
let numero = 10;
let booleano = true;
let resultado = `Número: ${numero}, Booleano: ${booleano}`;
console.log(resultado); // "Número: 10, Booleano: true"
```

#### **Funciones literales etiquetadas (avanzado)**

```javascript
function etiqueta(strings, ...valores) {
    console.log(strings);  // Array con partes de texto
    console.log(valores);  // Array con expresiones
    return strings[0] + valores[0] + strings[1];
}

let nombre = "Juan";
let resultado = etiqueta`Hola ${nombre}, ¿cómo estás?`;
```

***

### Resumen del Capítulo

Las cadenas de texto son fundamentales en JavaScript. Dominar los métodos de strings y template strings es esencial para manipular datos de texto de manera efectiva.

#### **💡 Conceptos Clave:**

* **Template strings**: Interpolación con ${}
* **length**: Propiedad para obtener la longitud
* **charAt(), indexOf()**: Acceso y búsqueda
* **toUpperCase(), toLowerCase()**: Transformación
* **trim()**: Elimina espacios
* **includes(), startsWith(), endsWith()**: Búsqueda
* **slice(), substring()**: Extracción
* **replace(), replaceAll()**: Reemplazo

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre `slice()` y `substring()`?
2. ¿Cuándo usarías template strings en lugar de concatenación con +?
3. ¿Cuál es la diferencia entre `replace()` e `replaceAll()`?
4. Escribe una función que invierta una cadena.
5. Crea una función que extrae el dominio de una URL.

***
