# BRIEF 7 — Nuevos precios por recinto + 2 recintos adicionales + móvil/animaciones (Brief 6)

Edita SOLO `index.html`, quirúrgicamente. Aplica TAMBIÉN todo `BRIEF_ANTIGRAVITY_6_MOVIL_ANIMACIONES.md` (léelo; es parte
de este trabajo). Orden sugerido: primero precios (parte A), luego recintos nuevos (parte B), luego Brief 6.

## A. Precios por persona (instrucción directa de Salo, 21-sep-2026) — SUSTITUYEN al precio único de $1,900

| Recinto | clave | Precio p/p | Total 500 invitados |
|---|---|---|---|
| Jardín Tsú Nuum | `tsunuum` | $1,000.00 MXN | $500,000.00 MXN |
| Centro de Convenciones Presidente | `presidente` | $850.00 MXN | $425,000.00 MXN |
| Finca Las Isabeles | `isabeles` | $1,000.00 MXN | $500,000.00 MXN |
| Jardín La Villa (nuevo) | `lavilla` | $1,000.00 MXN | $500,000.00 MXN |
| Jardín San Rafael (nuevo) | `sanrafael` | $1,000.00 MXN | $500,000.00 MXN |

Implementación:
- En el `<script>`: `var PRECIOS = { tsunuum:1000, presidente:850, isabeles:1000, lavilla:1000, sanrafael:1000 };` y elimina la constante única de $1,900. El precio por persona activo = `PRECIOS[venueActivo]`; `TOTAL_BASE = invitados × precioActivo`; total con extras = base + extras. Al cambiar de recinto o de número de invitados se recalculan TODOS los lugares: cajas resumen del encabezado, sección "Inversión Total", cotizador (`ctbBase`, `ctbPorPersona`, `ctbTotal`), resumen final, tabla de impresión (`pdfTotalPersona`, `pdfTotalEvento`), tabla comparativa (filas "Precio por persona" e "Inversión 500 invitados" — cada columna con su propio precio, no el mismo), mensajes de WhatsApp y texto de compartir.
- Busca y reemplaza TODOS los textos fijos: "$1,900.00", "$1,900", "$950,000.00", "$950,000", "1,900 p/p", "mismo precio por persona en los tres recintos", "Mismo precio y mismo paquete en los tres recintos", "al mismo precio por persona que en los otros dos recintos", "todo dentro de los $1,900.00 MXN por persona", "dentro de la inversión de $950,000.00 MXN". Donde se hable del precio, usa spans dinámicos (`<span class="pp-activo"></span>` y `<span class="total-activo"></span>`) que el JS rellena con el recinto activo. La frase de la sección de precio pasa a: "Precio por persona según recinto · <span class=invitados-activo>500</span> invitados". En las tarjetas de paquete oficial (Brief 5) las notas "en esta propuesta, $1,900.00 MXN por persona" pasan a "en esta propuesta, $1,000.00 MXN por persona" (Tsú Nuum, Isabeles) y "$850.00 MXN por persona" (Presidente); en el bloque A/B la intro dice "Todo está considerado dentro de la inversión de <span class=total-activo></span> (<span class=invitados-activo>500</span> invitados)".
- Meta description / OG: "desde $850 por persona" en lugar de $1,900.
- Verifica con grep que no quede ningún "1,900" ni "950,000" en el archivo (salvo que sea otro número legítimo, que no lo hay).

## B. Dos recintos nuevos SIN imágenes ni logo: Jardín La Villa y Jardín San Rafael
Reglas de Salo: "simplemente ponlos con datos, no hay imágenes, sin logo, solo el precio; clona los mismos servicios que
tienen Tsú Nuum e Isabeles, sin imágenes personalizadas, usando las de los servicios y amenidades (genéricas)".
- Agrega dos pastillas más al selector (5 en total): "Jardín La Villa" (corto móvil: "La Villa") y "Jardín San Rafael" (corto: "San Rafael"). Ajusta el CSS móvil del Brief 6 para 5 pastillas: dos filas de pastillas (3 + 2) con `flex-wrap:wrap`, cada una `flex:1 1 30%`; la barra puede medir hasta 125px en móvil.
- Clases nuevas: `venue-block venue-lavilla` / `venue-sanrafael` y `body.venue-active-lavilla` / `venue-active-sanrafael` en el mismo mecanismo de mostrar/ocultar. `localStorage` y `?venue=` aceptan las claves nuevas.
- Hero para estos dos: sin video ni foto. Fondo degradado de marca (`linear-gradient(135deg, #1F1F1F 0%, #3a2a30 60%, #F65C7A 140%)`) con el nombre del recinto en Playfair y el eyebrow "CÁSATE EN MORELOS PRESENTA"; sin botón "Ver Video del Recinto".
- `.venue-logo-wrap`: solo el nombre tipográfico (Playfair, 1.6rem) y la leyenda "Recinto asociado". Sin `<img>`.
- Datos del recinto (`venue-info-grid`):
  - Jardín La Villa: Ubicación "Morelos (dirección a confirmar con tu planner)" · Capacidad "500 invitados (montaje sujeto a confirmación)" · Estilo "Jardín de eventos" — marca los tres con `.pendiente-confirmar`.
  - Jardín San Rafael: Ubicación "Jiutepec, Morelos" · Capacidad "500 invitados" · Estilo "Jardín de eventos de gran capacidad" (capacidad marcada `.pendiente-confirmar`).
- BLOQUE 1 "Recinto y áreas": NO crees tarjetas con fotos de otro recinto ni placeholders; en su lugar un solo párrafo dentro del bloque: "Las fotografías y el recorrido de este recinto se comparten directamente con tu planner. Todos los servicios y amenidades que se muestran a continuación son los mismos que en los demás recintos."
- Tabla comparativa: 5 columnas (una por recinto). En escritorio, contenedor con `overflow-x:auto` y columnas de mínimo 190px; en móvil ya se muestra solo el recinto activo. Miniatura: para los dos nuevos, un cuadro con el degradado de marca y el nombre (sin foto).
- Sección "Paquete Oficial del Recinto vs. Esta Propuesta" (Brief 5): para estos dos NO hay paquete oficial publicado → muestra una sola tarjeta "Esta propuesta incluye" con la intro: "Este recinto no tiene un paquete publicado en el sitio de Primavera Events Group; la propuesta se integra con el mismo paquete completo de servicios y amenidades de los demás recintos, a $1,000.00 MXN por persona." y el bloque de cortesías con un solo grupo "Incluido en esta propuesta" = la unión de los grupos A y B de Tsú Nuum (misma redacción, sin la nota de hotel asociado). Igual en la versión PDF.
- Hospedaje (fila de impresión y comparativa): "Consultar con tu planner". Ceremonia en sitio: "Consultar con tu planner". Estacionamiento: "Consultar con tu planner". Horario: "10 hrs de presencia (1 hr ceremonia + 1 hr cóctel + 8 hrs de servicio)".
- Todo lo demás (BLOQUES 2–10, cotizador, cortesías genéricas, croquis "ejemplo del servicio", minuto a minuto, WhatsApp con el nombre del recinto) funciona igual que en Tsú Nuum, con las imágenes genéricas ya existentes. Tarjetas "Sanitarios": sin foto propia → mismo placeholder `pendiente-foto` que Tsú Nuum.

## C. Brief 6 completo (pastillas pulsables en móvil + animaciones de scroll en todas las secciones), adaptado a 5 recintos.

## D. Verificación (`REPORTE_ANTIGRAVITY_7.md`)
- `node --check`.
- `grep -c "1,900" index.html` = 0 · `grep -c "950,000" index.html` = 0 · "shots"/"Tequila"/"gratis"/"Ana"(palabra)/"150 invitados" = 0.
- En headless: para cada uno de los 5 recintos, al activarlo, `ctbPorPersona` y `ctbTotal` muestran el precio correcto de la tabla A con 500 invitados; con 550 invitados Presidente = $467,500.00 y los demás $550,000.00; la columna del comparativo muestra el precio de cada recinto.
- Mediciones del Brief 6 (elementFromPoint en las 5+2 pastillas a 375 px; conteo de `.reveal` activos tras scroll = 100%).
- Ningún `<img>` con foto de Tsú Nuum/Presidente/Isabeles dentro de `.venue-lavilla` ni `.venue-sanrafael`.
