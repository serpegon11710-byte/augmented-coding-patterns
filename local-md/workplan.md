# Workplan: Ejecutar "augmented-coding-patterns" desde file://

Resumen
- Objetivo: Permitir abrir `augmented-coding-patterns.htm` con Chrome usando `file://` sin servidor, o bien documentar y facilitar la opción de servirlo localmente.
- Estructura: tickets (Planificacion, Correcciones, Ruta Independiente, Multi-idioma) con Definition Of Done (DoD) para cada uno.

Tickets principales
1. Planificacion — `local-md/tickets/TICKET-01-planificacion.md`
2. Correcciones — `local-md/tickets/TICKET-02-correcciones.md`
3. Ruta Independiente — `local-md/tickets/TICKET-03-ruta-independiente.md`
4. Multi-idioma — `local-md/tickets/TICKET-04-multi-idioma.md`

Flujo de trabajo
- Crear una rama por ticket: `ticket/TICKET-<NN>-short-desc`.
- Commits atómicos en la rama del ticket.
- Se realizan commits atómicos bajo supervisión. No realizarlos automáticamente, puedes pueden haber ficheros pendientes de validar los cambios.
- No se marcarán tareas como completadas sin confirmación explícita del responsable.
- Se realizarán PRs una vez que la tarea esté completada y haya superado el DoD.
- Los ficheros de la carpeta back no se modifican
- Antes de reemplazar rutas hay que verificar que el fichero exista en "augmented-coding-patterns_files"
- Las descargas se harán directamente en "augmented-coding-patterns_files" (sin subcarpetas)
- Las rutas en el fichero 
"augmented-coding-patterns.htm" apuntarán a "./augmented-coding-patterns_files/<archivo>"
- Las rutas en los ficheros CSS
 apuntarán a "./<archivo>"
- Las rutas en los JS son susceptibles de análisis. En principio apuntarán a "./augmented-coding-patterns_files/<archivo>"