# REPORTE DE EJECUCIÓN ANTIGRAVITY 2
## Correcciones Quirúrgicas sobre `index.html`
**Fecha de ejecución:** 21 de septiembre de 2026  
**Documentos base:** `BRIEF_ANTIGRAVITY_2_CORRECCIONES.md` y `MATRIZ_IMAGENES_POR_VENUE.md`  
**Archivo intervenido:** `index.html` (edición quirúrgica sin regeneración)  
**Archivo original resguardado:** `index_original_tsunum_ana.html` (intacto, 211,665 bytes)  

---

## 1. Resumen de Puntos Aplicados

### Punto 1: Logos de recinto (archivos PNG en la carpeta)
- **Jardín Tsú Nuum (`.venue-logo-wrap.venue-tsunuum`):** Se sustituyó el encabezado tipográfico por `<img src="logo_tsu_nuum.png" alt="Jardín Tsú Nuum">` (alto máx. 120px, `object-fit:contain`), enlazado a `https://primaveraeventsgroup.com/jardin-tsu-nuum/` con atributo `target="_blank"` y la leyenda `"Recinto Oficial Asociado"`.
- **Finca Las Isabeles (`.venue-logo-wrap.venue-isabeles`):** Se sustituyó el texto por `<img src="logo_finca_las_isabeles.png" alt="Finca Las Isabeles">` (alto máx. 140px, `object-fit:contain`), enlazado a `https://primaveraeventsgroup.com/finca-las-isabeles/` y con la leyenda `"Recinto Oficial Asociado"`.
- **Tabla Comparativa ("Foto miniatura"):** Debajo de la fotografía miniatura de cada recinto se agregó su logotipo oficial pequeño (40px de alto):
  - Jardín Tsú Nuum: `logo_tsu_nuum.png` centrado.
  - Centro de Convenciones Presidente: `logo_ccpresidente.png` sobre contenedor negro redondeado (`background:#1F1F1F; border-radius:8px`).
  - Finca Las Isabeles: `logo_finca_las_isabeles.png` centrado.

### Punto 2: Logo Cásate en Morelos en preloader, header de impresión y footer
- Se reemplazó en las 3 ubicaciones el archivo antiguo `logo_casate_en_morelos.jpg` por el nuevo asset recortado `logo_casate_en_morelos_recorte.png` (880×330 px):
  - **Preloader:** Se eliminó el recorte circular (`border-radius:0; border:none; background:transparent; width:min(260px,70vw); height:auto; object-fit:contain`). Inmediatamente debajo se ubicó el texto `"presenta"` en tipografía dorada (`font-size:0.7rem; letter-spacing:3px; color:var(--gold-accent); font-weight:700`) seguido del logo de Primavera Events Group.
  - **Header de impresión (`.print-header`):** Imagen con alto proporcional de 38px, sin bordes ni recortes circulares.
  - **Footer (`footer`):** Imagen con alto de 38px, sin bordes ni recortes circulares, conservando el co-branding con Primavera Events Group.

### Punto 3: Croquis interactivo por recinto (Sección 2D y 3D)
El contenedor de visualización se segmentó en tres variantes con las clases dinámicas `.venue-block .venue-xxx`:
- **`venue-presidente`:** Se retiró el reproductor de video genérico y se implementó un botón interactivo de alta visibilidad clase `.btn-enter` con ícono Font Awesome que abre en nueva pestaña el planificador espacial real del recinto:  
  `https://5410m0n0c001.github.io/centro-de-convenciones-presidente-croquis/`  
  Debajo se colocó el texto aclaratorio en 0.8rem:  
  *"Herramienta desarrollada por Primavera Events Group para este recinto: distribuye mesas, stands y mobiliario sobre el plano real."*
- **`venue-isabeles`:** Conserva el video oficial `croquis_interactivo.mp4/.webm` con la leyenda `"Croquis real de Finca Las Isabeles"`.
- **`venue-tsunuum`:** Conserva el video con la leyenda `"Ejemplo del servicio de croquis interactivo (el de tu recinto se diseña a medida al contratar)"`.

### Punto 4: Fila "Hospedaje" en la tabla de impresión (`#tablaCotizacion`)
Se sustituyó la fila única por tres filas con clases `.venue-block .venue-xxx` para respetar la visibilidad del recinto activo al imprimir o guardar en PDF:
- **Tsú Nuum:** Thumbnail `hospedaje_habitacion.png` · *"Hospedaje sujeto a disponibilidad; se confirma con tu planner al apartar."*
- **Presidente:** Sin thumbnail · *"No disponible en el recinto. Convenios especiales con hoteles de Cuernavaca (a 5–10 min)."*
- **Isabeles:** Thumbnail `finca_hospedaje.webp` · *"Cabañas ecológicas rústicas y suite nupcial, previa reserva y costo adicional."*
- **Columnas:** Cantidad: `—` | P. Unitario: `Según recinto` | Total: `Según recinto`.

### Punto 5: Tarjeta "Sanitarios y Limpieza General" (BLOQUE 6)
Se dividió la tarjeta de sanitarios en tres variantes `.venue-block`:
- **Presidente:** Utiliza la fotografía real del recinto `presidente_12.webp` con la descripción: *"Baños múltiples de lujo para damas y caballeros, con personal de limpieza durante todo el evento."*
- **Tsú Nuum e Isabeles:** Se utilizó el patrón `pendiente-foto` (`data-venue="tsunuum"` / `data-venue="isabeles"`), sin etiqueta `<img>`, con contenedor `#EFE7E1`, ícono `<i class="fas fa-restroom"></i>` en tamaño grande (3rem) y la leyenda `"Foto del recinto por integrar"` (0.72rem, mayúsculas con espaciado). Descripción: *"Sanitarios del recinto con personal de limpieza durante todo el evento."*

### Punto 6: Tarjetas nuevas con foto pendiente (patrón `pendiente-foto`)
Conforme a `MATRIZ_IMAGENES_POR_VENUE.md` y el punto 6:
- **BLOQUE 1 de Centro de Convenciones Presidente:**
  1. *"Montaje de Ceremonia Religiosa en Jardín"* (ícono `fa-church`) — *"Montaje de ceremonia con mobiliario elegante en el jardín de la entrada, con fuente artificial iluminada."*
  2. *"Área de Cocina Profesional"* (ícono `fa-kitchen-set`) — *"Cocina amplia adaptada para banquetes masivos."*
- **BLOQUE 1 de Finca Las Isabeles:**
  1. *"Salón Montado con Pista de Baile"* (ícono `fa-champagne-glasses`) — *"Área techada montada para banquete y pista de baile."*
- **Jardín Tsú Nuum:** No se agregaron tarjetas adicionales.

### Punto 7: Barra sticky en móvil (`@media (max-width: 600px)`)
Se rediseñó la estructura y estilos CSS de `.controls-sticky-bar`:
1. **Fila 1 (Recintos):** Contenedor `.pills-venue` con scroll horizontal táctil (`overflow-x:auto; white-space:nowrap; -webkit-overflow-scrolling:touch; scrollbar-width:none`), manteniendo las 3 opciones en una sola línea sin desbordar la pantalla.
2. **Pills compactas:** `padding: 6px 12px !important; font-size: 0.78rem !important;`.
3. **Fila 2 (Evento + Invitados):** Contenedor `.controls-row-secondary` que alinea horizontalmente el selector de Boda / XV Años a la izquierda y el input de invitados a la derecha con ancho optimizado (54px).
4. **Leyenda informativa:** Se ocultó en móvil (`.invitados-subtext { display: none !important; }`) y se integró como atributo `title` en el `<input id="inputInvitados">`.
5. **Comportamiento en escritorio:** La regla `@media (min-width: 601px) { .controls-row-secondary { display: contents; } }` preserva intacta la distribución horizontal nativa en pantallas grandes.

---

## 2. Resultados de la Verificación Real (Punto 8)

### A. Medición de Altura de la Barra Sticky en Móvil
- **Dispositivo / Viewport emulado:** Ancho 375px (iPhone SE / estándar móvil).
- **Motor de renderizado real:** Microsoft Edge Chromium (Modo Headless Oficial).
- **Método:** Extracción vía `document.querySelector('.controls-sticky-bar').getBoundingClientRect().height`.
- **Altura inicial reportada en el brief:** `290px`
- **Límite máximo permitido en el brief:** `110px`
- **Altura real medida:** **`87px`**  
- **Estado:** **APROBADO** (Cumple con holgura de 23px bajo el límite máximo).

### B. Verificación de Scripts con `node --check`
- **Script inline analizado:** 37,879 caracteres extraídos a entorno de prueba sintáctica de Node.js v26.4.0.
- **Resultado de ejecución:** `Exit Code 0` (cero errores de sintaxis, cero advertencias).
- **Estado:** **APROBADO**.

### C. Existencia y Peso de Archivos Clave en Disco
Se corroboró la existencia física de los 6 assets especificados en el punto 8:

| Archivo | Ruta Relativa | Tamaño en Disco | Estado en Sistema |
| :--- | :--- | :---: | :---: |
| `logo_tsu_nuum.png` | `./logo_tsu_nuum.png` | 113,919 bytes | **EXISTE** |
| `logo_finca_las_isabeles.png` | `./logo_finca_las_isabeles.png` | 53,813 bytes | **EXISTE** |
| `logo_casate_en_morelos_recorte.png` | `./logo_casate_en_morelos_recorte.png` | 197,008 bytes | **EXISTE** |
| `presidente_12.webp` | `./presidente_12.webp` | 19,006 bytes | **EXISTE** |
| `finca_hospedaje.webp` | `./finca_hospedaje.webp` | 189,060 bytes | **EXISTE** |
| `hospedaje_habitacion.png` | `./hospedaje_habitacion.png` | 208,984 bytes | **EXISTE** |

*Nota adicional:* Se verificaron los **131 assets locales** referenciados en `index.html`; el 100% (131 de 131) existen en la carpeta de trabajo, con 0 referencias rotas.

### D. Grep de Cadenas Prohibidas en `index.html`
Se ejecutó validación estricta de expresiones regulares sobre el código fuente final:

| Cadena Evaluada | Patrón Regex | Coincidencias Reales | Estado |
| :--- | :--- | :---: | :---: |
| Palabra `Ana` | `/\bAna\b/g` | **0** | **PASÓ** |
| `150 invitados` | `/150\s*invitados/gi` | **0** | **PASÓ** |
| `285,000` | `/285[,.]000/g` | **0** | **PASÓ** |
| `314,850` | `/314[,.]850/g` | **0** | **PASÓ** |
| `septiembre 2026` | `/septiembre\s*2026/gi` | **0** | **PASÓ** |
| `gratis` | `/\bgratis\b/gi` | **0** | **PASÓ** |

---

## 3. Estado de Pendientes (Imágenes Propias de Recinto)

Conforme a `MATRIZ_IMAGENES_POR_VENUE.md`, todas las áreas o servicios propios del recinto que carecen de material gráfico propio quedaron identificadas en el DOM con la clase CSS `.pendiente-foto` y su atributo identificador `data-venue="tsunuum|presidente|isabeles"`:

1. **Jardín Tsú Nuum:**
   - Sanitarios y Limpieza General (`data-venue="tsunuum"`)
2. **Centro de Convenciones Presidente:**
   - Montaje de Ceremonia Religiosa en Jardín (`data-venue="presidente"`)
   - Área de Cocina Profesional (`data-venue="presidente"`)
3. **Finca Las Isabeles:**
   - Salón Montado con Pista de Baile (`data-venue="isabeles"`)
   - Sanitarios y Limpieza General (`data-venue="isabeles"`)

Dichas tarjetas presentan una visualización profesional mediante contenedor en tono crema (`#EFE7E1`), ícono temático institucional y la leyenda descriptiva correspondiente, evitando el uso de fotos engañosas de stock o de otros recintos. En cuanto se cuente con las fotografías reales de Salo, podrán sustituirse directamente sin alterar la estructura ni la lógica de la propuesta.
