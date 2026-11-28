# Kinoura

**Kinoura** es un sitio web estático, en español, pensado para centralizar la búsqueda de una salida al cine: permite explorar películas, cines y promociones, comparar precios y formatos, y encontrar la mejor opción sin tener que saltar entre distintas plataformas. Nuestro lema es: **«Menos tiempo buscando, más tiempo viviendo el cine»**.

- 🌐 **Sitio publicado:** [https://arleygutarra.github.io/kinoura/index.html](https://arleygutarra.github.io/kinoura/index.html)

- 🧱 Construido con HTML5, Bootstrap 5.3.3 y estilos authoriales en **SCSS**, compilados a CSS.

---

## Índice

1. [Qué incluye el proyecto](#1-qué-incluye-el-proyecto)
2. [Páginas y funcionalidades](#2-páginas-y-funcionalidades)
3. [Stack tecnológico](#3-stack-tecnológico)
4. [Estructura del repositorio](#4-estructura-del-repositorio)
5. [Arquitectura SCSS](#5-arquitectura-scss)
6. [Cómo ejecutar el proyecto](#6-cómo-ejecutar-el-proyecto)
7. [Compilación de los estilos](#7-compilación-de-los-estilos)

---

## 1. Qué incluye el proyecto

El sitio está compuesto por cinco páginas HTML enlazadas entre sí mediante una navegación común (barra superior en escritorio y menú *offcanvas* en móvil):

- **Carrusel de promociones** con banners específicos para móvil y escritorio.
- **Catálogo de películas** con pestañas («En cartelera», «Preventa», «Próximos estrenos») y una grilla de pósters que cambia de forma según el ancho de pantalla.
- **Listados de cines y promociones** con panel de filtros lateral y tarjetas reutilizables.
- **Página «Nosotros»** con historia, misión, equipo y formulario de contacto de demostración.
- **Diseño responsive** con dos breakpoints principales: `768px` (tablet) y `1024px` (escritorio), con enfoque *mobile-first*.
- **Accesibilidad básica**: idioma declarado (`lang="es"`), `viewport`, textos alternativos en imágenes, `aria-label` / `aria-current` en controles y modo oscuro de Bootstrap (`data-bs-theme="dark"`).

Toda la interfaz usa una paleta oscura: fondo `#101000`, superficies grises, acentos rojos (`#7f211e` / `#e53935`) y tipografía **Montserrat**, complementada con iconos **Material Symbols Outlined**.

---

## 2. Páginas y funcionalidades

| Página      | Archivo                                              | Contenido principal                                                                                                                                          |
| ----------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Inicio      | [`index.html`](./index.html)                         | Carrusel automático de 3 banners (Street Fighter, Hot Dog Prime y preventa Arirang), pestañas de películas y vista previa de 6 pósters en grilla adaptativa. |
| Cines       | [`pages/cines.html`](./pages/cines.html)             | Encabezado con ordenamiento por popularidad, precio o cercanía; filtros por cadena, ciudad y precio; tarjetas de cines con calificación y rango de precios.  |
| Películas   | [`pages/peliculas.html`](./pages/peliculas.html)     | Pestañas de cartelera / estrenos / preventa, filtros laterales y tarjetas de películas con póster, título y descripción.                                     |
| Promociones | [`pages/promociones.html`](./pages/promociones.html) | Filtros por cadena y categoría (películas, dulcería, merchandising) y tarjetas de promociones.                                                               |
| Nosotros    | [`pages/nosotros.html`](./pages/nosotros.html)       | Banner con eslogan, secciones de historia y misión, tarjetas del equipo y formulario de contacto.                                                            |

Comportamiento responsive destacado:

- En móvil, los listados se apilan en una sola columna y los filtros se muestran antes que el contenido.
- Desde `768px`, `.container` pasa a una grilla con `grid-template-areas` (`heading` / `sidebar` / `content`) y las tarjetas cambian a diseño horizontal o grillas de varias columnas.
- Desde `1024px`, la vista previa de películas del inicio usa una composición configurada con `grid-template-areas` (`xl`, `m1`, `m2`, `l`, `s1`, `s2`) para crear un mosaico editorial de pósters.
- El carrusel intercambia entre imágenes `carousel__image--mobile` y `carousel__image--desktop` según el breakpoint.
- En la página «Nosotros», las imágenes de las tarjetas del equipo pasan a blanco y negro en escritorio y recuperan color al pasar el cursor.

---

## 3. Stack tecnológico

| Capa                 | Tecnología                        | Uso                                                                                      |
| -------------------- | --------------------------------- | ---------------------------------------------------------------------------------------- |
| Estructura           | HTML5                             | Lenguaje de marcado de las cinco páginas, con atributos semánticos y de accesibilidad.   |
| Estilos              | **Sass / SCSS** → CSS             | Código fuente en `scss/`, salida compilada en `css/styles.css` (+ `css/styles.css.map`). |
| UI base              | Bootstrap 5.3.3 (CDN de jsDelivr) | Navbar, *offcanvas*, carrusel, grillas utilitarias, formularios y clases de espaciado.   |
| Tipografía e iconos  | Google Fonts                      | Montserrat (variable 100–900) y Material Symbols Outlined.                               |
| Comportamiento       | Bootstrap Bundle JS (CDN)         | Habilita el carrusel automático y el menú lateral sin JavaScript propio.                 |
| Control de versiones | Git / GitHub                      | Repositorio y publicación mediante GitHub Pages.                                         |

> El sitio **no requiere instalar dependencias npm** para verse: Bootstrap, los fonts y su JavaScript se cargan desde CDN. Sass solo es necesario si vas a modificar los estilos.

---

## 4. Estructura del repositorio

```text
kinoura/
├── index.html                 # Página de inicio
├── pages/
│   ├── cines.html
│   ├── peliculas.html
│   ├── promociones.html
│   └── nosotros.html
├── scss/                      # FUENTE de los estilos (editar aquí)
│   ├── main.scss              # Punto de entrada: une todos los parciales
│   ├── base/
│   │   ├── _tipografia.scss   # Fuentes, iconos y configuración de Material Symbols
│   │   └── _base.scss         # Reset, tokens locales, layout y reglas de las páginas
│   ├── layout/
│   │   ├── _nav.scss          # Navbar, offcanvas y menú de escritorio
│   │   ├── _header.scss       # Marcador de posición (el header solo contiene el navbar)
│   │   └── _footer.scss       # Pie de página
│   ├── components/
│   │   ├── _buttons.scss      # Botón principal `.btn-solid`
│   │   └── _cards.scss        # Variantes de tarjetas: cine, película, promoción y equipo
│   └── utilities/
│       ├── _variables.scss    # Colores, fuentes, breakpoints y degradado
│       └── _mixins.scss       # Archivo reservado para futuros mixins (vacío)
├── css/
│   ├── styles.css             # CSS generado (no editar a mano)
│   └── styles.css.map         # Source map para las DevTools del navegador
├── assets/
│   ├── kinoura-logo-white.svg / .png
│   ├── kinoura-logo-black.svg
│   ├── logo.png
│   ├── banners/               # Banners de escritorio y versión móvil
│   ├── movie-posters/         # Pósters de las películas
│   ├── cinemas/               # Imágenes de cines
│   ├── promos/                # Imágenes de promociones
│   └── about/                 # Banners, historia, misión y fotos del equipo
├── test/                      # Experimentos y notas (animación, ToDo)
├── .gitignore
└── README.md                  # Este documento
```

---

## 5. Arquitectura SCSS

La refactorización a SCSS separó un único archivo de estilos en capas, usando **parciales** (archivos con prefijo `_`, que Sass no compila por separado) y el módulo `@use` en lugar de `@import` para las dependencias internas.

### 5.1 Punto de entrada: `scss/main.scss`

Importa las capas en orden, de lo general a lo específico:

```scss
@use 'base/tipografia';
@use 'base/base';

@use 'layout/nav';
@use 'layout/footer';

@use 'components/buttons';
@use 'components/cards';

// @use 'pages/home'; // espacio reservado para reglas por página
```

De ahí se genera `css/styles.css`, que es el único archivo enlazado por los HTML (`./css/styles.css` en el inicio y `../css/styles.css` en `pages/`).

### 5.2 Capas

| Capa          | Responsabilidad                                                                                                                                                                                                                                                                                                       |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `utilities/`  | Tokens compartidos. `_variables.scss` define `$color-background`, `$color-surface`, `$color-divider`, `$color-primary`, `$color-accent`, `$color-highlight`, `$color-font`, `$font-primary`, `$breakpoint-tablet`, `$breakpoint-desktop` y `$overlay-gradient`. Se consume con `@use '../utilities/variables' as *;`. |
| `base/`       | Reset global (`*`, `body`, encabezados), carga de fuentes e iconos, espaciados, radios y pesos de fuente, además de las secciones de inicio, cines y nosotros con sus *media queries*.                                                                                                                                |
| `layout/`     | Estructura «de armazón»: navegación (incluida la personalización de variables de Bootstrap `--bs-offcanvas-*`), pie de página y el archivo vacío de header.                                                                                                                                                           |
| `components/` | Piezas reutilizables con modificadores BEM: `.btn-solid`, `.my-card`, `.card--cinema`, `.card--movie`, `.card--promotion`, `.card--team`, etc.                                                                                                                                                                        |
| `pages/`      | Espacio previsto en `main.scss` para reglas exclusivas de una página; hoy no hay archivos aquí.                                                                                                                                                                                                                       |

### 5.3 Técnicas aplicadas

- **Anidamiento** para agrupar selectores relacionados, p. ej. `.movies-preview { &__card { img { ... } } }`, manteniendo el contexto visual cerca de cada elemento.
- **Nomenclatura tipo BEM** con bloque, elemento y modificador (`movies-tabs__tab--selected`, `carousel__image--mobile`, `card--movie`, `about-container--contact-us`) para evitar colisiones con Bootstrap.
- **Variables centralizadas** para colores, tipografía, breakpoints y gradientes. Los tokens de espaciado/radio (`$spacing-xs` … `$spacing-xxl`, `$radius-md`, `$radius-lg`) viven en `_base.scss` por ser de uso interno de esa capa.
- **Funciones de Sass** como `darken()` para estados de iconos y enlaces, en lugar de colores hardcodeados.
- **Media queries `min-width`** con las variables de breakpoints: móvil es la base y las reglas se añaden progresivamente en tablet (`768px`) y escritorio (`1024px`).
- **CSS Grid + `grid-template-areas`** en el layout de dos columnas y en el mosaico de pósters; Flexbox para barras, tarjetas y alineaciones simples.

> Nota: `_header.scss` existe solo como marcador de posición porque el `<header>` de las páginas únicamente contiene el `<nav>`, cuyos estilos están en `_nav.scss`. `_mixins.scss` aún no contiene mixins; está preparado para futuras abstracciones (por ejemplo, atajos de *media queries* o estados de foco).

---

## 6. Cómo ejecutar el proyecto

### Requisitos

- Un navegador moderno con conexión a internet (Bootstrap, Google Fonts y los iconos se sirven por CDN).
- Opcional: **Python 3**, **Node.js** o la extensión *Live Server* de VS Code para servir los archivos localmente.
- Opcional: **Dart Sass** si vas a editar `scss/`.

### 1. Clonar el repositorio

```bash
git clone https://github.com/arleygutarra/kinoura.git
cd kinoura
```

### 2. Servir el sitio

Aunque `index.html` puede abrirse directamente, se recomienda usar un servidor estático para que las rutas relativas (`./assets/...`, `../css/styles.css`) se comporten igual que en GitHub Pages.

Con Python:

```bash
python -m http.server 8000
```

Luego abre <http://localhost:8000/index.html>.

Con Node.js:

```bash
npx serve .
```

Con VS Code: clic derecho sobre `index.html` → **Open with Live Server**.

Desde ahí puedes navegar a las cinco páginas usando el logo (volver al inicio) o el menú *offcanvas*.

---

## 7. Compilación de los estilos

El CSS versionado ya está compilado, así que **no hace falta compilar para ver el sitio**. Si modificas SCSS, debes regenerar `css/styles.css`:

```bash
# Instalación única (una de las dos opciones)
npm install -g sass
# o, sin instalar globalmente: usar npx sass en cada comando

# Compilación puntual
sass scss/main.scss css/styles.css

# Modo watch: recompila automáticamente al guardar
sass --watch scss/main.scss css/styles.css
```

Con `npx`, los comandos equivalentes son `npx sass scss/main.scss css/styles.css` y `npx sass --watch scss/main.scss css/styles.css`.

Sass genera `css/styles.css.map` de forma predeterminada; déjalo junto al CSS para que las DevTools muestren el archivo SCSS original. **Edita siempre `scss/`, nunca `css/styles.css`**, porque la salida se sobrescribe en cada compilación.
