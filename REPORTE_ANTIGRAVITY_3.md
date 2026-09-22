# REPORTE DE EJECUCIÓN ANTIGRAVITY 3
## Correcciones Quirúrgicas sobre `index.html`
**Fecha de ejecución:** 21 de septiembre de 2026  
**Documentos base:** `BRIEF_ANTIGRAVITY_3_CORRECCIONES.md` y referencia literal `index_original_tsunum_ana.html`  
**Archivo intervenido:** `index.html` (edición quirúrgica sin regeneración)  
**Archivo original resguardado:** `index_original_tsunum_ana.html` (intacto, 211,665 bytes)  

---

## 1. Resumen Detallado de los 8 Puntos Aplicados

### Punto 1: Videos de la Expo Boda & 15 Años Morelos
- Se identificó que los IDs `G3c1zJ-g51E` y `3J5i6F85xNk` arrojaban error 404 en YouTube.
- Se restauraron exactamente los IDs originales legítimos del proyecto en el contenedor `.expo-videos`:
  ```html
  <div class="expo-video is-short is-short-video-box" data-video="P9MxVEjGA98"></div>
  <div class="expo-video is-short is-short-video-box" data-video="xdPO6q93pMM"></div>
  ```

### Punto 2: Restauración de Tarjetas con Video y Markup Literal del Original
- **BLOQUE 3:** Se restauró la tarjeta con video vertical para "Alfombra Roja en la Recepción":
  ```html
  <div class="include-img-container is-short is-short-video-box" data-video="xNc85w8ZOCk" data-inicio="123"></div>
  ```
  Con los textos adaptativos según el evento (`data-evento-boda="para recibir a los novios y a sus invitados"` y `data-evento-xv="para recibir a la quinceañera y a sus invitados"`).
- **BLOQUE 9 (Cortesías):** Se recuperaron las tarjetas con video con su estructura y clases originales:
  - *"Social Media Content"*: con `data-video="7r6OV9qjS30"`.
  - *"Kit Organizador de Eventos"*: con `data-video="Q4L2srgBU2E"`.
  - *"Ejemplo: La Ceremonia"* (Reel vertical): con `data-video="7r6OV9qjS30"`.
  - *"Ejemplo: La Fiesta"* (Reel vertical): con `data-video="xNc85w8ZOCk"`.
- **Soporte en `montaVideo()` para `data-inicio` y `data-fin`:**
  Se actualizó la función `montaVideo` en JavaScript para parsear dinámicamente `data-inicio` (parámetro `&start=...`) y `data-fin` (parámetro `&end=...`) en la URL del iframe de YouTube.
- **Corrección en tabla de impresión (`#tablaCotizacion`):**
  Se removió la etiqueta errónea `<img class="tbl-thumb" src="guia_maestra_primavera.pdf">`, dejando la fila de cortesía del Kit Organizador con su descripción textual limpia.

### Punto 3: Optimización del Video "Evento Real en Centro de Convenciones Presidente"
- Se corrigió el despliegue del iframe 16:9 que se distorsionaba por heredar estilos de video vertical 9:16.
- Se agregaron las reglas CSS específicas:
  ```css
  .include-img-container.is-short-video-box:not(.is-short) { height: auto !important; }
  .is-short-video-box:not(.is-short) iframe { position: absolute; inset: 0; width: 100% !important; height: 100% !important; border: 0; }
  ```
- Se eliminó el estilo inline `max-height: 420px;` que recortaba la caja contenedora del video `AjOVYnYQ6cQ`.

### Punto 4: Eliminación Integral de la Categoría "Souvenirs" y Tequila
- Se eliminó la categoría `"Souvenirs"` y su ítem `"Tequila personalizado Don Ramón (750 ml, botella corte diamante)"` del array `EXTRAS` en JavaScript.
- Se eliminó la categoría `"SOUVENIRS"` de la tabla de impresión `#tablaExtrasPrint`.
- Se eliminó la mención de "souvenirs," en la nota descriptiva de extras opcionales.
- Se sustituyó la tarjeta en la sección de complementos (`tequila_personalizado.png`) por la tarjeta original de *"Barra de Bebidas Premium"* con imagen oficial `cristaleria.webp`.

### Punto 5: Corrección de "Barra de Shots" y Restauración de Textos Originales
- Se erradicó el término "shots", el cual no formaba parte del paquete base ni del contenido original.
- **Tarjeta web:** Título *"Cóctel de Bienvenida & Aguas Frescas"*, imagen `aguas_frescas.webp`, texto:  
  *"Margaritas, piñadas, azulitos y mojitos —en versión con y sin alcohol—, aguas frescas de fruta natural y agua natural."*
- **Fila de impresión (`#tablaCotizacion`):** Título *"Bebidas de Bienvenida"*, miniaturas `margaritas.webp` + `aguas_frescas.webp`, descripción limpia sin mención de shots.
- **Revisión integral de tarjetas y filas:**
  - En BLOQUE 3 y `#tablaCotizacion`: se restauraron *"Salas Lounge"* (`sala_lounge_1.webp`), *"Periqueras y Sombrillas"* (`periqueras_real.jpg`) y *"Barra de Snacks (12 Toppings)"* (`barra_snacks_real.jpg`).
  - En BLOQUE 8: se restauró la tarjeta *"Amenidades de Pista"* (`amenidades_pista.jpg`) que había sido duplicada por error con la alfombra roja.

### Punto 6: Centro de Convenciones Presidente — Video en Montaje de Ceremonia
- Se sustituyó el placeholder `.pendiente-foto` en el BLOQUE 1 de Presidente por un reproductor interactivo de YouTube:
  ```html
  <div class="include-img-container is-short-video-box" data-video="W0IPzy0dFwk" data-inicio="9" data-fin="40" style="aspect-ratio:16/9;"></div>
  ```
- Título: *"Montaje de Ceremonia en el Jardín"* + badge Video.
- Texto descriptivo: *"Montaje de ceremonia con mobiliario elegante en el jardín de la entrada, con fuente artificial iluminada."*
- Se retiró la clase `.pendiente-foto`.

### Punto 7: Jardín Tsú Nuum — Salón Montado con Foto Real
- En el BLOQUE 1 de Tsú Nuum:
  - La tarjeta existente se transformó en: *"Salón Montado con Pista de Baile"* utilizando la fotografía de alta resolución `tsunuum_salon_montado.webp` (1920×1280 px), con texto: *"Área techada montada para banquete con pista de baile, candil floral suspendido y mesa de honor iluminada."*
  - Se colocó inmediatamente después la tarjeta *"Pista de Baile y Área de DJ"* con la imagen `tsunuum_area_techada_2.webp` y su redacción original.

### Punto 8: Finca Las Isabeles — Video Local Real de Salón Montado
- Se sustituyó el placeholder `.pendiente-foto` en el BLOQUE 1 de Isabeles por un reproductor de video HTML5 vertical local (9:16, loop, autoplay, muted, playsinline, sin audio):
  ```html
  <div class="include-img-container is-video">
      <video class="include-video" autoplay muted loop playsinline webkit-playsinline poster="isabeles_salon_montado_poster.jpg">
          <source src="isabeles_salon_montado.mp4" type="video/mp4">
      </video>
  </div>
  ```
- Título: *"Montaje Real en Finca Las Isabeles"* + badge Video.
- Texto descriptivo: *"Montaje real de mesas y ceremonia en los jardines de la finca, con pasarela de madera sobre el estanque."*
- Se retiró la clase `.pendiente-foto`.

---

## 2. Resultados de la Verificación Real (Punto 9)

Todas las pruebas se ejecutaron sobre el archivo final `index.html` y el sistema de archivos local de manera automatizada y con datos reales verificables.

### A. Verificación de Sintaxis JavaScript (`node --check`)
- **Procedimiento:** Se extrajo el bloque `<script>` inline completo (37,215 bytes de código JS) y se evaluó con el motor Node.js v26.4.0 (`node --check`).
- **Resultado:** `Exit Code 0` (0 errores de sintaxis, 0 advertencias).
- **Estado:** **APROBADO**.

### B. Auditoría de YouTube IDs y Consulta Real a oEmbed
Se identificaron todas las ocurrencias del atributo `data-video` en el código fuente de `index.html`. Cada ID fue consultado mediante petición HTTP GET directa a la API oficial de oEmbed de YouTube (`https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=ID`):

| # | Línea en `index.html` | Video ID | HTTP Status | Título Oficial Obtenido de YouTube |
| :-: | :-: | :-: | :-: | :--- |
| 1 | 1104 | `5xVqNRu6nu8` | **200 OK** | Jardín Tsu Nuum 🌿 El lugar PERFECTO para bodas y XV en Morelos \| Paquete Vuelo Esmeralda ✨ |
| 2 | 1892 | `W0IPzy0dFwk` | **200 OK** | Centro de Convenciones Presidente \| El venue ideal en Cuernavaca |
| 3 | 1916 | `AjOVYnYQ6cQ` | **200 OK** | Los XV de Elisa en el Centro de Convenciones Presidente ✨ |
| 4 | 2049 | `xNc85w8ZOCk` | **200 OK** | Título: La Fiesta de los XV Años de Aline \| Rancho Los Potrillos |
| 5 | 2201 | `7r6OV9qjS30` | **200 OK** | Título: La Ceremonia de los XV Años de Aline \| Rancho Los Potrillos |
| 6 | 2202 | `Q4L2srgBU2E` | **200 OK** | Kit Planner GRATIS: organiza tu evento sin estrés \| Primavera Events Group |
| 7 | 2209 | `7r6OV9qjS30` | **200 OK** | Título: La Ceremonia de los XV Años de Aline \| Rancho Los Potrillos |
| 8 | 2210 | `xNc85w8ZOCk` | **200 OK** | Título: La Fiesta de los XV Años de Aline \| Rancho Los Potrillos |
| 9 | 2412 | `P9MxVEjGA98` | **200 OK** | 🌸✨ ¡POR FIN REVELADO! Conoce a los creadores del evento de tus sueños ✨🌸 |
| 10 | 2413 | `xdPO6q93pMM` | **200 OK** | ✨ ESTE 21 DE JUNIO… NO ASISTAS A UNA EXPO. VIVE UNA EXPERIENCIA. ✨ |

- **Total de IDs únicos encontrados:** 8
- **IDs no autorizados / inventados:** 0 (Ninguno)
- **IDs faltantes de la lista permitida:** 0 (Ninguno)
- **Estado:** **APROBADO (100% de videos válidos y activos en YouTube)**.

### C. Existencia Física de Archivos Clave en Disco
Comprobación del sistema de archivos mediante `fs.existsSync` y `fs.statSync`:

| Archivo | Ruta Relativa | Tamaño Real en Disco | Estado en Sistema |
| :--- | :--- | :---: | :---: |
| `tsunuum_salon_montado.webp` | `./tsunuum_salon_montado.webp` | 157,446 bytes | **EXISTE** |
| `isabeles_salon_montado.mp4` | `./isabeles_salon_montado.mp4` | 5,966,029 bytes | **EXISTE** |
| `isabeles_salon_montado_poster.jpg` | `./isabeles_salon_montado_poster.jpg` | 89,155 bytes | **EXISTE** |
| `aguas_frescas.webp` | `./aguas_frescas.webp` | 31,740 bytes | **EXISTE** |
| `margaritas.webp` | `./margaritas.webp` | 43,842 bytes | **EXISTE** |

- **Estado:** **APROBADO (Todos los archivos requeridos están presentes)**.

### D. Conteo Estricto de Cadenas Prohibidas en `index.html`

| Parámetro Evaluado | Expresión / Comando | Conteo Real Obtenido | Requisito del Brief | Estado |
| :--- | :--- | :---: | :---: | :---: |
| `shots` (insensible a mayúsculas) | `grep -ci "shots"` | **0** | `= 0` | **APROBADO** |
| `Tequila` (sensible a mayúsculas) | `grep -c "Tequila"` | **0** | `= 0` | **APROBADO** |
| `Souvenirs` (sensible a mayúsculas) | `grep -c "Souvenirs"` | **0** | `= 0` | **APROBADO** |
| Atributo `src="guia_maestra_primavera.pdf"` | `grep -c 'src="guia_maestra_primavera.pdf"'` | **0** | `= 0` | **APROBADO** |

### E. Cadenas Críticas de Negocio que se Mantienen en Cero

| Cadena Evaluada | Patrón de Búsqueda | Conteo Real Obtenido | Estado |
| :--- | :--- | :---: | :---: |
| Palabra `Ana` (nombre cliente anterior) | `/\bAna\b/g` | **0** | **APROBADO** |
| `150 invitados` (capacidad anterior) | `/150\s*invitados/gi` | **0** | **APROBADO** |
| `285,000` (precio base anterior) | `/285[,.]000/g` | **0** | **APROBADO** |
| `septiembre 2026` (fecha anterior) | `/septiembre\s*2026/gi` | **0** | **APROBADO** |
| Palabra `gratis` (política comercial) | `/\bgratis\b/gi` | **0** | **APROBADO** |

---

## 3. Conclusión
El archivo `index.html` ha sido actualizado quirúrgicamente cumpliendo con la totalidad de los requerimientos de contenido, diseño y funcionalidad establecidos en `BRIEF_ANTIGRAVITY_3_CORRECCIONES.md`. Todos los videos y assets multimedia están validados física y remotamente, sin dependencias rotas, con sintaxis limpia y cero violaciones a las reglas editoriales y comerciales de Primavera Events Group.
