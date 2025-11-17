# Capítulo 5: Sintaxis Básica y tu Primer Script

Antes de poder correr, debes aprender a caminar. Antes de poder escribir aplicaciones complejas, debes dominar la sintaxis fundamental de JavaScript. Este capítulo te introduce a los bloques de construcción básicos: variables, tipos de datos, operadores y tu primer programa ejecutable. Estos conceptos, aunque simples, son los cimientos sobre los que se construye todo el desarrollo JavaScript.

### 5.1. Variables y declaración

#### **¿Qué es una variable?**

Una variable es un **contenedor de datos** que almacena un valor bajo un nombre. Es como una caja etiquetada donde guardas información:

```javascript
// Caja etiquetada "edad" que contiene el número 25
const edad = 25;

// Caja etiquetada "nombre" que contiene el texto "Juan"
const nombre = "Juan";
```

JavaScript ofrece tres palabras clave para declarar variables, cada una con comportamientos diferentes como se verá a continuación.

#### **`var`** <mark style="background-color:$danger;">(</mark>_<mark style="background-color:$danger;">Legacy</mark>_ <mark style="background-color:$danger;"></mark><mark style="background-color:$danger;">- No recomendado)</mark>

```javascript
var contador = 0;
var contador = 1;  // ⚠️ Se puede redeclarar
contador = 2;      // ✓ Se puede reasignar
```

**Problemas con var:**

* Scope confuso (function-scoped, no block-scoped)
* Permite redeclaración accidental
* Hoisting confuso
* Deprecated en código moderno

```javascript
// ❌ NO USES VAR
if (true) {
    var x = 5;
}
console.log(x);  // 5 (¡está fuera del if!)
```

#### **`let`** <mark style="background-color:$primary;">(Moderno - Recomendado para variables que cambian)</mark>

```javascript
let contador = 0;
// let contador = 1;  // ❌ Error: ya existe
contador = 1;        // ✓ Se puede reasignar
```

**Ventajas de let:**

* Block-scoped (solo existe en el bloque donde se declara)
* No permite redeclaración
* Hoisting predecible
* Uso moderno y recomendado

```javascript
// ✓ CORRECTO
if (true) {
    let x = 5;
}
console.log(x);  // Error: x no existe aquí
```

#### &#x20;**`const`** <mark style="background-color:$success;">(Moderno - Recomendado por defecto)</mark>

```javascript
const PI = 3.14159;
// const PI = 3.14;  // ❌ Error: no se puede redeclarar
// PI = 3;           // ❌ Error: no se puede reasignar
```

**Ventajas de const:**

* Valores inmutables (no se pueden reasignar)
* Block-scoped
* Comunica intención: "este valor no cambia"
* Mejor para optimización del motor

{% hint style="warning" %}
**Importante:** const no significa que el valor sea inmutable en el sentido profundo:



```javascript
const usuario = { nombre: "Juan" };
usuario.nombre = "María";  // ✓ PERMITIDO (mutar objeto)
// usuario = {};           // ❌ No permitido (reasignar)
```
{% endhint %}

#### **Buenas prácticas**

```javascript
// ✅ PATRÓN RECOMENDADO
const nombre = "Juan";           // Por defecto, const
let contador = 0;               // Si necesita cambiar
const calcularPromedio = () => {}; // Funciones: const

// ❌ EVITA
var x = 5;  // Legacy
let y = 5;  // Si realmente no va a cambiar
```

***

### 5.2. Tipos de datos primitivos

#### **Los 7 tipos primitivos de JavaScript**

```
typeof operador te dice qué tipo es una variable
```

#### **`Number` (Números)**

```javascript
let entero = 42;
let decimal = 3.14;
let negativo = -10;
let infinito = Infinity;
let noNumero = NaN;  // "Not a Number" (resultado de cálculo inválido)

console.log(typeof 42);  // "number"

// Operaciones
console.log(10 + 5);     // 15
console.log(10 - 5);     // 5
console.log(10 * 5);     // 50
console.log(10 / 5);     // 2
console.log(10 % 3);     // 1 (módulo)
console.log(2 ** 8);     // 256 (exponente)

// Cuidado con punto flotante
console.log(0.1 + 0.2);  // 0.30000000000000004 (error de precisión)
```

#### **`String` (Texto)**

```javascript
let nombre = "Juan";
let apellido = 'García';
let mensaje = `Hola, ${nombre} ${apellido}`;  // Template literal (ES6)

console.log(typeof "texto");  // "string"

// Propiedades y métodos
console.log(nombre.length);       // 4
console.log(nombre[0]);           // "J"
console.log(nombre.toUpperCase()); // "JUAN"
console.log(nombre.toLowerCase()); // "juan"
console.log(nombre.includes("uan")); // true
console.log(nombre.slice(0, 2));   // "Ju"
console.log(nombre.replace("Juan", "José")); // "José"

// Escapar caracteres
let ruta = "C:\\Users\\Juan\\Documentos";  // \\ para barra invertida
let comilla = "Dijo \"Hola\"";            // \" para comilla
let saltoLinea = "Primera\nSegunda";      // \n para salto de línea
```

#### **`Boolean` (Verdadero/Falso)**

```javascript
let activo = true;
let inactivo = false;

console.log(typeof true);  // "boolean"

// Conversión implícita a boolean
console.log(Boolean(1));       // true
console.log(Boolean(0));       // false
console.log(Boolean("texto")); // true
console.log(Boolean(""));      // false
console.log(Boolean(null));    // false
console.log(Boolean(undefined)); // false

// Truthy vs Falsy
if (1) console.log("1 es truthy");
if ("") console.log("cadena vacía es falsy");
```

#### **`Undefined`**

```javascript
let variable;
console.log(variable);      // undefined
console.log(typeof undefined); // "undefined"

// Undefined significa "no has asignado un valor"
function saludar() {
    // Sin return explícito
}
console.log(saludar());    // undefined
```

#### **`Null`**

```javascript
let usuario = null;  // Explícitamente sin valor
console.log(typeof null);  // "object" (¡es un bug histórico!)

// Null vs Undefined
let a;           // undefined (no asignado)
let b = null;    // null (intencionalmente sin valor)
```

#### **`Symbol` (ES6)**

```javascript
let id = Symbol("id");
let id2 = Symbol("id");

console.log(typeof id);   // "symbol"
console.log(id === id2);  // false (cada símbolo es único)

// Uso: Crear propiedades privadas de objetos
const obj = {};
obj[id] = 123;
console.log(obj[id]);  // 123
```

#### **`BigInt` (ES2020)**

```javascript
let numeroGrande = 9007199254740991n;  // 'n' al final
let masgigante = BigInt("999999999999999999999");

console.log(typeof 123n);  // "bigint"

// Para números que exceden el límite de Number
const limite = Number.MAX_SAFE_INTEGER;  // 9007199254740991
```

***

### 5.3. Operadores básicos

#### **Operadores aritméticos**

```javascript
console.log(10 + 5);   // 15 (suma)
console.log(10 - 5);   // 5 (resta)
console.log(10 * 5);   // 50 (multiplicación)
console.log(10 / 5);   // 2 (división)
console.log(10 % 3);   // 1 (módulo/residuo)
console.log(2 ** 3);   // 8 (potencia)
```

#### **Operadores de asignación**

```javascript
let x = 10;
x += 5;    // x = x + 5 → 15
x -= 3;    // x = x - 3 → 12
x *= 2;    // x = x * 2 → 24
x /= 4;    // x = x / 4 → 6
x %= 4;    // x = x % 4 → 2
```

#### **Operadores de comparación**

```javascript
console.log(5 == 5);      // true (igualdad débil)
console.log(5 != 3);      // true (desigualdad débil)
console.log(5 === 5);     // true (igualdad estricta)
console.log(5 !== "5");   // true (desigualdad estricta)

console.log(5 > 3);       // true
console.log(5 < 3);       // false
console.log(5 >= 5);      // true
console.log(5 <= 10);     // true

// ⚠️ Cuidado con == vs ===
console.log(5 == "5");    // true (conversión de tipo)
console.log(5 === "5");   // false (sin conversión)
```

#### **Operadores lógicos**

```javascript
console.log(true && false);   // false (AND - ambos deben ser true)
console.log(true || false);   // true (OR - al menos uno true)
console.log(!true);           // false (NOT - invierte)

// Uso en condicionales
if (edad >= 18 && tieneCarnet) {
    console.log("Puedes conducir");
}

if (esAdministrador || esOwner) {
    console.log("Acceso completo");
}

if (!usuarioLogueado) {
    console.log("Debes iniciar sesión");
}
```

#### **Operador ternario (condicional acortado)**

```javascript
// Sintaxis: condición ? valorSiTrue : valorSiFalse
const edad = 20;
const estado = edad >= 18 ? "Adulto" : "Menor";
console.log(estado);  // "Adulto"

// Equivalente a:
let estado2;
if (edad >= 18) {
    estado2 = "Adulto";
} else {
    estado2 = "Menor";
}

// Ternarios anidados (evita esto)
const categoria = edad < 13 ? "Niño" : edad < 18 ? "Adolescente" : "Adulto";
```

***

### 5.4. Tu primer programa JavaScript

#### **Programa 1: Calculadora simple**

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Calculadora</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 400px;
            margin: 50px auto;
            padding: 20px;
            background: #f5f5f5;
        }
        .calculadora {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 16px;
        }
        button {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            background: #007bff;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background: #0056b3;
        }
        .resultado {
            margin-top: 20px;
            padding: 15px;
            background: #e8f4f8;
            border-left: 4px solid #007bff;
            border-radius: 4px;
            font-size: 18px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="calculadora">
        <h2>Calculadora Simple</h2>
        
        <input type="number" id="numero1" placeholder="Primer número">
        <input type="number" id="numero2" placeholder="Segundo número">
        
        <button onclick="sumar()">Sumar</button>
        <button onclick="restar()">Restar</button>
        <button onclick="multiplicar()">Multiplicar</button>
        <button onclick="dividir()">Dividir</button>
        
        <div class="resultado" id="resultado" style="display: none;"></div>
    </div>

    <script>
        function obtenerNumeros() {
            const num1 = parseFloat(document.getElementById('numero1').value);
            const num2 = parseFloat(document.getElementById('numero2').value);
            
            if (isNaN(num1) || isNaN(num2)) {
                alert('Por favor ingresa números válidos');
                return null;
            }
            
            return { num1, num2 };
        }
        
        function mostrarResultado(operacion, resultado) {
            const elementoResultado = document.getElementById('resultado');
            elementoResultado.textContent = `${operacion} = ${resultado}`;
            elementoResultado.style.display = 'block';
        }
        
        function sumar() {
            const numeros = obtenerNumeros();
            if (numeros) {
                const resultado = numeros.num1 + numeros.num2;
                mostrarResultado(`${numeros.num1} + ${numeros.num2}`, resultado);
            }
        }
        
        function restar() {
            const numeros = obtenerNumeros();
            if (numeros) {
                const resultado = numeros.num1 - numeros.num2;
                mostrarResultado(`${numeros.num1} - ${numeros.num2}`, resultado);
            }
        }
        
        function multiplicar() {
            const numeros = obtenerNumeros();
            if (numeros) {
                const resultado = numeros.num1 * numeros.num2;
                mostrarResultado(`${numeros.num1} × ${numeros.num2}`, resultado);
            }
        }
        
        function dividir() {
            const numeros = obtenerNumeros();
            if (numeros) {
                if (numeros.num2 === 0) {
                    alert('No se puede dividir entre cero');
                    return;
                }
                const resultado = numeros.num1 / numeros.num2;
                mostrarResultado(`${numeros.num1} ÷ ${numeros.num2}`, resultado.toFixed(2));
            }
        }
    </script>
</body>
</html>
```

#### **Programa 2: Convertidor de temperatura**

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Convertidor de Temperatura</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 0;
        }
        .contenedor {
            background: white;
            padding: 40px;
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            width: 100%;
            max-width: 400px;
        }
        h1 {
            color: #667eea;
            text-align: center;
            margin-bottom: 30px;
        }
        .grupo {
            margin-bottom: 20px;
        }
        label {
            display: block;
            margin-bottom: 8px;
            color: #333;
            font-weight: bold;
        }
        input, select {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
            box-sizing: border-box;
        }
        select {
            cursor: pointer;
        }
        .resultado {
            margin-top: 30px;
            padding: 20px;
            background: #f0f0f0;
            border-radius: 5px;
            text-align: center;
        }
        .resultado-texto {
            font-size: 24px;
            font-weight: bold;
            color: #667eea;
        }
        .resultado-descripcion {
            font-size: 14px;
            color: #666;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="contenedor">
        <h1>🌡️ Convertidor de Temperatura</h1>
        
        <div class="grupo">
            <label for="temperatura">Temperatura:</label>
            <input type="number" id="temperatura" placeholder="Ingresa la temperatura" value="0">
        </div>
        
        <div class="grupo">
            <label for="conversion">Convertir de:</label>
            <select id="conversion">
                <option value="celcius-fahrenheit">Celsius → Fahrenheit</option>
                <option value="fahrenheit-celcius">Fahrenheit → Celsius</option>
                <option value="celcius-kelvin">Celsius → Kelvin</option>
            </select>
        </div>
        
        <div id="resultado" class="resultado">
            <div class="resultado-texto" id="resultado-valor">-</div>
            <div class="resultado-descripcion" id="resultado-desc"></div>
        </div>
    </div>

    <script>
        const inputTemperatura = document.getElementById('temperatura');
        const selectConversion = document.getElementById('conversion');
        const divResultado = document.getElementById('resultado');
        const resultadoValor = document.getElementById('resultado-valor');
        const resultadoDesc = document.getElementById('resultado-desc');
        
        function convertir() {
            const temp = parseFloat(inputTemperatura.value);
            
            if (isNaN(temp)) {
                resultadoValor.textContent = 'Ingresa un número';
                resultadoDesc.textContent = '';
                return;
            }
            
            const tipo = selectConversion.value;
            let resultado;
            let descripcion;
            
            if (tipo === 'celcius-fahrenheit') {
                resultado = (temp * 9/5) + 32;
                descripcion = `${temp}°C = ${resultado.toFixed(2)}°F`;
            } else if (tipo === 'fahrenheit-celcius') {
                resultado = (temp - 32) * 5/9;
                descripcion = `${temp}°F = ${resultado.toFixed(2)}°C`;
            } else if (tipo === 'celcius-kelvin') {
                resultado = temp + 273.15;
                descripcion = `${temp}°C = ${resultado.toFixed(2)}K`;
            }
            
            resultadoValor.textContent = resultado.toFixed(2);
            resultadoDesc.textContent = descripcion;
        }
        
        inputTemperatura.addEventListener('input', convertir);
        selectConversion.addEventListener('change', convertir);
        
        convertir();  // Calcular inicial
    </script>
</body>
</html>
```

***

### 5.5. Manejo de errores inicial

#### **Entender los errores**

```javascript
// Error de referencia: variable no existe
console.log(variableNoExistente);  // ReferenceError

// Error de tipo: operación inválida
const numero = 5;
numero.toUpperCase();              // TypeError

// Error de sintaxis: código mal escrito
conol.log("Hola");                 // SyntaxError (typo en console)
```

#### **Try-catch básico**

```javascript
try {
    // Código que podría fallar
    const resultado = 10 / 0;
    console.log(resultado);
} catch (error) {
    // Si hay error, ejecuta esto
    console.log("Ocurrió un error:", error.message);
}
```

#### **Validación de entrada**

```javascript
function dividir(a, b) {
    // Validar tipos
    if (typeof a !== 'number' || typeof b !== 'number') {
        console.error('Los argumentos deben ser números');
        return null;
    }
    
    // Validar divisor
    if (b === 0) {
        console.error('No se puede dividir entre cero');
        return null;
    }
    
    return a / b;
}

console.log(dividir(10, 2));   // 5
console.log(dividir(10, 0));   // null (error manejado)
console.log(dividir("10", 2)); // null (error manejado)
```

***

### 5.6. Buenas prácticas desde el inicio

#### **Nomenclatura consistente**

```javascript
// ✅ BUENO: Nombres descriptivos y claros
const edadDelUsuario = 25;
const calcularPromedio = (notas) => { /* ... */ };
const isActivo = true;

// ❌ MALO: Nombres genéricos o abreviados
const x = 25;
const calc = (arr) => { /* ... */ };
const a = true;
```

#### **Comentarios útiles**

```javascript
// ❌ MALO: Comentario obvio
const edad = 25;  // edad es 25

// ✅ BUENO: Comentario explicativo
const edad = 25;  // Edad mínima requerida para conducir en EU

// ✅ BUENO: Comentario de lógica compleja
// Usamos parseInt porque trim() devuelve string
const numero = parseInt(entrada.trim());
```

#### **Espaciado y formato**

```javascript
// ❌ MALO: Sin espacios
const usuario={nombre:"Juan",edad:25};
if(edad>18){}
for(let i=0;i<10;i++){}

// ✅ BUENO: Espaciado consistente
const usuario = { nombre: "Juan", edad: 25 };
if (edad > 18) {}
for (let i = 0; i < 10; i++) {}
```

#### **Evitar código anidado profundo**

```javascript
// ❌ MALO: Muy anidado (Pyramid of Doom)
if (usuario) {
    if (usuario.activo) {
        if (usuario.permisos) {
            if (usuario.permisos.admin) {
                // Hacer algo
            }
        }
    }
}

// ✅ BUENO: Early return (Guard clauses)
if (!usuario) return;
if (!usuario.activo) return;
if (!usuario.permisos) return;
if (!usuario.permisos.admin) return;
// Hacer algo
```

***

### Resumen del Capítulo

Dominar la sintaxis básica de JavaScript es fundamental para tu desarrollo como programador. Variables, tipos de datos y operadores son los ladrillos con los que construyes todo lo demás. La buena noticia es que estos conceptos son simples, pero poderosos cuando se aplican con consistencia y claridad.

#### **💡 Conceptos Clave:**

* **const por defecto, let si cambia, nunca var**: Patrón moderno
* **Siete tipos primitivos**: Number, String, Boolean, Undefined, Null, Symbol, BigInt
* **=== sobre ==**: Siempre usa igualdad estricta
* **Operadores lógicos**: &&, ||, ! para control de flujo
* **Try-catch**: Para manejar errores de forma controlada
* **Validación de entrada**: Siempre valida los datos que recibes
* **Nomenclatura clara**: El código se lee más que se escribe
* **Espaciado y formato**: La legibilidad es prioridad

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia fundamental entre var, let y const?
2. ¿Por qué === es preferible a == en JavaScript?
3. ¿Qué son los valores "truthy" y "falsy" y por qué importan?
4. ¿Cómo validarías la entrada de un usuario antes de usarla?
5. ¿Cuál es la ventaja de usar const para variables que no cambian?
6. ¿Cómo escribirías un código limpio que sea fácil de mantener?

***
