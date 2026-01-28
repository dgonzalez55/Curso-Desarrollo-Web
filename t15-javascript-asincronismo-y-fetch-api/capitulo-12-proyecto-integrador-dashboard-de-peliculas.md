# Capítulo 12: Proyecto Integrador - Dashboard de Películas

En este capítulo final, crearemos una **aplicación completa** que integra todo lo aprendido: Fetch, async/await, manipulación del DOM, localStorage y buenas prácticas.

### 12.1. Descripción del Proyecto

**"Movie Dashboard"**: Una aplicación que:

* Muestra películas populares desde una API (The Movie Database)
* Permite buscar películas en vivo
* Guarda favoritos en localStorage
* Filtra por géneros
* Muestra detalles de películas

***

### 12.2. Estructura del Proyecto

```
movie-dashboard/
├── index.html
├── style.css
├── js/
│   ├── app.js          (entrada principal)
│   ├── api.js          (llamadas a la API)
│   ├── storage.js      (gestión de localStorage)
│   └── ui.js           (manipulación del DOM)
└── assets/
    └── spinner.svg
```

***

### 12.3. HTML Base

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Movie Dashboard</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header class="navbar">
        <h1>🎬 Movie Dashboard</h1>
        <input type="text" id="buscar" placeholder="Buscar película...">
        <button id="favoritos-btn">⭐ Favoritos</button>
    </header>
    
    <main>
        <aside class="sidebar">
            <h3>Géneros</h3>
            <div id="generos" class="generos"></div>
        </aside>
        
        <section class="contenido">
            <div id="spinner" class="spinner" style="display: none;">
                <div class="spinner-animacion"></div>
                <p>Cargando películas...</p>
            </div>
            
            <div id="peliculas" class="grid"></div>
            <div id="error" class="error-box" style="display: none;"></div>
        </section>
    </main>
    
    <script src="js/api.js"></script>
    <script src="js/storage.js"></script>
    <script src="js/ui.js"></script>
    <script src="js/app.js"></script>
</body>
</html>
```

***

### 12.4. Módulos JavaScript

#### **api.js - Llamadas a la API**

```javascript
// api.js
const API_KEY = "TU_API_KEY_DE_TMDB";
const API_BASE = "https://api.themoviedb.org/3";

class MovieAPI {
    async obtenerPopulares(pagina = 1) {
        try {
            const respuesta = await fetch(
                `${API_BASE}/movie/popular?api_key=${API_KEY}&page=${pagina}&language=es`
            );
            
            if (!respuesta.ok) throw new Error(`HTTP ${respuesta.status}`);
            
            return await respuesta.json();
            
        } catch (error) {
            console.error("Error obteniendo películas populares:", error);
            throw error;
        }
    }
    
    async buscar(termino) {
        try {
            const respuesta = await fetch(
                `${API_BASE}/search/movie?api_key=${API_KEY}&query=${termino}&language=es`
            );
            
            if (!respuesta.ok) throw new Error(`HTTP ${respuesta.status}`);
            
            return await respuesta.json();
            
        } catch (error) {
            console.error("Error buscando películas:", error);
            throw error;
        }
    }
    
    async obtenerGeneros() {
        try {
            const respuesta = await fetch(
                `${API_BASE}/genre/movie/list?api_key=${API_KEY}&language=es`
            );
            
            if (!respuesta.ok) throw new Error(`HTTP ${respuesta.status}`);
            
            return await respuesta.json();
            
        } catch (error) {
            console.error("Error obteniendo géneros:", error);
            throw error;
        }
    }
    
    async obtenerPorGenero(generoId, pagina = 1) {
        try {
            const respuesta = await fetch(
                `${API_BASE}/discover/movie?api_key=${API_KEY}&with_genres=${generoId}&page=${pagina}&language=es`
            );
            
            if (!respuesta.ok) throw new Error(`HTTP ${respuesta.status}`);
            
            return await respuesta.json();
            
        } catch (error) {
            console.error("Error obteniendo películas por género:", error);
            throw error;
        }
    }
}

const api = new MovieAPI();
```

#### **storage.js - Gestión de localStorage**

```javascript
// storage.js
class FavoritosStorage {
    constructor(clave = "favoritos") {
        this.clave = clave;
    }
    
    obtenerTodos() {
        const json = localStorage.getItem(this.clave);
        return json ? JSON.parse(json) : [];
    }
    
    agregar(pelicula) {
        const favoritos = this.obtenerTodos();
        
        // Evitar duplicados
        if (!favoritos.find(f => f.id === pelicula.id)) {
            favoritos.push(pelicula);
            localStorage.setItem(this.clave, JSON.stringify(favoritos));
        }
    }
    
    eliminar(peliculaId) {
        const favoritos = this.obtenerTodos();
        const filtrados = favoritos.filter(f => f.id !== peliculaId);
        localStorage.setItem(this.clave, JSON.stringify(filtrados));
    }
    
    isFavorito(peliculaId) {
        return this.obtenerTodos().some(f => f.id === peliculaId);
    }
}

const storage = new FavoritosStorage();
```

#### **ui.js - Manipulación del DOM**

```javascript
// ui.js
class MovieUI {
    constructor() {
        this.contenedor = document.querySelector("#peliculas");
        this.spinner = document.querySelector("#spinner");
        this.error = document.querySelector("#error");
        this.generos = document.querySelector("#generos");
    }
    
    mostrarSpinner(mostrar) {
        this.spinner.style.display = mostrar ? "block" : "none";
    }
    
    mostrarError(mensaje) {
        this.error.textContent = mensaje;
        this.error.style.display = "block";
        this.contenedor.innerHTML = "";
    }
    
    ocultarError() {
        this.error.style.display = "none";
    }
    
    renderizarPeliculas(peliculas) {
        this.contenedor.innerHTML = peliculas
            .map(p => this.tarjetaPelicula(p))
            .join("");
        
        // Agregar event listeners a botones de favoritos
        this.contenedor.querySelectorAll(".favorito-btn").forEach(btn => {
            btn.addEventListener("click", (e) => {
                const id = parseInt(e.target.dataset.id);
                const pelicula = peliculas.find(p => p.id === id);
                
                if (storage.isFavorito(id)) {
                    storage.eliminar(id);
                    e.target.classList.remove("activo");
                } else {
                    storage.agregar(pelicula);
                    e.target.classList.add("activo");
                }
            });
        });
    }
    
    tarjetaPelicula(pelicula) {
        const esFavorito = storage.isFavorito(pelicula.id);
        const posterUrl = `https://image.tmdb.org/t/p/w300${pelicula.poster_path}`;
        
        return `
            <div class="tarjeta">
                <img src="${posterUrl}" alt="${pelicula.title}" class="poster">
                <div class="info">
                    <h3>${pelicula.title}</h3>
                    <p class="rating">⭐ ${pelicula.vote_average.toFixed(1)}/10</p>
                    <p class="sinopsis">${pelicula.overview || "Sin descripción"}</p>
                </div>
                <button class="favorito-btn ${esFavorito ? "activo" : ""}" data-id="${pelicula.id}">
                    ${esFavorito ? "⭐" : "☆"}
                </button>
            </div>
        `;
    }
    
    renderizarGeneros(generos) {
        this.generos.innerHTML = generos
            .map(g => `
                <button class="genero-btn" data-id="${g.id}">
                    ${g.name}
                </button>
            `)
            .join("");
    }
}

const ui = new MovieUI();
```

#### **app.js - Orquestración**

```javascript
// app.js

class App {
    constructor() {
        this.currentPage = 1;
        this.currentGenero = null;
        this.mostradorFavoritos = false;
        this.init();
    }
    
    async init() {
        // Cargar géneros
        try {
            const { genres } = await api.obtenerGeneros();
            ui.renderizarGeneros(genres);
            
            // Event listeners para géneros
            document.querySelectorAll(".genero-btn").forEach(btn => {
                btn.addEventListener("click", (e) => {
                    document.querySelectorAll(".genero-btn").forEach(b => b.classList.remove("activo"));
                    e.target.classList.add("activo");
                    
                    this.currentGenero = parseInt(e.target.dataset.id);
                    this.currentPage = 1;
                    this.cargarPeliculas();
                });
            });
        } catch (error) {
            ui.mostrarError("Error cargando géneros");
        }
        
        // Búsqueda en vivo
        let controladorBusqueda = null;
        const debounceSearch = this.debounce(async (termino) => {
            if (!termino.trim()) {
                this.currentPage = 1;
                this.currentGenero = null;
                this.cargarPeliculas();
                return;
            }
            
            // Cancelar búsqueda anterior
            if (controladorBusqueda) controladorBusqueda.abort();
            
            controladorBusqueda = new AbortController();
            
            try {
                ui.mostrarSpinner(true);
                ui.ocultarError();
                
                const { results } = await api.buscar(termino);
                ui.renderizarPeliculas(results);
                
            } catch (error) {
                if (error.name !== "AbortError") {
                    ui.mostrarError("Error en la búsqueda");
                }
            } finally {
                ui.mostrarSpinner(false);
            }
        }, 500);
        
        document.querySelector("#buscar").addEventListener("input", (e) => {
            debounceSearch(e.target.value);
        });
        
        // Botón de favoritos
        document.querySelector("#favoritos-btn").addEventListener("click", () => {
            this.mostrarFavoritos();
        });
        
        // Cargar películas iniciales
        this.cargarPeliculas();
    }
    
    async cargarPeliculas() {
        try {
            ui.mostrarSpinner(true);
            ui.ocultarError();
            document.querySelector("#buscar").value = "";
            
            let datos;
            
            if (this.currentGenero) {
                datos = await api.obtenerPorGenero(this.currentGenero, this.currentPage);
            } else {
                datos = await api.obtenerPopulares(this.currentPage);
            }
            
            ui.renderizarPeliculas(datos.results);
            
        } catch (error) {
            ui.mostrarError("Error cargando películas");
        } finally {
            ui.mostrarSpinner(false);
        }
    }
    
    mostrarFavoritos() {
        const favoritos = storage.obtenerTodos();
        
        if (favoritos.length === 0) {
            ui.mostrarError("No tienes películas favoritas");
            return;
        }
        
        ui.renderizarPeliculas(favoritos);
    }
    
    debounce(func, delay) {
        let timeoutId;
        return function(...args) {
            clearTimeout(timeoutId);
            timeoutId = setTimeout(() => func(...args), delay);
        };
    }
}

// Iniciar aplicación
const app = new App();
```

***

### 12.5. CSS Básico

```css
/* style.css */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background: #f0f0f0;
}

.navbar {
    background: #222;
    color: white;
    padding: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 20px;
}

#buscar {
    padding: 10px 15px;
    border: none;
    border-radius: 4px;
    width: 300px;
}

main {
    display: flex;
    gap: 20px;
    padding: 20px;
}

.sidebar {
    width: 200px;
}

.genero-btn {
    display: block;
    width: 100%;
    padding: 10px;
    margin-bottom: 5px;
    background: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.genero-btn.activo {
    background: #ff6b6b;
    color: white;
}

.contenido {
    flex: 1;
}

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 20px;
}

.tarjeta {
    background: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.poster {
    width: 100%;
    height: 300px;
    object-fit: cover;
}

.info {
    padding: 15px;
}

.favorito-btn {
    position: absolute;
    top: 10px;
    right: 10px;
    font-size: 24px;
    background: rgba(0,0,0,0.5);
    border: none;
    color: white;
    cursor: pointer;
    padding: 5px 10px;
    border-radius: 4px;
}

.error-box {
    background: #ffe0e0;
    color: #c00;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
}

.spinner {
    text-align: center;
    padding: 40px;
}
```

***

### Resumen del Capítulo

Este proyecto integrador combina:

* ✅ Fetch API y async/await
* ✅ Manipulación del DOM (T14)
* ✅ localStorage para persistencia
* ✅ Debouncing para búsqueda en vivo
* ✅ Delegación de eventos
* ✅ Modularización y buenas prácticas

#### 🎯 Siguientes Pasos

* Agregar paginación
* Mostrar detalles completos de películas
* Agregar rating del usuario
* Integrar con backend propio
* Desplegar en Netlify/Vercel

***

