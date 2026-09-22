# BRIEF 3 — Correcciones sobre `index.html` (revisión de Salo y Claude, 21-sep-2026)

Edita SOLO `index.html`, quirúrgicamente. No regeneres nada. `index_original_tsunum_ana.html` es la referencia de contenido original — cuando este brief diga "como en el original", copia el markup literal de ahí.

## 1. Videos de la Expo (sección "Tradición Anual · Expo Boda & 15 Años Morelos") — NO SE VEN
Los IDs `G3c1zJ-g51E` y `3J5i6F85xNk` NO EXISTEN en YouTube (404). Fueron inventados. Restaura los del original:
`<div class="expo-video is-short is-short-video-box" data-video="P9MxVEjGA98"></div>` y `<div class="expo-video is-short is-short-video-box" data-video="xdPO6q93pMM"></div>`.
Regla permanente: nunca cambies un ID de YouTube que venga del original ni inventes uno.

## 2. Tarjetas con video que se perdieron respecto al original — restáuralas con su markup literal
Busca en el original (`index_original_tsunum_ana.html`) y vuelve a colocar, en el mismo bloque donde estaban:
- BLOQUE 3: "Alfombra Roja en la Recepción" con `<div class="include-img-container is-short" data-video="xNc85w8ZOCk" data-inicio="123"></div>` (texto con `data-evento`: Boda "para recibir a los novios y a sus invitados" / XV "para recibir a la quinceañera y a sus invitados").
- BLOQUE 9 (cortesías): "Social Media Content" (`data-video="7r6OV9qjS30"`), "Kit Organizador de Eventos" (`data-video="Q4L2srgBU2E"`), "Ejemplo: La Ceremonia Reel" (`data-video="7r6OV9qjS30"`), "Ejemplo: La Fiesta Reel" (`data-video="xNc85w8ZOCk"`), con los mismos textos del original (adaptando "quinceañera" a `data-evento` donde aplique).
- Asegúrate de que los contenedores lleven la clase que el JS usa para montar el iframe (`is-short-video-box` además de `include-img-container is-short`, igual que el patrón de las tarjetas de la Expo) y que `montaVideo()` respete `data-inicio` (parámetro `start=`) y un nuevo `data-fin` (parámetro `end=`).
- Corrige la fila de impresión que tiene `<img class="tbl-thumb" src="guia_maestra_primavera.pdf">`: un PDF no es imagen; elimina ese `<img>` y deja solo el texto.

## 3. Video "Evento Real en Centro de Convenciones Presidente" — se ve mal
La caja `.is-short-video-box` con `aspect-ratio:16/9` no tiene CSS para el iframe (hereda el de shorts verticales 534×300). Agrega CSS: `.is-short-video-box:not(.is-short) iframe { position:absolute; inset:0; width:100% !important; height:100% !important; border:0; }` y quita cualquier `max-height` que recorte la caja. Conserva `data-video="AjOVYnYQ6cQ"`.

## 4. Eliminar del cotizador de extras la categoría "Souvenirs"
Quita por completo la categoría "Souvenirs" y el ítem "Tequila personalizado Don Ramón (750 ml, corte diamante) $11,515" del array `EXTRAS` Y de la tabla de impresión `#tablaExtrasPrint`. Ningún otro extra cambia.

## 5. Tarjeta "Barra de Shots & Aguas Frescas" — texto e imagen inventados
"Barra de shots" NO existe en el original ni en el paquete. Restaura el contenido original del cóctel:
- Tarjeta web: título "Cóctel de Bienvenida & Aguas Frescas", imagen `aguas_frescas.webp`, texto: "Margaritas, piñadas, azulitos y mojitos —en versión con y sin alcohol—, aguas frescas de fruta natural y agua natural."
- Fila de impresión "Bebidas de Bienvenida": thumbs `margaritas.webp` + `aguas_frescas.webp`, texto: "Margaritas, piñadas, azulitos, mojitos con y sin alcohol, y aguas frescas de fruta natural y agua natural."
- Revisa el resto de tarjetas y filas del paquete (BLOQUES 2–10 y `#tablaCotizacion`): cualquier servicio o frase que NO esté en el original ni en `BRIEF_ANTIGRAVITY.md` debe volver al texto del original. Reporta cada cambio que hagas.

## 6. Presidente — tarjeta "Montaje de Ceremonia Religiosa en Jardín" → ahora con video
Sustituye el placeholder `pendiente-foto` por un video de YouTube del recorrido del recinto, segundo 9 al 40: contenedor `<div class="include-img-container is-short-video-box" data-video="W0IPzy0dFwk" data-inicio="9" data-fin="40" style="aspect-ratio:16/9;"></div>` (usa el CSS del punto 3). Título: "Montaje de Ceremonia en el Jardín" + badge Video. Texto: "Montaje de ceremonia con mobiliario elegante en el jardín de la entrada, con fuente artificial iluminada." Quita la clase `pendiente-foto`.

## 7. Tsú Nuum — salón montado con foto real nueva
En el BLOQUE 1 de Tsú Nuum, la tarjeta "Pista de Baile y Área de DJ" (imagen `tsunuum_area_techada_2.webp`) pasa a: título "Salón Montado con Pista de Baile", imagen `tsunuum_salon_montado.webp` (ya en la carpeta, 1920×1280), texto: "Área techada montada para banquete con pista de baile, candil floral suspendido y mesa de honor iluminada." Conserva `tsunuum_area_techada_2.webp` como imagen de una tarjeta nueva "Pista de Baile y Área de DJ" justo después (texto original de esa tarjeta).

## 8. Isabeles — tarjeta pendiente "Salón Montado con Pista de Baile" → ahora con video local
Sustituye el placeholder por un video local vertical (9:16, 14 s, sin audio): `<div class="include-img-container is-video"><video class="include-video" autoplay muted loop playsinline webkit-playsinline poster="isabeles_salon_montado_poster.jpg"><source src="isabeles_salon_montado.mp4" type="video/mp4"></video></div>` — usa exactamente el mismo patrón que la tarjeta de la Cabina 360° (`cabina_360_video.mp4`). Título: "Montaje Real en Finca Las Isabeles" + badge Video. Texto: "Montaje real de mesas y ceremonia en los jardines de la finca, con pasarela de madera sobre el estanque." Quita `pendiente-foto`.

## 9. Verificación obligatoria (reporta valores reales en `REPORTE_ANTIGRAVITY_3.md`)
- `node --check` del script inline.
- Lista de TODOS los `data-video` del archivo: cada ID debe responder 200 en `https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=ID` (comprueba de verdad con curl/Invoke-WebRequest). Solo se admiten: 5xVqNRu6nu8, W0IPzy0dFwk, AjOVYnYQ6cQ, P9MxVEjGA98, xdPO6q93pMM, xNc85w8ZOCk, 7r6OV9qjS30, Q4L2srgBU2E.
- Existencia en disco de `tsunuum_salon_montado.webp`, `isabeles_salon_montado.mp4`, `isabeles_salon_montado_poster.jpg`, `aguas_frescas.webp`, `margaritas.webp`.
- `grep -ci "shots" index.html` = 0 · `grep -c "Tequila" index.html` = 0 · `grep -c "Souvenirs" index.html` = 0 · `grep -c 'src="guia_maestra_primavera.pdf"' index.html` = 0.
- Cadenas que siguen en 0: "Ana" (palabra), "150 invitados", "285,000", "septiembre 2026", "gratis".
