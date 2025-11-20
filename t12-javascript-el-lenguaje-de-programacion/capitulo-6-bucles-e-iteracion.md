# Capítulo 6: Bucles e Iteración

Los bucles permiten ejecutar el mismo código múltiples veces. Son fundamentales para procesar colecciones de datos, generar patrones y automatizar tareas repetitivas.

### 6.1. ¿Cuándo Necesitamos Repetir Código?

Los bucles resuelven el problema de la repetición:

```javascript
// Sin bucle: verboso y propenso a errores
console.log(1);
console.log(2);
console.log(3);
console.log(4);
console.log(5);

// Con bucle: conciso y escalable
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```

***

### 6.2. Bucle `while`: Repetición Condicional

El bucle `while` repite un bloque de código **mientras** una condición sea verdadera.

```javascript
let contador = 0;

while (contador < 5) {
    console.log(contador);
    contador++;                 // ¡No olvides incrementar!
}
// Output: 0, 1, 2, 3, 4
```

#### **Bucles infinitos (¡evita!)**

```javascript
// PELIGRO: bucle infinito
// while (true) {
//     console.log("Esto nunca termina");
// }

// Versión segura con condición de salida
let contador = 0;
while (true) {
    console.log(contador);
    contador++;
    if (contador >= 5) break;   // Salida explícita
}
```

#### **Patrón: lectura hasta una condición**

```javascript
let numero = parseInt(prompt("Introduce un número (0 para salir):"));

while (numero !== 0) {
    console.log(`Introdujiste: ${numero}`);
    numero = parseInt(prompt("Introduce un número (0 para salir):"));
}

console.log("¡Finalizaste!");
```

***

### 6.3. Bucle `do-while`: Garantía de Ejecución

El bucle `do-while` se ejecuta **al menos una vez**, incluso si la condición es falsa desde el principio.

```javascript
let contador = 0;

do {
    console.log(contador);
    contador++;
} while (contador < 5);

// Útil cuando necesitas ejecutar al menos una vez
let respuesta;
do {
    respuesta = prompt("¿Es esto correcto? (sí/no)");
} while (respuesta !== "sí" && respuesta !== "no");
```

#### **Diferencia while vs do-while**

```javascript
// while: podría no ejecutarse
let x = 10;
while (x < 5) {
    console.log(x);             // Nunca se ejecuta
}

// do-while: se ejecuta al menos una vez
let y = 10;
do {
    console.log(y);             // Se ejecuta una vez
} while (y < 5);
```

***

### 6.4. Bucle `for`: Iteración Controlada

El bucle `for` es la forma más común de repetir código con número conocido de iteraciones.

#### **Sintaxis: `for (inicialización; condición; incremento)`**

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
// Output: 0, 1, 2, 3, 4

// Equivalente con while
let i = 0;
while (i < 5) {
    console.log(i);
    i++;
}
```

#### **Componentes del `for`**

```javascript
for (let i = 0; i < 10; i += 2) {
    //  i = 0;        Inicialización (ejecuta una vez)
    //  i < 10;       Condición (se verifica cada iteración)
    //  i += 2;       Incremento (ejecuta después de cada iteración)
    console.log(i);   // 0, 2, 4, 6, 8
}
```

#### **Bucles hacia atrás**

```javascript
for (let i = 5; i > 0; i--) {
    console.log(i);
}
// Output: 5, 4, 3, 2, 1

// Cuenta regresiva
for (let i = 10; i >= 1; i--) {
    console.log(`Lanzamiento en ${i}...`);
}
```

#### **Omitir partes del for**

```javascript
// Omitir inicialización
let j = 0;
for (; j < 3; j++) {
    console.log(j);             // 0, 1, 2
}

// Omitir condición (¡será infinito!)
// for (let k = 0; ; k++) {
//     if (k === 5) break;
// }

// Omitir incremento
for (let m = 0; m < 3;) {
    console.log(m);
    m++;
}
```

***

### 6.5. Sentencias de Control: `break` y `continue`

#### **`break`: Salir del bucle**

```javascript
for (let i = 0; i < 10; i++) {
    if (i === 5) break;         // Sale del bucle cuando i es 5
    console.log(i);
}
// Output: 0, 1, 2, 3, 4

// Usar para buscar
let encontrado = false;
for (let i = 0; i < 100; i++) {
    if (i === 42) {
        encontrado = true;
        break;
    }
}
```

#### **`continue`: Saltar a la siguiente iteración**

```javascript
for (let i = 0; i < 10; i++) {
    if (i === 5) continue;      // Salta esta iteración
    console.log(i);
}
// Output: 0, 1, 2, 3, 4, 6, 7, 8, 9 (5 no aparece)

// Usar para filtrar
for (let i = 1; i <= 10; i++) {
    if (i % 2 === 0) continue;  // Salta números pares
    console.log(i);             // 1, 3, 5, 7, 9
}
```

***

### 6.6. Bucles Anidados

Bucles dentro de bucles permiten trabajar con estructuras multidimensionales.

```javascript
// Tabla de multiplicar
for (let i = 1; i <= 3; i++) {
    for (let j = 1; j <= 3; j++) {
        console.log(`${i} × ${j} = ${i * j}`);
    }
}

// Generar patrón visual
for (let filas = 1; filas <= 3; filas++) {
    let patrón = "";
    for (let estrellas = 0; estrellas < filas; estrellas++) {
        patrón += "⭐";
    }
    console.log(patrón);
}
// Output:
// ⭐
// ⭐⭐
// ⭐⭐⭐
```

#### **`break` y `continue` en bucles anidados**

```javascript
// break solo sale del bucle más interno
for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 5; j++) {
        if (j === 2) break;     // Sale del bucle j, no del i
        console.log(`i=${i}, j=${j}`);
    }
}

// Para salir de bucles anidados, usa una etiqueta
externo: for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 5; j++) {
        if (j === 2) break externo; // Sale de ambos bucles
        console.log(`i=${i}, j=${j}`);
    }
}
```

***

### 6.7. Bucle `for-of`: Iteración sobre Valores (ES6+)

Introduce una forma más moderna de iterar sobre valores en arrays.

```javascript
const frutas = ["manzana", "plátano", "naranja"];

// for-of: accede directamente a los valores
for (const fruta of frutas) {
    console.log(fruta);
}
// Output: manzana, plátano, naranja

// Equivalente con for tradicional
for (let i = 0; i < frutas.length; i++) {
    console.log(frutas[i]);
}
```

#### **`for-of` vs `for` tradicional**

```javascript
const numeros = [10, 20, 30];

// for-of: valores
for (const num of numeros) {
    console.log(num);           // 10, 20, 30
}

// for tradicional: índices
for (let i = 0; i < numeros.length; i++) {
    console.log(i);             // 0, 1, 2
}
```

#### **`for-of` con `strings`**

```javascript
const palabra = "JavaScript";

for (const letra of palabra) {
    console.log(letra);
}
// Output: J, a, v, a, S, c, r, i, p, t
```

***

### 6.8. Casos Prácticos Avanzados

#### **Validación con bucle**

```javascript
function validarContraseña(contraseña) {
    // Debe contener al menos un número
    for (const carácter of contraseña) {
        if (carácter >= '0' && carácter <= '9') {
            return true;
        }
    }
    return false;
}
```

#### **Búsqueda en array**

```javascript
function encontrarElemento(array, objetivo) {
    for (let i = 0; i < array.length; i++) {
        if (array[i] === objetivo) {
            return i;               // Retorna el índice
        }
    }
    return -1;                      // No encontrado
}

console.log(encontrarElemento([10, 20, 30, 40], 30)); // 2
```

#### **Suma acumulativa**

```javascript
let suma = 0;
for (let i = 1; i <= 100; i++) {
    suma += i;
}
console.log(suma);                  // 5050
```

***

### Resumen del Capítulo

Los bucles son herramientas poderosas para la repetición. Comprender cuándo usar `while`, `do-while`, `for` y `for-of` te permitirá escribir código más limpio y eficiente.

#### **💡 Conceptos Clave:**

* **while**: Repite mientras condición sea verdadera
* **do-while**: Se ejecuta al menos una vez
* **for**: Bucle controlado (inicialización, condición, incremento)
* **for-of**: Itera sobre valores (moderno, ES6+)
* **break**: Sale del bucle
* **continue**: Salta a la siguiente iteración
* **Bucles anidados**: Múltiples niveles de repetición

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuándo usarías `do-while` en lugar de `while`?
2. ¿Cuál es la diferencia entre `break` y `continue`?
3. Escribe una función que imprima un triángulo de estrellas usando bucles anidados.
4. ¿Por qué `for-of` es mejor que `for` tradicional para iterar arrays?
5. Diseña un programa que encuentre todos los divisores de un número usando un bucle.

***
