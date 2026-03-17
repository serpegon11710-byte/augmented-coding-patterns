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
