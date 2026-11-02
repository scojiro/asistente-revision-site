# CONTINUAR-AQUÍ — sitio asistente-revision-site

> Archivo de reanudación del SITIO (no de la app). Repo:
> `/home/casa/asistente-revision-site` · rama `main` · remoto
> `origin` = https://github.com/scojiro/asistente-revision-site ·
> publicado en https://scojiro.github.io/asistente-revision-site/
> Última actualización de este archivo: **2026-11-02 17:00 -03**.

## Estado: web v5 — dos temas (claro/oscuro) y sistema de diseño

Publicada el 2026-11-02. **Solo piel**: mismo HTML de contenido, mismas
secciones, mismas 9 capturas, mismos textos. Cambió el CSS (inline, en un
solo `<style>`), se agregó el **botón redondo de tema** (arriba a la derecha,
luna/sol) y los **2 únicos scripts inline** que lo hacen funcionar.

### Sistema de diseño aplicado (valores exactos)

- Paleta por variables CSS, dos juegos: claro (`--fondo #fbfbf8`,
  `--verde #0e7a4f`, `--alterna #f3f7f3`) y oscuro
  (`html[data-tema="oscuro"]`: `--fondo #101815`, `--verde #45c98d`).
  Ningún componente usa colores sueltos: solo `var(--…)`.
- Tipografía del sistema (cero fuentes web): h1 `clamp(1.9rem, 5vw, 2.6rem)`,
  h2 `clamp(1.4rem, 3.5vw, 1.8rem)`, cuerpo 1 rem, leyendas 0.9 rem, párrafos
  con `max-width: 65ch`.
- Contenedor 1080 px: `header/section/footer` usan
  `padding-inline: max(clamp(1rem,4vw,2rem), calc(50% - 540px + clamp(1rem,4vw,2rem)))`,
  así el contenido queda alineado a 1080 px sin envoltorios extra en el HTML.
- Secciones a sangre con `padding-block clamp(3rem, 8vw, 5rem)` y alternancia
  de fondo (`section:nth-of-type(even)` → `--alterna`), sin líneas duras.
- Tarjetas de captura: superficie, borde 1 px, radio 14 px, padding .6 rem,
  sombra `0 1px 2px rgba(0,0,0,.06)`; imagen con radio 10 px; hover real
  (`@media (hover:hover) and (pointer:fine)`) con `translateY(-2px)` y sombra
  `0 6px 16px rgba(0,0,0,.10)`, transición 180 ms ease-out.
- `:focus-visible` con contorno verde de 2 px en todo lo interactivo; zonas
  táctiles ≥ 44 px medidas.
- `@media (prefers-reduced-motion: reduce)` anula transiciones y el scroll
  suave.
- Botón de tema: 44×44 px, `position: fixed; top .9rem; right .9rem`, radio
  999 px, borde 1 px, fondo superficie, icono `currentColor` de 20 px; la luna
  se ve en claro y el sol en oscuro solo con CSS (sin JS extra).

### Los 2 scripts (los únicos del sitio)

1. En `<head>`, **antes** del `<style>`: lee `localStorage['tema']`; si no hay
   elección usa `prefers-color-scheme`; si toca oscuro pone
   `data-tema="oscuro"` en `<html>` antes de pintar (evita el destello).
2. Antes de `</body>`: alterna `data-tema` y guarda `claro`/`oscuro` en
   `localStorage`. `try/catch` en ambos (si `localStorage` está bloqueado, la
   página sigue en claro).

Sin `src`, sin librerías, sin `${`, sin frameworks, sin fuentes web.

### Verificación medida (2026-11-02 17:00 -03)

- `wc -c index.html` = **24.873 B** (< 40 KB). Las 9 capturas WebP no se
  tocaron: mismos nombres y mismos md5 que en v4.
- `grep -c '<script'` = **2**; `boton-tema` = 6; `data-tema` = 7; un solo
  `<style>`; `loading="lazy"` = 8 (igual que v4).
- `grep -nE 'fonts.googleapis|fonts.gstatic|cdn\.|https?://[^"]*\.(js|css)'`
  → **sin resultados**. `grep -nE '\$|CLP|USD|14\.990|14990'` → **sin
  resultados**. `prontamente disponible` = 1; `Funciones finas` = 1;
  `1.9.5` = 1; `id="privacidad"` = 1; `mailto:scojiro+mesa-ayuda@gmail.com` = 1.
- Texto del cuerpo comparado con el de `HEAD` (quitando etiquetas): **idéntico**
  salvo el emoji 📦 del héroe (decorativo, `aria-hidden`, se retiró por la
  regla «sin iconos emoji»).
- Navegador real (Firefox headless) sobre copia local servida por HTTP:
  - 390 px → `scrollWidth` 378 (sin desborde), galería 2 columnas
    (tarjeta 167 px), rejilla 1 columna, 9/9 imágenes (720×1409, la novena
    720×1410).
  - 768 px → galería 3 columnas (221 px), rejilla 3 columnas, 9/9.
  - 1280 px → galería 4 columnas (237 px), rejilla 3 columnas, 9/9.
  - Botón de tema 44×44; enlace de contacto 291×44; ningún objetivo táctil
    menor de 44 px en el `nav`.
- Funcional (arnés same-origin con iframes): sin preferencia arranca claro
  (`fondo rgb(251,251,248)`, luna visible); un clic → `data-tema="oscuro"`,
  `localStorage.tema="oscuro"`, fondo `rgb(16,24,21)`, sol visible; otro clic
  → claro; un documento nuevo con la preferencia guardada **arranca ya en
  oscuro** (anti-destello). Estructura contada en el DOM: 5 secciones, 9
  capturas, 2 scripts, 4 enlaces de `nav`.
- Contraste WCAG de los pares principales: claro 14,43:1 (texto/fondo) y
  5,45:1 (texto suave); verde sobre fondo 5,17:1; oscuro 15,4:1 y 7,93:1;
  verde oscuro sobre fondo 8,59:1. Todos ≥ 4,5:1.
- Validador del W3C (`validator.w3.org/nu`, POST del archivo): **0 mensajes**.

> Nota de instrumento: el «9/9 imágenes cargadas» se midió sobre una **copia
> de QA sin `loading="lazy"`** (el archivo publicado conserva el lazy de v4,
> 8 de 9). El headless de Firefox no completa la carga diferida de una página
> larga dentro del mismo `load`, así que contar `naturalWidth` ahí daría un
> falso negativo; la copia de QA solo elimina el atributo, nada más.

### Desviaciones declaradas (y por qué)

1. **No se agregaron «kickers»** (la etiqueta pequeña sobre cada título de
   sección que describe el sistema de diseño). Habría exigido **texto nuevo**
   en el HTML; manda la regla dura «no cambiar textos / solo piel». El estilo
   queda definido en la lista de componentes por si el dueño autoriza el texto.
2. **Se retiró el emoji 📦 del héroe** (era decorativo y `aria-hidden`): el
   sistema prohíbe iconos emoji y deja como únicos iconos los 2 SVG del botón.
3. Los tres párrafos que traían color en línea (`style="…color:#5c6f6a…"`) y
   el `margin-top` en línea de la nota pasaron a la clase `.meta` / al CSS,
   para que ningún color quede fuera de las variables. El texto no cambió.

## Historial: web v4 publicada (capturas, búsqueda, funciones finas, precio pendiente)

Publicado y verificado el 2026-11-02 (estado **histórico**: la v5 lo
reemplazó). `index.html` era una sola página estática: HTML + CSS propios,
**cero JavaScript** (hasta la v5), cero frameworks, cero fuentes web, cero CSS
de terceros.

> **El precio quedó PENDIENTE A PROPÓSITO.** La app está en prueba cerrada y
> no es pública: la web no muestra ningún monto (ni `$`, ni `CLP`, ni cifras).
> El único texto sobre dinero es el bloque de la sección «Precio y
> disponibilidad» con «prontamente disponible». Cuando la app salga a
> producción hay que reemplazar ese bloque por el monto real y agregar el
> enlace a la ficha de Google Play (ver «Tarea futura»).

Commits (rama `main`, con el correo noreply del repo):

| hash | mensaje |
|------|---------|
| `99f2c06` | web: novena captura del dueno (despliegue automatico real) en lugar de la del emulador |
| `14d792d` | web v4: precio pendiente sin montos y pie de la novena captura |

(Historial anterior: `de820eb` capturas WebP · `726faa9` web v2 · `689b6fd`
docs.)

`git ls-remote origin refs/heads/main` valía
`14d792d1a4679edbe5972ca9c37eab19d6e79df6` **al cierre de la v4** (hoy la rama
va más adelante: verificar con `ls-remote`, no fiarse de este párrafo). El
commit de este archivo se agrega después; su hash va al correo, no aquí.

### Qué hay en la página

- Sección **«Mírala en acción»** (`#capturas`): 9 capturas con pie de foto de
  una línea. Grilla 2 columnas en celular (147 px cada una a 390 px de ancho),
  3 desde 768 px, 4 desde 1200 px. Cada miniatura abre el WebP completo en
  pestaña nueva (`target="_blank" rel="noopener"`), sin JS.
  `loading="lazy"` en todas menos la primera (esa eager) y `decoding="async"`
  en todas; `width`/`height` reales en cada una. Enlace «Capturas» en el `nav`.
  (Las 147 px por tarjeta eran con el CSS de la v4; con el de la v5 son 167 px
  a 390 px de ancho, misma grilla de 2/3/4 columnas.)
- Bullet de búsqueda en «En ambas tareas»: «Consulta al instante: teclea el
  código o la descripción y aparece la ficha con su precio, sin escanear.»
- Subsección **«Funciones finas»**: precio corregido y recordado, alta de
  producto con su código de barra, alias, lectura óptica con barra dañada,
  modo claro y oscuro.
- Sección **«Precio y disponibilidad»** (`#precio`) antes de Contacto, con
  etiqueta «Prueba cerrada» y este bloque: «La app está en prueba cerrada.
  Llegará a Google Play prontamente. Pago único. Sin suscripción, sin
  publicidad. Precio: prontamente disponible — se verá en la ficha de la app
  en Google Play.» + requisitos Android 7.0 · ~24 MB · sin internet ni permisos
  de red.
- Política de privacidad: intacta, sección de la misma página (`#privacidad`),
  misma URL.
- Línea de versión 1.9.5 y footer: intactos.

### Capturas

8 JPG del zip del dueño (`~/Descargas/capturas-play-asistente-revision.zip`,
1080 × 2113) y la **novena aportada por el dueño**:
`~/Descargas/1000089072.jpg` (817 × 1600, 97.456 B), copiada sin retoque y
convertida a WebP. La captura del emulador de la ronda anterior **quedó
reemplazada** por esta.

| archivo | origen | WebP publicado | dimensiones |
|---------|-------:|---------------:|-------------|
| 1-detalle-cubeta | 350.724 B | 40.234 B | 720 × 1409 |
| 2-escaneo | 565.217 B | 47.718 B | 720 × 1409 |
| 3-detalle-sector | 313.814 B | 35.982 B | 720 × 1409 |
| 4-items-sector | 291.765 B | 32.780 B | 720 × 1409 |
| 5-inicio-cubetas | 362.775 B | 39.382 B | 720 × 1409 |
| 6-inicio-inventario | 351.380 B | 38.628 B | 720 × 1409 |
| 7-historial-cubetas | 303.990 B | 33.840 B | 720 × 1409 |
| 8-extra-nueva-cubeta | 260.565 B | 26.446 B | 720 × 1409 |
| 9-despliegue-automatico | 97.456 B (dueño) | 47.364 B | 720 × 1410 |

Total WebP: **373.374 B**; HTML 19.336 B; página completa ≈ 392 KB. Todas bajo
150 KB con `quality=78` (Pillow, `method=6`, LANCZOS; el host no tiene
`cwebp`). Ninguna se agrandó: la novena mide 817 px y se bajó a 720.
sha256 de la novena: `6b83d5c6fecad6dc8d7b6256a2ef76c59a01c201c3aaf7c82196e6434434dcd3`.

### Verificación medida (2026-11-02 15:56 -03)

- `grep -nE '\$|CLP|USD|14\.990|14990' index.html` → **sin resultados**.
  `grep -c 'prontamente disponible' index.html` → **1**.
- `grep -c '<script'` = **0**; 9 `<img>`; `loading="lazy"` = 8 (9 − la primera).
- Markup: parser de Python, sin etiquetas sin cerrar ni desbalanceadas.
- Publicado: 200; el HTML servido tiene el mismo md5 que el local
  (`4279e8c66b0e9903fd9ede999ad6a73d`); las 9 capturas responden 200 con el
  mismo peso byte a byte; presentes «prontamente disponible», «Funciones
  finas», «Consulta al instante», `id="capturas"`, `id="precio"`,
  `id="privacidad"` y «1.9.5 (versionCode 20)».
- Render con navegador real sobre la URL publicada: a 390 px → 2 columnas
  (147 px), `scrollWidth` 390 (sin desborde) y **9/9 imágenes cargadas**
  (`naturalWidth` 720 × 1409/1410); a 1280 px → 4 columnas y 9/9 cargadas.

> Nota de instrumento: el Brave de flatpak con `--headless=new --screenshot`
> carga de forma intermitente las imágenes de una página larga (en varias
> corridas aparecieron entre 2 y 7 de 9), así que ese método **no sirve** para
> verificar la grilla; la verificación válida se hizo con el navegador real
> sobre la URL publicada, contando `document.images` con `naturalWidth > 0`.

## Tarea futura (cuando la app sea pública en Google Play) — SIGUE VIGENTE

1. Reemplazar el bloque «prontamente disponible» de `#precio` por el monto
   real (pago único) y **agregar el enlace a la ficha** de Google Play.
2. Quitar la etiqueta «Prueba cerrada» y la frase «Llegará a Google Play
   prontamente».
3. Actualizar este archivo y el correo de cierre.

## Pendientes del dueño

1. Revisar la página en su teléfono y en el computador antes de difundirla.
2. Aprobar la redacción del pie de la novena captura.

## Reglas para la próxima sesión

- Solo este repo. Nada de `revisor-cubetas`, builds, tags, AAB/APK; **nada de
  emulador ni adb** para las capturas: las aporta el dueño.
- JavaScript: **solo** los 2 scripts inline del botón de tema (PASO 2 de la v5).
  Cero frameworks, cero fuentes web, cero CSS de terceros.
- **Prohibido publicar montos** mientras la app no sea pública.
- Capturas: solo las del dueño. Prohibido descargar de internet o retocar
  contenido (recortes sí, retoques no).
- Un commit por paso, push solo del ref `main`, verificación con `ls-remote`.
- El correo de `git commit` debe ser el noreply del repo
  (`331839933+scojiro@users.noreply.github.com`, ya configurado): con otro
  correo GitHub rechaza el push por privacidad.
