# BRIEF 4 — Correcciones sobre `index.html` (pedidas por Salo, 21-sep-2026)

Edita SOLO `index.html`, quirúrgicamente. Mantén el mecanismo de video de YouTube con `data-video` + `data-inicio` + `data-fin` (ya implementado en el brief 3: iframe con `start=`/`end=`) y el CSS de la caja 16:9 (`.is-short-video-box:not(.is-short) iframe`).

## 1. Presidente — tarjeta "Área de Jardín y Lounge con Periqueras" con video 13–20 s
En el BLOQUE 1 de `venue-presidente`, sustituye la tarjeta "Área de Jardín" (imagen `presidente_14.webp`) por una tarjeta con video: `<div class="include-img-container is-short-video-box" data-video="W0IPzy0dFwk" data-inicio="13" data-fin="20" style="aspect-ratio:16/9;"></div>`. Título: "Área de Jardín · Lounge y Periqueras" + badge Video. Texto: "Jardín delantero con fuente artificial iluminada, donde se monta el cóctel de bienvenida con salas lounge, periqueras altas y sombrillas." Conserva `presidente_14.webp` en la tarjeta "Mesa de Honor en Jardín" si ya existe; si no, no la reutilices.

## 2. Presidente — estacionamiento con video 50–57 s
La tarjeta "Estacionamiento & Jardín" (imagen `presidente_07.webp`) pasa a: título "Estacionamiento Interno Vigilado" + badge Video, contenedor `<div class="include-img-container is-short-video-box" data-video="W0IPzy0dFwk" data-inicio="50" data-fin="57" style="aspect-ratio:16/9;"></div>`. Texto: "Estacionamiento privado interno y vigilado para 35 vehículos compactos." Elimina la referencia a `presidente_07.webp` en esa tarjeta (no la uses en otra).

## 3. Presidente — eliminar la tarjeta "Fachada Principal"
Elimina por completo la tarjeta "Fachada Principal" (imagen `presidente_01.webp`, texto "Fachada principal con logotipo del recinto y acceso ejecutivo"), incluyendo su `<div class="reveal ...">` envolvente. Si `presidente_01.webp` se usa como miniatura en la tabla comparativa, sustitúyela ahí por `presidente_03.webp` (salón montado con pista LED). Si se usa como poster/fallback del hero de Presidente, sustitúyela también por `presidente_03.webp`.

## 4. Botones flotantes — invertir posición de "compartir" y "redes sociales"
Hoy el botón de compartir queda encima de los iconos que despliega el botón de redes sociales y los tapa. Invierte el orden vertical de los dos botones dentro de `.floating-actions-container` (el de compartir arriba, el de redes abajo — o viceversa, lo que haga falta) de modo que los iconos desplegados de redes (Facebook, Instagram, TikTok, LinkedIn, YouTube) NO se superpongan con el botón de compartir. Verifica en el DOM que, con el menú de redes abierto, ningún icono comparta coordenadas con el botón de compartir (compara `getBoundingClientRect()`).

## 5. Verificación (reporta en `REPORTE_ANTIGRAVITY_4.md`)
- `node --check` del script inline.
- `grep -c "presidente_01.webp" index.html` = 0 · `grep -c "Fachada Principal" index.html` = 0.
- `grep -c 'data-inicio="13"' index.html` = 1 · `grep -c 'data-inicio="50"' index.html` = 1.
- Todos los `data-video` siguen dentro de la lista permitida: 5xVqNRu6nu8, W0IPzy0dFwk, AjOVYnYQ6cQ, P9MxVEjGA98, xdPO6q93pMM, xNc85w8ZOCk, 7r6OV9qjS30, Q4L2srgBU2E.
- Medición real de solapamiento de los botones flotantes (rectángulos).

## 6. (SUSTITUYE al punto 4) Botones flotantes: restaurar el bloque ORIGINAL completo
El bloque actual `.floating-actions-container` fue reescrito con URLs genéricas (`https://facebook.com`, `https://instagram.com`, `https://tiktok.com`) — eso es un error grave: son enlaces falsos. Además se agregó un botón flotante de WhatsApp ("Chatear con tu Planner") que NADIE pidió y no existe en el original.
Haz esto:
- Reemplaza TODO el `<div class="floating-actions-container">…</div>` por el bloque literal del original (`index_original_tsunum_ana.html`, líneas ~1776–1794): grupo de redes `#socialGroup` con las 5 URLs reales de PEG (Facebook `https://facebook.com/share/1GLd3Qt2Tj`, Instagram `https://instagram.com/primavera.events.group?igsh=Y2g4d3hvZW95dDc5`, TikTok `https://tiktok.com/@primavera_events_group?_r=1&_t=ZS-94uQ5m4lTyG`, LinkedIn `https://linkedin.com/in/richard-hernandez-3844ba3b9`, YouTube `https://www.youtube.com/@PrimaveraEventsGroup`), botón `#btnSocial` "Síguenos" y botón `#btnShare` "Compartir Propuesta". SIN botón de WhatsApp flotante.
- Restaura también el CSS original de `.floating-actions-container`, `.fab-group`, `.fab-menu`, `.fab-item`, `.fab-main`, `.fab-label`, `.fab-social`, `.fab-share` (cópialo del original) y el JS original de `btnSocial` (abre/cierra el menú) y `btnShare` (Web Share API con fallback a copiar enlace). El texto que se comparte debe decir "Propuesta para 500 invitados · [Boda/XV Años] en [recinto activo] · Cásate en Morelos × Primavera Events Group" y la URL actual.
- Orden/posición: para que el menú de redes desplegado NO quede debajo del botón de compartir, coloca el botón de compartir ARRIBA del grupo de redes (o el menú de redes desplegándose hacia la izquierda en horizontal). Verifica con `getBoundingClientRect()` que, con el menú abierto, ningún `.fab-item` se solape con `#btnShare`.

## 7. Optimización móvil (auditoría real a 375×812 y 390×844)
Revisa y corrige, midiendo con el DOM (no a ojo):
- Sin scroll horizontal: `document.documentElement.scrollWidth === innerWidth`.
- Barra sticky ≤ 110px de alto; el hero no debe medir más de 70vh en móvil y el H1 debe caber en ≤ 3 líneas (reduce `font-size` con `clamp()`).
- Tabla comparativa: en móvil, en lugar de 3 columnas apretadas, muestra SOLO la columna del recinto activo con un mini-selector encima (o una tarjeta por recinto apilada); la versión de 3 columnas se mantiene en ≥ 768px y en impresión.
- Tarjetas `.include-item`: una sola columna, imagen 16:9 o 4:3 completa (sin recortes raros), texto ≥ 0.85rem.
- Videos verticales (`.is-short`) centrados y sin desbordar; videos 16:9 al 100% de ancho.
- Sub-bloque Gobernador vs Presidente: en móvil, las dos columnas se apilan (una debajo de otra) con encabezado propio.
- Cotizador de extras: casillas y precios legibles, sin que el precio se corte; el resumen fijo (si lo hay) no debe tapar el contenido.
- Botones flotantes: no deben tapar el botón de WhatsApp de la sección de cierre ni el footer (agrega `padding-bottom` al footer en móvil si hace falta).
- Preloader: logo de Cásate en Morelos ≤ 70vw, todo el contenido visible sin scroll en 375×812.
Reporta cada medición (antes/después) en `REPORTE_ANTIGRAVITY_4.md`.
