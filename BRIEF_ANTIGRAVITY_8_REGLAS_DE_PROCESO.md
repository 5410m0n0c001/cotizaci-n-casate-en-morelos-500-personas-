# BRIEF 8 — Reglas de proceso (OBLIGATORIAS) + orden de trabajo

El intento anterior falló: el agente revirtió `index.html` a la versión de git (se perdió el trabajo del Brief 5) y pasó
40 minutos generando scripts de 100–200 KB que nunca terminaron. Para evitarlo:

1. **Nunca ejecutes comandos git** (ni checkout, ni stash, ni restore). No toques `.git`.
2. **Edita `index.html` en su lugar**, por bloques, con reemplazos pequeños y verificables. No generes el archivo desde
   un script gigante ni lo reconstruyas desde `index_original_tsunum_ana.html`.
3. **Guarda progreso**: después de terminar cada parte (5 → 7A → 7B → 6), guarda `index.html`, ejecuta `node --check`
   sobre el script inline y anota en `REPORTE_ANTIGRAVITY_8.md` qué parte quedó terminada. Si algo falla, el archivo
   debe quedar siempre funcional.
4. Scripts auxiliares (si los necesitas) van en la carpeta `scratch/` y deben ser pequeños (< 10 KB). Bórralos al final.
5. Tiempo objetivo: 25 minutos. Si una parte no sale, déjala documentada como pendiente y sigue con la siguiente.

## Orden de trabajo
A. `BRIEF_ANTIGRAVITY_5_COMPARATIVO_PAQUETES.md` completo (paquete oficial vs. propuesta + grupos A/B por recinto, web y PDF),
   PERO usando ya los precios nuevos del Brief 7 en sus textos ($1,000 Tsú Nuum/Isabeles, $850 Presidente) en lugar de $1,900.
B. `BRIEF_ANTIGRAVITY_7_PRECIOS_Y_VENUES.md` partes A y B (precios por recinto dinámicos + Jardín La Villa y Jardín San Rafael).
C. `BRIEF_ANTIGRAVITY_6_MOVIL_ANIMACIONES.md` (pastillas pulsables en móvil con 5 recintos + animaciones en todas las secciones).
D. Verificación final (parte D del Brief 7) y `REPORTE_ANTIGRAVITY_8.md`.

Marcadores que DEBEN existir al final (los comprobaré con grep): "Paquete Oficial del Recinto vs. Esta Propuesta",
"Se agrega de más", "venue-lavilla", "venue-sanrafael", "PRECIOS", "lbl-corto", "pp-activo"; y cero: "1,900", "950,000".
