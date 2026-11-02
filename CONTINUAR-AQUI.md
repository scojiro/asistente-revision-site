# CONTINUAR-AQUÍ — sitio asistente-revision-site

> Archivo de reanudación del SITIO (no de la app). Repo:
> `/home/casa/asistente-revision-site` · rama `main` · remoto
> `origin` = https://github.com/scojiro/asistente-revision-site ·
> publicado en https://scojiro.github.io/asistente-revision-site/
> Última actualización de este archivo: **2026-11-02 15:56 -03**.

## Estado: web v4 publicada — capturas, búsqueda, funciones finas y precio PENDIENTE

Publicado y verificado el 2026-11-02. `index.html` es una sola página
estática: HTML + CSS propios, **cero JavaScript**, cero frameworks, cero
fuentes web, cero CSS de terceros.

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

`git ls-remote origin refs/heads/main` = `14d792d1a4679edbe5972ca9c37eab19d6e79df6`
(igual a local). El commit de este archivo se agrega después; su hash va al
correo, no aquí.

### Qué hay en la página

- Sección **«Mírala en acción»** (`#capturas`): 9 capturas con pie de foto de
  una línea. Grilla 2 columnas en celular (147 px cada una a 390 px de ancho),
  3 desde 768 px, 4 desde 1200 px. Cada miniatura abre el WebP completo en
  pestaña nueva (`target="_blank" rel="noopener"`), sin JS.
  `loading="lazy"` en todas menos la primera (esa eager) y `decoding="async"`
  en todas; `width`/`height` reales en cada una. Enlace «Capturas» en el `nav`.
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

## Tarea futura (cuando la app sea pública en Google Play)

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
- Cero JavaScript, cero frameworks, cero fuentes web, cero CSS de terceros.
- **Prohibido publicar montos** mientras la app no sea pública.
- Capturas: solo las del dueño. Prohibido descargar de internet o retocar
  contenido (recortes sí, retoques no).
- Un commit por paso, push solo del ref `main`, verificación con `ls-remote`.
- El correo de `git commit` debe ser el noreply del repo
  (`331839933+scojiro@users.noreply.github.com`, ya configurado): con otro
  correo GitHub rechaza el push por privacidad.
