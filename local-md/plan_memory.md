## Plan actual (memoria de sesión)

## Plan: Hacer correr "augmented-coding-patterns" desde file://

TL;DR - Qué y por qué
- Objetivo: permitir ejecutar localmente la página descargada desde `file://` (Chrome), sin servidor HTTP, o bien documentar y preparar la opción alternativa de servirla localmente.
- Enfoque recomendado: documentar y ejecutar en fases; preferible usar un servidor estático cuando sea viable; si se exige `file://`, aplicar parches puntuales (HTML y bundles) y aceptar limitaciones en funcionalidades server-side.

**Steps**
1. Discovery (completado): inventario de archivos y puntos problemáticos (ver hallazgos).
2. Fase 1 — Planificación (esta tarea): crear estructura de trabajo, tickets y reglas de ramas, documentación `workplan.md`.
3. Fase 2 — Correcciones esenciales:
   3.1. Editar `augmented-coding-patterns.htm`: eliminar/reemplazar recursos absolutos, cambiar favicon, ajustar preloads.
   3.2. Corregir fetches absolutos en bundles: `page-f5622273e356b20c.js.descarga` (semantic_map.svg) -> ruta relativa o inline.
   3.3. Preparar carpeta `augmented-coding-patterns_files/maps/` con recursos faltantes (SVG, imágenes).
   3.4. Evaluar `255-466fbc12e2ae9324.js.descarga` (Next.js runtime / server actions): decidir entre mantener (requiere servidor) o intentar neutralizar llamadas (riesgo alto).
4. Fase 3 — Hacer la página independiente de la ruta:
   4.1. Reemplazar rutas absolutas root (`/...`) por rutas relativas basadas en ubicación del HTML.
   4.2. Añadir fallback de routing (hash-based) si el app usa pushState y no hay servidor.
   4.3. Probar en múltiples ubicaciones locales (rutas con espacios, rutas profundas) y corregir enlaces relativos.
5. Fase 4 — FEATURE EXTRA: multi-idioma ES/EN
   5.1. Detectar idioma del navegador y proporcionar selector manual.
   5.2. Implementar un simple loader de strings JSON local (`i18n/es.json`, `i18n/en.json`) y punto de entrada en `main-app-*.js` o mediante un pequeño script in-page que reemplace textos estáticos.
   5.3. Añadir tests manuales de alternancia y persistencia (localStorage).
6. Entrega y verificación:
   6.1. Verificar apertura por `file://` en Chrome sin errores críticos (consola limpia de 404 que impidan la UI).
   6.2. Documentar limitaciones (RSC/server-actions, formularios POST que dependen del servidor).

**Estructura de ficheros/artefactos a crear**
- `local-md/` — Todos los ficheros `.md` necesarios (documentación, tickets en formato Markdown).
- `local-py/` — Scripts `.py` auxiliares (por ejemplo, generador de rutas relativas, helper para convertir recursos absolutos a relativos).
- `local-ps/` — Scripts `.ps` (PowerShell) para Windows útiles para pruebas y comandos locales.
- `workplan.md` — Documento principal de trabajo (resumen del plan, decisiones, checklist de tareas).
- Cada tarea tendrá su ticket en `local-md/tickets/` como `TICKET-<NN>-short-title.md`.

**Archivos identificados para edición (discovery)**
- `augmented-coding-patterns.htm` — actualizar referencias externas y preloads.
- `augmented-coding-patterns_files/page-f5622273e356b20c.js.descarga` — cambiar fetch de `"/augmented-coding-patterns/maps/semantic_map.svg"` por ruta relativa o inline.
- `augmented-coding-patterns_files/255-466fbc12e2ae9324.js.descarga` — contiene runtime con server-actions; requiere decisión (host vs patch).
- Posible creación: `augmented-coding-patterns_files/maps/semantic_map.svg` si está disponible o conversión a inline.

**Verification**
1. Abrir `file:///.../augmented-coding-patterns.htm` en Chrome y comprobar consola:
   - No 404 en recursos locales corregidos.
   - No excepciones fatales que impidan render.
2. Verificar que la UI principal se muestra y la navegación básica funciona (clicks, cambio de vistas).
3. Probar alternancia ES/EN: cambiar idioma y comprobar textos y persistencia.
4. Documentar cualquier funcionalidad que requiera un servidor (formularios, server-actions) en `local-md/tickets/TICKET-XX-server-limits.md`.

**Decisiones / Suposiciones**
- Preferencia: usar servidor local cuando sea posible porque Next.js runtime y server actions no son triviales de neutralizar.
- Si la exigencia es estricta `file://`, aceptamos que algunas funcionalidades (POSTs, RSC) quedarán fuera de alcance o se simularán con stubs.

---
Fecha: 2026-03-17
