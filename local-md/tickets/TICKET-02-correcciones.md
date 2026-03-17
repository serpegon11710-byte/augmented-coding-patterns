# TICKET-02: Correcciones

Descripción
- Aplicar las correcciones necesarias para que la lógica crítica de la página cargue desde `file://`.

Tareas
- Modificar `augmented-coding-patterns.htm` para eliminar/reemplazar recursos absolutos y cambiar favicon a local.
- Corregir fetchs absolutos en bundles (`page-f5622273e356b20c.js.descarga` y otros) a rutas relativas o inlinear recursos faltantes.
- Añadir recursos faltantes en `augmented-coding-patterns_files/` (por ejemplo `maps/semantic_map.svg`).
- Documentar limitaciones en `local-md/tickets/TICKET-02-correcciones.md` si persisten dependencias server-side.

Propuestas:
- Objetivo: aplicar la primera corrección en `augmented-coding-patterns.htm` para eliminar/reemplazar recursos absolutos (fuentes, preloads, favicon) y ajustar rutas relativas.
- Pasos propuestos:
	1. Localizar referencias absolutas (https://... o rutas que empiezan con `/`) en `augmented-coding-patterns.htm`.
	2. Sustituir por rutas relativas hacia `augmented-coding-patterns_files/` o eliminar los preloads no necesarios.
	3. Documentar los cambios propuestos en este ticket antes de aplicar cualquier parche.


Entregables
- Ficheros HTML y assets corregidos en `augmented-coding-patterns.htm` y `augmented-coding-patterns_files/`.

Definition Of Done (DoD)
- Al abrir `file:///.../augmented-coding-patterns.htm` en Chrome, la página carga sin errores críticos de recursos faltantes (no 404 críticos en consola) y la UI principal es visible.
- La funcionalidad de los nodos se activa correctamente.
- Cambios documentados en este ticket con la lista de archivos editados.


Notas
- Evaluar si partes del runtime (Next.js server-actions) requieren servidor y documentarlo.

