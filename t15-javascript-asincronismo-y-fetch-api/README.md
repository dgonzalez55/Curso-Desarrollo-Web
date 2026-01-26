# T15: Javascript -Asincronismo y Fetch API

### Tabla de Contenidos

#### **⏳** [**Capítulo 1: Introducción a la Asincronía**](capitulo-1-introduccion-a-la-asincronia.md)

* 1.1. ¿Qué es la asincronía? Operaciones bloqueantes vs no bloqueantes
* 1.2. El Event Loop: Cómo JavaScript ejecuta código asíncrono
* 1.3. Call Stack, Web APIs y Task Queue (Macrotasks y Microtasks)
* 1.4. `setTimeout`: Primera aproximación al código asíncrono
* 1.5. Ejemplos prácticos del orden de ejecución

#### **📞** [**Capítulo 2: Callbacks**](capitulo-2-callbacks.md)

* 2.1. ¿Qué es un callback? Función pasada como argumento
* 2.2. Callbacks síncronos vs asíncronos
* 2.3. Error-first callbacks: Patrón estándar
* 2.4. Limitaciones: El "callback hell" o "pyramid of doom"
* 2.5. Cuándo usar callbacks y cuándo evitarlos
* 2.6. Convertir callbacks en Promesas

#### **🤝** [**Capítulo 3: Promesas**](capitulo-3-promesas.md)

* 3.1. Creación de promesas: `new Promise(executor)`
* 3.2. Estados: pending, fulfilled, rejected
* 3.3. Métodos `.then()`, `.catch()`, `.finally()`
* 3.4. Promise chaining: Encadenar promesas
* 3.5. Propagación de errores en cadenas
* 3.6. Promesas ya resueltas y perezosas

#### **🎯** [**Capítulo 4: Combinación de promesas**](capitulo-4-combinacion-de-promesas.md)

* 4.1. `Promise.all()`: Todas deben cumplirse
* 4.2. `Promise.race()`: La primera que se resuelva
* 4.3. `Promise.allSettled()`: Esperando a todas (ES2020)
* 4.4. `Promise.any()`: La primera que se cumpla (ES2021)
* 4.5. Casos prácticos y combinaciones

#### **⚡** [**Capítulo 5: Async/Await**](capitulo-5-async-await.md)

* 5.1. Funciones `async`: Definición y retorno implícito de promesas
* 5.2. La palabra clave `await`: Esperar una promesa
* 5.3. Equivalencia con `.then()` y por qué es más legible
* 5.4. Manejo de errores: `try/catch` asíncrono
* 5.5. Operaciones en paralelo vs secuencial con `async/await`&#x20;
* 5.6. Arrow functions async
* 5.7. Async IIFE (Immediately Invoked Function Expression)

#### **🌐** [**Capítulo 6: Introducción a Fetch API**](capitulo-6-introduccion-a-fetch-api.md)

* 6.1. ¿Qué es Fetch? Reemplazo moderno de `XMLHttpRequest`
* 6.2. `fetch(url, options)`: Parámetros y objeto Response
* 6.3. Peticiones GET: Obtener datos JSON
* 6.4. Métodos del Response: `.json()`, `.text()`, `.blob()`
* 6.5. Manejo de errores: Red vs HTTP status
* 6.6. Ejemplo completo: Cargar datos y mostrar en consola

#### **🚀** [**Capítulo 7: Fetch + Async/Await (Patrón Recomendado)**](capitulo-7-fetch-+-async-await-patron-recomendado.md)

* 7.1. Reescribir promesas con `async/await`
* 7.2. Estructura típica: `fetch` → `ok` → `json()`
* 7.3. Manejo de errores con `try/catch`
* 7.4. Casos prácticos: APIs públicas
* 7.5. Depuración: Inspeccionar respuestas
* 7.6. Patrón: Función reutilizable para fetch
* 7.7. Peticiones simultáneas con `Promise.all`

#### **📤 Capítulo 8: Peticiones POST/PUT/DELETE**

* 8.1. Configurar el objeto options en fetch
* 8.2. Body: `JSON.stringify` y Content-Type
* 8.3. Método POST: Enviar datos
* 8.4. Métodos PUT y DELETE: Actualizar y eliminar
* 8.5. Ejemplo completo: CRUD con una API

#### **🎨 Capítulo 9: Integración con el DOM**

* 9.1. Renderizar datos de una API en el DOM
* 9.2. Indicadores de carga (spinners, loading state)
* 9.3. Manejo de errores en la UI (mensajes)
* 9.4. Patrón: Fetch → Procesar → Renderizar
* 9.5. Actualizar la UI en tiempo real

#### **🔄 Capítulo 10: Patrones Avanzados**

* 10.1. AbortController: Cancelar peticiones
* 10.2. Reintentos y backoff exponencial
* 10.3. Peticiones en paralelo: Promise.all con fetch
* 10.4. Debouncing y throttling en búsquedas en vivo
* 10.5. Caché simple: Evitar peticiones repetidas

#### **✅ Capítulo 11: Buenas Prácticas**

* 11.1. Centralizar llamadas a APIs (módulos)
* 11.2. Manejo consistente de errores
* 11.3. Separar lógica de datos de renderizado
* 11.4. Testing de código asíncrono
* 11.5. Evitar antipatrones comunes

#### **🎯 Capítulo 12: Proyecto Integrador**

* 12.1. Proyecto: Dashboard con múltiples APIs
* 12.2. Estructura de la aplicación
* 12.3. Integración con localStorage
* 12.4. Gestión de estados (loading, error, success)
* 12.5. Mejoras: filtrados, búsqueda, actualización
