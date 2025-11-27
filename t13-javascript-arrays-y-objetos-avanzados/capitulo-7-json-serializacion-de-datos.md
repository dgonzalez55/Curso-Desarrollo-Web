# Capítulo 7: JSON - Serialización de Datos

JSON (JavaScript Object Notation) es el formato estándar para intercambiar datos en la web. Este capítulo explora cómo trabajar con JSON en JavaScript.

### 7.1. ¿Qué es JSON?

JSON es un formato de texto ligero basado en pares clave-valor, ideal para transmitir datos. Es el formato universal para APIs web.

```json
{
    "nombre": "Juan",
    "edad": 30,
    "activo": true,
    "hobbies": ["leer", "programar", "viajar"],
    "direccion": {
        "calle": "Main St",
        "ciudad": "Madrid"
    }
}
```

#### **Diferencia entre objeto JavaScript y JSON**:

```javascript
// Objeto JavaScript (válido)
let obj = { nombre: 'Juan', edad: 30 };

// JSON (los valores string tienen comillas dobles)
let json = '{"nombre": "Juan", "edad": 30}';
```

***

### 7.2. `JSON.stringify()`: Convertir a JSON

Transforma objetos/arrays JavaScript en cadenas JSON.

```javascript
let usuario = {
    id: 1,
    nombre: "Juan",
    edad: 30,
    activo: true
};

// Convertir a JSON
let json = JSON.stringify(usuario);
console.log(json);
// {"id":1,"nombre":"Juan","edad":30,"activo":true}

// Con indentación (pretty print)
let jsonFormateado = JSON.stringify(usuario, null, 2);
console.log(jsonFormateado);
// {
//   "id": 1,
//   "nombre": "Juan",
//   "edad": 30,
//   "activo": true
// }

// 4 espacios de indentación
let json4espacios = JSON.stringify(usuario, null, 4);
```

***

### 7.3. `JSON.parse()`: Convertir desde JSON

Transforma cadenas JSON en objetos JavaScript.

```javascript
let jsonString = '{"nombre":"María","edad":25,"activo":true}';

// Convertir a objeto
let usuario = JSON.parse(jsonString);
console.log(usuario.nombre); // "María"
console.log(typeof usuario); // "object"

// Arrays JSON
let jsonArray = '[1,2,3,4,5]';
let numeros = JSON.parse(jsonArray);
console.log(numeros[0]); // 1

// Anidado
let jsonAnidado = '{"usuario":{"nombre":"Juan","edad":30}}';
let datos = JSON.parse(jsonAnidado);
console.log(datos.usuario.nombre); // "Juan"
```

***

### 7.4. Parámetro replacer y space

#### **Parámetro `replacer`**

```javascript
let usuario = {
    id: 1,
    nombre: "Juan",
    contraseña: "secreta",
    edad: 30
};

// Excluir propiedades sensibles
let json = JSON.stringify(usuario, (clave, valor) => {
    if (clave === "contraseña") {
        return undefined; // Excluir
    }
    return valor;
});

console.log(json); // {"id":1,"nombre":"Juan","edad":30}

// Array de propiedades permitidas
let jsonFiltrado = JSON.stringify(usuario, ["nombre", "edad"]);
console.log(jsonFiltrado); // {"nombre":"Juan","edad":30}
```

#### **Parámetro `space`**

```javascript
let datos = { a: 1, b: 2, c: { d: 3 } };

// Sin indentación
console.log(JSON.stringify(datos));
// {"a":1,"b":2,"c":{"d":3}}

// 2 espacios
console.log(JSON.stringify(datos, null, 2));
// {
//   "a": 1,
//   "b": 2,
//   "c": {
//     "d": 3
//   }
// }

// Tabulación
console.log(JSON.stringify(datos, null, "\t"));
```

***

### 7.5. Validación de JSON

```javascript
// Función para validar JSON
function esJSON(texto) {
    try {
        JSON.parse(texto);
        return true;
    } catch (error) {
        return false;
    }
}

console.log(esJSON('{"a":1}'));     // true
console.log(esJSON('{a:1}'));       // false (sin comillas)
console.log(esJSON("no es JSON"));  // false

// Obtener objeto o null si es inválido
function parsearJSON(texto) {
    try {
        return JSON.parse(texto);
    } catch (error) {
        console.error("JSON inválido:", error.message);
        return null;
    }
}

let resultado = parsearJSON('{"nombre":"Juan"}');
console.log(resultado); // {nombre: "Juan"}
```

***

### 7.6. Casos Prácticos: Trabajar con APIs

```javascript
// Simular respuesta de API
let respuestaAPI = '{"usuarios":[{"id":1,"nombre":"Juan"},{"id":2,"nombre":"María"}]}';

// Parsear
let datos = JSON.parse(respuestaAPI);

// Procesar
let usuarios = datos.usuarios.map(u => u.nombre);
console.log(usuarios); // ["Juan", "María"]

// Preparar para enviar
let nuevoUsuario = { nombre: "Carlos", email: "carlos@ejemplo.com" };
let jsonEnviar = JSON.stringify(nuevoUsuario);
console.log(jsonEnviar); // {"nombre":"Carlos","email":"carlos@ejemplo.com"}
```

***

### 7.7. Almacenamiento en `localStorage`

```javascript
let usuario = {
    nombre: "Juan",
    edad: 30,
    preferencias: {
        tema: "oscuro",
        idioma: "es"
    }
};

// Guardar en localStorage (siempre como string)
localStorage.setItem("usuario", JSON.stringify(usuario));

// Leer desde localStorage
let usuarioGuardado = JSON.parse(localStorage.getItem("usuario"));
console.log(usuarioGuardado.nombre); // "Juan"

// Actualizar
usuarioGuardado.edad = 31;
localStorage.setItem("usuario", JSON.stringify(usuarioGuardado));

// Eliminar
localStorage.removeItem("usuario");
```

***

### 7.8. Errores Comunes con JSON

```javascript
// ✗ Error: undefined no es válido en JSON
let obj = { a: 1, b: undefined };
console.log(JSON.stringify(obj)); // {"a":1}

// ✗ Error: funciones no se serializan
let obj2 = { nombre: "Juan", saludar: () => "Hola" };
console.log(JSON.stringify(obj2)); // {"nombre":"Juan"}

// ✗ Error: referencias circulares
let a = { x: 1 };
let b = { y: a };
a.z = b; // Referencia circular
// JSON.stringify(a); // ¡Error!

// ✓ Solución: usar replacer
let json = JSON.stringify(a, (clave, valor) => {
    if (typeof valor === "object" && valor !== null) {
        if (visitados.has(valor)) {
            return "[Circular]";
        }
        visitados.add(valor);
    }
    return valor;
});

// ✗ Error: Fechas se convierten a string
let fecha = new Date();
console.log(JSON.stringify({ fecha })); // {"fecha":"2025-11-20T..."}

// ✓ Mejor: usar toISOString()
console.log(JSON.stringify({ fecha: fecha.toISOString() }));
```

### Resumen del Capítulo

JSON es el formato universal para intercambiar datos. Dominar JSON.stringify() y JSON.parse() es esencial para trabajar con APIs web y almacenar datos.

#### **💡 Conceptos Clave:**

* **JSON**: Formato de datos estándar web
* **JSON.stringify()**: Convertir objetos a JSON
* **JSON.parse()**: Convertir JSON a objetos
* **Validación**: Try-catch para detectar JSON inválido
* **localStorage**: Persistencia de datos
* **Replacer y space**: Personalizar serialización
* **Errores comunes**: undefined, funciones, referencias circulares
* **APIs**: Comunicación de datos en la web

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre un objeto JavaScript y una cadena JSON?
2. ¿Cuándo usarías JSON.stringify() vs JSON.parse()?
3. ¿Cómo validarías que una cadena es JSON válido?
4. ¿Qué propiedades no se pueden serializar en JSON?
5. ¿Cómo almacenarías objetos complejos en localStorage?

***
