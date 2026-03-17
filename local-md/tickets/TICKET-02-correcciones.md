# TICKET-02: Correcciones

Descripción
- Aplicar las correcciones necesarias para que la lógica crítica de la página cargue desde `file://`.

Tareas
- Objetivo: aplicar la primera corrección en `augmented-coding-patterns.htm` para eliminar/reemplazar recursos absolutos (fuentes, preloads, favicon) y ajustar rutas relativas.
- Pasos propuestos:
	1. Localizar referencias absolutas (https://... o rutas que empiezan con `/`) en `augmented-coding-patterns.htm`.
	- `augmented-coding-patterns.htm`
		[x] Comentario guardado: `<!-- saved from url=(0056)https://lexler.github.io/augmented-coding-patterns/talk/ -->` (origina el base URL remoto). No es necesario modificarlo
		- Fuentes preload: `https://lexler.github.io/augmented-coding-patterns/_next/static/media/4cf2300e9c8272f7-s.p.woff2`, `https://lexler.github.io/augmented-coding-patterns/_next/static/media/93f479601ee12b01-s.p.woff2`.
		- Preloads de CSS (ejemplos): `https://lexler.github.io/augmented-coding-patterns/_next/static/css/89a280c72bec5701.css`, `https://lexler.github.io/augmented-coding-patterns/_next/static/css/dcaae7946540df67.css`, `https://lexler.github.io/augmented-coding-patterns/_next/static/css/e8ff6f0eb86cab82.css`, `https://lexler.github.io/augmented-coding-patterns/_next/static/css/dddbf12c77d8c6c6.css`.
		- Favicon: `https://lexler.github.io/augmented-coding-patterns/favicon.ico` (link rel="icon").
		- Navegación / enlaces: múltiples `href` apuntando a `https://lexler.github.io/augmented-coding-patterns/`:
			- `https://lexler.github.io/augmented-coding-patterns/` (logo / Home)
			- `https://lexler.github.io/augmented-coding-patterns/pattern-catalog/` (Complete Catalog)
			- `https://lexler.github.io/augmented-coding-patterns/obstacles/` (Obstacles)
			- `https://lexler.github.io/augmented-coding-patterns/anti-patterns/` (Anti-Patterns)
			- `https://lexler.github.io/augmented-coding-patterns/patterns/` (Patterns)
			- `https://lexler.github.io/augmented-coding-patterns/talk/` (Talk)
			- `https://lexler.github.io/augmented-coding-patterns/contributors/` (Contributors)
	2.- Añadir recursos faltantes en `augmented-coding-patterns_files/` (por ejemplo `maps/semantic_map.svg`).
	3. Sustituir por rutas relativas hacia `augmented-coding-patterns_files/` o eliminar los preloads no necesarios.
		- Modificar `augmented-coding-patterns.htm` para eliminar/reemplazar recursos absolutos y cambiar favicon a local.
	4. Documentar los cambios propuestos en este ticket antes de aplicar cualquier parche.[x] Localizar Referencias absolutas



- Corregir fetchs absolutos en bundles (`page-f5622273e356b20c.js.descarga` y otros) a rutas relativas o inlinear recursos faltantes.
	- Bundles JS (ej.: `augmented-coding-patterns_files/page-f5622273e356b20c.js.descarga` y su copia en `back/original/...`)
		- Llamada a fetch con ruta absoluta desde raíz: `fetch("".concat("/augmented-coding-patterns","/maps/semantic_map.svg"))` → intenta cargar `/augmented-coding-patterns/maps/semantic_map.svg` (ruta raíz, no relativa al archivo `file://`).
		- Uso de `fetch(e.canonicalUrl)` / llamadas a server-actions (p. ej. funciones que construyen URLs canónicas o usan headers de Next.js) — pueden originar peticiones a URLs externas o al endpoint canónico.

	- Otros recursos en bundles y polyfills
		- Referencias a `https://react.dev/errors/...` (enlaces de error minificado de React) y a URLs de proyectos (`https://github.com/...`) dentro de dependencias/minificados. No siempre cargadas como recursos, pero presentes en código.

	Impacto inmediato
	- Los `https://lexler.github.io/...` y las rutas que empiezan por `/` impedirán que la página cargue correctamente desde `file://` porque el navegador intentará resolver recursos en la web o en la raíz del host.
	- Las llamadas a `fetch` con rutas raíz o `e.canonicalUrl` pueden fallar o intentar contactar al servidor (Next.js server-actions). Estas deben ser adaptadas a rutas relativas o mockeadas/inlined cuando sea posible.
- Documentar limitaciones en `local-md/tickets/TICKET-02-correcciones.md` si persisten dependencias server-side.

Propuestas:



Entregables
- Ficheros HTML y assets corregidos en `augmented-coding-patterns.htm` y `augmented-coding-patterns_files/`.

Definition Of Done (DoD)
- Al abrir `file:///.../augmented-coding-patterns.htm` en Chrome, la página carga sin errores críticos de recursos faltantes (no 404 críticos en consola) y la UI principal es visible.
- La funcionalidad de los nodos se activa correctamente.
- Cambios documentados en este ticket con la lista de archivos editados.


Notas
- Evaluar si partes del runtime (Next.js server-actions) requieren servidor y documentarlo.


	Próximos pasos sugeridos
	- Reemplazar los `https://lexler.github.io/...` por rutas relativas a `augmented-coding-patterns_files/` (copiar/descargar las fuentes y CSS necesarios) o eliminar preloads no críticos.
	- Convertir `/augmented-coding-patterns/maps/semantic_map.svg` a `augmented-coding-patterns_files/maps/semantic_map.svg` y añadir el archivo.
	- Revisar bundles para detectar y adaptar llamadas a `fetch` que dependan de un servidor; documentar las que no puedan evitarse.