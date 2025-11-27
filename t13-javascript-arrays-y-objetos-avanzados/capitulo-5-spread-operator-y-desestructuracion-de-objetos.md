# Capítulo 5: Spread Operator y Desestructuración de Objetos

El spread operator y la desestructuración también funcionan con objetos, permitiendo manipulaciones sofisticadas de datos estructurados.

### 5.1. Spread Operator (...) en Objetos

```javascript
let persona = { nombre: "Juan", edad: 30 };

// Expandir propiedades
let persona2 = { ...persona };
console.log(persona2); // { nombre: "Juan", edad: 30 }

// Agregar propiedades
let personaCompleta = {
    ...persona,
    ciudad: "Madrid",
    profesion: "Desarrollador"
};
console.log(personaCompleta);
// {nombre: "Juan", edad: 30, ciudad: "Madrid", profesion: "Desarrollador"}

// Sobrescribir propiedades
let personaActualizada = {
    ...persona,
    edad: 31  // Sobrescribe edad
};
console.log(personaActualizada); // {nombre: "Juan", edad: 31}
```

***

### 5.2. Copiar Objetos: Spread vs `Object.assign()`

```javascript
let original = { a: 1, b: 2 };

// Con spread
let copia1 = { ...original };

// Con Object.assign()
let copia2 = Object.assign({}, original);

// Mutador original
Object.assign(original, { a: 10 }); // Modifica original
console.log(original); // {a: 10, b: 2}

// Spread no muta
let copia3 = { ...original };
copia3.a = 100;
console.log(original.a); // 10 (sin cambios)
```

***

### 5.3. Fusionar Objetos

```javascript
let obj1 = { a: 1, b: 2 };
let obj2 = { c: 3, d: 4 };

// Fusionar con spread
let fusionado = { ...obj1, ...obj2 };
console.log(fusionado); // {a: 1, b: 2, c: 3, d: 4}

// Orden importa: las propiedades posteriores sobrescriben
let conflicto1 = { ...obj1, a: 10 };
console.log(conflicto1); // {a: 10, b: 2}

let conflicto2 = { a: 10, ...obj1 };
console.log(conflicto2); // {a: 1, b: 2}
```

***

### 5.4. Desestructuración de Objetos

```javascript
// Básico
let persona = { nombre: "Juan", edad: 30, ciudad: "Madrid" };

let { nombre, edad } = persona;
console.log(nombre, edad); // "Juan", 30

// Ignorar propiedades
let { nombre, ...resto } = persona;
console.log(nombre); // "Juan"
console.log(resto);  // {edad: 30, ciudad: "Madrid"}

// Extraer todo
let { nombre, edad, ciudad } = persona;
```

***

### 5.5. Renombrar Propiedades

```javascript
let usuario = { user_name: "juan", user_email: "juan@ejemplo.com" };

// Renombrar con desestructuración
let { user_name: nombre, user_email: email } = usuario;
console.log(nombre, email); // "juan", "juan@ejemplo.com"

// Original no cambia
console.log(usuario); // {user_name: "juan", user_email: "juan@ejemplo.com"}
```

***

### 5.6. Valores por Defecto

```javascript
// Si la propiedad no existe
let { nombre = "Anónimo", edad = 0 } = { nombre: "Juan" };
console.log(nombre, edad); // "Juan", 0

// Con objetos vacíos
let { x = 10, y = 20 } = {};
console.log(x, y); // 10, 20

// Renombrar con defecto
let { user_name: nombre = "Desconocido" } = {};
console.log(nombre); // "Desconocido"
```

***

### 5.7. Rest Properties

```javascript
let usuario = {
    id: 1,
    nombre: "Juan",
    email: "juan@ejemplo.com",
    rol: "admin",
    activo: true
};

// Capturar algunas propiedades, resto en variable
let { id, nombre, ...datos } = usuario;
console.log(id);     // 1
console.log(nombre); // "Juan"
console.log(datos);  // {email: "...", rol: "admin", activo: true}
```

***

### 5.8. Desestructuración Anidada

```javascript
let empresa = {
    nombre: "TechCorp",
    direccion: {
        calle: "Main St",
        ciudad: "Madrid",
        pais: "España"
    },
    empleados: [
        { nombre: "Juan", rol: "Dev" },
        { nombre: "María", rol: "Designer" }
    ]
};

// Extraer propiedades anidadas
let { nombre, direccion: { ciudad } } = empresa;
console.log(nombre, ciudad); // "TechCorp", "Madrid"

// Extraer de arrays anidados
let { empleados: [{ nombre: primerEmpleado }] } = empresa;
console.log(primerEmpleado); // "Juan"

// Renombrar propiedades anidadas
let { direccion: { ciudad: localidad } } = empresa;
console.log(localidad); // "Madrid"
```

***

### Resumen del Capítulo

El spread operator y la desestructuración de objetos permiten manipulaciones elegantes y concisas. Combinados con los métodos vistos para arrays, representan las herramientas modernas de JavaScript.

#### **💡 Conceptos Clave:**

* **Spread operator (...)**: Expande propiedades en nuevo objeto
* **Copiar objetos**: `{...obj}` crea copia superficial
* **Fusionar objetos**: `{...obj1, ...obj2}`
* **Desestructuración**: Extrae propiedades en variables
* **Renombrar**: `{prop: nueva_variable}`
* **Valores por defecto**: En desestructuración
* **Rest properties**: `{a, b, ...resto}`
* **Anidación**: Desestructuración de propiedades anidadas

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre spread operator y Object.assign()?
2. ¿Cómo renombramos propiedades en la desestructuración?
3. ¿Qué son las rest properties y cuándo las usarías?
4. ¿Cómo la desestructuración anidada ayuda a limpiar el código?
5. Demuestra cómo fusionar dos objetos manteniendo valores existentes.

***
