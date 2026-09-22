# Reporte: Eliminación de Totales Agregados del Evento (Solo Precio por Persona)

**Fecha:** 22 de septiembre de 2026  
**Archivo intervenido:** [index.html](file:///C:/Users/Lenovo/Documents/cotizacion%20500%20personas/index.html)  
**Objetivo cumplido:** Se eliminó cualquier mención visible de totales agregados del evento ($500,000.00 MXN, $425,000.00 MXN o cálculos de precio por persona &times; número de invitados), mostrando exclusivamente la tarifa por persona ($1,000.00 MXN / $850.00 MXN según recinto) en todos los módulos de la cotización web y versión para impresión / PDF.

---

## 1. Estado de Bloques de Trabajo

| Bloque | Descripción | Estado |
|---|---|:---:|
| **BLOQUE A** | **Header/Hero Superior (`.ph-meta`)**: Remoción de cualquier mención de inversión total base ($500,000), finalizando la línea con el precio por persona (`$1,000.00 MXN por persona`). | **Completado** |
| **BLOQUE B** | **Tabla Comparativa de Recintos (`#seccionComparativo`)**: Eliminación completa de la fila `<tr>` con los totales por recinto (`total-val-*`). Se conserva la fila de "Precio por persona" con los valores dinámicos para los 5 recintos. | **Completado** |
| **BLOQUE C** | **Info Boxes (`.summary-boxes`)**: Se eliminó el box con "Inversión Base" y montos totales; se conservan únicamente Invitados (`500 Px`), Precio p/p (`$1,000.00`) y Duración (`10 hrs` / `9 hrs`). | **Completado** |
| **BLOQUE D** | **Tabla de Impresión / PDF (`.pricing-table`)**: Se eliminó `pdfTotalEvento` de la fila final del `<tfoot>`, conservando `pdfTotalPersona` con la etiqueta "PRECIO BASE POR PERSONA (500 INVITADOS)", manteniendo la alineación de las 5 columnas (`colspan="4"` + celda derecha de precio por persona). | **Completado** |
| **BLOQUE E** | **Caja Hero Oscura (`#inversionBase`)**: Título actualizado a `<h3>Precio por Persona</h3>`, manteniendo el monto grande en `totalBaseDisplay` (`$1,000.00 MXN`) y retirando cualquier renglón de monto total agregado del evento. | **Completado** |
| **BLOQUE F** | **Caja Sticky del Cotizador (`#calcTotalBox`) y Resumen Web**: Se eliminó el gran total del evento (`ctb-total` / `ctbTotal`) y el renglón de total estimado en el resumen final (`resumenFinalTotal`). Solo se muestra el precio base por persona del recinto activo y la lista de extras con su costo individual. | **Completado** |
| **BLOQUE G** | **Lógica JavaScript (`actualizarTotal()` y `actualizarEnlacesWhatsapp()`)**: Se eliminaron las asignaciones a elementos de totales eliminados (`total-base-txt`, `ctbTotal`, `resumenFinalTotal`, `totalEventoChico`, `pdfTotalEvento`). El mensaje predeterminado de WhatsApp se parametrizó con `porPersona` para cotizar y apartar indicando explícitamente el precio por persona (`$1,000.00 MXN por persona` o `$850.00 MXN por persona`). | **Completado** |
| **BLOQUE H** | **Barrido Integral de Verificación**: Búsqueda global de selectores (`total-base-txt`, `total-activo`, `ctb-total`, `price-total-chico`, `total-val-`, `pdfTotalEvento`, etc.) y patrones monetarios. Cero menciones de cifras agregadas de evento ($500,000 / $425,000) en toda la interfaz. | **Completado** |

---

## 2. Decisiones de Diseño en el Bloque F (Caja Sticky del Cotizador y Resumen Web)

1. **Caja Sticky (`#calcTotalBox`)**:
   - En lugar de sumar los extras al precio base para arrojar un total del evento, la caja destaca claramente:
     - **Precio Base**: `$1,000.00 p/p` (o `$850.00 p/p` para CC Presidente).
     - **Contexto**: `Recinto activo · 500 invitados`.
     - **Extras Seleccionados**: Lista dinámica con el nombre y precio unitario fijo en MXN de cada servicio adicional seleccionado (ej. `+ Pista de Baile LED 6×6 m: $10,900.00`).
     - Al estar vacía la selección, muestra `Sin extras seleccionados`.
   - Se removió por completo el contenedor de gran total (`.ctb-total` con `#ctbTotal`).

2. **Resumen de Propuesta Web (`.resumen-web`)**:
   - Muestra el renglón de **Precio Base por Persona** (`$1,000.00 MXN` / `$850.00 MXN`).
   - Muestra el renglón de **Servicios Adicionales Seleccionados** (`#resumenFinalExtras`) únicamente cuando el cliente selecciona extras opcionales, indicando la suma de los servicios adicionales solicitados sin mezclarlo en una cifra agregada total del evento.
   - Se eliminó el renglón `resumenFinalTotal` ("Total Estimado del Evento").

---

## 3. Verificaciones de Calidad

- **Validación de JavaScript**: El código inline fue verificado con `node --check`, confirmando cero errores de sintaxis (`JS syntax OK!`).
- **Respeto a Tarifas**: Se mantienen exactamente las tarifas oficiales del negocio:
  - Tsú Nuum: `$1,000.00 MXN p/p`
  - Centro de Convenciones Presidente: `$850.00 MXN p/p`
  - Finca Las Isabeles: `$1,000.00 MXN p/p`
  - Jardín La Villa: `$1,000.00 MXN p/p`
  - Jardín San Rafael: `$1,000.00 MXN p/p`
- **Reglas de Proceso**:
  - No se ejecutó ningún comando `git`.
  - No se modificó el directorio `.git`.
  - La carpeta temporal `scratch/` fue eliminada al concluir.
