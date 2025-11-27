# Capítulo 4: Métodos de Objetos

Este capítulo explora los métodos estáticos de `Object` que permiten inspeccionar, copiar, modificar y controlar objetos.

### 4.1. `Object.keys()`: Obtener Propiedades

```javascript
let persona = { nombre: "Juan", edad: 30, ciudad: "Madrid" };

let propiedades = Object.keys(persona);
console.log(propiedades); // ["nombre", "edad", "ciudad"]

// Iterar sobre propiedades
propiedades.forEach(prop => {
    console.log(`${prop}: ${persona[prop]}`);
});

// Contar propiedades
console.log(Object.keys(persona).length); // 3

// Con arrays
let numeros = ["a", "b", "c"];
console.log(Object.keys(numeros)); // ["0", "1", "2"]
```

***

### 4.2. `Object.values()`: Obtener Valores

```javascript
let persona = { nombre: "Juan", edad: 30, ciudad: "Madrid" };

let valores = Object.values(persona);
console.log(valores); // ["Juan", 30, "Madrid"]

// Útil para procesamiento
let edades = Object.values({ juan: 30, maria: 25, carlos: 35 });
let promedioEdad = edades.reduce((a, b) => a + b) / edades.length;
console.log(promedioEdad); // 30
```

***

### 4.3. `Object.entries()`: Pares Clave-Valor

```javascript
let persona = { nombre: "Juan", edad: 30 };

let pares = Object.entries(persona);
console.log(pares);
// [["nombre", "Juan"], ["edad", 30]]

// Convertir a Map
let mapa = new Map(Object.entries(persona));
console.log(mapa.get("nombre")); // "Juan"

// Iterar con destructuring
for (const [clave, valor] of Object.entries(persona)) {
    console.log(`${clave}: ${valor}`);
}
```

***

### 4.4. `Object.assign()`: Copiar Propiedades

```javascript
let original = { a: 1, b: 2 };

// Copiar a objeto vacío (copia superficial)
let copia = Object.assign({}, original);
copia.a = 10;
console.log(original.a); // 1 (sin cambios)

// Fusionar múltiples objetos
let obj1 = { a: 1, b: 2 };
let obj2 = { c: 3, d: 4 };
let fusionado = Object.assign({}, obj1, obj2);
console.log(fusionado); // {a: 1, b: 2, c: 3, d: 4}

// Propiedades posteriores sobrescriben
let conflicto = Object.assign({ a: 10 }, { a: 1 });
console.log(conflicto); // {a: 1}

// ⚠️ MUTA el primer argumento
Object.assign(original, { a: 100 });
console.log(original.a); // 100 (modificado!)
```

***

### 4.5. `Object.create()`: Crear Prototipos

```javascript
// Crear con prototipo específico
let prototipo = {
    saludar() {
        return `Hola, ${this.nombre}`;
    }
};

let persona = Object.create(prototipo);
persona.nombre = "Juan";
console.log(persona.saludar()); // "Hola, Juan"

// Con propiedades iniciales
let usuario = Object.create(prototipo, {
    nombre: { value: "María", writable: true },
    edad: { value: 25, writable: true }
});
console.log(usuario.nombre); // "María"
```

***

### 4.6. `Object.freeze()` y `Object.seal()`

#### **`Object.freeze()`: Inmutable total**

```javascript
let persona = { nombre: "Juan", edad: 30 };

Object.freeze(persona);

persona.edad = 31;        // Silenciosamente falla
persona.ciudad = "Madrid"; // No se añade
delete persona.nombre;    // No se elimina

console.log(persona); // {nombre: "Juan", edad: 30} (sin cambios)

// Verificar si está congelado
console.log(Object.isFrozen(persona)); // true
```

#### **`Object.seal()`: No agregar/eliminar, pero sí modificar**

```javascript
let persona = { nombre: "Juan", edad: 30 };

Object.seal(persona);

persona.edad = 31;        // ✓ Funciona
persona.ciudad = "Madrid"; // ✗ No se añade
delete persona.nombre;    // ✗ No se elimina

console.log(persona); // {nombre: "Juan", edad: 31}

console.log(Object.isSealed(persona)); // true
```

***

### 4.7. `Object.hasOwnProperty()` y operador `in`

```javascript
let persona = { nombre: "Juan", edad: 30 };

// hasOwnProperty: verificar propiedad propia
console.log(persona.hasOwnProperty("nombre")); // true
console.log(persona.hasOwnProperty("toString")); // false

// in: incluye propiedades heredadas
console.log("nombre" in persona); // true
console.log("toString" in persona); // true

// Diferencia
for (let clave in persona) {
    console.log(clave); // nombre, edad (propias)
}
```

***

### 4.8. Iteración sobre Objetos

```javascript
let usuario = { id: 1, nombre: "Juan", activo: true };

// for...in
for (let clave in usuario) {
    if (usuario.hasOwnProperty(clave)) {
        console.log(clave, usuario[clave]);
    }
}

// Object.keys() + forEach
Object.keys(usuario).forEach(clave => {
    console.log(clave, usuario[clave]);
});

// Object.entries() + for...of
for (const [clave, valor] of Object.entries(usuario)) {
    console.log(clave, valor);
}

// Object.values() (solo valores)
Object.values(usuario).forEach(valor => {
    console.log(valor);
});
```

***

### Resumen del Capítulo

Los métodos de `Object` son herramientas poderosas para inspeccionar, manipular y controlar objetos. Son fundamentales para trabajar con datos estructurados.

#### **💡 Conceptos Clave:**

* **Object.keys()**: Array de propiedades
* **Object.values()**: Array de valores
* **Object.entries()**: Array de pares \[clave, valor]
* **Object.assign()**: Copiar/fusionar (muta primer argumento)
* **Object.freeze()**: Inmutabilidad total
* **Object.seal()**: Inmutabilidad parcial
* **hasOwnProperty()**: Verificación de propiedad propia
* **Iteración**: for...in, forEach, for...of

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre Object.keys(), Object.values() y Object.entries()?
2. ¿Cuándo usarías Object.assign() vs spread operator?
3. ¿Cuál es la diferencia entre freeze() y seal()?
4. ¿Cómo iterarías sobre las propiedades de un objeto?
5. ¿Por qué Object.assign() es peligroso (muta el primer argumento)?

***
