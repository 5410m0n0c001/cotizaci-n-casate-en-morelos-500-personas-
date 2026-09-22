# BRIEF — Cotización comparativa 500 invitados (Boda / XV Años)
## Cásate en Morelos presenta · Cotización elaborada por Primavera Events Group

Tu tarea: construir `index.html` en ESTA carpeta, partiendo de `index_original_tsunum_ana.html`
(copia exacta de la cotización real https://5410m0n0c001.github.io/cotizacion-tsunum-ana/).
Todos los assets (imágenes, videos, audio, PDF, XLSX) ya están en esta carpeta, en la raíz, sin subcarpetas.
NO descargues nada de internet, NO inventes precios ni inclusiones, NO cambies el sistema de diseño.

---

## 0. Reglas innegociables

1. **Diseño intacto**: misma paleta (rosa `#F65C7A`/`#f05a7e`, oro `#C9A96E`, negro `#1F1F1F`, fondo `#F8F6F4`), mismas tipografías (Playfair Display + Poppins), mismo preloader con `precarga.mp4`, mismo mecanismo de `reveal`, mismos botones flotantes de redes, misma vista de impresión (`@media print` + clase `solo-print`), misma sección de publicidad, Kit Planner, firma (`firma.mp4`), contacto planners y footer. Solo se sustituye contenido.
2. **Un solo archivo** `index.html` autocontenido (CSS y JS inline como el original). Sin build, sin frameworks nuevos, sin dependencias adicionales (puedes seguir usando Font Awesome y Google Fonts que ya usa el original).
3. **Cero datos de "Ana"**: elimina nombre de cliente, fecha 27-Nov-2027, 150 invitados, "precio especial de septiembre 2026", "precio regular de lista $314,850", "ahorras $29,850", tachados de precio, y cualquier mención a "XV Años de la hija de Ana". Esta cotización es GENÉRICA (sin cliente), para 500 invitados, y aplica tanto a Boda como a XV Años.
4. **Precio**: $1,900.00 MXN por persona × 500 invitados = **$950,000.00 MXN** en LOS TRES venues (mismo precio, mismo paquete). `TOTAL_BASE = 950000`, `INVITADOS_BASE = 500`. Precio neto, IVA 16% solo con factura. Vigencia 15 días. Anticipo de apartado 10%, liquidación 30 días naturales antes del evento. Hora extra $12,000 MXN. Cancelación: reintegro del 10% de lo acumulado dentro de 48 h (NO uses la línea de "no aplica reembolso" del original). Degustación: cortesía para 4 personas, se programa una vez firmado el contrato y cubierto el apartado (nunca "gratis antes de firmar").
5. **Nunca la palabra "gratis"** en complementos. La única promoción sin costo es la Invitación Digital Premium (valor comercial $4,000–$8,000 MXN, incluida al contratar el paquete). Descorche libre en todos los paquetes.
6. No dejes ningún placeholder `[CORCHETES]`, ningún `TODO`, ningún texto lorem.

---

## 1. Co-branding Cásate en Morelos

- `logo_casate_en_morelos.jpg` es el logo del presentador. `logo_primavera_events_group.png` es el logo de quien cotiza. Ambos van juntos siempre que aparezca marca.
- **Preloader**: logo Cásate en Morelos arriba (más grande), debajo texto pequeño "presenta", luego logo Primavera Events Group. Título "Bienvenidos". Texto: "Le presentamos la propuesta integral para un evento de <strong>500 invitados</strong> — Boda o XV Años — en tres recintos exclusivos de Morelos." Botón "Ingresar a la Propuesta". Mantén la leyenda "Primavera Events Group® · Marca Registrada".
- **Hero eyebrow**: "CÁSATE EN MORELOS PRESENTA". H1: "Propuesta para 500 Invitados · Boda o XV Años". Sub: nombre del venue activo.
- **Encabezado de impresión** (`.print-header`): ambos logos + "Cotización elaborada por Primavera Events Group® · Presentada por Cásate en Morelos".
- **Footer**: agrega una línea "Propuesta presentada por Cásate en Morelos en alianza con Primavera Events Group®" con ambos logos pequeños. NO cambies los datos de contacto de PEG (primaveraeventsgroup.com · contacto@primaveraeventsgroup.com · WhatsApp +52 777 458 7923 · Cuernavaca, Morelos · Jessy Sandoval y Richard Hernández).
- `<title>`: "Cotización 500 Invitados · Boda o XV Años · Cásate en Morelos × Primavera Events Group". Actualiza meta description, OG y Twitter con el mismo sentido (500 invitados, 3 venues, $1,900 p/p). Conserva `og_image.jpg`.
- QR de impresión: apunta a `https://5410m0n0c001.github.io/cotizacion-500-personas/` (URL tentativa, se confirmará).

---

## 2. Controles globales (nuevo, es el corazón de la comparativa)

Justo debajo del hero, una barra **sticky** (fondo blanco, sombra suave, borde inferior oro fino) con:

**A) Selector de venue** — 3 pestañas tipo "pill" (activa = fondo rosa `#F65C7A` texto blanco; inactiva = borde rosa texto negro):
1. Jardín Tsú Nuum
2. Centro de Convenciones Presidente
3. Finca Las Isabeles

**B) Toggle tipo de evento** — dos opciones: **Boda** | **XV Años** (mismo estilo pill, pero en oro `#C9A96E` cuando activa).

**C) Contador de invitados** — input numérico (min 400, max 600, step 10, default 500) con label "Invitados". Al cambiar recalcula `total = invitados × 1900` en todos los lugares donde aparece el total. Debajo, en 0.72rem gris: "Proyección al mismo precio por persona; el número final se confirma con tu planner."

Comportamiento:
- Cambiar venue actualiza TODO lo marcado `[VENUE]` en la sección 3 sin recargar (JS con `data-venue="tsunuum|presidente|isabeles"` en los bloques y mostrando/ocultando, o rellenando desde un objeto `VENUES` en JS — elige lo más limpio, pero las fotos y textos del recinto deben existir en el HTML para que la vista de impresión también funcione).
- Cambiar tipo de evento actualiza todos los `<span data-evento>` (ver sección 4) y el hero H1 sub-línea ("Boda" / "XV Años").
- Persiste selección en `localStorage` y, si viene `?venue=presidente&evento=boda` en la URL, respétalo. Los botones de WhatsApp y el botón compartir deben incluir el venue y tipo de evento seleccionados.
- Estado inicial: Tsú Nuum + Boda + 500.
- Al imprimir (`window.print()`) solo se imprime el venue activo.

Además, ANTES de la barra de inclusiones, agrega una sección nueva **"Comparativo de los 3 Recintos"** (`section-title` con icono `fa-scale-balanced`): tabla responsive de 3 columnas (una por venue, la activa resaltada en rosa suave) con filas: Foto miniatura · Ubicación · Estilo · Capacidad · Ceremonia en sitio · Hospedaje · Estacionamiento · Horario de cierre · Precio por persona ($1,900.00) · Inversión 500 invitados ($950,000.00) · Botón "Ver esta propuesta" (activa ese venue y hace scroll suave a los datos del recinto). Esta tabla sí aparece completa en la impresión.

---

## 3. Datos por venue (fuente: base de datos oficial de PEG, verificada 2026-08-10 — cópialos tal cual)

### 3.1 Jardín Tsú Nuum  (`data-venue="tsunuum"`)
- Ubicación: Xochitepec, Morelos (dirección exacta a confirmar con tu coordinador)
- Estilo: Jardín zen moderno minimalista con paisajismo de diseñador
- Capacidad: 500 invitados (montaje para 500 sujeto a confirmación con tu planner)
- Ceremonia en sitio: Sí — área de ceremonia al aire libre
- Hospedaje: Sujeto a disponibilidad (se confirma con tu planner)
- Estacionamiento: Consultar con tu coordinador
- Horario: 10 hrs de presencia (1 hr ceremonia + 1 hr cóctel + 8 hrs de servicio)
- URL oficial: https://primaveraeventsgroup.com/jardin-tsu-nuum/
- Video hero: YouTube `5xVqNRu6nu8` (mismo mecanismo del original). Botón "Ver Video del Recinto" → https://youtu.be/5xVqNRu6nu8
- Logo: `logo_tsu_nuum.png` (PNG transparente) en el `.venue-logo-wrap`, enlazado a la URL oficial.
- Fotos (ya en carpeta): `tsunuum_1.webp`, `tsunuum_2.webp`, `tsunuum_3.webp`, `tsunuum_4.webp`, `tsunuum_area_ceremonia.webp`, `tsunuum_area_techada.webp`, `tsunuum_area_techada_2.webp`. Úsalas exactamente como el original las usa en el BLOQUE 1 "Recinto y áreas" y la galería.

### 3.2 Centro de Convenciones Presidente  (`data-venue="presidente"`)
- Ubicación: Avenida Defensa Nacional #8, Col. Chamilpa, 62210 Cuernavaca, Morelos
- Estilo: Arquitectónico modernista, elegante e industrial con amplias alturas
- Capacidad: Desde 100 hasta 500 personas máximo — salón techado climatizado
- Ceremonia en sitio: Sí — montaje de ceremonia con mobiliario elegante en el jardín de la entrada
- Hospedaje: No disponible en el recinto; convenios especiales con hoteles de Cuernavaca (a 5–10 min)
- Estacionamiento: Interno y vigilado para 35 vehículos compactos
- Horario: 9 horas de servicio continuo (cierre 00:00 hrs con Paquete Gobernador · 01:00 hrs con Paquete Presidente)
- URL oficial: https://primaveraeventsgroup.com/centro-de-convenciones-presidente/
- Video hero: YouTube `W0IPzy0dFwk` ("Centro de Convenciones Presidente | El venue ideal en Cuernavaca"). Video adicional en el bloque de recinto: YouTube `AjOVYnYQ6cQ` ("Los XV de Elisa en el Centro de Convenciones Presidente").
- Logo: `logo_ccpresidente.png` (fondo negro con diamante dorado — colócalo sobre fondo negro `#1F1F1F` con `object-fit:contain`, alto máx. 140px).
- Características del recinto (tarjetas con foto, BLOQUE 1):
  - `presidente_01.webp` — Fachada principal con logotipo del recinto
  - `presidente_02.webp` — Gran salón techado climatizado, excelentes acabados y acústica
  - `presidente_03.webp` — Salón montado con entelado de techo y pista de baile LED
  - `presidente_04.webp` — Vista completa del salón en evento (entelado, iluminación arquitectónica)
  - `presidente_05.webp` — Terraza y pasillos techados de acceso
  - `presidente_06.webp` — Área infantil con juegos múltiples fijos y seguros
  - `presidente_07.webp` — Jardín delantero y estacionamiento interno vigilado (35 vehículos)
  - `presidente_08.webp` — Mesa principal de honor montada en el salón
  - `presidente_09.webp` — Montaje de mesas con sillas Tiffany y equipo de meseros
  - `presidente_10.webp` — Templete para DJ/grupo con letras gigantes iluminadas
  - `presidente_11.webp` — Mesa principal con sillones y centro floral natural
  - `presidente_12.webp` — Baños múltiples de lujo para damas y caballeros
  - `presidente_13.webp` — Acceso lateral con jardineras y fuente
  - `presidente_14.webp` — Mesa de honor en jardín
  - `presidente_15.webp` — Firma de acta en ceremonia civil dentro del salón
- **Sub-bloque informativo "Paquetes oficiales del recinto: Gobernador vs Presidente"** (solo en la pestaña Presidente, debajo de las tarjetas del recinto, estilo tabla 2 columnas con encabezado oro): copia EXACTAMENTE estas diferencias, sin agregar nada:
  - Gobernador: Uso de salón 8 hrs (9 hrs de servicio continuo, cierre 00:00) · Cóctel con margaritas sin alcohol (2 sabores) y agua fresca (2 sabores) · Mesa principal con sillón o sillones · Centros de mesa naturales (largos, redondos y altos) · Mesa redonda/cuadrada/tipo mármol/vintage con sillas Tiffany, Crossback, Lotus o Boss · Banquete a 3 tiempos (Entrada, Plato Fuerte, Tornafiesta) · Equipo: Coordinador General, Hostess, Meseros, Barra, Stewart, Cocina, Personal de baños · DJ profesional con cabina, cabezas robóticas, proyector/pantalla, láser y humo.
  - Presidente: Uso de salón 9 hrs continuas (cierre 01:00) · Cóctel premium con margaritas, piñada y mojito sin alcohol + agua fresca (2 sabores) · Mesa principal con sillones Rey & Reyna · Centros de mesa naturales + bases de metal altas · Mesa tipo mármol cuadrada/redonda para 10–12 personas con silla Tiffany blanca · Banquete a 4 tiempos (Entrada, Plato Fuerte, Postre, Tornafiesta) · Equipo: Coordinador General, Capitán de Meseros, Hostess, Meseros, Barra, Stewart, Cocina, Personal de baños · DJ profesional + pista de baile LED 5×5 y 2 chisperos a control remoto · Opción de montaje de ceremonia con mobiliario elegante.
  - Nota al pie del sub-bloque (texto literal): "Los precios oficiales publicados de los paquetes Gobernador y Presidente aplican hasta 400 invitados; para 500 invitados esta propuesta se personaliza con el paquete integral descrito abajo, al mismo precio por persona que en los otros dos recintos."

### 3.3 Finca Las Isabeles  (`data-venue="isabeles"`)
- Ubicación: Xochitepec, Morelos
- Estilo: Finca campestre rústica elegante de gran exclusividad
- Capacidad: 500 invitados (montaje para 500 sujeto a confirmación con tu planner)
- Ceremonia en sitio: Sí — área consagrada dentro de la finca
- Hospedaje: Cabañas ecológicas rústicas y suite nupcial (previa reserva y costo adicional)
- Estacionamiento: Valet parking
- Horario: 9 horas continuas de servicio
- URL oficial: https://primaveraeventsgroup.com/finca-las-isabeles/
- Video hero: usa `<video autoplay muted loop playsinline poster="portada_finca_las_isabeles.webp">` con `<source src="https://primaveraeventsgroup.com/wp-content/uploads/2026/03/i2.mp4" type="video/mp4">` (video oficial alojado en el sitio de PEG; no lo descargues). Botón "Ver Video del Recinto" → esa misma URL.
- Logo: `logo_finca_las_isabeles.png` (PNG transparente, mostrar máx. 150px de alto) en el `.venue-logo-wrap`, enlazado a la URL oficial.
- Portada/hero fallback: `portada_finca_las_isabeles.webp`.
- Características del recinto (tarjetas con foto, BLOQUE 1):
  - `finca_area_consagrada.webp` + `finca_area_consagrada_2.webp` — Área consagrada para ceremonia religiosa
  - `finca_area_techada.webp` + `finca_area_techada_2.webp` — Área techada para banquete
  - `finca_jardin_cascada.webp` — Jardín con cascada
  - `finca_cocina.webp` — Cocina profesional para banquetes
  - `finca_hospedaje.webp` — Hospedaje en cabañas (previa reserva, costo adicional)
  - `finca_suite_nupcial.webp` — Suite nupcial (previa reserva, costo adicional)
  - `finca_valet_parking.webp` — Valet parking
- Galería adicional (sección galería): `isabeles_galeria_01.webp` (puente de madera sobre el estanque), `02` (estanque con esculturas), `03` (jardín de palmeras al atardecer), `04` (estanque y puente), `05` (montaje de mesa bajo pérgola), `06` (gazebo de ceremonia con telas), `07` (jardín iluminado al atardecer), `08` (estanque iluminado de noche).

---

## 4. Paquete integral (IGUAL en los 3 venues) — base: el desglose del original

Conserva el desglose completo del original (tabla de impresión `#tablaCotizacion` + tarjetas "Todo lo que Incluye, Servicio por Servicio" BLOQUES 2 a 10, con sus imágenes y videos), con estas adaptaciones:

- Todas las cantidades que dependan de invitados se expresan para 500 (ej. "periqueras y sombrillas para el 30% de los invitados" se mantiene en porcentaje; "60 sillas Tiffany para ceremonia" → "sillas Tiffany blancas para ceremonia (cantidad según montaje)").
- Nombre del paquete: **"Paquete Integral 500 · Personalizado"** (deja de llamarse "Vuelo Esmeralda Personalizado para Ana"). Puedes mencionar una sola vez que "toma como base el paquete Vuelo Esmeralda de Primavera Events Group".
- **Hospedaje cortesía** (fila del original): cámbiala a "Hospedaje: según recinto — ver datos del recinto arriba" y quita la palabra "Cortesía" en esa fila (en Presidente no hay hospedaje; en Isabeles tiene costo adicional; en Tsú Nuum está sujeto a disponibilidad).
- El bloque "CORTESÍAS SIN COSTO: comparativo paquete oficial vs. esta propuesta personalizada" (grupo A / grupo B) se simplifica a una sola lista "Cortesías incluidas en la inversión" (une A y B, sin mencionar septiembre ni precio especial).
- Textos con `data-evento`: cada frase que dependa del tipo de evento debe llevar `<span data-evento-boda="…" data-evento-xv="…"></span>` y el JS los rellena. Mínimo estos:
  - Letras gigantes: Boda = «LOVE» · XV = «XV»
  - Ceremonia religiosa: Boda = "misa de boda" · XV = "misa de acción de gracias"
  - Protagonistas: Boda = "los novios" · XV = "la quinceañera"
  - Pastel: Boda = "Pastel de Boda de Autor" · XV = "Pastel de XV Años de Autor"
  - Alfombra roja: Boda = "para recibir a los novios y a sus invitados" · XV = "para recibir a la quinceañera y a sus invitados"
  - Mesa principal: Boda = "Mesa de honor para los novios" · XV = "Mesa de honor para la quinceañera y su familia"
  - Buenos deseos en video: Boda = "para los novios" · XV = "para la quinceañera"
  - Mensajes de WhatsApp: incluyen "Boda" o "XV Años".
- Sección **"Inversión Total"** (fondo oscuro): muestra "$1,900.00 MXN por persona · 500 invitados" y "Inversión total del evento: $950,000.00 MXN". Sin tachados, sin badge de ahorro. Nota: "Precios netos, no incluyen IVA (16% solo aplica si se solicita factura oficial). Cotización con validez de 15 días a partir de su emisión. Mismo precio y mismo paquete en los tres recintos."
- **Cotizador Dinámico de Extras**: conserva el array `EXTRAS` del original (Fotografía & Video: Memoria Clásica 9,350 · Experiencia Deluxe 10,900 · Cinematic Prestige 13,900 — elige 1; Efectos: pirotecnia 6 chisperos 4,500; Entretenimiento adicional: cabina inflable adicional 7,000 · cabina 360 adicional 5,000; Repostería: pastel de autor 9,000) y AGREGA estas categorías/ítems con precio verificado del catálogo oficial de PEG (no agregues ningún otro):
  - "Música en Vivo": Banda (1 hr) 14,000 · Mariachi (1 hr) 9,000 · Saxofonista (1 hr) 5,000
  - "Animación y Shows": Show men animador (2 hrs) 7,000 · Robot LED (1 hr) 5,000
  - "Personal Extra": Capitán de meseros extra 3,000 · Mesero adicional (8 hrs) 1,000
  - "Souvenirs": Tequila personalizado Don Ramón (750 ml, corte diamante) 11,515
  - "Tiempo Extra": Hora extra de banquete 12,000
  El nombre del ítem de pastel usa `data-evento` (Boda/XV). La tabla de impresión `#tablaExtrasPrint` debe quedar sincronizada con el array (mismos ítems, mismos precios). El total = (invitados × 1,900) + extras. La línea "Paquete base · 150 invitados" pasa a "Paquete base · <span id=invitadosTxt>500</span> invitados".
- Croquis interactivo y Ficha técnica minuto a minuto: consérvalos como en el original (son servicios incluidos que PEG entrega en todos los recintos), pero cambia el título de la ficha a "Ejemplo de Minuto a Minuto (se diseña a medida para tu evento)".
- Sección "Contacto Directo con tus Wedding & Event Planners", Publicidad, Expo Boda, Kit Planner, Firma, botón imprimir, botones flotantes: intactos.

---

## 5. Entregables

1. `index.html` terminado (único archivo nuevo, además de este brief). No borres `index_original_tsunum_ana.html`.
2. Al final, escribe `REPORTE_ANTIGRAVITY.md` con: (a) lista de todos los `src=` de imágenes/videos usados y confirmación de que cada archivo existe en la carpeta (haz la verificación real), (b) lista de textos con `data-evento`, (c) cualquier dato que NO hayas podido resolver con este brief (no lo inventes: déjalo marcado con la clase `.pendiente-confirmar` y repórtalo).
3. Verifica que no queden las cadenas: "Ana", "150 invitados", "285,000", "314,850", "29,850", "septiembre 2026", "27 de noviembre", "gratis", "[".
