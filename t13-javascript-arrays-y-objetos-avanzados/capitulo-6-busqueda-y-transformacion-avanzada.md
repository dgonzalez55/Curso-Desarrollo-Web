# Capítulo 6: Búsqueda y Transformación Avanzada

Este capítulo aborda técnicas avanzadas para buscar, transformar y reorganizar datos complejos.

### 6.1. Búsquedas Complejas: Filtrar y Mapear Juntos

```javascript
let usuarios = [
    { id: 1, nombre: "Juan", edad: 30, activo: true, rol: "admin" },
    { id: 2, nombre: "María", edad: 25, activo: false, rol: "user" },
    { id: 3, nombre: "Carlos", edad: 35, activo: true, rol: "user" },
    { id: 4, nombre: "Ana", edad: 22, activo: true, rol: "admin" }
];

// Obtener nombres de usuarios activos mayores de 25
let resultado = usuarios
    .filter(u => u.activo && u.edad > 25)
    .map(u => u.nombre);

console.log(resultado); // ["Juan", "Carlos"]
```

***

### 6.2. Transformar Arrays de Objetos

```javascript
let productos = [
    { id: 1, nombre: "Laptop", precio: 1000, stock: 5 },
    { id: 2, nombre: "Mouse", precio: 20, stock: 50 }
];

// Crear vista simplificada
let resumen = productos.map(p => ({
    id: p.id,
    titulo: p.nombre.toUpperCase(),
    disponible: p.stock > 0
}));

console.log(resumen);
// [{id: 1, titulo: "LAPTOP", disponible: true}, ...]

// Agregar IVA
let conIVA = productos.map(p => ({
    ...p,
    precioConIVA: p.precio * 1.21
}));
```

***

### 6.3. Agrupar Datos

```javascript
let ventas = [
    { producto: "Laptop", monto: 1000 },
    { producto: "Mouse", monto: 20 },
    { producto: "Laptop", monto: 1000 },
    { producto: "Teclado", monto: 80 }
];

// Agrupar por producto
let agrupado = ventas.reduce((acc, venta) => {
    if (!acc[venta.producto]) {
        acc[venta.producto] = { total: 0, cantidad: 0 };
    }
    acc[venta.producto].total += venta.monto;
    acc[venta.producto].cantidad += 1;
    return acc;
}, {});

console.log(agrupado);
// {
//   Laptop: {total: 2000, cantidad: 2},
//   Mouse: {total: 20, cantidad: 1},
//   Teclado: {total: 80, cantidad: 1}
// }
```

***

### 6.4. Ordenar Arrays de Objetos

```javascript
let usuarios = [
    { nombre: "Juan", edad: 30 },
    { nombre: "María", edad: 25 },
    { nombre: "Carlos", edad: 35 }
];

// Ordenar por edad (ascendente)
usuarios.sort((a, b) => a.edad - b.edad);

// Ordenar por nombre
usuarios.sort((a, b) => a.nombre.localeCompare(b.nombre));

// Ordenar descendente
usuarios.sort((a, b) => b.edad - a.edad);

// Múltiples criterios
let tareas = [
    { prioridad: 1, titulo: "Urgente" },
    { prioridad: 2, titulo: "Normal" },
    { prioridad: 1, titulo: "Crítico" }
];

tareas.sort((a, b) => {
    if (a.prioridad !== b.prioridad) {
        return a.prioridad - b.prioridad;
    }
    return a.titulo.localeCompare(b.titulo);
});
```

***

### 6.5. Buscar en Arrays Anidados

```javascript
let empresa = {
    departamentos: [
        {
            nombre: "IT",
            empleados: [
                { id: 1, nombre: "Juan" },
                { id: 2, nombre: "María" }
            ]
        },
        {
            nombre: "RRHH",
            empleados: [
                { id: 3, nombre: "Carlos" }
            ]
        }
    ]
};

// Buscar empleado por nombre
function buscarEmpleado(nombre) {
    for (const depto of empresa.departamentos) {
        const empleado = depto.empleados.find(e => e.nombre === nombre);
        if (empleado) return empleado;
    }
    return null;
}

console.log(buscarEmpleado("María")); // {id: 2, nombre: "María"}
```

***

### 6.6. Casos Prácticos: Datos desde APIs

```javascript
// Simular respuesta API
let respuestaAPI = {
    usuarios: [
        { id: 1, nombre: "Juan", email: "juan@example.com", premium: true },
        { id: 2, nombre: "María", email: "maria@example.com", premium: false },
        { id: 3, nombre: "Carlos", email: "carlos@example.com", premium: true }
    ]
};

// Procesamiento completo
let usuariosPremium = respuestaAPI.usuarios
    .filter(u => u.premium)
    .map(u => ({
        id: u.id,
        nombre: u.nombre.toUpperCase(),
        email: u.email
    }))
    .sort((a, b) => a.nombre.localeCompare(b.nombre));

console.log(usuariosPremium);
```

***

### 6.7. Composición de Funciones

```javascript
// Funciones pequeñas
const filtroActivos = usuarios => usuarios.filter(u => u.activo);
const mapNombres = usuarios => usuarios.map(u => u.nombre);
const ordenar = array => array.sort();

// Composición (de derecha a izquierda)
const compose = (...fns) => x => fns.reduceRight((v, f) => f(v), x);

const obtenerNombresActivos = compose(
    ordenar,
    mapNombres,
    filtroActivos
);

let resultado = obtenerNombresActivos(usuarios);
```

***

### 6.8. Casos Extremos y Edge Cases

```javascript
// Array vacío
let vacio = [];
console.log(vacio.filter(x => true)); // []
console.log(vacio.find(x => true));   // undefined

// Valores null/undefined
let conNull = [1, null, 2, undefined, 3];
let limpio = conNull.filter(x => x != null);
console.log(limpio); // [1, 2, 3]

// Comparaciones NaN
let numeros = [1, 2, NaN, 3];
console.log(numeros.includes(NaN)); // true
console.log(numeros.find(x => isNaN(x))); // NaN

// Objetos con referencias circulares
let obj = { a: 1 };
obj.self = obj;
// JSON.stringify(obj); // Error!
```

***

### Resumen del Capítulo

Las técnicas avanzadas permiten trabajar con datos complejos de manera elegante. Dominar composición, transformación y búsqueda es esencial para programación profesional.

#### **💡 Conceptos Clave:**

* **Encadenamiento**: Combinar filter, map, reduce
* **Transformación**: Crear nuevas estructuras desde datos
* **Agrupación**: Reorganizar datos con reduce
* **Ordenamiento**: Múltiples criterios
* **Composición**: Reutilizar funciones
* **Edge cases**: Manejar datos extremos
* **APIs**: Procesar respuestas reales

#### **🤔 Preguntas de Reflexión:**

1. ¿Cómo agruparías datos por categoría usando reduce()?
2. ¿Cuál es la ventaja de la composición de funciones?
3. ¿Cómo manejarías arrays con valores null/undefined?
4. Diseña una función que transforme datos de API complejos.
5. ¿Cuándo es mejor usar sort() vs crear un nuevo array ordenado?

***
