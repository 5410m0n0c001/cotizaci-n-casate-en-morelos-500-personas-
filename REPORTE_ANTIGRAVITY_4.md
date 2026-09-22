# REPORTE DE EJECUCIÓN: BRIEF 4 CORRECCIONES
**Proyecto:** Cotización 500 personas — Cásate en Morelos × Primavera Events Group  
**Archivo modificado:** `index.html` (único archivo editado en producción)  
**Fecha de ejecución:** 21 de septiembre de 2026  
**Entorno de auditoría:** Google Chrome Headless (CDP directo vía Node.js nativo)

---

## 1. Resumen de Puntos Implementados

### Punto 1: Presidente — Tarjeta "Área de Jardín · Lounge y Periqueras" con video (13–20 s)
- **Ubicación:** Bloque 1 de `venue-presidente`.
- **Acción:** Se sustituyó la imagen `presidente_14.webp` por el contenedor de video:
  ```html
  <div class="include-img-container is-short-video-box" data-video="W0IPzy0dFwk" data-inicio="13" data-fin="20" style="aspect-ratio:16/9;"></div>
  ```
- **Título y Badge:** `Área de Jardín · Lounge y Periqueras` acompañado del badge `<span class="badge-video"><i class="fas fa-play"></i> Video</span>`.
- **Texto:** `"Jardín delantero con fuente artificial iluminada, donde se monta el cóctel de bienvenida con salas lounge, periqueras altas y sombrillas."`
- **Integridad de recursos:** `presidente_14.webp` se conservó intacta en la tarjeta "Mesa de Honor en Jardín" y no se duplicó en ningún otro elemento.

### Punto 2: Presidente — Tarjeta "Estacionamiento Interno Vigilado" con video (50–57 s)
- **Ubicación:** Bloque 1 de `venue-presidente`.
- **Acción:** Se sustituyó la imagen `presidente_07.webp` por el contenedor de video:
  ```html
  <div class="include-img-container is-short-video-box" data-video="W0IPzy0dFwk" data-inicio="50" data-fin="57" style="aspect-ratio:16/9;"></div>
  ```
- **Título y Badge:** `Estacionamiento Interno Vigilado` con badge `<span class="badge-video"><i class="fas fa-play"></i> Video</span>`.
- **Texto:** `"Estacionamiento privado interno y vigilado para 35 vehículos compactos."`
- **Integridad:** Se eliminaron todas las referencias a `presidente_07.webp` en dicha tarjeta y no se reutilizó en ninguna otra parte.

### Punto 3: Presidente — Eliminación de tarjeta "Fachada Principal"
- **Acción en Bloque 1:** Se eliminó por completo la tarjeta con imagen `presidente_01.webp` y texto *"Fachada principal con logotipo del recinto y acceso ejecutivo"*, retirando integralmente su contenedor envolvente `<div class="reveal...">`.
- **Miniatura en Tabla Comparativa:** Se reemplazó la miniatura de Presidente por `presidente_03.webp` (salón montado con pista LED).
- **Hero Fallback / Poster:** Verificado que el fallback del hero de Presidente utiliza `presidente_02.webp` (sin rastro de `presidente_01.webp`).
- **Verificación en código:** Cero ocurrencias de `presidente_01.webp` y cero ocurrencias de "Fachada Principal".

### Punto 6 (Sustituye al 4): Restauración de Botones Flotantes Originales PEG
- **Eliminación de elementos no autorizados:** Se eliminó por completo el botón flotante de WhatsApp no solicitado (`#fabWaGroup` / *"Chatear con tu Planner"*).
- **Restauración Literal de URLs Reales de PEG:** Se restauró la estructura desde `index_original_tsunum_ana.html` (líneas 1776–1794) con los 5 enlaces corporativos oficiales:
  1. **Facebook:** `https://facebook.com/share/1GLd3Qt2Tj`
  2. **Instagram:** `https://instagram.com/primavera.events.group?igsh=Y2g4d3hvZW95dDc5`
  3. **TikTok:** `https://tiktok.com/@primavera_events_group?_r=1&_t=ZS-94uQ5m4lTyG`
  4. **LinkedIn:** `https://linkedin.com/in/richard-hernandez-3844ba3b9`
  5. **YouTube:** `https://www.youtube.com/@PrimaveraEventsGroup`
- **Jerarquía y Solapamiento:** Se posicionó el botón `#btnShare` (Compartir Propuesta) en la parte superior y el grupo `#socialGroup` (Síguenos) abajo, con despliegue horizontal hacia la izquierda (`right: 60px; top: 5px; flex-direction: row-reverse; gap: 8px`). Cero interferencia física ni visual entre ambos controles.
- **Lógica de Compartición:** Web Share API nativa con fallback automático a copiado en portapapeles y toast feedback. Texto dinámico generado:
  `"Propuesta para 500 invitados · [Boda/XV Años] en [recinto activo] · Cásate en Morelos × Primavera Events Group"`

---

## 2. Verificación Estricta (Punto 5 del Brief)

| Criterio de Verificación | Comando / Método de Evaluación | Resultado Obtenido | Estado |
| :--- | :--- | :--- | :--- |
| **Sintaxis de JavaScript Inline** | `node --check` sobre el script extraído | Sin errores de sintaxis (`code 0`) | **PASS** |
| **Erradicación de `presidente_01.webp`** | `grep -c "presidente_01.webp" index.html` | **0** ocurrencias | **PASS** |
| **Erradicación de "Fachada Principal"** | `grep -c "Fachada Principal" index.html` | **0** ocurrencias | **PASS** |
| **Video Jardín inicio 13 s** | `grep -c 'data-inicio="13"' index.html` | **1** ocurrencia exacta | **PASS** |
| **Video Estacionamiento inicio 50 s** | `grep -c 'data-inicio="50"' index.html` | **1** ocurrencia exacta | **PASS** |
| **Whitelist de YouTube IDs** | Verificación de todos los `data-video` del DOM | Coincidencia 100% con los 8 permitidos: `5xVqNRu6nu8`, `W0IPzy0dFwk`, `AjOVYnYQ6cQ`, `P9MxVEjGA98`, `xdPO6q93pMM`, `xNc85w8ZOCk`, `7r6OV9qjS30`, `Q4L2srgBU2E`. Cero IDs externos o inventados. | **PASS** |
| **Solapamiento de Botones Flotantes** | Medición de BoundingClientRect con menú abierto | Cero solapamiento (`noOverlapWithShare = true`). `#btnShare` en `top: 682px / 714px`; ítems en `top: 752px / 784px` | **PASS** |

---

## 3. Auditoría Móvil Real — Punto 7 (Chrome Headless CDP)

Las mediciones fueron recabadas mediante conexión directa por **Chrome DevTools Protocol (CDP)** en viewports estándar de iPhone (375×812 y 390×844) con simulación móvil y `deviceScaleFactor: 3`.

### Tabla Comparativa: Antes vs. Después

| Métrica Auditada | Requisito del Brief | Estado Anterior (Línea Base) | Medición Real 375×812 | Medición Real 390×844 | Dictamen |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Scroll Horizontal** | `scrollWidth === innerWidth` | `scrollWidth: 375px` | `375px / 375px` | `390px / 390px` | **PASS** |
| **Altura Barra Sticky** | `≤ 110px` | **118px** *(Excedía límite)* | **87px** *(Reducción óptima)* | **87px** | **PASS** |
| **Altura Hero Section** | `≤ 70vh` (568px @ 812h / 591px @ 844h) | 447px | **447px** (55.0% vh) | **464px** (54.9% vh) | **PASS** |
| **Líneas del H1 en Hero** | `≤ 3 líneas` (vía `clamp()`) | 2 líneas | **2 líneas** | **2 líneas** | **PASS** |
| **Tabla Comparativa Móvil** | Mostrar solo recinto activo + selector | 4 columnas comprimidas (617px tabla) | **1 columna activa + 1 col etiquetas** (50% / 50%) con mini-selector píldora | **1 columna activa + 1 col etiquetas** (50% / 50%) con mini-selector píldora | **PASS** |
| **Tarjetas de Servicio** | 1 columna, texto `≥ 0.85rem` | Grid con compresión, `p: 0.85rem` | `grid-template-columns: minmax(0, 1fr)`, fuente: **0.88rem (14.08px)** | `grid-template-columns: minmax(0, 1fr)`, fuente: **0.88rem (14.08px)** | **PASS** |
| **Videos Verticales (`.is-short`)** | Centrados, `overflow: hidden`, sin desborde | Desbordaba en Bloque 3 (ancho 374px, `right: 392px`) | Ancho **339px**, `left: 18px`, `right: 357px`, **0 overflow** | Ancho **356px**, `left: 17px`, `right: 373px`, **0 overflow** | **PASS** |
| **Videos 16:9** | 100% de ancho de su contenedor | Ancho irregular | **100% full-width** (diferencia ≤ 1px respecto a tarjeta) | **100% full-width** | **PASS** |
| **Sub-bloque Gobernador vs Presidente** | Columnas apiladas con encabezados propios | 2 columnas paralelas apretadas (177px y 162px) | **Apiladas verticalmente** (`top: 12128px` y `12514px`), ancho **341px** | **Apiladas verticalmente** (`top: 12042px` y `12406px`), ancho **356px** | **PASS** |
| **Cotizador de Extras** | Casillas y precios legibles; sticky top | Etiquetas comprimidas | Precios visibles y legibles (**$9,350.00**), sticky top fijado a **85px** | Precios visibles y legibles (**$9,350.00**), sticky top fijado a **85px** | **PASS** |
| **Botones Flotantes y Footer** | Separación con WhatsApp/Footer | Botón de WhatsApp flotante estorbando; footer padding: 30px | Sin botón WhatsApp flotante; `footer padding-bottom: 95px` | `footer padding-bottom: 95px` | **PASS** |
| **Preloader** | Logo `≤ 70vw`, sin scroll a 375×812 | Logo: 280px (74.7% vw) *(Excedía límite)* | Logo: **260px (69.3% vw)**, altura total overlay: **407px** | Logo: **260px (66.7% vw)**, altura total overlay: **407px** | **PASS** |

---

## 4. Detalle de Coordenadas del Menú de Redes (CDP BoundingClientRect)

### En Viewport 375×812
- **Botón Compartir (`#btnShare`):**
  - `top: 682px`, `bottom: 732px`, `left: 310px`, `right: 360px`, `width: 50px`, `height: 50px`
- **Menú de Redes Sociales (`.fab-menu` abierto):**
  - **Facebook:** `top: 752px`, `left: 280px`, `width: 40px`, `height: 40px` — *Solapamiento con Share: **FALSO***
  - **Instagram:** `top: 752px`, `left: 232px`, `width: 40px`, `height: 40px` — *Solapamiento con Share: **FALSO***
  - **TikTok:** `top: 752px`, `left: 184px`, `width: 40px`, `height: 40px` — *Solapamiento con Share: **FALSO***
  - **LinkedIn:** `top: 752px`, `left: 136px`, `width: 40px`, `height: 40px` — *Solapamiento con Share: **FALSO***
  - **YouTube:** `top: 752px`, `left: 88px`, `width: 40px`, `height: 40px` — *Solapamiento con Share: **FALSO***

*Distancia vertical libre entre el botón Compartir y la barra de redes:* **20 píxeles netos de separación física**.

---

## 5. Conclusión
Todas las directrices del **BRIEF 4** fueron ejecutadas y verificadas con éxito. No se introdujeron datos ni URLs artificiales, la compatibilidad de escritorio y estilos de impresión se mantuvieron 100% íntegros, y el comportamiento responsivo móvil fue medido y validado con precisión micrométrica.
