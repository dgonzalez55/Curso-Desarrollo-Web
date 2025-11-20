# Capítulo 9: Números y Aritmética

JavaScript trata todos los números como el tipo `number`, sin distinguir entre enteros y decimales. Este capítulo explora cómo trabajar con números de forma profesional.

### 9.1. Representación de Números en JavaScript

```javascript
let entero = 42;
let decimal = 3.14;
let notacionCientifica = 1.23e2;  // 123
let hexadecimal = 0x1A;           // 26
let octal = 0o12;                 // 10
let binario = 0b1010;             // 10
```

***

### 9.2. Enteros y Decimales: Precisión de Punto Flotante

JavaScript usa el estándar IEEE 754 (64 bits), causando problemas de precisión:

```javascript
console.log(0.1 + 0.2);           // 0.30000000000000004
console.log(0.1 + 0.2 === 0.3);   // false (¡problema clásico!)

// Solución: margen de tolerancia
const EPSILON = 1e-10;
console.log(Math.abs((0.1 + 0.2) - 0.3) < EPSILON); // true
```

***

### 9.3. NaN (Not-a-Number) e Infinity

```javascript
console.log(0 / 0);               // NaN
console.log(1 / 0);               // Infinity
console.log(-1 / 0);              // -Infinity
console.log(Number.isNaN(NaN));   // true
console.log(Number.isNaN("NaN")); // false
console.log(Number.isFinite(42)); // true
console.log(Number.isFinite(Infinity)); // false
```

***

### 9.4. Métodos de Conversión

```javascript
// parseInt: convierte a entero
console.log(parseInt("42"));       // 42
console.log(parseInt("42.99"));    // 42
console.log(parseInt("42px"));     // 42
console.log(parseInt("0xFF", 16)); // 255

// parseFloat: convierte a decimal
console.log(parseFloat("3.14"));   // 3.14
console.log(parseFloat("3.14.15")); // 3.14

// Number: conversión explícita
console.log(Number("42"));         // 42
console.log(Number("3.14"));       // 3.14
console.log(Number(""));           // 0
console.log(Number(true));         // 1
console.log(Number(false));        // 0
```

***

### 9.5. Métodos de Redondeo

```javascript
let numero = 3.7;

console.log(Math.round(numero));   // 4 (redondea al entero más cercano)
console.log(Math.floor(numero));   // 3 (redondea hacia abajo)
console.log(Math.ceil(numero));    // 4 (redondea hacia arriba)
console.log(Math.trunc(numero));   // 3 (trunca decimales)

// Redondear a N decimales
let valor = 3.14159;
console.log(Math.round(valor * 100) / 100); // 3.14
console.log(valor.toFixed(2));      // "3.14" (retorna string)
console.log(Number(valor.toFixed(2))); // 3.14
```

***

### 9.6. Métodos de la Clase Math

```javascript
// Potencia y raíz
console.log(Math.pow(2, 3));       // 8
console.log(Math.sqrt(16));        // 4
console.log(Math.cbrt(27));        // 3 (raíz cúbica)

// Valor absoluto
console.log(Math.abs(-5));         // 5

// Mínimo y máximo
console.log(Math.min(3, 1, 4, 1, 5)); // 1
console.log(Math.max(3, 1, 4, 1, 5)); // 5

// Constantes
console.log(Math.PI);              // 3.141592653589793
console.log(Math.E);               // 2.718281828459045
```

***

### 9.7. Generación de Números Aleatorios

```javascript
// Número entre 0 y 1
console.log(Math.random());        // 0.123... a 0.999...

// Entero entre 1 y 10
function aleatorioEntre(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

console.log(aleatorioEntre(1, 10));
```

***

### 9.8. Números Grandes: BigInt (ES2020+)

```javascript
// number tiene límite: 2^53 - 1
console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991

// BigInt para números más grandes
let grande = 9007199254740992n;  // Sufijo 'n'
let otroGrande = BigInt("9007199254740992");

console.log(grande + 1n);        // Funciona
// console.log(grande + 1);      // ERROR: no puedes mezclar
```

***

### Resumen del Capítulo

Los números en JavaScript tienen características únicas derivadas del estándar IEEE 754. Comprender los límites de precisión y usar los métodos apropiados es esencial para trabajar con datos numéricos de forma confiable.

#### **💡 Conceptos Clave:**

* **IEEE 754**: Causa imprecisión con decimales
* **NaN e Infinity**: Valores especiales
* **Métodos de conversión**: parseInt, parseFloat, Number
* **Redondeo**: round, floor, ceil, trunc, toFixed
* **Math**: Objeto con métodos matemáticos
* **Random**: Generación de números pseudoaleatorios
* **BigInt**: Para números muy grandes

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué 0.1 + 0.2 no es exactamente 0.3?
2. ¿Cuándo usarías parseInt vs Number?
3. ¿Cuál es la diferencia entre Math.floor y Math.trunc?
4. Escribe una función que genere un número aleatorio entre dos valores.

***
