# Capítulo 11: Manipulación Segura de Datos

Este capítulo aborda patrones para trabajar con datos de forma segura, evitando mutaciones accidentales y errores.

### 11.1. Inmutabilidad: Por qué es Importante ?

```javascript
// Problema: mutación accidental
let original = { nombre: "Juan", edad: 30 };
let copia = original;
copia.edad = 31;

console.log(original.edad); // 31 (¡cambió el original!)

// Solución: copias inmutables
let copia2 = { ...original };
copia2.edad = 32;

console.log(original.edad); // 30 (sin cambios)
```

***

### 11.2. Copias Profundas (_Deep Copy_) vs Superficiales

```javascript
// Copia superficial (spread, Object.assign)
let obj1 = { usuario: { nombre: "Juan" } };
let obj2 = { ...obj1 };
obj2.usuario.nombre = "María";

console.log(obj1.usuario.nombre); // "María" (¡mutó!)

// Copia profunda con JSON
let obj3 = JSON.parse(JSON.stringify(obj1));
obj3.usuario.nombre = "Carlos";

console.log(obj1.usuario.nombre); // "María" (sin cambios)

// Copia profunda recursiva
function copiasProfunda(obj) {
    if (obj === null || typeof obj !== "object") return obj;
    if (Array.isArray(obj)) return obj.map(copiasProfunda);
    
    let copia = {};
    for (let clave in obj) {
        copia[clave] = copiasProfunda(obj[clave]);
    }
    return copia;
}
```

***

### 11.3. Evitar Mutaciones Accidentales

```javascript
// Usar const (protege contra reasignación)
const datos = { x: 1 };
// datos = {}; // Error: no puedes reasignar

// Usar Object.freeze() para objetos
const congelado = Object.freeze({ a: 1, b: 2 });
// congelado.a = 10; // Falla silenciosamente

// Usar spread para crear nuevos objetos
let usuario = { nombre: "Juan" };
let actualizado = { ...usuario, nombre: "María" };
```

***

### 11.4. Validación de Estructuras

```javascript
// Validar que un objeto tenga la estructura esperada
function validarUsuario(obj) {
    if (typeof obj !== "object" || obj === null) {
        throw new TypeError("Debe ser un objeto");
    }
    if (typeof obj.nombre !== "string") {
        throw new TypeError("nombre debe ser string");
    }
    if (typeof obj.edad !== "number" || obj.edad < 0) {
        throw new TypeError("edad debe ser número positivo");
    }
    return true;
}

try {
    validarUsuario({ nombre: "Juan", edad: 30 });
    console.log("Válido");
} catch (error) {
    console.error(error.message);
}
```

***

### 11.5. Transformaciones sin Mutación

```javascript
// Array original
const numeros = [1, 2, 3, 4, 5];

// ✗ Mutante
numeros.push(6);
numeros.reverse();

// ✓ Sin mutar
const conNuevo = [...numeros, 6];
const invertido = [...numeros].reverse();

console.log(numeros); // [1, 2, 3, 4, 5] (sin cambios)

// Actualizar elemento de array
function actualizarElemento(array, indice, nuevoValor) {
    return array.map((item, i) => i === indice ? nuevoValor : item);
}

const actualizado = actualizarElemento([1, 2, 3], 1, 20);
console.log(actualizado); // [1, 20, 3]
```

***

### 11.6. Optional Chaining (`?.`)

```javascript
// Problema: errores al acceder propiedades profundas
let usuario = { perfil: { nombre: "Juan" } };
console.log(usuario.datos.edad); // TypeError

// Solución: optional chaining
console.log(usuario.datos?.edad); // undefined (sin error)

// Encadenado
console.log(usuario?.perfil?.nombre); // "Juan"

// Con arrays
let tareas = null;
console.log(tareas?.[0]); // undefined

// Con funciones
let callback = null;
callback?.(); // No ejecuta si es null
```

***

### 11.7. Nullish Coalescing (`??`)

```javascript
// Problema: 0 y "" son falsy
let valor = 0;
console.log(valor || 10); // 10 (incorrecto, 0 es válido)

// Solución: ?? solo considera null/undefined
console.log(valor ?? 10); // 0 (correcto)

// Uso común
let nombre = null;
let nombreDefault = nombre ?? "Anónimo";
console.log(nombreDefault); // "Anónimo"

// Con strings
let configuracion = "" ?? "defecto";
console.log(configuracion); // "" (conserva)
```

***

### 11.8. Casos Prácticos: Datos de APIs

```javascript
// Respuesta API con datos anidados
const respuesta = {
    status: 200,
    data: {
        usuarios: [
            { id: 1, nombre: "Juan", contacto: { email: "juan@example.com" } },
            { id: 2, nombre: "María" }
        ]
    }
};

// Acceso seguro con optional chaining
respuesta.data?.usuarios?.forEach(u => {
    console.log(u.contacto?.email ?? "sin email");
});

// Transformación segura
const usuariosProcessados = respuesta.data?.usuarios?.map(u => ({
    id: u.id,
    nombre: u.nombre,
    email: u.contacto?.email ?? "no disponible"
})) ?? [];

console.log(usuariosProcessados);
```

***

### Resumen del Capítulo

La manipulación segura de datos previene bugs y hace el código más predecible.

#### **💡 Conceptos Clave:**

* **Inmutabilidad**: Evita efectos secundarios
* **Copias profundas**: Necesarias para datos anidados
* **Object.freeze()**: Congelación de objetos
* **Optional chaining (?.)**: Acceso seguro
* **Nullish coalescing (??)**: Valores por defecto seguros
* **Validación**: Verificar estructura de datos
* **Transformaciones**: Crear nuevos datos sin mutar

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre copias superficiales y profundas?
2. ¿Cuándo usarías optional chaining?
3. ¿Cuál es la diferencia entre ?? y ||?
4. ¿Cómo validarías datos de una API?

***
