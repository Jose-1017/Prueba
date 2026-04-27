# Guía de HTML y CSS — Prueba de Desempeño

Referencia rápida para recrear bocetos de páginas web. Cubre estructura, propiedades, casos frecuentes y patrones de layout.

---

## Tabla de contenidos

1. [Estructura base siempre usada](#1-estructura-base-siempre-usada)
2. [El body](#2-el-body)
3. [El header](#3-el-header)
4. [El footer](#4-el-footer)
5. [Cómo encajan body + header + footer](#5-cómo-encajan-body--header--footer)
6. [Imagen al lado de texto (sin estar en el mismo div)](#6-imagen-al-lado-de-texto-sin-estar-en-el-mismo-div)
7. [Casos particulares frecuentes](#7-casos-particulares-frecuentes)
8. [Flexbox completo](#8-flexbox-completo)
9. [CSS Grid completo](#9-css-grid-completo)
10. [Columnas con Grid y Flexbox](#10-columnas-con-grid-y-flexbox)
11. [Posicionamiento](#11-posicionamiento)
12. [Tipografía](#12-tipografía)
13. [Colores y fondos](#13-colores-y-fondos)
14. [Bordes, sombras y esquinas](#14-bordes-sombras-y-esquinas)
15. [Formularios](#15-formularios)
16. [Todas las propiedades CSS explicadas](#16-todas-las-propiedades-css-explicadas)
17. [Todas las etiquetas HTML explicadas](#17-todas-las-etiquetas-html-explicadas)
18. [Decisiones rápidas para la prueba](#18-decisiones-rápidas-para-la-prueba)
19. [Lista de verificación antes de entregar](#19-lista-de-verificación-antes-de-entregar)

---

## 1. Estructura base siempre usada

Todo archivo HTML debe comenzar con esta base. Nunca la omitas.

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Título de la página</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <!-- Tu contenido aquí -->

</body>
</html>
```

Y el CSS siempre debe comenzar con el reset:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

---

## 2. El body

El `body` es el lienzo de toda la página. Lo que definas aquí se hereda en todos los elementos.

### Body básico (cualquier página)

```css
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background-color: #f5f5f5;
  color: #111;
}
```

### Body con elemento centrado en pantalla (tarjetas, formularios solos)

```css
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background-color: #f5f5f5;
  color: #111;
  display: flex;
  justify-content: center;   /* centra horizontalmente */
  align-items: center;       /* centra verticalmente */
  min-height: 100vh;         /* ocupa al menos toda la pantalla */
}
```

### Body con header + contenido + footer

```css
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background-color: #f5f5f5;
  color: #111;
  display: flex;
  flex-direction: column;    /* apila header, main y footer */
  min-height: 100vh;
}
```

### Qué tener en cuenta

- `color` y `font-family` definidos en body se heredan en todos los hijos automáticamente.
- `input` y `textarea` NO heredan `font-family` del body. Siempre ponles `font-family: inherit`.
- Nunca uses `height: 100vh` en el body, siempre `min-height: 100vh`. Con `height` fijo el contenido se desborda.
- El fondo del body es lo que se ve en los espacios vacíos alrededor del contenido.

---

## 3. El header

La barra superior de la página. Casi siempre lleva logo a la izquierda y navegación a la derecha.

### HTML

```html
<header>
  <div class="logo">MiSitio</div>
  <nav>
    <a href="#" class="active">Inicio</a>
    <a href="#">Servicios</a>
    <a href="#">Nosotros</a>
    <a href="#">Contacto</a>
  </nav>
</header>
```

### CSS — header oscuro (el más común)

```css
header {
  background-color: #111;
  padding: 16px 32px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo {
  color: white;
  font-size: 20px;
  font-weight: bold;
  letter-spacing: 1px;
  text-decoration: none;  /* si el logo es un <a> */
}

nav {
  display: flex;
  gap: 24px;
}

nav a {
  color: #ccc;
  text-decoration: none;
  font-size: 14px;
}

nav a:hover {
  color: white;
}

nav a.active {
  color: white;
  font-weight: 600;
  text-decoration: underline;
  text-underline-offset: 4px;
}
```

### CSS — header claro

```css
header {
  background-color: white;
  border-bottom: 1px solid #e5e5e5;
  padding: 16px 32px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo { color: #111; font-size: 20px; font-weight: bold; }
nav a { color: #555; text-decoration: none; font-size: 14px; }
nav a:hover { color: #111; }
nav a.active { color: #2563eb; font-weight: 600; }
```

### CSS — header fijo (se queda al hacer scroll)

```css
header {
  position: sticky;
  top: 0;
  z-index: 100;  /* queda por encima del resto del contenido */
  background-color: #111;
  padding: 16px 32px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
```

### Qué tener en cuenta

- `justify-content: space-between` es la propiedad más importante del header. Separa logo y nav automáticamente.
- El header va pegado al tope sin margen. El reset `margin: 0` en body lo garantiza.
- Fondo oscuro → texto claro. Fondo claro → texto oscuro. Nunca texto gris claro sobre fondo blanco.
- Si el logo es un enlace, usa `<a>` con `text-decoration: none` y el color del logo en CSS.

---

## 4. El footer

La barra inferior de la página.

### Footer simple

```html
<footer>
  <p>© 2025 MiSitio. Todos los derechos reservados.</p>
</footer>
```

```css
footer {
  background-color: #111;
  color: #aaa;
  text-align: center;
  padding: 20px 32px;
  font-size: 13px;
}
```

### Footer con columnas

```html
<footer>
  <div class="footer-grid">
    <div class="col">
      <h4>MiSitio</h4>
      <p>Descripción breve de la empresa o proyecto.</p>
    </div>
    <div class="col">
      <h4>Enlaces</h4>
      <a href="#">Inicio</a>
      <a href="#">Servicios</a>
      <a href="#">Contacto</a>
    </div>
    <div class="col">
      <h4>Contacto</h4>
      <p>correo@misitio.com</p>
      <p>+57 300 000 0000</p>
    </div>
  </div>
  <div class="footer-bottom">
    <p>© 2025 MiSitio. Todos los derechos reservados.</p>
  </div>
</footer>
```

```css
footer {
  background-color: #111;
  color: #aaa;
  font-size: 14px;
  padding: 48px 32px 24px;
}

.footer-grid {
  display: flex;
  gap: 40px;
  margin-bottom: 32px;
}

.col {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.col h4 {
  color: white;
  font-size: 14px;
  margin-bottom: 4px;
}

.col a {
  color: #aaa;
  text-decoration: none;
  font-size: 13px;
}

.col a:hover { color: white; }

.footer-bottom {
  border-top: 1px solid #333;
  padding-top: 20px;
  text-align: center;
  font-size: 12px;
}
```

### Qué tener en cuenta

- El footer debe pegarse siempre al fondo aunque haya poco contenido. Se logra con `flex: 1` en el `<main>`.
- `padding: 48px 32px 24px` — más espacio arriba que abajo para que se vea balanceado.
- Los enlaces del footer casi siempre son del mismo color que el texto base (`#aaa`) y cambian a blanco en `:hover`.

---

## 5. Cómo encajan body + header + footer

Esta es la plantilla completa para cualquier página con las tres secciones.

```html
<body>
  <header>...</header>
  <main>...</main>
  <footer>...</footer>
</body>
```

```css
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f5f5f5;
  display: flex;
  flex-direction: column;
  min-height: 100vh;  /* el body ocupa toda la pantalla */
}

header {
  background: #111;
  padding: 16px 32px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

main {
  flex: 1;          /* crece y empuja el footer al fondo */
  padding: 40px 32px;
}

footer {
  background: #111;
  color: #aaa;
  text-align: center;
  padding: 20px 32px;
  font-size: 13px;
}
```

> **La clave:** `body` con `flex-direction: column` + `min-height: 100vh`, y `main` con `flex: 1`. Sin esto, el footer queda en la mitad de la pantalla cuando hay poco contenido.

---

## 6. Imagen al lado de texto (sin estar en el mismo div)

Este es uno de los casos más frecuentes en pruebas. Tienes dos elementos hermanos que quieres poner en fila, no dentro de uno al otro.

### Caso 1 — Imagen y texto como hermanos directos

```html
<section class="hero">
  <img src="foto.jpg" alt="Descripción">
  <div class="texto">
    <h2>Título principal</h2>
    <p>Descripción del contenido.</p>
    <button>Ver más</button>
  </div>
</section>
```

```css
.hero {
  display: flex;          /* pone los hijos en fila */
  align-items: center;    /* los centra verticalmente */
  gap: 48px;              /* espacio entre imagen y texto */
  padding: 60px 80px;
  background: white;
}

.hero img {
  width: 400px;           /* tamaño fijo de la imagen */
  height: 300px;
  object-fit: cover;      /* recorta la imagen para que llene el espacio */
  border-radius: 12px;
}

.texto {
  flex: 1;                /* el texto ocupa el resto del espacio disponible */
  display: flex;
  flex-direction: column;
  gap: 16px;
}
```

### Caso 2 — Imagen a la derecha, texto a la izquierda

Solo cambia el orden en el HTML o usa `flex-direction: row-reverse`:

```css
.hero {
  display: flex;
  flex-direction: row-reverse;  /* invierte el orden sin cambiar el HTML */
  align-items: center;
  gap: 48px;
  padding: 60px 80px;
}
```

### Caso 3 — Imagen circular al lado de un nombre (perfil)

```html
<div class="perfil">
  <img src="avatar.jpg" alt="Foto de perfil">
  <div class="info">
    <h3>Carlos Gómez</h3>
    <p>Desarrollador web</p>
  </div>
</div>
```

```css
.perfil {
  display: flex;
  align-items: center;
  gap: 16px;
}

.perfil img {
  width: 60px;
  height: 60px;
  border-radius: 50%;     /* hace la imagen circular */
  object-fit: cover;
}

.info h3 { font-size: 16px; color: #111; }
.info p  { font-size: 13px; color: #888; }
```

### Caso 4 — Imagen de fondo con texto encima

Cuando la imagen no está en el HTML sino como fondo CSS, y el texto va encima:

```html
<section class="hero-bg">
  <div class="contenido">
    <h1>Bienvenido</h1>
    <p>Texto sobre la imagen</p>
  </div>
</section>
```

```css
.hero-bg {
  background-image: url('imagen.jpg');
  background-size: cover;       /* la imagen cubre todo el elemento */
  background-position: center;  /* centra la imagen */
  min-height: 500px;
  display: flex;
  align-items: center;
  padding: 0 80px;
}

.hero-bg::before {             /* capa oscura semitransparente sobre la imagen */
  content: '';
  position: absolute;
  inset: 0;                    /* equivale a top:0 right:0 bottom:0 left:0 */
  background: rgba(0, 0, 0, 0.5);
}

.contenido {
  position: relative;          /* queda por encima del ::before */
  color: white;
}
```

### Qué tener en cuenta con imágenes

- `object-fit: cover` recorta la imagen para que llene el espacio sin deformarse. Úsalo siempre que la imagen tenga un tamaño fijo.
- `object-fit: contain` muestra la imagen completa dentro del espacio sin recortarla (puede dejar espacios vacíos a los lados).
- `border-radius: 50%` en una imagen la hace circular, pero solo funciona bien si la imagen es cuadrada (mismo ancho y alto).
- El atributo `alt` en `<img>` siempre debe describir la imagen. No lo omitas.
- Si no tienes imagen real, usa un div con `background-color` como placeholder.

```html
<!-- Placeholder de imagen sin archivo real -->
<div class="img-placeholder">Imagen del producto</div>
```

```css
.img-placeholder {
  width: 400px;
  height: 300px;
  background-color: #e0e7ff;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #6366f1;
  font-size: 14px;
  border-radius: 12px;
}
```

---

## 7. Casos particulares frecuentes

### Tarjeta con badge/etiqueta flotante

```html
<div class="card">
  <span class="badge">NUEVO</span>
  <h3>Título</h3>
  <p>Descripción</p>
</div>
```

```css
.card {
  position: relative;   /* ancla para el badge */
  background: white;
  border-radius: 12px;
  padding: 24px;
}

.badge {
  position: absolute;
  top: 12px;
  right: 12px;
  background: #dc2626;
  color: white;
  font-size: 11px;
  font-weight: 700;
  padding: 4px 10px;
  border-radius: 99px;
}
```

### Dos precios: tachado y rebajado

```html
<div class="precios">
  <span class="precio-original">$120.000</span>
  <span class="precio-rebajado">$89.900</span>
</div>
```

```css
.precios {
  display: flex;
  align-items: center;
  gap: 10px;
}

.precio-original {
  color: #aaa;
  text-decoration: line-through;
  font-size: 14px;
}

.precio-rebajado {
  color: #2563eb;
  font-size: 22px;
  font-weight: 700;
}
```

### Botón primario y botón secundario (outline) juntos

```html
<div class="botones">
  <a class="btn-primary" href="#">Empezar ahora</a>
  <a class="btn-secondary" href="#">Ver más</a>
</div>
```

```css
.botones {
  display: flex;
  gap: 14px;
}

.btn-primary {
  background: #2563eb;
  color: white;
  padding: 12px 28px;
  border-radius: 8px;
  text-decoration: none;
  font-size: 15px;
  font-weight: 600;
  border: 2px solid #2563eb;
}

.btn-secondary {
  background: transparent;
  color: #2563eb;
  padding: 12px 28px;
  border-radius: 8px;
  text-decoration: none;
  font-size: 15px;
  font-weight: 600;
  border: 2px solid #2563eb;
}
```

### Grid de tarjetas (3 en fila)

```html
<section class="grid">
  <div class="card">...</div>
  <div class="card">...</div>
  <div class="card">...</div>
</section>
```

```css
.grid {
  display: flex;
  gap: 24px;
  padding: 40px 32px;
}

.card {
  flex: 1;              /* cada tarjeta ocupa el mismo ancho */
  background: white;
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}
```

### Línea divisoria entre secciones

```css
.seccion {
  border-top: 1px solid #e5e5e5;
  padding-top: 32px;
  margin-top: 32px;
}
```

O como elemento HTML:

```html
<hr>
```

```css
hr {
  border: none;
  border-top: 1px solid #e5e5e5;
  margin: 32px 0;
}
```

### Texto que no se baja de línea (una sola línea)

```css
.titulo {
  white-space: nowrap;     /* el texto no baja de línea */
  overflow: hidden;        /* oculta lo que se salga */
  text-overflow: ellipsis; /* pone "..." al final si se corta */
}
```

### Elemento que ocupa todo el ancho disponible

```css
.boton-completo {
  width: 100%;
  display: block;          /* los <a> son inline por defecto, esto los hace bloque */
}
```

### Lista sin bullets (puntos)

```html
<ul class="lista">
  <li>Elemento uno</li>
  <li>Elemento dos</li>
</ul>
```

```css
.lista {
  list-style: none;     /* quita los bullets */
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
}
```

### Avatar con iniciales (sin imagen)

```html
<div class="avatar">CG</div>
```

```css
.avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: #dbeafe;
  color: #1d4ed8;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 15px;
}
```

### Contenido con ancho máximo centrado (contenedor principal)

Cuando el contenido no debe estirarse en pantallas grandes:

```html
<main>
  <div class="container">
    <!-- Todo el contenido aquí -->
  </div>
</main>
```

```css
.container {
  max-width: 1100px;     /* ancho máximo del contenido */
  margin: 0 auto;        /* centra el div horizontalmente */
  padding: 0 32px;       /* espacio en los lados en pantallas pequeñas */
}
```

### Sección hero de pantalla completa

```html
<section class="hero">
  <div class="hero-content">
    <h1>Título grande</h1>
    <p>Subtítulo descriptivo</p>
    <a href="#" class="btn">Llamada a la acción</a>
  </div>
</section>
```

```css
.hero {
  min-height: 100vh;
  background: #0f172a;
  display: flex;
  align-items: center;
  padding: 0 10%;
}

.hero-content {
  max-width: 600px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.hero h1 {
  color: white;
  font-size: 48px;
  line-height: 1.2;
}

.hero p {
  color: #94a3b8;
  font-size: 18px;
  line-height: 1.7;
}
```

### Menú de navegación vertical (sidebar)

```html
<aside class="sidebar">
  <nav>
    <a href="#" class="active">Dashboard</a>
    <a href="#">Perfil</a>
    <a href="#">Configuración</a>
    <a href="#">Cerrar sesión</a>
  </nav>
</aside>
```

```css
.sidebar {
  width: 220px;
  background: #111;
  min-height: 100vh;
  padding: 32px 16px;
}

.sidebar nav {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.sidebar nav a {
  color: #aaa;
  text-decoration: none;
  padding: 10px 16px;
  border-radius: 8px;
  font-size: 14px;
}

.sidebar nav a:hover {
  background: #1f1f1f;
  color: white;
}

.sidebar nav a.active {
  background: #2563eb;
  color: white;
}
```

---

## 8. Flexbox completo

El sistema de layout más importante. Resuelve el 80% de los diseños.

### Propiedades del contenedor (padre)

```css
.contenedor {
  display: flex;

  /* Dirección */
  flex-direction: row;         /* fila (por defecto) */
  flex-direction: column;      /* columna */
  flex-direction: row-reverse; /* fila invertida */

  /* Alineación en el eje principal */
  justify-content: flex-start;    /* al inicio */
  justify-content: flex-end;      /* al final */
  justify-content: center;        /* centrado */
  justify-content: space-between; /* primero al inicio, último al final */
  justify-content: space-around;  /* espacio igual alrededor de cada elemento */
  justify-content: space-evenly;  /* espacio exactamente igual entre todos */

  /* Alineación en el eje secundario */
  align-items: stretch;    /* estira (por defecto) */
  align-items: flex-start; /* arriba */
  align-items: flex-end;   /* abajo */
  align-items: center;     /* centrado */
  align-items: baseline;   /* alineados por la línea base del texto */

  /* Espacio entre hijos */
  gap: 24px;         /* mismo espacio en todos los lados */
  gap: 16px 32px;    /* 16px vertical, 32px horizontal */

  /* Si los hijos no caben, bajar a la siguiente línea */
  flex-wrap: wrap;
  flex-wrap: nowrap; /* (por defecto) no baja de línea nunca */
}
```

### Propiedades de los hijos

```css
.hijo {
  flex: 1;        /* ocupa todo el espacio disponible */
  flex: 0;        /* no crece ni se encoge */
  flex: 2;        /* ocupa el doble que un hijo con flex: 1 */

  align-self: center;     /* sobreescribe el align-items solo para este hijo */
  align-self: flex-end;

  order: 1;       /* cambia el orden visual sin cambiar el HTML */
}
```

---

## 9. CSS Grid completo

Grid es el sistema de layout en **dos dimensiones**: maneja filas Y columnas al mismo tiempo. Flexbox maneja una sola dirección (fila o columna). Usa Grid cuando el diseño tiene estructura de tabla o cuadrícula.

### Cuándo usar Grid vs Flexbox

| Situación | Usa |
|---|---|
| Elementos en una sola fila o columna | Flexbox |
| Tarjetas en filas y columnas a la vez | Grid |
| Navbar (logo + links) | Flexbox |
| Galería de imágenes | Grid |
| Layout de página completo (sidebar + contenido) | Grid |
| Botones alineados | Flexbox |

### Grid básico — columnas iguales

```html
<div class="grid">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
  <div class="item">4</div>
  <div class="item">5</div>
  <div class="item">6</div>
</div>
```

```css
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr; /* 3 columnas iguales */
  gap: 24px;                          /* espacio entre celdas */
}
```

> `1fr` = 1 fracción del espacio disponible. Si tienes `1fr 1fr 1fr`, cada columna ocupa 1/3 del ancho total.

### Forma corta con repeat()

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* igual que 1fr 1fr 1fr */
  gap: 24px;
}
```

### Columnas de ancho fijo y flexible mezcladas

```css
/* Sidebar fijo + contenido flexible */
.layout {
  display: grid;
  grid-template-columns: 250px 1fr;  /* sidebar 250px, contenido ocupa el resto */
  gap: 32px;
}

/* Imagen fija + texto flexible */
.card {
  display: grid;
  grid-template-columns: 200px 1fr;
  gap: 24px;
  align-items: center;
}
```

### Grid con filas definidas

```css
.layout {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: auto 1fr auto; /* header auto, contenido flexible, footer auto */
  min-height: 100vh;
}
```

### auto-fill y auto-fit — columnas responsivas automáticas

```css
/* Las columnas se crean solas según el ancho disponible */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  /* minmax(250px, 1fr): cada columna mide mínimo 250px y máximo 1fr */
  gap: 24px;
}
```

> Con `auto-fill`, si el contenedor tiene 800px y cada columna mide mínimo 250px, crea 3 columnas. Si el contenedor tiene 500px, crea 2. Las columnas se ajustan solas.

### Un elemento ocupa varias columnas

```css
.item-ancho {
  grid-column: span 2; /* este elemento ocupa 2 columnas */
}

.item-muy-ancho {
  grid-column: span 3; /* ocupa 3 columnas */
}

.item-alto {
  grid-row: span 2; /* ocupa 2 filas */
}
```

### Ubicar elementos en posiciones exactas

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(2, 200px);
}

/* Este elemento empieza en columna 1, termina en columna 3 */
.header-item {
  grid-column: 1 / 3;
}

/* Empieza en fila 1, termina en fila 3 */
.sidebar-item {
  grid-row: 1 / 3;
}
```

### Alineación en Grid

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);

  /* Alinea todos los items dentro de su celda */
  justify-items: center;  /* horizontal: start | end | center | stretch */
  align-items: center;    /* vertical:   start | end | center | stretch */

  /* Alinea el grid completo dentro del contenedor */
  justify-content: center;
  align-content: center;
}

/* Alinear un item individual */
.item {
  justify-self: end;
  align-self: start;
}
```

### Caso completo — galería de tarjetas

```html
<section class="galeria">
  <div class="card">Tarjeta 1</div>
  <div class="card">Tarjeta 2</div>
  <div class="card">Tarjeta 3</div>
  <div class="card">Tarjeta 4</div>
  <div class="card">Tarjeta 5</div>
  <div class="card">Tarjeta 6</div>
</section>
```

```css
.galeria {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  padding: 40px 32px;
}

.card {
  background: white;
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}
```

### Caso completo — layout de página con sidebar

```html
<div class="page-layout">
  <header class="top-bar">Header</header>
  <aside class="sidebar">Sidebar</aside>
  <main class="content">Contenido principal</main>
  <footer class="bottom-bar">Footer</footer>
</div>
```

```css
.page-layout {
  display: grid;
  grid-template-columns: 240px 1fr;
  grid-template-rows: 60px 1fr 60px;
  min-height: 100vh;
}

.top-bar {
  grid-column: 1 / 3;  /* el header ocupa ambas columnas */
  background: #111;
  color: white;
  display: flex;
  align-items: center;
  padding: 0 24px;
}

.sidebar {
  background: #1f2937;
  color: white;
  padding: 24px 16px;
}

.content {
  padding: 32px;
  background: #f5f5f5;
}

.bottom-bar {
  grid-column: 1 / 3;  /* el footer ocupa ambas columnas */
  background: #111;
  color: #aaa;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 13px;
}
```

---

## 10. Columnas con Grid y Flexbox

Hay varias formas de crear columnas según el caso. Esta sección cubre cuándo y cómo usar cada una.

### Columnas iguales con Flexbox

Usa cuando los elementos deben estar en una sola fila y distribuirse equitativamente.

```html
<div class="columnas">
  <div class="col">Columna 1</div>
  <div class="col">Columna 2</div>
  <div class="col">Columna 3</div>
</div>
```

```css
.columnas {
  display: flex;
  gap: 24px;
}

.col {
  flex: 1;  /* cada columna ocupa el mismo espacio */
}
```

### Columnas iguales con Grid

Usa cuando los elementos deben alinearse en filas Y columnas (cuadrícula).

```css
.columnas {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}
```

### Columnas de diferente ancho

```css
/* 2 columnas: una ocupa 2/3, la otra 1/3 */
.columnas {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 32px;
}

/* Equivalente con porcentajes */
.columnas {
  display: grid;
  grid-template-columns: 66% 33%;
  gap: 32px;
}

/* Sidebar fijo + contenido flexible */
.columnas {
  display: grid;
  grid-template-columns: 280px 1fr;
  gap: 32px;
}
```

### Columna centrada con ancho máximo

El patrón más común para secciones de contenido que no deben ser muy anchas.

```css
.seccion {
  max-width: 720px;
  margin: 0 auto;       /* centra horizontalmente */
  padding: 60px 32px;
}
```

### Dos columnas: imagen y texto (patrón muy frecuente)

```html
<section class="dos-columnas">
  <div class="col-imagen">
    <img src="foto.jpg" alt="Descripción">
  </div>
  <div class="col-texto">
    <h2>Título de la sección</h2>
    <p>Descripción del contenido.</p>
    <a href="#" class="btn">Ver más</a>
  </div>
</section>
```

```css
/* Con Flexbox */
.dos-columnas {
  display: flex;
  align-items: center;
  gap: 60px;
  padding: 60px 80px;
}

.col-imagen img {
  width: 440px;
  height: 320px;
  object-fit: cover;
  border-radius: 12px;
}

.col-texto {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

/* Con Grid */
.dos-columnas {
  display: grid;
  grid-template-columns: 440px 1fr;
  align-items: center;
  gap: 60px;
  padding: 60px 80px;
}
```

### Tres columnas de tarjetas (muy frecuente en pruebas)

```html
<section class="tarjetas">
  <div class="card">
    <h3>Servicio 1</h3>
    <p>Descripción del servicio.</p>
  </div>
  <div class="card">
    <h3>Servicio 2</h3>
    <p>Descripción del servicio.</p>
  </div>
  <div class="card">
    <h3>Servicio 3</h3>
    <p>Descripción del servicio.</p>
  </div>
</section>
```

```css
/* Con Grid (recomendado para tarjetas) */
.tarjetas {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  padding: 48px 32px;
}

.card {
  background: white;
  border-radius: 12px;
  padding: 28px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
  display: flex;
  flex-direction: column;
  gap: 12px;
}
```

### Cuatro columnas (features, estadísticas)

```css
.features {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
  padding: 48px 32px;
}
```

### Columnas que se adaptan al contenido (no al contenedor)

```css
/* Cada columna mide lo que necesita su contenido */
.columnas {
  display: flex;
  gap: 24px;
  justify-content: center;
}

/* Sin flex: 1, cada hijo ocupa solo lo que su contenido necesita */
```

### Tabla de referencia rápida de columnas

| Necesito... | Uso |
|---|---|
| 2 columnas iguales | `grid-template-columns: 1fr 1fr` |
| 3 columnas iguales | `grid-template-columns: repeat(3, 1fr)` |
| 4 columnas iguales | `grid-template-columns: repeat(4, 1fr)` |
| Sidebar 250px + contenido | `grid-template-columns: 250px 1fr` |
| Imagen 400px + texto | `grid-template-columns: 400px 1fr` |
| Columnas que llenan filas | `flex: 1` en cada hijo con `display: flex` en padre |
| Tarjetas responsivas | `repeat(auto-fill, minmax(250px, 1fr))` |
| Columna centrada limitada | `max-width: 720px; margin: 0 auto` |

---

## 11. Posicionamiento

### Los 4 valores de position

**`static`** — es el valor por defecto. El elemento sigue el flujo normal del documento. No acepta `top`, `right`, `bottom`, `left`.

**`relative`** — el elemento sigue en el flujo normal pero puede desplazarse con `top/right/bottom/left`. Su uso más importante es servir de ancla para hijos con `position: absolute`.

**`absolute`** — saca el elemento del flujo normal. Se ubica con coordenadas relativas al ancestro más cercano que tenga `position: relative`. Si ninguno lo tiene, se va al borde de la página.

**`fixed`** — igual que `absolute` pero relativo a la ventana del navegador. Se queda fijo al hacer scroll.

**`sticky`** — el elemento se comporta como `relative` hasta que el usuario llega a él al hacer scroll, entonces se queda fijo como `fixed`.

### Regla de oro

```
position: absolute SIEMPRE necesita un padre con position: relative
```

### Posiciones comunes

```css
/* Esquina superior derecha */
.elemento { position: absolute; top: 12px; right: 12px; }

/* Esquina superior izquierda */
.elemento { position: absolute; top: 12px; left: 12px; }

/* Esquina inferior derecha */
.elemento { position: absolute; bottom: 12px; right: 12px; }

/* Centrado horizontalmente */
.elemento { position: absolute; left: 50%; transform: translateX(-50%); }

/* Centrado completo (horizontal y vertical) */
.elemento {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

---

## 12. Tipografía

```css
.texto {
  font-family: Arial, sans-serif;
  font-size: 16px;           /* tamaño */
  font-weight: 400;          /* 400 = normal, 600 = semibold, 700 = bold */
  line-height: 1.6;          /* altura de línea (sin unidad = multiplicador) */
  color: #111;               /* color del texto */
  text-align: left;          /* left | center | right | justify */
  text-transform: uppercase; /* uppercase | lowercase | capitalize | none */
  text-decoration: none;     /* none | underline | line-through */
  text-underline-offset: 4px;/* distancia del subrayado al texto */
  letter-spacing: 1px;       /* espacio entre letras */
  white-space: nowrap;       /* no baja de línea */
}
```

### Tamaños de texto recomendados

| Uso | Tamaño |
|---|---|
| Titular hero | 40px – 56px |
| Título de sección (h2) | 28px – 36px |
| Título de tarjeta (h3) | 18px – 22px |
| Texto normal | 14px – 16px |
| Texto secundario / muted | 12px – 13px |
| Badge / etiqueta | 10px – 12px |

---

## 13. Colores y fondos

```css
.elemento {
  /* Colores de texto */
  color: #111;                    /* casi negro */
  color: #555;                    /* gris medio */
  color: #888;                    /* gris claro */
  color: #aaa;                    /* gris muy claro */
  color: white;
  color: rgba(0, 0, 0, 0.5);     /* negro al 50% de opacidad */

  /* Fondos sólidos */
  background-color: white;
  background-color: #f5f5f5;
  background-color: #111;

  /* Degradados */
  background: linear-gradient(180deg, #1e3a5f, #000); /* de arriba a abajo */
  background: linear-gradient(90deg, #1e3a5f, #000);  /* de izquierda a derecha */
  background: linear-gradient(135deg, #1e3a5f, #000); /* diagonal */

  /* Imagen de fondo */
  background-image: url('imagen.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}
```

### Colores más usados en pruebas

| Color | Hex | Uso típico |
|---|---|---|
| Azul primario | `#2563eb` | botones, enlaces activos |
| Rojo | `#dc2626` | botones de alerta, badges |
| Verde | `#16a34a` | botones de confirmación, éxito |
| Negro | `#111` | header, footer, texto principal |
| Gris claro | `#f5f5f5` | fondo de página |
| Gris medio | `#555` | texto de párrafos |
| Gris sutil | `#e5e5e5` | bordes y líneas separadoras |
| Blanco | `#ffffff` | fondo de tarjetas |

---

## 14. Bordes, sombras y esquinas

```css
.elemento {
  /* Bordes */
  border: 1px solid #ddd;               /* todos los lados */
  border-top: 1px solid #e5e5e5;        /* solo arriba */
  border-bottom: 1px solid #333;        /* solo abajo */
  border: none;                         /* sin borde */

  /* Esquinas redondeadas */
  border-radius: 8px;     /* leve */
  border-radius: 12px;    /* moderado (tarjetas) */
  border-radius: 16px;    /* pronunciado */
  border-radius: 50%;     /* círculo (imágenes, avatares) */
  border-radius: 99px;    /* píldora (badges, botones redondeados) */

  /* Sombras */
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);    /* sutil */
  box-shadow: 0 4px 16px rgba(0,0,0,0.15);  /* moderada */
  box-shadow: 0 8px 32px rgba(0,0,0,0.2);   /* pronunciada */
  box-shadow: none;                          /* sin sombra */
}
```

---

## 15. Formularios

### HTML completo

```html
<form>
  <h3>Contáctanos</h3>

  <div class="field">
    <label for="nombre">Nombre</label>
    <input type="text" id="nombre" placeholder="Tu nombre">
  </div>

  <div class="field">
    <label for="email">Email</label>
    <input type="email" id="email" placeholder="correo@ejemplo.com">
  </div>

  <div class="field">
    <label for="telefono">Teléfono</label>
    <input type="tel" id="telefono" placeholder="300 000 0000">
  </div>

  <div class="field">
    <label for="mensaje">Mensaje</label>
    <textarea id="mensaje" placeholder="Escribe tu mensaje..."></textarea>
  </div>

  <button type="submit">Enviar</button>
</form>
```

### CSS

```css
form {
  background: white;
  padding: 28px;
  border-radius: 12px;
  width: 340px;
}

.field {
  display: flex;
  flex-direction: column;
  gap: 6px;
  margin-bottom: 14px;
}

label {
  font-size: 13px;
  font-weight: 600;
  color: #444;
}

input,
textarea {
  border: 1px solid #ddd;
  border-radius: 6px;
  padding: 9px 12px;
  font-size: 14px;
  font-family: inherit;  /* IMPORTANTE: sin esto usan fuente distinta */
  outline: none;
}

input:focus,
textarea:focus {
  border-color: #2563eb;  /* siempre reemplaza outline con border-color */
}

textarea {
  resize: vertical;
  min-height: 90px;
}

button[type="submit"] {
  width: 100%;
  background: #2563eb;
  color: white;
  border: none;
  padding: 11px;
  border-radius: 8px;
  font-size: 14px;
  cursor: pointer;
}
```

### Tipos de input

| `type=""` | Para qué sirve |
|---|---|
| `text` | Texto libre |
| `email` | Valida formato de correo |
| `password` | Oculta el texto |
| `tel` | Teléfonos |
| `number` | Solo números |
| `date` | Selector de fecha |
| `checkbox` | Casilla de verificación |
| `radio` | Opción única entre varias |
| `file` | Subir archivos |

---

## 16. Todas las propiedades CSS explicadas

### Modelo de caja

| Propiedad | Qué hace |
|---|---|
| `box-sizing: border-box` | El padding y border se cuentan dentro del ancho, no se suman |
| `width` | Ancho fijo del elemento |
| `max-width` | Ancho máximo (el elemento puede ser más angosto) |
| `min-width` | Ancho mínimo |
| `height` | Alto fijo |
| `min-height` | Alto mínimo (el elemento puede crecer) |
| `margin` | Espacio exterior entre el elemento y sus vecinos |
| `margin: 0 auto` | Centra un elemento bloque horizontalmente |
| `padding` | Espacio interior entre el borde y el contenido |
| `overflow: hidden` | Oculta lo que se salga del contenedor |
| `overflow: auto` | Agrega scroll si el contenido se sale |

### Display

| Propiedad | Qué hace |
|---|---|
| `display: block` | Ocupa toda la fila, baja a la siguiente línea |
| `display: inline` | Solo ocupa lo que necesita, no acepta width/height |
| `display: inline-block` | Como inline pero acepta width/height |
| `display: flex` | Activa flexbox en el contenedor |
| `display: grid` | Activa CSS Grid en el contenedor |
| `display: none` | Oculta el elemento completamente |

### Flexbox

| Propiedad | Qué hace |
|---|---|
| `flex-direction: row` | Hijos en fila horizontal |
| `flex-direction: column` | Hijos en columna vertical |
| `justify-content` | Alinea en el eje principal |
| `align-items` | Alinea en el eje secundario |
| `gap` | Espacio entre hijos |
| `flex: 1` | El hijo ocupa todo el espacio disponible |
| `flex-wrap: wrap` | Los hijos bajan de línea si no caben |

### CSS Grid

| Propiedad | Qué hace |
|---|---|
| `grid-template-columns` | Define el número y ancho de las columnas |
| `grid-template-rows` | Define el número y alto de las filas |
| `repeat(3, 1fr)` | Crea 3 columnas iguales (forma corta) |
| `1fr` | Una fracción del espacio disponible |
| `auto` | La fila/columna mide lo que necesita su contenido |
| `minmax(250px, 1fr)` | Mínimo 250px, máximo 1fr |
| `auto-fill` | Crea tantas columnas como quepan |
| `gap` | Espacio entre filas y columnas |
| `grid-column: span 2` | El elemento ocupa 2 columnas |
| `grid-row: span 2` | El elemento ocupa 2 filas |
| `grid-column: 1 / -1` | El elemento ocupa todas las columnas |
| `justify-items` | Alinea horizontalmente el contenido de cada celda |
| `align-items` | Alinea verticalmente el contenido de cada celda |

### Tipografía

| Propiedad | Qué hace |
|---|---|
| `font-family` | Fuente del texto |
| `font-size` | Tamaño del texto |
| `font-weight` | Grosor (400 normal, 700 bold) |
| `line-height` | Altura de cada línea |
| `text-align` | Alineación horizontal del texto |
| `text-decoration` | Subrayado, tachado, ninguno |
| `text-transform` | Mayúsculas, minúsculas, capitalizar |
| `letter-spacing` | Espacio entre letras |
| `color` | Color del texto |

### Posicionamiento

| Propiedad | Qué hace |
|---|---|
| `position: relative` | Sirve de ancla para hijos absolutos |
| `position: absolute` | Se ubica relativo al padre relative |
| `position: fixed` | Se queda fijo al hacer scroll |
| `position: sticky` | Fijo al llegar al tope al hacer scroll |
| `top / right / bottom / left` | Coordenadas del elemento posicionado |
| `z-index` | Orden de capas (mayor = encima) |

### Bordes y decoración

| Propiedad | Qué hace |
|---|---|
| `border` | Borde completo (grosor estilo color) |
| `border-radius` | Esquinas redondeadas |
| `box-shadow` | Sombra del elemento |
| `outline: none` | Quita el anillo de foco del navegador |
| `cursor: pointer` | Cambia el cursor a mano |
| `opacity` | Transparencia del elemento (0 a 1) |

### Imágenes

| Propiedad | Qué hace |
|---|---|
| `object-fit: cover` | Recorta la imagen para llenar el espacio |
| `object-fit: contain` | Muestra la imagen completa sin recortar |
| `background-image` | Imagen de fondo |
| `background-size: cover` | La imagen de fondo cubre todo el elemento |
| `background-position: center` | Centra la imagen de fondo |

---

## 17. Todas las etiquetas HTML explicadas

### Estructura semántica

| Etiqueta | Para qué sirve |
|---|---|
| `<header>` | Encabezado de la página o sección |
| `<nav>` | Bloque de navegación con enlaces |
| `<main>` | Contenido principal de la página |
| `<section>` | Sección temática del documento |
| `<article>` | Contenido independiente (noticia, post) |
| `<aside>` | Contenido secundario (sidebar, panel lateral) |
| `<footer>` | Pie de página o sección |

### Contenedores genéricos

| Etiqueta | Para qué sirve |
|---|---|
| `<div>` | Contenedor de bloque sin significado semántico |
| `<span>` | Contenedor en línea sin significado semántico |

### Texto

| Etiqueta | Para qué sirve |
|---|---|
| `<h1>` al `<h6>` | Títulos jerárquicos (h1 = más importante) |
| `<p>` | Párrafo de texto |
| `<strong>` | Texto importante (negrita semántica) |
| `<em>` | Texto enfatizado (cursiva semántica) |
| `<small>` | Texto pequeño o secundario |
| `<br>` | Salto de línea |
| `<hr>` | Línea divisoria horizontal |

### Interactivos

| Etiqueta | Para qué sirve |
|---|---|
| `<a href="">` | Enlace. `href="#"` es enlace vacío |
| `<button>` | Botón interactivo |
| `<input type="">` | Campo de entrada de datos |
| `<textarea>` | Área de texto multilínea |
| `<label>` | Etiqueta descriptiva de un campo |
| `<form>` | Contenedor de formulario |

### Multimedia

| Etiqueta | Para qué sirve |
|---|---|
| `<img src="" alt="">` | Imagen. `alt` describe la imagen |
| `<video>` | Video |
| `<audio>` | Audio |

### Listas

| Etiqueta | Para qué sirve |
|---|---|
| `<ul>` | Lista sin orden (bullets) |
| `<ol>` | Lista ordenada (números) |
| `<li>` | Elemento de lista |

### En el `<head>`

| Etiqueta | Para qué sirve |
|---|---|
| `<meta charset="UTF-8">` | Codificación de caracteres (tildes y ñ) |
| `<meta name="viewport" ...>` | Hace la página responsiva en móvil |
| `<title>` | Título en la pestaña del navegador |
| `<link rel="stylesheet">` | Conecta el archivo CSS externo |

---

## 18. Decisiones rápidas para la prueba

| Lo que ves en el boceto | Lo que debes escribir |
|---|---|
| Elemento centrado en toda la pantalla | `body { display:flex; justify-content:center; align-items:center; min-height:100vh; }` |
| Elementos en fila horizontal | `display: flex` en el contenedor |
| Logo izquierda + nav derecha | `display:flex; justify-content:space-between` en header |
| Elementos apilados con espacio | `display:flex; flex-direction:column; gap:Xpx` |
| Imagen al lado de texto | `display:flex; gap:Xpx; align-items:center` en el contenedor padre |
| Etiqueta flotando en esquina | `position:relative` en padre + `position:absolute; top:X; right:X` en etiqueta |
| Texto tachado | `text-decoration: line-through` |
| Fondo degradado | `background: linear-gradient(135deg, color1, color2)` |
| Imagen circular | `border-radius: 50%; object-fit: cover` |
| Botón sin borde del navegador | `border: none` |
| Texto en mayúsculas | `text-transform: uppercase` |
| Campo resaltado al hacer clic | `input:focus { border-color: #2563eb; }` |
| Footer pegado al fondo | `body { display:flex; flex-direction:column; min-height:100vh; }` + `main { flex:1; }` |
| Contenido con ancho máximo | `.container { max-width: 1100px; margin: 0 auto; padding: 0 32px; }` |
| Enlace sin subrayado | `text-decoration: none` |
| Elemento que ocupa todo el ancho | `width: 100%` |
| 2 columnas iguales | `display:grid; grid-template-columns: 1fr 1fr` |
| 3 tarjetas en fila | `display:grid; grid-template-columns: repeat(3, 1fr); gap: 24px` |
| 4 columnas iguales | `display:grid; grid-template-columns: repeat(4, 1fr)` |
| Sidebar fijo + contenido | `display:grid; grid-template-columns: 250px 1fr` |
| Tarjetas responsivas automáticas | `grid-template-columns: repeat(auto-fill, minmax(250px, 1fr))` |
| Un elemento ocupa 2 columnas | `grid-column: span 2` en ese elemento |
| Header/footer que cruza todo el grid | `grid-column: 1 / -1` (de la primera a la última columna) |

---

## 19. Lista de verificación antes de entregar

```
ESTRUCTURA
□ <!DOCTYPE html> al inicio
□ <meta charset="UTF-8"> en el head
□ <link rel="stylesheet"> conectado correctamente
□ HTML semántico (header, main, footer donde corresponda)

CSS BASE
□ * { margin:0; padding:0; box-sizing:border-box; }
□ font-family definida en body
□ background-color definido en body

BOCETO RECREADO
□ Fondo de página correcto
□ Elemento principal centrado o posicionado correctamente
□ Colores de texto, fondos y botones similares al boceto
□ Tamaños de texto proporcionales
□ Esquinas redondeadas donde corresponda
□ Espacios internos (padding) similares al boceto
□ ¿Hay algo flotando (badge, etiqueta) que olvidaste?

IMÁGENES
□ object-fit: cover si la imagen tiene tamaño fijo
□ border-radius: 50% si debe ser circular
□ font-family: inherit en inputs y textarea

CAMBIOS SOLICITADOS
□ Cambio 1 aplicado y verificado en el navegador
□ Cambio 2 aplicado y verificado en el navegador
□ Los cambios no rompieron el diseño base

FOOTER
□ Pegado al fondo (main con flex:1 si hay poco contenido)
□ Color de texto legible sobre su fondo
□ Padding suficiente
```

---

*Guía preparada para prueba de desempeño HTML y CSS — 2025*
