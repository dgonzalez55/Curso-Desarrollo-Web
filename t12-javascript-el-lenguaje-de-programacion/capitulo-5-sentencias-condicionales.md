# Capítulo 5: Sentencias Condicionales

Las estructuras condicionales permiten que tu código tome decisiones basadas en ciertas condiciones. Son fundamentales para la lógica de programación y permite que los programas respondan de manera diferente según el contexto.

### 5.1. Introducción: Lógica de Decisión

En la vida real, tomamos decisiones constantemente: "Si llueve, cojo paraguas; si no, no lo cojo". La programación funciona exactamente igual. Las estructuras condicionales evaluanuna condición y ejecutan código diferente según el resultado.

```javascript
let clima = "lluvia";

if (clima === "lluvia") {
    console.log("Coge un paraguas");
} else {
    console.log("No necesitas paraguas");
}
```

***

### 5.2. Sentencia `if`: La Decisión Básica

La sentencia `if` es la más simple: ejecuta un bloque de código **si** una condición es verdadera.

```javascript
let edad = 20;

if (edad >= 18) {
    console.log("Eres mayor de edad");
}

// Sin paréntesis en una línea (válido pero no recomendado)
if (edad >= 18) console.log("Mayor de edad");
```

#### **Condiciones que se evalúan**

```javascript
if (true) {
    console.log("Siempre se ejecuta");
}

if (false) {
    console.log("Nunca se ejecuta");
}

// Cualquier condición que retorne un booleano funciona
if (5 > 3) {
    console.log("5 es mayor que 3");
}

if ("texto") {
    console.log("Se ejecuta (texto es truthy)");
}

if (0) {
    console.log("NO se ejecuta (0 es falsy)");
}
```

#### **Errores comunes**

```javascript
// INCORRECTO: asignación en lugar de comparación
let x = 5;
if (x = 10) {                   // Esto asigna, no compara
    console.log(x);             // Se ejecuta, x ahora es 10
}

// CORRECTO: usar === para comparar
if (x === 10) {
    console.log("x es 10");
}
```

***

### 5.3. Sentencia `if-else`: Rama Alternativa

Cuando una condición es falsa, ejecuta un bloque alternativo con `else`.

```javascript
let edad = 15;

if (edad >= 18) {
    console.log("Mayor de edad");
} else {
    console.log("Menor de edad");
}

// if sin else también es válido
if (llueve) {
    console.log("Está lloviendo");
}
// Si no llueve, no pasa nada
```

#### **Condiciones complejas con operadores lógicos**

```javascript
let edad = 25;
let tienePermiso = true;

if (edad >= 18 && tienePermiso) {
    console.log("Puedes acceder");
} else {
    console.log("Acceso denegado");
}

// Usar NOT para negar una condición
if (!tienePermiso) {
    console.log("No tienes permiso");
}
```

***

### 5.4. Sentencia `if-else if-else`: Múltiples Alternativas

Cuando tienes más de dos opciones, usa `else if`.

```javascript
let nota = 75;
let calificacion;

if (nota >= 90) {
    calificacion = "A";
} else if (nota >= 80) {
    calificacion = "B";
} else if (nota >= 70) {
    calificacion = "C";
} else if (nota >= 60) {
    calificacion = "D";
} else {
    calificacion = "F";
}

console.log(calificacion);      // "C"
```

{% hint style="danger" %}
**Importante**: JavaScript evalúa las condiciones de arriba hacia abajo y se detiene en la primera que sea verdadera.
{% endhint %}

```javascript
let numero = 5;

if (numero > 0) {
    console.log("Positivo");
} else if (numero > 3) {        // Nunca se alcanza si numero es 5
    console.log("Mayor que 3");
}
```

***

### 5.5. Sentencia `switch-case`: Selección por Casos

Cuando comparas una variable contra múltiples valores específicos, `switch` es más legible que múltiples `if-else if`.

#### **Estructura básica de `switch`**

```javascript
let dia = "lunes";

switch (dia) {
    case "lunes":
        console.log("Inicio de semana");
        break;                          // Detiene la ejecución
    case "viernes":
        console.log("¡Casi fin de semana!");
        break;
    case "sábado":
    case "domingo":
        console.log("Fin de semana");
        break;
    default:                            // Si no coincide nada
        console.log("Día desconocido");
}
```

#### **Importancia del `break`**

Sin `break`, la ejecución **continúa** al siguiente caso (fall-through).

```javascript
let x = 2;

switch (x) {
    case 1:
        console.log("Uno");
    case 2:
        console.log("Dos");             // Se ejecuta
    case 3:
        console.log("Tres");            // También se ejecuta (¡sin break!)
    default:
        console.log("Otro");
}
// Output: Dos, Tres, Otro
```

#### **Fall-through intencional**

A veces, el fall-through es útil para agrupar casos:

```javascript
let mes = 2;

switch (mes) {
    case 12:
    case 1:
    case 2:
        console.log("Invierno");
        break;
    case 3:
    case 4:
    case 5:
        console.log("Primavera");
        break;
    // ...
}
```

***

### 5.6. El Operador Ternario: Condición en Línea

Para asignaciones simples basadas en una condición, el operador ternario es más conciso.

**Sintaxis**: `condición ? valor_si_verdadero : valor_si_falso`

```javascript
let edad = 20;
let estado = edad >= 18 ? "Mayor" : "Menor";
console.log(estado);            // "Mayor"

// Equivalente con if-else
let estado2;
if (edad >= 18) {
    estado2 = "Mayor";
} else {
    estado2 = "Menor";
}
```

#### **Ternarios anidados (usar con cuidado)**

```javascript
let nota = 85;
let grado = nota >= 90 ? "A" : nota >= 80 ? "B" : nota >= 70 ? "C" : "F";
console.log(grado);             // "B"

// Es más legible usar if-else if para muchas opciones
```

### 5.7. Condiciones Complejas y Operadores Lógicos

Combina operadores lógicos para crear condiciones sofisticadas.

#### **Operador AND (`&&`)**

Ambas condiciones deben ser verdaderas.

```javascript
let edad = 25;
let salario = 30000;

if (edad > 21 && salario > 20000) {
    console.log("Califica para préstamo");
}
```

#### **Operador OR (`||`)**

Al menos una condición debe ser verdadera.

```javascript
let esLunes = true;
let esViernes = false;

if (esLunes || esViernes) {
    console.log("Es un día importante");
}
```

#### **Operador NOT (`!`)**

Niega una condición.

```javascript
let tieneInternet = true;

if (!tieneInternet) {
    console.log("No tienes internet");
} else {
    console.log("Tienes conexión");
}
```

#### **Combinaciones complejas**

```javascript
let edad = 25;
let esEstudiante = true;
let ingresoAnual = 25000;

if ((edad >= 18 && edad <= 30) && (esEstudiante || ingresoAnual < 30000)) {
    console.log("Califica para descuento de joven");
}
```

***

### 5.8. Casos Prácticos Avanzados

#### **Validación de entrada**

```javascript
function validarEdad(edad) {
    if (typeof edad !== "number") {
        console.log("La edad debe ser un número");
        return false;
    }
    
    if (edad < 0 || edad > 150) {
        console.log("La edad debe estar entre 0 y 150");
        return false;
    }
    
    console.log("Edad válida");
    return true;
}
```

#### **Lógica de descuentos**

```javascript
function calcularDescuento(edad, esMiembro) {
    let descuento = 0;
    
    if (edad >= 65) {
        descuento = 0.20;               // 20% para seniors
    } else if (edad >= 18 && esMiembro) {
        descuento = 0.10;               // 10% para miembros adultos
    } else if (edad < 18) {
        descuento = 0.05;               // 5% para menores
    }
    
    return descuento;
}
```

#### **Switch con comparaciones complejas**

```javascript
function obtenerEstacion(mes) {
    switch (true) {                     // Usa true como selector
        case mes >= 3 && mes <= 5:
            return "Primavera";
        case mes >= 6 && mes <= 8:
            return "Verano";
        case mes >= 9 && mes <= 11:
            return "Otoño";
        case mes === 12 || mes <= 2:
            return "Invierno";
        default:
            return "Mes inválido";
    }
}
```

***

### Resumen del Capítulo

Las estructuras condicionales son los bloques construcción de la lógica. Este capítulo ha cubierto `if`, `else if`, `else`, `switch` y el operador ternario. Elegir la estructura correcta hace que el código sea más legible y mantenible.

#### **💡 Conceptos Clave:**

* **if**: Ejecuta código si una condición es verdadera
* **else**: Rama alternativa
* **else if**: Múltiples alternativas
* **switch**: Selección por casos específicos (requiere break)
* **Ternario**: Asignación condicional en una línea
* **Operadores lógicos**: &&, ||, ! para condiciones complejas
* **Comparación estricta**: Usa === en lugar de ==

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuándo es mejor usar `switch` en lugar de múltiples `if-else if`?
2. Explica qué ocurre sin `break` en un `switch`. ¿Cuándo es útil esto?
3. ¿Cuál es la diferencia entre `if (x = 5)` e `if (x === 5)`?
4. Diseña una función que determine si una año es bisiesto usando condicionales.
5. Convierte una larga cadena de `if-else if-else` a un `switch` donde sea posible.

***
