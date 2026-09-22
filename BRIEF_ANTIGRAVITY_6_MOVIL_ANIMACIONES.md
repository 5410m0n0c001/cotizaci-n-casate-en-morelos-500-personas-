# BRIEF 6 — Móvil: botones de recinto no pulsables + animaciones de scroll en todas las secciones

Edita SOLO `index.html`, quirúrgicamente. No toques contenido, precios ni textos.

## 1. Botones de recinto en móvil: 2 de 3 no se pueden pulsar
Diagnóstico medido a 375 px: la fila `.pills-venue` tiene `clientWidth 276px` y `scrollWidth 541px`; las pastillas
"Centro de Convenciones Presidente" (x 230→483) y "Finca Las Isabeles" (x 488→628) quedan fuera de la pantalla y el
usuario no descubre que hay que deslizar. Solución (solo `@media (max-width: 600px)`):
- La fila de recintos ocupa el 100% del ancho, SIN scroll horizontal: `display:flex; gap:6px;` y cada `.venue-pill` con
  `flex:1 1 0; min-width:0; padding:8px 4px; font-size:0.74rem; line-height:1.15; white-space:normal; text-align:center;`.
- Etiquetas cortas en móvil: envuelve el texto de cada pastilla en dos spans — `<span class="lbl-largo">Centro de Convenciones Presidente</span><span class="lbl-corto">Presidente</span>` (Tsú Nuum → "Tsú Nuum", Finca Las Isabeles → "Isabeles"); en ≥ 601px se muestra `.lbl-largo`, en móvil `.lbl-corto`.
- La etiqueta "RECINTO:" y el icono se ocultan en móvil (ya se entiende); "EVENTO:" también. El input de invitados conserva su label.
- Verifica con `document.elementFromPoint()` en el centro de cada una de las 5 pastillas (3 recintos + Boda + XV) a 375×812 y 360×780 que el elemento golpeado sea la propia pastilla, y que la barra siga midiendo ≤ 100px.

## 2. Animaciones al hacer scroll en TODAS las secciones (escritorio y móvil)
Hoy solo animan las tarjetas y algunos títulos; las secciones nuevas (barra comparativa, tarjetas de paquete oficial,
bloque A/B, datos del recinto, cotizador, precio, notas, contacto planners) aparecen sin animación, y en móvil la
sensación es que "nada se mueve". Objetivo: la misma experiencia del original de Tsú Nuum — todo va apareciendo con
fade-in + desplazamiento/escala al entrar en pantalla.
- Agrega la clase `reveal` (con variantes `reveal-left`, `reveal-right`, `reveal-zoom` alternadas para dar ritmo) a:
  todos los `h3.section-title`, todos los `.gallery-block-title`, los 6 `.include-item` que hoy no están envueltos en
  `<div class="reveal">`, la sección "Comparativo de los 3 Recintos" (título + tabla), cada tarjeta de "Paquete Oficial
  del Recinto", el bloque A/B de cortesías (cada columna por separado), `.venue-info-grid`, `.venue-logo-wrap`, la sección
  de precio (`.price-section` o equivalente) con `reveal-zoom`, el cotizador de extras (cada categoría), el resumen
  final, publicidad (cada tarjeta), Expo, Kit Planner, firma, notas/condiciones, CTA de WhatsApp y contacto planners.
  NO agregues `reveal` a la barra sticky, al preloader, al hero ni a elementos `solo-print`.
- Los elementos dentro de `.venue-block` deben animar cada vez que se cambia de recinto: al cambiar de pestaña, quita
  `active` a los `.reveal` del bloque que se muestra y vuelve a evaluarlos (o vuelve a llamar a `initReveals()` para ellos)
  para que entren animados.
- Robustez en móvil: además del `IntersectionObserver`, agrega un respaldo por scroll con `requestAnimationFrame`
  (como hace `cargaVideosYoutube`): en cada scroll/resize, cualquier `.reveal` con `getBoundingClientRect().top <
  innerHeight - 40` recibe `active`. Así nunca queda una sección invisible aunque el observador no dispare.
- Mantén las transiciones del original (0.6 s cubic-bezier, `transition-delay` escalonado en grids) y respeta
  `prefers-reduced-motion`. No uses librerías externas.
- Verificación: en headless a 375×812, tras entrar a la propuesta, cuenta `.reveal` totales y, después de hacer scroll
  hasta el final en pasos de 400px con esperas de 150 ms, cuenta los que tienen `active`: debe ser el 100%. Cuenta también
  cuántos `.reveal` NO tenían `active` justo al entrar (deben ser la mayoría: eso demuestra que sí animan al hacer scroll).

## 3. Verificación (`REPORTE_ANTIGRAVITY_6.md`)
- `node --check` del script inline.
- Mediciones del punto 1 (elementFromPoint por pastilla, altura de barra) y del punto 2 (conteos de reveal).
- Cadenas en 0: "Ana" (palabra), "150 invitados", "285,000", "septiembre 2026", "gratis", "shots", "Tequila".
