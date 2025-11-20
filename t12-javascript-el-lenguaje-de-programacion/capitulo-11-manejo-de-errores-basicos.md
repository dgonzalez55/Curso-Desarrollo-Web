# Capítulo 11: Manejo de Errores Básicos

Los errores son inevitables en la programación. Este capítulo explora cómo capturar, manejar y prevenir errores de forma elegante.

### 11.1. ¿Qué son los Errores en JavaScript?

Los errores son eventos que interrumpen la ejecución normal del código. JavaScript proporciona mecanismos para capturarlos y manejarlos.

```javascript
// Error no controlado
let resultado = 10 / 0;          // Infinity (no es error)
let undefined_propiedad = null.nombre; // TypeError
```

***

### 11.2. Tipos de Errores Comunes

#### **SyntaxError**

Error en la sintaxis del código (detectado antes de ejecutar):

```javascript
// let x =;  // SyntaxError: Unexpected token
// if (true  // SyntaxError: Missing closing parenthesis
```

#### **ReferenceError**

Referencia a una variable no declarada:

```javascript
console.log(variableNoExiste); // ReferenceError: variableNoExiste is not defined
```

#### **TypeError**

Operación sobre un tipo incorrecto:

```javascript
let numero = 5;
numero.toUpperCase();           // TypeError: numero.toUpperCase is not a function

let nulo = null;
nulo.propiedad;                 // TypeError: Cannot read property 'propiedad' of null
```

#### **RangeError**

Valor fuera de rango permitido:

```javascript
let array = [];
array.length = -1;              // RangeError: Invalid array length
```

***

### 11.3. Estructura `try-catch`: Captura de Errores

La estructura `try-catch` permite ejecutar código y capturar errores si ocurren.

```javascript
try {
    // Código que podría generar error
    let resultado = JSON.parse("no es JSON");
} catch (error) {
    // Código que se ejecuta si hay error
    console.log("Error capturado:", error.message);
} finally {
    // Código que siempre se ejecuta
    console.log("Finalizando...");
}
```

#### **Objeto error**

El objeto error contiene información útil:

```javascript
try {
    let x = undefined;
    x.propiedadInexistente;
} catch (error) {
    console.log("Nombre:", error.name);        // TypeError
    console.log("Mensaje:", error.message);    // Cannot read property
    console.log("Stack:", error.stack);        // Trace completo
}
```

***

### 11.4. Bloque `finally`: Código que Siempre se Ejecuta

`finally` se ejecuta independientemente de si hay error o no:

```javascript
function abrirArchivo() {
    let archivo = abrirRecurso();
    try {
        procesarArchivo(archivo);
    } catch (error) {
        console.log("Error:", error);
    } finally {
        archivo.cerrar();              // Siempre se ejecuta
    }
}
```

***

### 11.5. Lanzar Errores: `throw`

Puedes lanzar errores personalizados con `throw`:

```javascript
function validarEdad(edad) {
    if (typeof edad !== "number") {
        throw new TypeError("La edad debe ser un número");
    }
    if (edad < 0 || edad > 150) {
        throw new RangeError("La edad debe estar entre 0 y 150");
    }
    return true;
}

try {
    validarEdad("25");              // Lanza TypeError
} catch (error) {
    console.log(error.message);
}
```

***

### 11.6. Errores de Validación en Entrada de Datos

```javascript
function validarEmail(email) {
    try {
        if (!email.includes("@")) {
            throw new Error("Email debe contener @");
        }
        if (!email.includes(".")) {
            throw new Error("Email debe contener un punto");
        }
        return true;
    } catch (error) {
        console.log("Email inválido:", error.message);
        return false;
    }
}
```

***

### 11.7. Buenas Prácticas de Manejo de Errores

#### **No ocultes errores**

```javascript
// Malo: Captura pero ignora
try {
    codigoComplejo();
} catch (error) {
    // Silencio ominoso
}

// Mejor: Registra o propaga
try {
    codigoComplejo();
} catch (error) {
    console.error("Error:", error);
    throw error;  // Re-lanza si es crítico
}
```

#### **Sé específico en catches**

```javascript
// Malo: Captura todo
try {
    JSON.parse(datos);
} catch (e) {
    console.log("Error");
}

// Mejor: Especifica el tipo
try {
    JSON.parse(datos);
} catch (error) {
    if (error instanceof SyntaxError) {
        console.log("JSON inválido");
    } else {
        throw error;
    }
}
```

***

### 11.8. Depuración con Herramientas del Navegador

```javascript
// Usa console para depuración
console.log("Información", valor);
console.warn("Advertencia", algo);
console.error("Error", problema);
console.table(array);             // Visualiza arrays como tabla

// Breakpoints en DevTools: F12 → Sources → Click número línea
```

***

### Resumen del Capítulo

El manejo de errores es esencial para escribir código robusto. `try-catch-finally` proporciona mecanismos para capturar y responder a errores de forma controlada.

#### **💡 Conceptos Clave:**

* **try-catch-finally**: Estructura de manejo de errores
* **throw**: Lanzar errores personalizados
* **Objeto error**: name, message, stack
* **Tipos comunes**: SyntaxError, ReferenceError, TypeError, RangeError
* **Validación**: Prevenir errores antes de que ocurran
* **Debugging**: Uso de console y herramientas del navegador

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre un TypeError y un ReferenceError?
2. ¿Cuándo usarías throw en lugar de retornar false?
3. ¿Por qué es importante el bloque finally?
4. Escribe una función que valide un número de teléfono y lance errores específicos.

***
