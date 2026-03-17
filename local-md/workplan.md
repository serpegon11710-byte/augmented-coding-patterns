# Workplan: Ejecutar "augmented-coding-patterns" desde file://

Resumen
- Objetivo: Permitir abrir `augmented-coding-patterns.htm` con Chrome usando `file://` sin servidor, o bien documentar y facilitar la opción de servirlo localmente.
- Estructura: tickets (Planificacion, Correcciones, Ruta Independiente, Multi-idioma) con Definition Of Done (DoD) para cada uno.

Tickets principales
1. Planificacion — `local-md/tickets/TICKET-01-planificacion.md`
2. Correcciones — `local-md/tickets/TICKET-02-correcciones.md`
3. Ruta Independiente — `local-md/tickets/TICKET-03-ruta-independiente.md`
4. Multi-idioma — `local-md/tickets/TICKET-04-multi-idioma.md`

Entregables
- `local-md/` con tickets y documentación.
- `local-py/` y `local-ps/` para scripts auxiliares.
- Ficheros HTML y assets corregidos en `augmented-coding-patterns.htm` y `augmented-coding-patterns_files/`.

Flujo de trabajo
- Crear una rama por ticket: `ticket/TICKET-<NN>-short-desc`.
- Commits atómicos en la rama del ticket.
- PR solo cuando la tarea esté verificada y validada.

Verificación final
- Abrir `file:///.../augmented-coding-patterns.htm` en Chrome.
- No 404 críticos ni errores fatales en consola.
- Documentar limitaciones en `local-md/tickets/TICKET-02-correcciones.md` si persisten dependencias server-side.

Fecha: 2026-03-17
