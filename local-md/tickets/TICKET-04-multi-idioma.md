# TICKET-04: Multi-idioma ES/EN

Descripción
- Añadir soporte de idioma ES/EN mediante recursos locales sin recompilar bundles.

Tareas
- Crear `i18n/es.json` y `i18n/en.json` en `augmented-coding-patterns_files/i18n/` o en `local-md/i18n/`.
- Implementar un pequeño script in-page que cargue y aplique textos desde JSON según `navigator.language` y un selector manual.
- Guardar la preferencia en `localStorage`.

Definition Of Done (DoD)
- El selector de idioma cambia los textos visibles entre ES/EN.
- La preferencia persiste en `localStorage`.
- Documentación y ejemplo de uso en este ticket.
