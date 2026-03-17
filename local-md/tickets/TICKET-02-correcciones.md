# TICKET-02: Correcciones

Descripción
- Aplicar las correcciones necesarias para que la lógica crítica de la página cargue desde `file://`.

Tareas
- Modificar `augmented-coding-patterns.htm` para eliminar/reemplazar recursos absolutos y cambiar favicon a local.
- Corregir fetchs absolutos en bundles (`page-f5622273e356b20c.js.descarga` y otros) a rutas relativas o inlinear recursos faltantes.
- Añadir recursos faltantes en `augmented-coding-patterns_files/` (por ejemplo `maps/semantic_map.svg`).

Definition Of Done (DoD)
- Al abrir `file:///.../augmented-coding-patterns.htm` en Chrome, la página carga sin errores críticos de recursos faltantes (no 404 críticos en consola) y la UI principal es visible.
- Cambios documentados en este ticket con la lista de archivos editados.

Notas
- Evaluar si partes del runtime (Next.js server-actions) requieren servidor y documentarlo.
