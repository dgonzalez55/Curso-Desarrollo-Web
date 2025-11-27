# Capítulo 12: Buenas Prácticas con Arrays y Objetos

Este capítulo final consolida las mejores prácticas para trabajar con arrays y objetos en proyectos reales.

### 12.1. Elegir entre Array y Objeto

```javascript
// Usar ARRAY cuando:
// - Datos ordenados por índice
// - Múltiples elementos similares
// - Necesitas métodos como map, filter, reduce

const estudiantes = [
    { id: 1, nombre: "Juan" },
    { id: 2, nombre: "María" }
];

// Usar OBJETO cuando:
// - Datos con propiedades nombradas
// - Acceso por clave
// - Pocos elementos

const configuracion = {
    tema: "oscuro",
    idioma: "es",
    notificaciones: true
};
```

***

### 12.2. Normalización de Datos

```javascript
// Estructura NO normalizada (redundancia)
const libros_denormalizados = [
    { titulo: "JS 1", autor: { id: 1, nombre: "Juan" } },
    { titulo: "JS 2", autor: { id: 1, nombre: "Juan" } }
];

// Estructura NORMALIZADA (eficiente)
const autores = {
    1: { id: 1, nombre: "Juan" },
    2: { id: 2, nombre: "María" }
};

const libros = [
    { titulo: "JS 1", autorId: 1 },
    { titulo: "JS 2", autorId: 1 }
];

// Denormalizar cuando sea necesario
function obtenerLibroConAutor(libro) {
    return {
        ...libro,
        autor: autores[libro.autorId]
    };
}
```

***

### 12.3. Esquemas y Validación

```javascript
// Definir esquema esperado
const esquemaUsuario = {
    id: "number",
    nombre: "string",
    email: "string",
    edad: "number",
    activo: "boolean"
};

// Función validadora
function validar(obj, esquema) {
    for (let clave in esquema) {
        if (typeof obj[clave] !== esquema[clave]) {
            throw new Error(`${clave} debe ser ${esquema[clave]}`);
        }
    }
    return true;
}

// Usar
const usuario = { id: 1, nombre: "Juan", email: "juan@", edad: 30, activo: true };
validar(usuario, esquemaUsuario);
```

***

### 12.4. Depuración de Estructuras Complejas

```javascript
// console.table para ver arrays de objetos
const usuarios = [
    { id: 1, nombre: "Juan", edad: 30 },
    { id: 2, nombre: "María", edad: 25 }
];

console.table(usuarios);

// console.log con JSON formatting
console.log(JSON.stringify(usuarios, null, 2));

// console.group para organizar
console.group("Usuarios Activos");
console.log("Count:", 2);
console.table(usuarios);
console.groupEnd();

// Debugging selectivo
const debug = process.env.NODE_ENV === "development";
if (debug) {
    console.log("Estado actual:", usuarios);
}
```

***

### 12.5. Rendimiento: Evitar Operaciones Caras

```javascript
// ✗ Ineficiente: O(n²)
function buscarLineal(array, valor) {
    return array.includes(valor); // Búsqueda lineal
}

// ✓ Eficiente: O(1)
const conjuntoVaores = new Set(array);
function buscarRapido(valor) {
    return conjuntoValores.has(valor);
}

// ✗ Ineficiente: O(n) por elemento
let resultado = [];
for (let i = 0; i < array.length; i++) {
    resultado = [...resultado, array[i]]; // Copia el array cada vez
}

// ✓ Eficiente: O(n) total
let resultado2 = [];
for (let elemento of array) {
    resultado2.push(elemento);
}

// Usar método apropiado
array.push(elemento);     // O(1)
array.unshift(elemento);  // O(n)
```

***

### 12.6. Documentar Estructuras

```javascript
/**
 * Usuario del sistema
 * @typedef {Object} Usuario
 * @property {number} id - ID único
 * @property {string} nombre - Nombre completo
 * @property {string} email - Email válido
 * @property {Date} fechaCreacion - Cuándo se creó
 */

/**
 * Obtener usuarios activos
 * @param {Usuario[]} usuarios - Array de usuarios
 * @returns {Usuario[]} Usuarios con estatus activo
 */
function obtenerActivos(usuarios) {
    return usuarios.filter(u => u.activo);
}
```

***

### 12.7. Patrones Comunes: CRUD

```javascript
// Create, Read, Update, Delete

let usuarios = [];
let idCounter = 1;

// CREATE
function crearUsuario(nombre, email) {
    const usuario = { id: idCounter++, nombre, email, activo: true };
    usuarios.push(usuario);
    return usuario;
}

// READ
function obtenerUsuario(id) {
    return usuarios.find(u => u.id === id);
}

// UPDATE
function actualizarUsuario(id, datos) {
    const usuario = usuarios.find(u => u.id === id);
    if (!usuario) throw new Error("Usuario no encontrado");
    Object.assign(usuario, datos);
    return usuario;
}

// DELETE
function eliminarUsuario(id) {
    const indice = usuarios.findIndex(u => u.id === id);
    if (indice === -1) throw new Error("Usuario no encontrado");
    return usuarios.splice(indice, 1)[0];
}
```

***

### 12.8. Integración con el Siguiente Tema (DOM)

```javascript
// Tema 13 prepara para Tema 14: Manipulación del DOM

// Ejemplo: Renderizar lista de usuarios en HTML
function renderizarUsuarios(usuarios) {
    return usuarios
        .map(u => ({
            ...u,
            html: `<li>${u.nombre} - ${u.email}</li>`
        }))
        .map(u => u.html)
        .join("");
}

// Preparar datos desde API para mostrar en UI
async function cargarYMostrar() {
    const respuesta = await fetch("/api/usuarios");
    const usuarios = await respuesta.json();
    
    const usuariosValidos = usuarios
        .filter(u => u.email && u.nombre)
        .map(u => ({ ...u, nombreFormato: u.nombre.toUpperCase() }))
        .sort((a, b) => a.nombre.localeCompare(b.nombre));
    
    // En el Tema 14 insertaremos esto en el DOM
    return usuariosValidos;
}
```

***

### Resumen del Capítulo

Las buenas prácticas aseguran código mantenible, eficiente y predecible en proyectos reales.

#### **💡 Conceptos Clave:**

* **Elegir entre Array y Objeto**: Según el caso de uso
* **Normalización**: Evitar redundancia
* **Esquemas y Validación**: Verificar estructura
* **Depuración**: Herramientas y técnicas
* **Rendimiento**: Elegir algoritmos eficientes
* **Documentación**: Explicar estructuras complejas
* **CRUD**: Patrones básicos de datos
* **Integración**: Preparar datos para UI

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuándo usarías normalización de datos?
2. ¿Cómo depurarías un array de objetos complejos?
3. ¿Cuál es la complejidad de diferentes operaciones?
4. ¿Cómo documentarías estructuras de datos complejas?
5. Implementa un sistema CRUD simple.

***
