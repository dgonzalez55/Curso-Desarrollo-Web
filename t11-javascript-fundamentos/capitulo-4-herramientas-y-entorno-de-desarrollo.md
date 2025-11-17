# Capítulo 4: Herramientas y Entorno de Desarrollo

Un carpintero con herramientas deficientes produce trabajos deficientes, sin importar cuál sea su habilidad. Del mismo modo, un desarrollador web con un entorno de desarrollo inadecuado será menos productivo, cometerá más errores y tendrá una experiencia frustante. Este capítulo te guía a través de la configuración de un entorno profesional de desarrollo JavaScript, desde la selección del editor hasta la comprensión del ecosistema de Node.js y npm.

### 4.1. Editores de código recomendados

#### **Visual Studio Code (VSCode) - RECOMENDADO**

**Visual Studio Code** es la opción estándar en la industria para desarrollo JavaScript. Es gratuito, ligero, rápido y altamente extensible.

**Por qué elegir VSCode:**

* **Gratuito y de código abierto**
* **Rendimiento excelente**: Abre en menos de un segundo
* **Ecosistema de extensiones masivo**: Miles de extensiones disponibles
* **Integración Git nativa**: Control de versiones incorporado
* **Terminal integrada**: No necesitas cambiar de ventana
* **IntelliSense potente**: Autocompletado inteligente
* **Debugging integrado**: Breakpoints, stepping, watchers

**Instalación:**

1. Descarga desde [https://code.visualstudio.com/](https://code.visualstudio.com/)
2. Instala siguiendo el asistente
3. Abre y listo para usar

#### **Alternativas respetables**

**WebStorm** (JetBrains)

* Más completo que VSCode
* De Pago (\~$200/año)
* Ideal para proyectos empresariales grandes
* Mejor autocompletado de JavaScript

**Sublime Text**

* Muy ligero y rápido
* De Pago (\~$80 única compra)
* Excelente para edición rápida
* Menos comunidad que VSCode

**Vim/Neovim**

* Curva de aprendizaje pronunciada
* Gratuito y ultra-ligero
* Para desarrolladores experimentados
* Productividad máxima una vez dominado

***

### 4.2. Extensiones esenciales para JavaScript

Extensiones que TODO desarrollador JavaScript debe instalar:

#### **ESLint**

Detecta errores y malas prácticas automáticamente:

```javascript
// ESLint detecta:
var x = 5;  // ⚠️ 'var' es problemático, usar 'let' o 'const'
f( )        // ⚠️ Espacios innecesarios
if(x) {}    // ⚠️ Falta espacio después de 'if'
```

**Instalación:**

```
Extensiones → Buscar "ESLint" → Instalar
```

#### **Prettier**

Formatea el código automáticamente siguiendo estándares:

```javascript
// Antes (desordenado):
function foo(a,b,c){return a+b+c;}

// Después (formateado por Prettier):
function foo(a, b, c) {
    return a + b + c;
}
```

**Instalación:**

```
Extensiones → Buscar "Prettier" → Instalar
```

#### **Live Server**

Actualiza automáticamente la página cuando cambias el código:

```
Click derecho en archivo HTML → Open with Live Server
```

Esto es extraordinario para desarrollo frontend: cambias el código, la página se actualiza automáticamente sin presionar F5.

#### **Thunder Client / REST Client**

Para probar APIs sin abandonar VSCode:

```javascript
// Rest Client example
@baseUrl = https://api.github.com

GET @baseUrl/users/github
```

#### **Better Comments**

Hace comentarios más legibles y categorizados:

```javascript
// ! Esto es importante
// ? Esto es una pregunta
// * Esto es un punto clave
// TODO: Esto hay que hacerlo
// HACK: Solución temporal
```

#### **Extensiones recomendadas adicionales**

| Extensión              | Propósito                                   |
| ---------------------- | ------------------------------------------- |
| **Path Intellisense**  | Autocompletado de rutas de archivos         |
| **Code Spell Checker** | Verifica ortografía en código y comentarios |
| **GitLens**            | Ver historia de cambios en Git              |
| **Thunder Client**     | Cliente HTTP para probar APIs               |
| **Dark+ Material**     | Tema profesional y cómodo para la vista     |

***

### 4.3. Node.js y npm: El ecosistema de JavaScript

#### **¿Qué es Node.js?**

**Node.js** es un entorno de ejecución que permite ejecutar JavaScript fuera del navegador, en el servidor:

```
JavaScript en navegador:  ← El usuario interactúa
JavaScript en Node.js:    ← El servidor procesa
```

Esto es revolucionario porque permite usar el mismo lenguaje en frontend y backend.

**Instalación de Node.js:**

1. Descarga desde [https://nodejs.org/](https://nodejs.org/)
2. Descarga la versión **LTS** (Long Term Support)
3. Instala siguiendo el asistente
4. Verifica en terminal:

```bash
node --version    # v18.17.0
npm --version     # 9.8.1
```

#### **¿Qué es npm?**

**npm** (Node Package Manager) es el gestor de paquetes de JavaScript. Es como un "App Store" para código reutilizable:

```
┌─────────────────────────────────────────┐
│          npm Registry                   │
│  (Repositorio central de 2M paquetes)   │
└──────────────────┬──────────────────────┘
                   │
            npm install paquete
                   │
                   ▼
         Descarga e instala
                   │
                   ▼
         proyecto/node_modules/
```

#### **Primeras órdenes npm**

**Crear un proyecto:**

```bash
mkdir mi-proyecto
cd mi-proyecto
npm init
```

Esto crea un archivo `package.json`:

```json
{
  "name": "mi-proyecto",
  "version": "1.0.0",
  "description": "Mi primer proyecto",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "keywords": [],
  "author": "Tu nombre",
  "license": "ISC"
}
```

**Instalar paquetes:**

```bash
# Instalar un paquete
npm install lodash

# El paquete se descarga en node_modules/
# Y se registra en package.json
```

```json
{
  "dependencies": {
    "lodash": "^4.17.21"
  }
}
```

**Usar el paquete:**

```javascript
// index.js
const _ = require('lodash');

const números = [3, 1, 4, 1, 5, 9, 2, 6];
console.log(_.uniq(números));  // [3, 1, 4, 5, 9, 2, 6]
```

**Ejecutar scripts:**

```bash
# Ejecutar el script definido en package.json
npm start

# O ejecutar un script personalizado
npm run miScript
```

```json
{
  "scripts": {
    "start": "node index.js",
    "dev": "node --watch index.js",
    "test": "jest"
  }
}
```

```bash
npm run dev      # Ejecuta node con --watch (recarga automática)
```

***

### 4.4. Iniciando tu primer proyecto

**Estructura típica de un proyecto JavaScript**

```
mi-proyecto/
├── src/                    # Código fuente
│   ├── index.js           # Archivo principal
│   ├── utils.js           # Funciones reutilizables
│   └── components/        # Componentes reutilizables
├── public/                # Archivos estáticos
│   ├── index.html
│   └── style.css
├── node_modules/          # Paquetes instalados (no versionable)
├── package.json           # Información del proyecto
├── package-lock.json      # Lock de versiones exactas
├── .gitignore            # Archivos a ignorar en Git
└── README.md             # Documentación del proyecto
```

#### **Paso a paso: Crear un proyecto desde cero**

**1. Crear carpeta del proyecto:**

```bash
mkdir contador-app
cd contador-app
```

**2. Inicializar npm:**

```bash
npm init -y  # -y usa valores por defecto
```

**3. Crear estructura:**

```bash
mkdir src public
touch src/index.js public/index.html public/style.css
```

**4. Crear .gitignore:**

```
node_modules/
.DS_Store
.env
dist/
build/
```

**5. Editar package.json:**

```json
{
  "name": "contador-app",
  "version": "1.0.0",
  "description": "Una aplicación contador simple",
  "main": "src/index.js",
  "scripts": {
    "start": "node src/index.js",
    "dev": "node --watch src/index.js"
  },
  "author": "Tu nombre",
  "license": "MIT"
}
```

**6. Crear index.html:**

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Contador App</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <h1>Contador Interactivo</h1>
        <div class="contador" id="contador">0</div>
        <button id="decrementar">-</button>
        <button id="incrementar">+</button>
        <button id="reiniciar">Reiniciar</button>
    </div>
    <script src="../src/index.js"></script>
</body>
</html>
```

**7. Crear style.css:**

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
}

.container {
    background: white;
    padding: 40px;
    border-radius: 10px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
    text-align: center;
}

h1 {
    color: #333;
    margin-bottom: 30px;
}

.contador {
    font-size: 64px;
    font-weight: bold;
    color: #667eea;
    margin: 30px 0;
}

button {
    padding: 12px 24px;
    margin: 5px;
    font-size: 16px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: all 0.3s ease;
    font-weight: bold;
}

button:hover {
    transform: scale(1.05);
}

#decrementar, #incrementar {
    background: #e74c3c;
    color: white;
}

#incrementar {
    background: #2ecc71;
}

#reiniciar {
    background: #95a5a6;
    color: white;
    display: block;
    width: 100%;
    margin-top: 20px;
}
```

**8. Crear index.js:**

```javascript
// src/index.js
let contador = 0;

const elementoContador = document.getElementById('contador');
const btnDecrementar = document.getElementById('decrementar');
const btnIncrementar = document.getElementById('incrementar');
const btnReiniciar = document.getElementById('reiniciar');

function actualizar() {
    elementoContador.textContent = contador;
}

btnDecrementar.addEventListener('click', () => {
    contador--;
    actualizar();
});

btnIncrementar.addEventListener('click', () => {
    contador++;
    actualizar();
});

btnReiniciar.addEventListener('click', () => {
    contador = 0;
    actualizar();
});

actualizar();
```

**9. Ejecutar el proyecto:**

```bash
# Instalar Live Server para desarrollo
npm install --save-dev live-server

# O simplemente abrir index.html en el navegador
```

***

### 4.5. Control de versiones con Git

#### **¿Por qué usar Git?**

Git es un sistema de control de versiones esencial para:

* **Histórico de cambios**: Revertir a versiones anteriores
* **Colaboración**: Trabajar con otros desarrolladores
* **Branches**: Desarrollar features sin afectar el código principal
* **Backup remoto**: Guardar código en la nube (GitHub, GitLab)

#### **Configuración inicial de Git**

```bash
# Instalar Git desde https://git-scm.com/

# Configurar identidad
git config --global user.name "Tu nombre"
git config --global user.email "tu@email.com"

# Verificar configuración
git config --global --list
```

#### **Órdenes Git básicas**

```bash
# Inicializar un repositorio
git init

# Ver estado
git status

# Agregar cambios al staging area
git add .                 # Agregar todos
git add archivo.js        # Agregar archivo específico

# Hacer commit
git commit -m "Descripción del cambio"

# Ver histórico
git log

# Ver cambios
git diff

# Crear rama
git branch mi-feature

# Cambiar de rama
git checkout mi-feature
git switch mi-feature     # Forma moderna

# Fusionar rama
git merge mi-feature
```

#### **Ejemplo completo: Tu primer commit**

```bash
# 1. Inicializar repositorio
cd mi-proyecto
git init

# 2. Agregar archivo .gitignore (creado previamente)
git add .gitignore

# 3. Primer commit
git commit -m "Initial commit: proyecto configurado"

# 4. Ver el registro
git log
```

#### **Conectar a GitHub**

```bash
# Crear repositorio vacío en GitHub web

# Agregar origen remoto
git remote add origin https://github.com/usuario/mi-proyecto.git

# Renombrar rama principal (si es necesario)
git branch -M main

# Subir código
git push -u origin main
```

***

### Resumen del Capítulo

Un entorno de desarrollo profesional es la base para escribir código profesional. Desde la selección de un buen editor de código hasta la comprensión del ecosistema de Node.js y npm, cada decisión impacta tu productividad y la calidad de tu trabajo.

#### **💡 Conceptos Clave:**

* **VSCode**: El editor estándar de la industria para JavaScript
* **Extensiones críticas**: ESLint, Prettier, Live Server
* **Node.js**: Permite ejecutar JavaScript fuera del navegador
* **npm**: Gestor de paquetes con acceso a 2M+ librerías reutilizables
* **package.json**: Define el proyecto y sus dependencias
* **Estructura de proyecto**: Organización lógica para escalabilidad
* **Git**: Control de versiones esencial para desarrollo profesional
* **.gitignore**: Evita versionear archivos innecesarios

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué es importante usar ESLint y Prettier en un equipo de desarrollo?
2. ¿Cuál es la diferencia entre `npm install` y `npm install --save-dev`?
3. ¿Por qué no debemos versionear la carpeta `node_modules/` en Git?
4. ¿Cómo podrías colaborar con otro desarrollador en el mismo proyecto?
5. ¿Qué es `package-lock.json` y por qué es importante?
6. ¿Cómo crearías un script npm personalizado que ejecute múltiples tareas?

***
