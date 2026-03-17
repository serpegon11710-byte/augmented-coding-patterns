# TICKET-04: Multi-idioma ES/EN

Descripción
- Añadir soporte de idioma ES/EN mediante recursos locales sin recompilar bundles.

Tareas
- Crear `i18n/es.json` y `i18n/en.json` en `augmented-coding-patterns_files/i18n/` o en `local-md/i18n/`.
- Implementar un pequeño script in-page que cargue y aplique textos desde JSON según `navigator.language` y un selector manual.
- Guardar la preferencia en `localStorage`.

Propuestas:
- Objetivo: crear `i18n/es.json` y `i18n/en.json` y añadir un script in-page que aplique textos sin recompilar bundles.
- Pasos propuestos:
	1. Añadir `augmented-coding-patterns_files/i18n/es.json` y `.../en.json` con pares clave/valor para los textos a sustituir.
	2. Insertar un pequeño script en el `head` o al final del `body` que:
		 - lea `localStorage` para preferencia de idioma;
		 - cargue el JSON correspondiente con `fetch` relativo (`./augmented-coding-patterns_files/i18n/es.json`);
		 - reemplace los textos de elementos identificados por `data-i18n` o por selectores acordados;
		 - exponga un selector UI para cambiar idioma y persistir la preferencia.
	3. Documentar las claves usadas y el mecanismo en este ticket antes de aplicar cambios.


Definition Of Done (DoD)
- El selector de idioma cambia los textos visibles entre ES/EN.
- La preferencia persiste en `localStorage`.
- Documentación y ejemplo de uso en este ticket.