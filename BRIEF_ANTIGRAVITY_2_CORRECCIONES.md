# BRIEF 2 — Correcciones sobre `index.html` (revisión de Claude, 21-sep-2026)

Edita SOLO `index.html` (ya construido). No regeneres el archivo desde cero. No toques `index_original_tsunum_ana.html`.
Lee también `MATRIZ_IMAGENES_POR_VENUE.md` (regla de Salo: cada recinto con imágenes propias en lo que es del recinto; servicios genéricos comparten imagen).

Lo que YA está bien y no debes tocar: mecanismo de pestañas por venue (`.venue-block .venue-xxx` + `body.venue-active-xxx`), toggle Boda/XV (`.txt-evento`), contador de invitados, cotizador de extras y su tabla de impresión, tabla comparativa, sub-bloque Gobernador vs Presidente, mensajes de WhatsApp, condiciones de pago.

## 1. Logos de recinto (archivos nuevos ya en la carpeta)
- `.venue-logo-wrap.venue-tsunuum`: sustituye el nombre tipográfico por `<img src="logo_tsu_nuum.png" alt="Jardín Tsú Nuum">` (PNG transparente 478×293; mostrar alto máx. 120px, `object-fit:contain`), enlazado a https://primaveraeventsgroup.com/jardin-tsu-nuum/ y con la leyenda "Recinto Oficial Asociado".
- `.venue-logo-wrap.venue-isabeles`: igual con `<img src="logo_finca_las_isabeles.png" alt="Finca Las Isabeles">` (PNG transparente 198×199; alto máx. 140px), enlazado a https://primaveraeventsgroup.com/finca-las-isabeles/.
- En la tabla comparativa, fila "Foto miniatura": debajo de la foto de cada recinto agrega su logo pequeño (alto 40px; Presidente sobre fondo negro redondeado).

## 2. Logo Cásate en Morelos en el preloader, header de impresión y footer
- Usa `logo_casate_en_morelos_recorte.png` (880×330, ya recortado al corazón + texto) en lugar de `logo_casate_en_morelos.jpg`.
- Preloader: muéstralo SIN recorte circular ni borde: `width:min(260px,70vw); height:auto; border-radius:0; border:none; object-fit:contain; background:transparent`. Debajo, la palabra "presenta" (0.7rem, oro, letter-spacing 3px) y luego el logo de Primavera Events Group como está.
- Header de impresión y footer: mismo archivo recortado, alto 34–40px, sin recorte circular.

## 3. Croquis interactivo por recinto (sección "Croquis Interactivo 2D y 3D")
Envuelve el contenido en tres variantes `.venue-block`:
- `venue-presidente`: en lugar del video, un botón grande estilo `.btn-enter` con texto "Abrir el croquis interactivo 2D/3D del Centro de Convenciones Presidente" que abre en nueva pestaña https://5410m0n0c001.github.io/centro-de-convenciones-presidente-croquis/ (planificador real del recinto). Debajo, en 0.8rem: "Herramienta desarrollada por Primavera Events Group para este recinto: distribuye mesas, stands y mobiliario sobre el plano real."
- `venue-isabeles`: conserva el video `croquis_interactivo.mp4/.webm` con la leyenda "Croquis real de Finca Las Isabeles".
- `venue-tsunuum`: conserva el mismo video con la leyenda "Ejemplo del servicio de croquis interactivo (el de tu recinto se diseña a medida al contratar)".

## 4. Fila "Hospedaje" de la tabla de impresión (`#tablaCotizacion`)
Reemplaza la fila única por tres filas, cada una con clase `venue-block venue-xxx` (para que solo se imprima la del recinto activo):
- tsunuum: thumb `hospedaje_habitacion.png` · "Hospedaje sujeto a disponibilidad; se confirma con tu planner al apartar."
- presidente: sin thumb · "No disponible en el recinto. Convenios especiales con hoteles de Cuernavaca (a 5–10 min)."
- isabeles: thumb `finca_hospedaje.webp` · "Cabañas ecológicas rústicas y suite nupcial, previa reserva y costo adicional."
En las tres, columnas Cantidad/P. Unitario/Total = "—" / "Según recinto" / "Según recinto".

## 5. Tarjeta "Sanitarios y Limpieza General" (BLOQUE 6) → propia por recinto
Convierte esa tarjeta en tres variantes `.venue-block`:
- presidente: `presidente_12.webp` — "Baños múltiples de lujo para damas y caballeros, con personal de limpieza durante todo el evento."
- tsunuum e isabeles: tarjeta con clase adicional `pendiente-foto`, sin `<img>`: en el contenedor de imagen pon fondo `#EFE7E1`, ícono `<i class="fas fa-restroom"></i>` grande y la leyenda "Foto del recinto por integrar" (0.72rem). Texto: "Sanitarios del recinto con personal de limpieza durante todo el evento."

## 6. Tarjetas nuevas con foto pendiente (usar el mismo patrón `pendiente-foto` del punto 5)
- En BLOQUE 1 de **presidente**, agrega: "Montaje de Ceremonia Religiosa en Jardín" (ícono `fa-church`) — "Montaje de ceremonia con mobiliario elegante en el jardín de la entrada, con fuente artificial iluminada." y "Área de Cocina Profesional" (ícono `fa-kitchen-set`) — "Cocina amplia adaptada para banquetes masivos."
- En BLOQUE 1 de **isabeles**, agrega: "Salón Montado con Pista de Baile" (ícono `fa-champagne-glasses`) — "Área techada montada para banquete y pista de baile."
- No agregues tarjetas nuevas a tsunuum.

## 7. Barra sticky en móvil (hoy mide 290px de alto en 375px de ancho — demasiado)
En `@media (max-width: 600px)`: la barra debe medir como máximo 110px. Logra esto con: pestañas de recinto en una sola fila con scroll horizontal (`overflow-x:auto; white-space:nowrap; -webkit-overflow-scrolling:touch`), pills más compactas (padding 6px 12px, 0.78rem), toggle de evento + input de invitados en una segunda fila compacta, y oculta la línea "Proyección al mismo precio…" (pásala al atributo `title` del input). Verifica midiendo `getBoundingClientRect().height` del `.controls-sticky-bar` a 375px.

## 8. Verificación final (obligatoria, reporta resultados reales)
- Los dos scripts deben pasar `node --check` (extrae el `<script>` inline a un archivo temporal y ejecútalo).
- Confirma con el sistema de archivos que existen: `logo_tsu_nuum.png`, `logo_finca_las_isabeles.png`, `logo_casate_en_morelos_recorte.png`, `presidente_12.webp`, `finca_hospedaje.webp`, `hospedaje_habitacion.png`.
- Cadenas que deben seguir en 0: "Ana" (palabra), "150 invitados", "285,000", "314,850", "septiembre 2026", "gratis".
- Escribe `REPORTE_ANTIGRAVITY_2.md` con lo hecho, la altura medida de la barra móvil y cualquier pendiente.
