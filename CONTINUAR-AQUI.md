# CONTINUAR-AQUÍ — sitio asistente-revision-site

> Archivo de reanudación del SITIO (no de la app). Repo:
> `/home/casa/asistente-revision-site` · rama `main` · remoto
> `origin` = https://github.com/scojiro/asistente-revision-site ·
> publicado en https://scojiro.github.io/asistente-revision-site/
> Última actualización de este archivo: **2026-11-02 17:35 -03**.

## Estado: web v6 — piel de la v4 + modo nocturno (LOOK OFICIAL)

Publicada el 2026-11-02. **Decisión del dueño**: la v5 se descartó como piel
(«volver a la piel v4») y este es el look oficial. El `index.html` es otra vez
el de la v4 (banner verde con degradado, icono de caja, tarjetas blancas
redondeadas) con **una sola cosa encima**: el sistema de dos temas que la v5
dejó probado.

- Commit base restaurado: `c3ed6f9:index.html` (v4). El árbol volvió a la v4
  byte a byte antes de injertar nada (`md5 4279e8c6…`).
- Se agregó: `<meta name="color-scheme" content="light dark">`, el script
  anti-destello en `<head>` (antes del `<style>`), el bloque
  `html[data-tema="oscuro"]` con la paleta oscura, las reglas oscuras de los
  colores «duros» de la v4, el botón `#boton-tema` (44×44, fijo arriba a la
  derecha) con sus dos SVG, su script y el bloque
  `prefers-reduced-motion: reduce`.
- Los 3 colores en línea (`style="…color:#5c6f6a…"`) pasaron a
  `.meta` / `.meta.mt14` / `.meta.mtn6` con `color: var(--suave)`. Texto
  idéntico. Queda **un** `style="margin-top:14px"` en el `div.nota` (es
  espaciado, no color; estaba en la v4 y se dejó tal cual).

### Paleta oscura (la única novedad visual)

    html[data-tema="oscuro"] {
      --verde: #4dbfa0; --verde-oscuro: #8fd9c6; --fondo: #101a17;
      --texto: #e6efeb; --suave: #a3b5af; --borde: #24352f;
      --blanco: #182320; color-scheme: dark;
    }

Más los colores duros de la v4 llevados a oscuro: banner
`linear-gradient(145deg, #0b4f43, #062f28)`, `nav rgba(24,35,32,.96)`,
`nav a:hover #1d302b`, `.nota #152924/#cfe6dc`, `.dato #1b2a26`,
`.estado #152924/#8fd9c6`. El pie no se toca (`#10201d` ya era oscuro).

> **Trampa corregida (v6)**: la v4 hereda el color del texto del banner con
> `color: var(--blanco)`. Al redefinir `--blanco` como superficie oscura
> (`#182320`), el `h1` del banner quedaba casi negro sobre verde oscuro. Se
> agregó `color: #ffffff` al `header` solo en tema oscuro. Si alguna vez se
> cambia `--blanco`, revisar el banner.

### Verificación medida (2026-11-02 17:35 -03)

- `wc -c index.html` = **23.759 B** (< 40 KB; la v4 eran 19.336 B).
  `grep -c '<script'` = 2 · `boton-tema` = 6 · `data-tema` = 14 · un solo
  `<style>` · `loading="lazy"` = 8 · 9 capturas.
- Sin externos (`fonts.googleapis|fonts.gstatic|cdn.|https?://…(js|css)` →
  nada) y **sin montos** (`\$|CLP|USD|14.990|14990` → nada). «prontamente
  disponible» = 1. Presentes: 📦, «Funciones finas», `id="privacidad"`,
  el mailto y «1.9.5 (versionCode 20)».
- **Texto del cuerpo idéntico a la v4** (7.685 caracteres, comparación
  ignorando etiquetas): sin una sola diferencia.
- **`:root` idéntico a la v4**: los 7 valores son los mismos (`--verde
  #00695c`, `--verde-oscuro #004d40`, `--fondo #f5f8f7`, `--texto #1b2b28`,
  `--suave #526662`, `--borde #d6e2de`, `--blanco #ffffff`); la única línea
  agregada es `color-scheme: light`.
- **Diferencia de píxeles contra la v4** (Firefox headless, mismas capturas):
  - 390 px: 6.232 px distintos de 2.808.000 (**0,22 %**), en 4 bandas: el
    botón (y 14-58) y los 3 párrafos `.meta` (color `#5c6f6a` → `#526662`).
  - 1280 px: 6.254 px distintos de 7.936.000 (**0,08 %**), las mismas causas.
  - No hay ninguna otra diferencia: el resto es píxel a píxel la v4.
- Tema oscuro medido en el DOM: `body` fondo `rgb(16, 26, 23)`, texto
  `rgb(230, 239, 235)`; sección `rgb(24, 35, 32)`; `h2` y `nav a`
  `rgb(143, 217, 198)`; banner `rgb(11, 79, 67) → rgb(6, 47, 40)`; `.nota
  rgb(21, 41, 36)`; `.dato rgb(27, 42, 38)`; `.estado rgb(21, 41, 36)` +
  `rgb(143, 217, 198)`; pie `rgb(16, 32, 29)` (sin cambios).
- Arnés funcional: arranque sin preferencia → `data-tema=null`, fondo
  `rgb(245, 248, 247)`; clic → `oscuro`, `localStorage.tema="oscuro"`, sol
  visible; segundo clic → claro; documento nuevo con la preferencia guardada
  arranca en oscuro. 5 secciones, 9 capturas, 2 scripts, 4 enlaces de nav.
- Contraste WCAG (AA ≥ 4,5:1) en ambos temas: claro 13,81 / 14,76 (texto),
  5,72 / 6,11 (suave), 6,19 / 6,61 (verde), blanco sobre banner 6,61 y 9,83,
  párrafo del banner 5,51 y 8,01; oscuro 15,15 / 13,78, 8,28 / 7,53, 7,85 /
  7,13, blanco sobre banner 9,49 y 14,53, párrafo 7,76 y 11,52.
- Layout: 390 px → `scrollWidth` 378, galería 2 columnas (141 px), rejilla 1;
  768 → 756, 3 columnas; 1280 → 1.268, 4 columnas. El botón **no se superpone**
  al `h1`, al párrafo, al icono ni al `nav`: 0 px² de intersección a 390, 768
  y 1280 (el `h1` empieza en y=166 y el botón termina en y=58).
- W3C (`validator.w3.org/nu`, POST del archivo): **0 mensajes**.

### Desviación declarada (una)

- **No se aplicó `header { padding-right: 4.6rem }` en móvil** (lo pedía el
  PASO 2f). Medido: el botón va de y=14 a y=58 y el título empieza en y=166,
  así que no tapa nada, y el `padding` solo conseguía que el párrafo del
  banner ocupara una línea más y el banner creciera 28 px (rompiendo «el tema
  claro idéntico a la v4»). Si el dueño prefiere el hueco, es una línea:
  `@media (max-width: 700px) { header { padding-right: 4.6rem; } }`.
- Nota de instrumento: el `theme-color` cambia con el botón (`#00695c` /
  `#0b201d`), pero el script anti-destello no lo reescribe al cargar, así que
  en una recarga en oscuro la barra del navegador arranca en verde hasta el
  primer toque. Es el comportamiento del código entregado, no un fallo del
  CSS.

## Historial: web v5 (descartada como piel; su sistema de temas es el que usa la v6)

Publicada y luego **descartada por el dueño** (prefirió la piel de la v4).
Se conserva el commit `40bdd96` por si algún día se quiere retomar; de ahí se
reutilizaron los dos scripts del tema. **Solo piel**: mismo HTML de contenido,
mismas secciones, mismas 9 capturas, mismos textos. Cambió el CSS (inline, en un
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

1. Probar el botón de tema en su teléfono (luna/sol, elección guardada).
2. Aprobar la redacción del pie de la novena captura.
3. Decidir si quiere el hueco de 4,6 rem para el botón en móvil (ver
   «Desviación declarada» de la v6).

## Reglas para la próxima sesión

- Solo este repo. Nada de `revisor-cubetas`, builds, tags, AAB/APK; **nada de
  emulador ni adb** para las capturas: las aporta el dueño.
- JavaScript: **solo** los 2 scripts inline del botón de tema. Cero
  frameworks, cero fuentes web, cero CSS de terceros.
- **El look oficial es la piel de la v4 + el botón de tema** (v6). No
  reintroducir el sistema de diseño de la v5 sin autorización del dueño.
- **Prohibido publicar montos** mientras la app no sea pública.
- Capturas: solo las del dueño. Prohibido descargar de internet o retocar
  contenido (recortes sí, retoques no).
- Un commit por paso, push solo del ref `main`, verificación con `ls-remote`.
- El correo de `git commit` debe ser el noreply del repo
  (`331839933+scojiro@users.noreply.github.com`, ya configurado): con otro
  correo GitHub rechaza el push por privacidad.
