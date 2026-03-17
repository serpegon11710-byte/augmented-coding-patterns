# TICKET-02: Correcciones

Descripción
- Aplicar las correcciones necesarias para que la lógica crítica de la página cargue desde `file://`.
# TICKET-02: Correcciones

Resumen
-------
Objetivo: permitir que la lógica crítica de la página cargue desde `file://`, o bien documentar exactamente qué necesita servidor.

Estado de tareas
-----------------
- Completadas
  - Reformateo y edición de `augmented-coding-patterns.htm` para apuntar a assets locales.
  - Renombrado y unificación de `*.js.descarga` → `*.js` (commits locales realizados).
  - Documentación inicial de hallazgos añadida a este ticket.

- Pendientes
  - Copiar assets faltantes a `augmented-coding-patterns_files/` (fuentes y `maps/semantic_map.svg`).
  - Revisar y, si procede, parchear bundles minificados (`webpack-cd040e31edf92b00.js`, etc.) para eliminar `publicPath` absoluto.
  - Probar `file://` en Chrome y reportar errores de consola; decidir limpieza (eliminar wrappers/archivos obsoletos) tras las pruebas.

Hallazgos clave
---------------
- CSS fonts
  - Archivo: `augmented-coding-patterns_files/886ee8d28508f25a.css`
  - Problema: múltiples `@font-face` usan `src:url(/augmented-coding-patterns/_next/static/media/<archivo>.woff2)` (ruta absoluta desde la raíz).
  - Recomendación: copiar los `.woff2` referenciados a `augmented-coding-patterns_files/` y reescribir las URLs a rutas relativas `./augmented-coding-patterns_files/<archivo>.woff2`.

- PublicPath en bundles
  - Archivo: `augmented-coding-patterns_files/webpack-cd040e31edf92b00.js`
  - Problema: contiene `r.p="/augmented-coding-patterns/_next/"` — los chunks se cargarán desde la raíz y fallarán con `file://`.
  - Recomendación: si se necesita soporte `file://`, reescribir `r.p` a `"./"` o ajustar rutas (hacer copia de seguridad del bundle antes; riesgo en minificados).

- Fetch absoluto (mapa)
  - Archivo: `augmented-coding-patterns_files/page-f5622273e356b20c.js`
  - Problema: `fetch("/augmented-coding-patterns/maps/semantic_map.svg")` fallará desde `file://`.
  - Recomendación: copiar `semantic_map.svg` a `augmented-coding-patterns_files/maps/` y cambiar la llamada a fetch por una ruta relativa, o inlinear el SVG.

- BasePath en runtime
  - Archivo: `augmented-coding-patterns_files/255-466fbc12e2ae9324.js`
  - Problema: contiene `addBasePath/removeBasePath/hasBasePath` usando `"/augmented-coding-patterns"` — la app construye rutas con ese prefijo en tiempo de ejecución.
  - Recomendación: neutralizar o parchear estas utilidades para usar rutas relativas, o servir por HTTP.

Ficheros sugeridos a añadir
---------------------------
- `augmented-coding-patterns_files/maps/semantic_map.svg`
- Fuentes `.woff2` referenciadas en el CSS (copiar localmente)

Impacto
-------
- Sin correcciones, la página no carga correctamente desde `file://` (404s y fallos de fetch).
- Algunas funcionalidades (mapa interactivo y carga de chunks) dependen de reescrituras o de servir mediante HTTP.

Opciones de solución (priorizadas)
----------------------------------
- Opción 1 — Parchear para `file://` (más trabajo, sin servidor)
  1. Copiar assets faltantes a `augmented-coding-patterns_files/`.
  2. Reescribir en CSS las URLs de `/_next/static/media/` a `./augmented-coding-patterns_files/`.
  3. Cambiar `fetch("/augmented-coding-patterns/maps/semantic_map.svg")` a ruta relativa o inlinear el SVG.
  4. Revisar `webpack` bundle `r.p` y, si procede, reescribir a `"./"` (hacer copia de seguridad antes).

- Opción 2 — Servir la carpeta localmente (menos invasiva)
  - Ejecutar: `npx http-server . -p 8080` o `python -m http.server 8080` desde el root y abrir `http://localhost:8080/augmented-coding-patterns.htm`.

Comandos sugeridos (PowerShell)
-------------------------------
```
New-Item -ItemType Directory -Force -Path .\augmented-coding-patterns_files\maps
Copy-Item -Path <ruta_del_svg> -Destination .\augmented-coding-patterns_files\maps\semantic_map.svg
(Get-Content .\augmented-coding-patterns_files\886ee8d28508f25a.css) -replace '/augmented-coding-patterns/_next/static/media/', './augmented-coding-patterns_files/' | Set-Content .\augmented-coding-patterns_files\886ee8d28508f25a.css
git add -A
git commit -m "TICKET-02: Localizar assets y reescribir rutas para file://"
```

Notas y restricciones
---------------------
- No modificar la carpeta `back/` (restaurada por el usuario desde Git).
- Hacer copia de seguridad (`.bak`) antes de editar bundles minificados.

Siguiente paso propuesto
------------------------
Indica la preferencia:

- Si quieres trabajar sin servidor: doy el patch automático (Opción 1) y muestro un diff antes de commitear.
- Si prefieres evitar cambios en bundles: te preparo los comandos para servir localmente (Opción 2) y una checklist de verificación.

---

Documentado y reorganizado por el equipo el 2026-03-17.

**Comandos sugeridos (PowerShell) — ejemplo**
```
New-Item -ItemType Directory -Force -Path .\augmented-coding-patterns_files\maps
Copy-Item -Path <ruta_del_svg> -Destination .\augmented-coding-patterns_files\maps\semantic_map.svg
(Get-Content .\augmented-coding-patterns_files\886ee8d28508f25a.css) -replace '/augmented-coding-patterns/_next/static/media/', './augmented-coding-patterns_files/' | Set-Content .\augmented-coding-patterns_files\886ee8d28508f25a.css
git add -A
git commit -m "TICKET-02: Localizar assets y reescribir rutas para file://"
```

Si quieres, genero el parche listo para aplicar o ejecuto los cambios (no tocaré `back/`).