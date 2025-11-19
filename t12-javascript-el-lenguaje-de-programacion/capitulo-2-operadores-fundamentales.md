# Capítulo 2: Operadores Fundamentales

Los operadores son símbolos que realizan operaciones sobre valores. JavaScript posee una amplia variedad de operadores que te permiten manipular datos de formas sofisticadas. Este capítulo explora los operadores fundamentales que formarán la base de tu código JavaScript.

### 2.1. Operadores Aritméticos

Los operadores aritméticos realizan cálculos matemáticos sobre números.

| Operador | Descripción    | Ejemplo  | Resultado |
| -------- | -------------- | -------- | --------- |
| `+`      | Suma           | `5 + 3`  | `8`       |
| `-`      | Resta          | `5 - 3`  | `2`       |
| `*`      | Multiplicación | `5 * 3`  | `15`      |
| `/`      | División       | `15 / 3` | `5`       |
| `%`      | Módulo (resto) | `17 % 5` | `2`       |
| `**`     | Potencia       | `2 ** 3` | `8`       |

```javascript
let x = 10;
let y = 3;

console.log(x + y);      // 13
console.log(x - y);      // 7
console.log(x * y);      // 30
console.log(x / y);      // 3.333...
console.log(x % y);      // 1 (10 = 3*3 + 1)
console.log(x ** y);     // 1000 (10³)
console.log(x ** 0.5);   // 3.162... (raíz cuadrada)
```

**Casos especiales**:

```javascript
console.log(5 / 0);      // Infinity
console.log(-5 / 0);     // -Infinity
console.log(0 / 0);      // NaN
console.log("5" + 3);    // "53" (concatenación, + es ambiguo)
console.log("5" - 3);    // 2 (coerción a número)
```

***

### 2.2. Operadores de Asignación

Asignan un valor a una variable. Pueden ser simples o compuestos.

```javascript
let x = 10;              // Asignación simple

x += 5;                  // x = x + 5 => 15
x -= 3;                  // x = x - 3 => 12
x *= 2;                  // x = x * 2 => 24
x /= 4;                  // x = x / 4 => 6
x %= 4;                  // x = x % 4 => 2
x **= 3;                 // x = x ** 3 => 8
```

***

### 2.3. Operadores de Comparación

Comparan dos valores y retornan un booleano (`true` o `false`).

#### **Igualdad flexible vs estricta**

```javascript
// Igualdad flexible (==): realiza coerción de tipos
console.log(5 == "5");           // true
console.log(5 == 5);             // true
console.log(0 == false);         // true
console.log(null == undefined);  // true

// Igualdad estricta (===): no realiza coerción
console.log(5 === "5");          // false (tipos diferentes)
console.log(5 === 5);            // true
console.log(0 === false);        // false
console.log(null === undefined); // false
```

{% hint style="success" %}
**Recomendación**: Usa siempre `===` y `!==` para evitar sorpresas.
{% endhint %}

#### **Comparadores de magnitud**

```javascript
console.log(5 > 3);              // true
console.log(5 >= 5);             // true
console.log(3 < 5);              // true
console.log(3 <= 3);             // true
```

#### **La excepción de NaN**

```javascript
console.log(NaN === NaN);        // false (¡incluso NaN no es igual a NaN!)
console.log(NaN == NaN);         // false

// Forma correcta de verificar NaN
console.log(Number.isNaN(NaN));  // true
console.log(Object.is(NaN, NaN)); // true
```

***

### 2.4. Operadores Lógicos

Operan sobre booleanos y son fundamentales para la lógica de programación.

#### **AND (`&&`)**

Retorna `true` si ambas condiciones son verdaderas.

```javascript
console.log(true && true);       // true
console.log(true && false);      // false
console.log(5 > 3 && 10 > 5);    // true

// Cortocircuito: si la primera es falsa, no evalúa la segunda
let resultado = false && (console.log("No se ejecuta"));
```

#### **OR (`||`)**

Retorna `true` si al menos una condición es verdadera.

```javascript
console.log(true || false);      // true
console.log(false || false);     // false
console.log(5 > 10 || 10 > 5);   // true

// Cortocircuito: si la primera es verdadera, no evalúa la segunda
let resultado = true || (console.log("No se ejecuta"));
```

#### **NOT (`!`)**

Invierte el valor booleano.

```javascript
console.log(!true);              // false
console.log(!false);             // true
console.log(!(5 > 3));           // false
console.log(!!"valor");          // true (doble negación para booleano)
```

#### **Uso en control de flujo**

```javascript
let edad = 25;
let tienePermiso = true;

if (edad >= 18 && tienePermiso) {
    console.log("Puede acceder");
}

if (edad < 18 || !tienePermiso) {
    console.log("Acceso denegado");
}
```

***

### 2.5. Operadores Unarios

Operan sobre un único operando.

#### **Incremento (++) y Decremento (--)**

```javascript
let contador = 5;

// Pre-incremento: incrementa y retorna el nuevo valor
console.log(++contador);         // 6
console.log(contador);           // 6

// Post-incremento: retorna el valor antes de incrementar
console.log(contador++);         // 6
console.log(contador);           // 7

// Lo mismo aplica para decremento
let x = 10;
console.log(--x);                // 9 (pre-decremento)
console.log(x--);                // 9 (post-decremento)
console.log(x);                  // 8
```

#### **Operadores unarios + y -**

```javascript
let numero = 5;
console.log(+numero);            // 5 (conversión a número)
console.log(-numero);            // -5 (negación)

let cadena = "10";
console.log(+cadena);            // 10 (coerción a número)
console.log(-cadena);            // -10
```

***

### 2.6. Precedencia y Asociatividad de Operadores

Cuando JavaScript evalúa expresiones complejas, sigue reglas de precedencia. Los operadores con mayor precedencia se evalúan primero.

```javascript
// Multiplicación antes que suma (precedencia)
console.log(2 + 3 * 4);          // 14, no 20

// Uso de paréntesis para cambiar el orden
console.log((2 + 3) * 4);        // 20

// Potenciación tiene mayor precedencia que multiplicación
console.log(2 * 3 ** 2);         // 18 (no 36)
console.log((2 * 3) ** 2);       // 36
```

#### **Orden de precedencia (de mayor a menor)**:

1. Exponenciación (`**`)
2. Unarios (`++`, `--`, `+`, `-`, `!`)
3. Multiplicación, División, Módulo (`*`, `/`, `%`)
4. Suma, Resta (`+`, `-`)
5. Comparación (`<`, `>`, `<=`, `>=`)
6. Igualdad (`==`, `===`, `!=`, `!==`)
7. AND lógico (`&&`)
8. OR lógico (`||`)
9. Asignación (`=`, `+=`, `-=`, etc.)

***

### 2.7. El Operador Ternario

Un atajo para escribir condiciones simples en una sola línea.

**Sintaxis**: `condición ? valor_si_verdadero : valor_si_falso`

```javascript
let edad = 20;
let estado = edad >= 18 ? "Mayor de edad" : "Menor de edad";
console.log(estado);             // "Mayor de edad"

// Anidado (evitar exceso)
let nota = 85;
let calificacion = nota >= 90 ? "A" : nota >= 80 ? "B" : nota >= 70 ? "C" : "F";
console.log(calificacion);       // "B"

// Para operaciones
let numero = 5;
let resultado = numero % 2 === 0 ? "Par" : "Impar";
console.log(resultado);          // "Impar"
```

***

### 2.8. Operadores Especiales

#### **in**

Verifica si una propiedad existe en un objeto.

```javascript
let persona = { nombre: "Juan", edad: 30 };

console.log("nombre" in persona);     // true
console.log("apellido" in persona);   // false

let array = [1, 2, 3];
console.log(0 in array);              // true (índice 0 existe)
console.log(5 in array);              // false (índice 5 no existe)
```

#### **instanceof**

Verifica si un objeto es instancia de una clase.

```javascript
let array = [1, 2, 3];
let objeto = { a: 1 };

console.log(array instanceof Array);  // true
console.log(objeto instanceof Array); // false
console.log(objeto instanceof Object); // true (todo es objeto)
```

#### **delete**

Elimina una propiedad de un objeto.

```javascript
let persona = { nombre: "Juan", edad: 30 };
delete persona.edad;
console.log(persona);                 // { nombre: "Juan" }
```

***

### Resumen del Capítulo

Los operadores son herramientas fundamentales para manipular datos. Este capítulo ha cubierto operadores aritméticos, de asignación, comparación, lógicos y especiales. Comprender la precedencia de operadores y dominar los operadores lógicos es esencial para escribir código correcto.

#### **💡 Conceptos Clave:**

* **Operadores aritméticos**: +, -, \*, /, %, \*\*
* **Asignación compuesta**: +=, -=, \*=, /=, etc.
* **Comparación estricta**: usa siempre === en lugar de ==
* **Cortocircuito**: && y || no evalúan la segunda parte si no es necesario
* **Precedencia**: Los operadores tienen un orden definido de evaluación
* **Ternario**: Alternativa compacta a if-else simple
* **typeof, in, instanceof**: Operadores para introspección

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué es importante usar `===` en lugar de `==`? Da ejemplos de problemas que podrían surgir.
2. ¿Cuál es la diferencia entre ++x y x++? ¿Cuándo importa esta diferencia?
3. Explica el concepto de **cortocircuito** en operadores lógicos. ¿Cuáles son sus ventajas?
4. Dado el código `console.log(5 + "3" * "2")`, ¿cuál es el resultado? Explica la evaluación paso a paso.
5. Diseña una función que determine si un número es par, impar, o cero usando operadores ternarios anidados.

***
