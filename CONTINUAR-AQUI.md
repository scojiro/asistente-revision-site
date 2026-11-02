# CONTINUAR-AQUÍ — sitio asistente-revision-site

> Archivo de reanudación del SITIO (no de la app). Repo:
> `/home/casa/asistente-revision-site` · rama `main` · remoto
> `origin` = https://github.com/scojiro/asistente-revision-site ·
> publicado en https://scojiro.github.io/asistente-revision-site/
> Última actualización de este archivo: **2026-11-02 15:21 -03**.

## Estado: web v2 publicada (capturas + búsqueda + funciones finas + precio)

Publicado y verificado el 2026-11-02. `index.html` es una sola página
estática: HTML + CSS propios, **cero JavaScript**, cero frameworks, cero
fuentes web, cero CSS de terceros.

Commits (rama `main`, ambos con el correo noreply del repo):

| hash | mensaje |
|------|---------|
| `de820eb` | web: capturas WebP optimizadas (8 de Play + despliegue automatico desde el emulador) |
| `726faa9` | web v2: seccion Miralo en accion, busqueda al instante, funciones finas y precio |

`git ls-remote origin refs/heads/main` = `726faa948db24b4a8fc002e88f0e2ae3423d1eb7`
(igual a local).

### Qué se agregó (sin tocar lo existente)

- Sección **«Mírala en acción»** (`#capturas`), después de las 3 secciones de
  funciones: grilla de 9 capturas con pie de foto de una línea cada una.
  Enlace en el `nav` («Capturas»).
- Bullet de búsqueda en «En ambas tareas»: «Consulta al instante: teclea el
  código o la descripción y aparece la ficha con su precio, sin escanear.»
- Subsección **«Funciones finas»** (5 bullets: precio recordado, alta de
  producto con su código de barra, alias, lectura óptica con barra dañada,
  modo claro/oscuro).
- Sección **«Precio y disponibilidad»** (`#precio`), antes de Contacto:
  $14.990 pago único, sin suscripción ni publicidad, «Próximamente en Google
  Play» (sin enlace todavía) y requisitos Android 7.0 · ~24 MB · sin red.
- CSS: `.galeria` 2 columnas (móvil) → 3 desde 768 px → 4 desde 1200 px,
  bordes redondeados y sombra mínima; `.precio` y `.requisitos`.
- `width`/`height` en las 9 imágenes; `loading="lazy"` en 7 (las 2 primeras
  van eager); `decoding="async"` en todas; cada miniatura abre el WebP a
  tamaño completo en pestaña nueva (`target="_blank" rel="noopener"`), sin JS.

El `git show --stat` del commit de HTML es **133 inserciones y 0 borrados**:
no se modificó ni una línea previa (subtítulo, 3 secciones, características,
texto de la política, contacto, línea 1.9.5 y footer intactos).

### Capturas: 8 del dueño + 1 del emulador

Las 8 JPG salieron del zip del dueño
`~/Descargas/capturas-play-asistente-revision.zip` (1080 × 2113), extraídas a
un directorio de trabajo fuera del repo. Conversión con Pillow (`quality=78`,
`method=6`, ancho 720, alto proporcional; LANCZOS) — el host no tiene `cwebp`.

| archivo | JPG origen | WebP publicado | dimensiones |
|---------|-----------:|---------------:|-------------|
| 1-detalle-cubeta | 350.724 B | 40.234 B | 720 × 1409 |
| 2-escaneo | 565.217 B | 47.718 B | 720 × 1409 |
| 3-detalle-sector | 313.814 B | 35.982 B | 720 × 1409 |
| 4-items-sector | 291.765 B | 32.780 B | 720 × 1409 |
| 5-inicio-cubetas | 362.775 B | 39.382 B | 720 × 1409 |
| 6-inicio-inventario | 351.380 B | 38.628 B | 720 × 1409 |
| 7-historial-cubetas | 303.990 B | 33.840 B | 720 × 1409 |
| 8-extra-nueva-cubeta | 260.565 B | 26.446 B | 720 × 1409 |
| 9-despliegue-automatico | PNG 124.483 B | 30.772 B | 720 × 1239 |

Total WebP: **325.782 B** (todas por debajo de 150 KB; ninguna necesitó bajar
de `-q 78`). Página completa: HTML 19.065 B + 9 capturas = ~345 KB; primera
carga (HTML + las 2 eager) ~107 KB.

**La novena captura (`9-despliegue-automatico`) se hizo en el AVD
`cleanphone-api36` (emulator-5554) con la release v1.9.5**, no en el teléfono
del dueño. Método real y declarado: el host **no tiene webcam** (`/dev/video*`
no existe), así que no se pudo leer por cámara; las 3 lecturas se hicieron por
el ingreso manual de la app («⌨ Manual»), que pasa por el MISMO
`EscaneoViewModel.registrar(..., expandirAlRegistrar = true)`
(`EscaneoViewModel.kt:160` y `:297`), es decir el mismo camino que dispara el
despliegue automático. Los códigos usados son del maestro real
(7800007124326 PARACETAMOL 500MG 16COMP ×2 y 7800007771278 IBUPROFENO
400MG 20COMP ×1). Cubeta: CUBETA9021 (3 cajas, 2 productos, $1.880).
Recorte: solo las barras del sistema (arriba 123 px de status bar, abajo
132 px de taskbar; insets medidos con `dumpsys window displays`), sin ningún
otro retoque. El área de cámara muestra la **escena virtual del emulador**
(no hay cámara física), y se ve tal cual.

Si el dueño prefiere una foto real de esa pantalla, basta reemplazar
`capturas/9-despliegue-automatico.webp` (mismo nombre, 720 px de ancho) y
ajustar `width`/`height` del `<img>` en `index.html` si cambia la proporción.

### Verificación medida (2026-11-02 15:19 -03)

- `curl` a la URL publicada: **200**; `md5sum` del HTML servido
  (`475ff4ce5a2285c1a78b1a855b63c183`) **idéntico** al local; 19.065 B.
- Texto presente en lo publicado: «Consulta al instante», «Funciones finas»,
  «$14.990», «Mírala en acción», `id="capturas"`, `id="precio"`,
  `id="privacidad"`, «1.9.5 (versionCode 20)».
- Las 9 capturas responden **200** en
  `https://scojiro.github.io/asistente-revision-site/capturas/<nombre>.webp`,
  con el mismo peso byte a byte que en el repo.
- Render real con Brave headless (flatpak, `--headless=new`, perfil aparte):
  móvil 390 px → 2 columnas con pies parejos; escritorio 1280 px → 4 columnas.
  Sin desbordes ni saltos.
- `grep -c '<script'` = **0**.

## Pendientes del dueño

1. Revisar la página en su teléfono y en el computador antes de difundirla.
2. Decidir si la novena captura se queda la del emulador o la reemplaza una
   foto real (ver arriba).
3. Cuando la app esté en producción: agregar el enlace a Google Play en
   «Precio y disponibilidad» y quitar «Próximamente».
4. La política de privacidad sigue siendo una sección de esta misma página
   (`#privacidad`), misma URL; su texto no se tocó.

## Reglas para la próxima sesión

- Solo este repo. Nada de `revisor-cubetas`, builds, tags, AAB/APK.
- Cero JavaScript, cero frameworks, cero fuentes web, cero CSS de terceros.
- Capturas: solo las del dueño + las que se generen en el emulador y se
  declaren como tales. Prohibido descargar de internet o maquillar contenido
  (recortes sí, retoques no).
- Un commit por paso, mensaje claro, push solo del ref `main`, verificación
  con `ls-remote`.
- El correo de `git commit` debe ser el noreply del repo
  (`331839933+scojiro@users.noreply.github.com`, ya configurado en el repo):
  con otro correo GitHub rechaza el push por privacidad.
