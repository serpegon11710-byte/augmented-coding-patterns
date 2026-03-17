# TICKET-03: Ruta Independiente

Descripción
- Hacer que la página funcione correctamente desde cualquier ruta local (sin asumir root `/`).

Tareas
- Reemplazar rutas absolutas que comienzan con `/` por rutas relativas calculadas respecto a la ubicación del HTML.
- Implementar fallback hash-based para navegación si la app usa `pushState` y no hay servidor.
- Probar desde distintas rutas locales (carpetas con espacios, rutas profundas).

Definition Of Done (DoD)
- Abrir el HTML desde al menos 3 rutas locales distintas y confirmar que la navegación básica y enlaces funcionan.
- Registrar pruebas y resultados en este ticket.

Propuesta:
- Objetivo: añadir un README con comandos para servir la carpeta localmente (recomendado) y documentar los pasos de prueba.
- Pasos propuestos:
	1. Crear `README.md` con al menos estas opciones: `python -m http.server`, `npx serve .`, y `powershell` ejemplo para Windows.
	2. Documentar comandos y ejemplos de uso para probar la app sobre HTTP local.
	3. Incluir notas sobre por qué servir por HTTP es preferible (Next.js runtime, server-actions, CORS, rutas absolutas).

