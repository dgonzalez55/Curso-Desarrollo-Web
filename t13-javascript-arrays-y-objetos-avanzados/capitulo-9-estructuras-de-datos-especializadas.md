# Capítulo 9: Estructuras de Datos Especializadas

Este capítulo explora `Map` y `Set`, estructuras de datos especializadas más potentes que objetos y arrays en ciertos casos.

### 9.1. `Map`: Alternativa a Objetos

```javascript
let mapa = new Map();

// Establecer valores
mapa.set("nombre", "Juan");
mapa.set(1, "uno");
mapa.set({}, "objeto");

// Obtener valores
console.log(mapa.get("nombre")); // "Juan"
console.log(mapa.get(1));        // "uno"

// Verificar existencia
console.log(mapa.has("nombre")); // true

// Eliminar
mapa.delete("nombre");
console.log(mapa.has("nombre")); // false

// Tamaño
console.log(mapa.size); // 2

// Limpiar todo
mapa.clear();
console.log(mapa.size); // 0
```

#### **Ventajas de `Map` vs `Object`:**

* Claves pueden ser cualquier tipo
* Orden de inserción garantizado
* Método `.size` para cantidad
* Mejor rendimiento con muchas operaciones

***

### 9.2. `Set`: Colecciones Únicas

```javascript
let conjunto = new Set();

// Agregar valores
conjunto.add(1);
conjunto.add(2);
conjunto.add(1); // Se ignora (duplicado)

console.log(conjunto.size); // 2

// Verificar existencia
console.log(conjunto.has(1)); // true

// Eliminar
conjunto.delete(1);
console.log(conjunto.has(1)); // false

// Iterar
for (let valor of conjunto) {
    console.log(valor);
}

// De array a Set (eliminar duplicados)
let numeros = [1, 2, 2, 3, 3, 3];
let unicos = new Set(numeros);
console.log([...unicos]); // [1, 2, 3]
```

***

### 9.3. `WeakMap` y `WeakSet`

```javascript
// WeakMap: referencias débiles (no evita GC)
let wmap = new WeakMap();
let obj = {};

wmap.set(obj, "valor");
console.log(wmap.get(obj)); // "valor"

// WeakSet
let wset = new WeakSet();
let objeto1 = { id: 1 };
let objeto2 = { id: 2 };

wset.add(objeto1);
console.log(wset.has(objeto1)); // true
```

***

### 9.4. Métodos de `Map`

```javascript
let mapa = new Map([
    ["a", 1],
    ["b", 2],
    ["c", 3]
]);

// keys(): iterador de claves
for (let clave of mapa.keys()) {
    console.log(clave);
}

// values(): iterador de valores
for (let valor of mapa.values()) {
    console.log(valor);
}

// entries(): pares [clave, valor]
for (let [clave, valor] of mapa.entries()) {
    console.log(clave, valor);
}

// forEach()
mapa.forEach((valor, clave) => {
    console.log(`${clave}: ${valor}`);
});
```

***

### 9.5. Métodos de `Set`

```javascript
let set1 = new Set([1, 2, 3]);
let set2 = new Set([2, 3, 4]);

// Unión
let union = new Set([...set1, ...set2]);
console.log(union); // {1, 2, 3, 4}

// Intersección
let interseccion = new Set([...set1].filter(x => set2.has(x)));
console.log(interseccion); // {2, 3}

// Diferencia
let diferencia = new Set([...set1].filter(x => !set2.has(x)));
console.log(diferencia); // {1}
```

***

### 9.6. Cuándo Usar `Map` vs `Object`

| Característica | Map              | Object                 |
| -------------- | ---------------- | ---------------------- |
| Claves         | Cualquier tipo   | String/Symbol          |
| Orden          | Garantizado      | Incierto               |
| Tamaño         | `.size`          | Contar manual          |
| Rendimiento    | Mejor para maps  | Mejor para pocos datos |
| JSON           | No directo       | Nativo                 |
| Métodos        | .set, .get, .has | Asignación             |

***

### 9.7. Casos Prácticos

```javascript
// Cache usando Map
let cache = new Map();

function obtenerDatos(clave) {
    if (cache.has(clave)) {
        return cache.get(clave);
    }
    let datos = fetch(clave);
    cache.set(clave, datos);
    return datos;
}

// Contar palabras únicas
let texto = "hello world hello";
let palabras = texto.split(" ");
let conteo = new Map();

palabras.forEach(palabra => {
    conteo.set(palabra, (conteo.get(palabra) || 0) + 1);
});

console.log(conteo); // Map {'hello' => 2, 'world' => 1}
```

***

### Resumen del Capítulo

Map y Set son estructuras especializadas que completan el toolkit de JavaScript para manipulación de datos.

#### **💡 Conceptos Clave:**

* **Map**: Alternativa potente a objetos con claves flexibles
* **Set**: Colecciones de valores únicos
* **WeakMap/WeakSet**: Referencias débiles
* **Métodos**: keys(), values(), entries(), forEach()
* **Operaciones**: Unión, intersección, diferencia

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuándo usarías Map vs Object?
2. ¿Cómo eliminarías duplicados en un array usando Set?
3. ¿Qué ventajas tiene WeakMap sobre Map?
4. Crea un cache usando Map.
5. Implementa operaciones de conjuntos (unión, intersección).

***
