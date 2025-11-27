# Capítulo 8: Técnicas Avanzadas de Objetos

Este capítulo explora características avanzadas de objetos: computed properties, getters/setters, propiedades privadas y prototipos.

### 8.1. Computed Property Names

```javascript
// Propiedades dinámicas
let propiedad = "nombre";
let obj = {
    [propiedad]: "Juan",
    ["edad"]: 30,
    [1 + 2]: "tres"
};

console.log(obj.nombre); // "Juan"
console.log(obj[3]);     // "tres"

// Con expressions
let usuario = {
    id: 1,
    [`usuario_${1}`]: "Juan",
    [`get_${new Date().getFullYear()}`]: 2025
};

console.log(usuario.usuario_1); // "Juan"
console.log(usuario.get_2025);  // 2025
```

***

### 8.2. Getters y Setters

```javascript
let usuario = {
    _nombre: "Juan",
    _edad: 30,
    
    // Getter
    get nombre() {
        return this._nombre.toUpperCase();
    },
    
    // Setter
    set nombre(valor) {
        this._nombre = valor;
    },
    
    // Getter con lógica
    get esAdulto() {
        return this._edad >= 18;
    }
};

console.log(usuario.nombre);      // "JUAN"
usuario.nombre = "María";
console.log(usuario.nombre);      // "MARÍA"
console.log(usuario.esAdulto);    // true
```

***

### 8.3. Propiedades Privadas (`#`)

```javascript
class Cuenta {
    #saldo = 0;
    
    constructor(saldoInicial) {
        this.#saldo = saldoInicial;
    }
    
    depositar(cantidad) {
        this.#saldo += cantidad;
    }
    
    obtenerSaldo() {
        return this.#saldo;
    }
}

let cuenta = new Cuenta(1000);
cuenta.depositar(500);
console.log(cuenta.obtenerSaldo()); // 1500

// Acceso directo no funciona
console.log(cuenta.#saldo); // SyntaxError
```

***

### 8.4. `Symbol` como Clave de Propiedad

```javascript
// Símbolos únicos
const id = Symbol("id");
const usuario = {
    nombre: "Juan",
    [id]: 12345
};

console.log(usuario[id]); // 12345

// No aparece en Object.keys()
console.log(Object.keys(usuario)); // ["nombre"]

// Acceso con getOwnPropertySymbols()
console.log(Object.getOwnPropertySymbols(usuario)); // [Symbol(id)]
```

***

### 8.5. Prototipos y Herencia Prototípica

```javascript
// Objeto prototipo
let animalProto = {
    hacer_sonido() {
        return "Un sonido";
    }
};

// Crear objeto con prototipo
let perro = Object.create(animalProto);
perro.nombre = "Rex";
perro.hacer_sonido = function() {
    return "Woof!";
};

console.log(perro.hacer_sonido()); // "Woof!"

// Cadena de prototipos
console.log("hacer_sonido" in perro); // true
console.log(perro.hasOwnProperty("hacer_sonido")); // true
```

***

### 8.6. `Object.create()` y Herencia

```javascript
// Constructor
function Persona(nombre, edad) {
    this.nombre = nombre;
    this.edad = edad;
}

Persona.prototype.saludar = function() {
    return `Hola, soy ${this.nombre}`;
};

// Herencia
function Desarrollador(nombre, edad, lenguaje) {
    Persona.call(this, nombre, edad);
    this.lenguaje = lenguaje;
}

Desarrollador.prototype = Object.create(Persona.prototype);
Desarrollador.prototype.constructor = Desarrollador;
Desarrollador.prototype.codigoar = function() {
    return `${this.nombre} codifica en ${this.lenguaje}`;
};

let dev = new Desarrollador("Juan", 30, "JavaScript");
console.log(dev.saludar());    // "Hola, soy Juan"
console.log(dev.codigoar());   // "Juan codifica en JavaScript"
```

***

### 8.7. Verificación de Tipos: `instanceof`

```javascript
function Animal() {}
function Gato() {}
Gato.prototype = Object.create(Animal.prototype);

let minino = new Gato();

console.log(minino instanceof Gato);    // true
console.log(minino instanceof Animal);  // true
console.log(minino instanceof Object);  // true

// Con tipos built-in
console.log([] instanceof Array);       // true
console.log({} instanceof Object);      // true
console.log("texto" instanceof String); // false (primitivo)
```

***

### 8.8. Comparación de Objetos

```javascript
// Igualdad por referencia
let obj1 = { a: 1 };
let obj2 = { a: 1 };
let obj3 = obj1;

console.log(obj1 === obj2); // false (referencias diferentes)
console.log(obj1 === obj3); // true (misma referencia)

// Función para comparación profunda
function sonIguales(obj1, obj2) {
    return JSON.stringify(obj1) === JSON.stringify(obj2);
}

console.log(sonIguales({ a: 1 }, { a: 1 })); // true
```

***

### Resumen del Capítulo

Las técnicas avanzadas permiten crear objetos sofisticados con control fino sobre sus propiedades y comportamiento.

#### **💡 Conceptos Clave:**

* **Computed properties**: Nombres dinámicos de propiedades
* **Getters/Setters**: Control de acceso y modificación
* **Propiedades privadas**: Encapsulación con #
* **Símbolos**: Claves únicas y privadas
* **Prototipos**: Herencia en JavaScript
* **instanceof**: Verificación de tipo
* **Object.create()**: Crear con prototipo

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuándo usarías getters/setters?
2. ¿Cuál es la diferencia entre Symbol y propiedades normales?
3. ¿Cómo funciona la cadena de prototipos?
4. ¿Cuándo es mejor usar Object.create() vs spread?

***
