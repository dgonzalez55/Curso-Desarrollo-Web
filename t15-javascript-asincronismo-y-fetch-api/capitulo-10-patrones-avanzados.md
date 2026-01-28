# Capítulo 10: Patrones Avanzados

Este capítulo cubre técnicas avanzadas para escribir código asincrónico robusto y eficiente en aplicaciones reales.

### 10.1. AbortController: Cancelar peticiones

A veces necesitas **cancelar una petición** que ya está en curso (navegación rápida, cambio de búsqueda, etc.).

```javascript
// AbortController permite cancelar peticiones
const controller = new AbortController();

// Pasar la señal a fetch
fetch("/api/datos", {
    signal: controller.signal
});

// Cancelar después de 5 segundos
setTimeout(() => controller.abort(), 5000);
```

#### **Caso de uso: Búsqueda en vivo**

```javascript
let controladorBusqueda = null;

document.querySelector("#buscar").addEventListener("input", async (e) => {
    // Cancelar búsqueda anterior si existe
    if (controladorBusqueda) {
        controladorBusqueda.abort();
    }
    
    // Crear nuevo controlador
    controladorBusqueda = new AbortController();
    
    const termino = e.target.value.trim();
    
    if (!termino) {
        document.querySelector("#resultados").innerHTML = "";
        return;
    }
    
    try {
        const respuesta = await fetch(
            `/api/buscar?q=${termino}`,
            { signal: controladorBusqueda.signal }
        );
        
        const resultados = await respuesta.json();
        
        // Mostrar resultados solo si no fue cancelado
        document.querySelector("#resultados").innerHTML = resultados
            .map(r => `<div>${r.nombre}</div>`)
            .join("");
        
    } catch (error) {
        // AbortError significa que fue cancelado (no es un error real)
        if (error.name === "AbortError") {
            console.log("Búsqueda cancelada");
        } else {
            console.error("Error:", error);
        }
    }
});
```

#### **Timeout con AbortController:**

```javascript
async function fetchConTimeout(url, timeoutMs = 5000) {
    const controller = new AbortController();
    
    // Crear timeout
    const timeoutId = setTimeout(() => controller.abort(), timeoutMs);
    
    try {
        const respuesta = await fetch(url, {
            signal: controller.signal
        });
        
        return await respuesta.json();
        
    } catch (error) {
        if (error.name === "AbortError") {
            throw new Error(`Timeout: La petición tardó más de ${timeoutMs}ms`);
        }
        throw error;
        
    } finally {
        // Limpiar timeout
        clearTimeout(timeoutId);
    }
}

// Usar
fetchConTimeout("/api/datos", 3000)
    .then(datos => console.log(datos))
    .catch(error => console.error(error.message));
```

***

### 10.2. Reintentos y backoff exponencial

Si una petición falla, a menudo queremos **reintentar automáticamente**.

```javascript
async function fetchConReintento(url, maxReintentos = 3) {
    let intento = 0;
    
    while (intento < maxReintentos) {
        try {
            const respuesta = await fetch(url);
            
            if (!respuesta.ok) {
                throw new Error(`HTTP ${respuesta.status}`);
            }
            
            return await respuesta.json();
            
        } catch (error) {
            intento++;
            
            if (intento >= maxReintentos) {
                throw new Error(`Falló después de ${maxReintentos} intentos: ${error.message}`);
            }
            
            // Esperar antes de reintentar (exponencial)
            const delay = Math.pow(2, intento) * 1000; // 2s, 4s, 8s
            console.log(`Reintentando en ${delay}ms...`);
            await new Promise(resolve => setTimeout(resolve, delay));
        }
    }
}

// Usar
fetchConReintento("/api/datos")
    .then(datos => console.log("Éxito:", datos))
    .catch(error => console.error(error));
```

#### **Backoff exponencial con jitter:**

```javascript
async function fetchConBackoff(url, maxReintentos = 3) {
    let intento = 0;
    
    while (intento < maxReintentos) {
        try {
            const respuesta = await fetch(url);
            
            if (!respuesta.ok && respuesta.status >= 500) {
                throw new Error(`HTTP ${respuesta.status}`);
            }
            
            return await respuesta.json();
            
        } catch (error) {
            intento++;
            
            if (intento >= maxReintentos) throw error;
            
            // Backoff exponencial con jitter
            const baseDelay = Math.pow(2, intento) * 1000;
            const jitter = Math.random() * 1000; // Aleatorio 0-1s
            const delay = baseDelay + jitter;
            
            console.log(`Intento ${intento}/${maxReintentos}, esperando ${delay}ms`);
            await new Promise(resolve => setTimeout(resolve, delay));
        }
    }
}
```

***

### 10.3. Peticiones en paralelo: `Promise.all` con fetch

Cargar múltiples recursos eficientemente:

```javascript
async function cargarMultiples(...urls) {
    try {
        // Iniciar TODAS las peticiones en paralelo
        const promesas = urls.map(url => 
            fetch(url).then(r => {
                if (!r.ok) throw new Error(`${url}: HTTP ${r.status}`);
                return r.json();
            })
        );
        
        // Esperar a que TODAS terminen
        const resultados = await Promise.all(promesas);
        
        return resultados;
        
    } catch (error) {
        console.error("Error cargando recursos:", error);
        throw error;
    }
}

// Usar
try {
    const [usuarios, posts, comentarios] = await cargarMultiples(
        "/api/usuarios",
        "/api/posts",
        "/api/comentarios"
    );
    
    console.log(`Cargados: ${usuarios.length} usuarios, ${posts.length} posts`);
    
} catch (error) {
    console.error(error);
}
```

#### **`Promise.allSettled` para operaciones parciales:**

```javascript
async function cargarTodos(...urls) {
    // Esperar a TODAS, incluso si algunas fallan
    const resultados = await Promise.allSettled(
        urls.map(url => 
            fetch(url).then(r => r.json())
        )
    );
    
    const exitosos = resultados.filter(r => r.status === "fulfilled");
    const errores = resultados.filter(r => r.status === "rejected");
    
    console.log(`Éxito: ${exitosos.length}, Errores: ${errores.length}`);
    
    return {
        datos: exitosos.map(r => r.value),
        errores: errores.map(r => r.reason)
    };
}
```

***

### 10.4. _Debouncing_ y _throttling_ en búsquedas

Para evitar hacer demasiadas peticiones mientras el usuario escribe:

#### _**Debouncing**_**&#x20;(esperar a que deje de escribir):**

```javascript
function debounce(func, delay) {
    let timeoutId;
    
    return function(...args) {
        clearTimeout(timeoutId);
        
        timeoutId = setTimeout(() => {
            func(...args);
        }, delay);
    };
}

const buscarConDebounce = debounce(async (termino) => {
    const resultados = await fetch(`/api/buscar?q=${termino}`)
        .then(r => r.json());
    
    mostrarResultados(resultados);
}, 500); // Esperar 500ms después de dejar de escribir

document.querySelector("#buscar").addEventListener("input", (e) => {
    buscarConDebounce(e.target.value);
});
```

#### _**Throttling**_**&#x20;(máximo una petición cada X ms):**

```javascript
function throttle(func, delay) {
    let lastCall = 0;
    
    return function(...args) {
        const now = Date.now();
        
        if (now - lastCall >= delay) {
            func(...args);
            lastCall = now;
        }
    };
}

const autoguardadoThrottle = throttle(async (datos) => {
    await fetch("/api/guardar", {
        method: "POST",
        body: JSON.stringify(datos)
    });
}, 2000); // Máximo guardar cada 2 segundos

document.querySelector("#editor").addEventListener("input", (e) => {
    autoguardadoThrottle({ contenido: e.target.value });
});
```

***

### 10.5. Caché simple: Evitar peticiones repetidas

```javascript
class ApiCache {
    constructor(ttl = 60000) { // 60 segundos por defecto
        this.cache = new Map();
        this.ttl = ttl;
    }
    
    async obtener(url, opcionesCache = {}) {
        const { ttl = this.ttl, revalidar = false } = opcionesCache;
        
        // Verificar si está en caché y no está expirado
        if (!revalidar && this.cache.has(url)) {
            const { datos, timestamp } = this.cache.get(url);
            
            if (Date.now() - timestamp < ttl) {
                console.log("📦 Desde caché:", url);
                return datos;
            }
        }
        
        // Petición real
        console.log("📡 Descargando:", url);
        const respuesta = await fetch(url);
        
        if (!respuesta.ok) {
            throw new Error(`HTTP ${respuesta.status}`);
        }
        
        const datos = await respuesta.json();
        
        // Guardar en caché
        this.cache.set(url, {
            datos,
            timestamp: Date.now()
        });
        
        return datos;
    }
    
    limpiar(url) {
        if (url) {
            this.cache.delete(url);
        } else {
            this.cache.clear();
        }
    }
}

// Usar
const api = new ApiCache(30000); // 30 segundos de TTL

// Primera llamada: descarga
const usuarios1 = await api.obtener("/api/usuarios");

// Segunda llamada (dentro de 30s): desde caché
const usuarios2 = await api.obtener("/api/usuarios");

// Forzar revalidación
const usuarios3 = await api.obtener("/api/usuarios", { revalidar: true });
```

***

### Resumen del Capítulo

Los patrones avanzados como AbortController, reintentos, paralel loading, debouncing y caché hacen que tus aplicaciones sean más robustas, rápidas y responsivas. Son técnicas usadas en aplicaciones profesionales reales.

#### **💡 Conceptos Clave:**

* **AbortController**: Cancelar peticiones en curso
* **Reintentos**: Volver a intentar peticiones fallidas
* **Backoff exponencial**: Espaciar reintentos progresivamente
* **Promise.all**: Cargar múltiples recursos en paralelo
* **Promise.allSettled**: Esperar a todas, incluso si fallan
* **Debouncing**: Esperar a que deje de escribir
* **Throttling**: Máximo una acción cada X ms
* **Caché**: Guardar resultados para evitar peticiones

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuándo usarías AbortController?
2. ¿Cuál es la diferencia entre debouncing y throttling?
3. ¿Por qué el backoff exponencial es mejor que reintentos inmediatos?
4. ¿Cómo implementarías caché con expiración?
5. ¿Cuándo es apropiado usar Promise.all vs Promise.allSettled?
6. Crea una búsqueda en vivo con debouncing y AbortController.

***
