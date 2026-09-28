# 🧠 Obsidian - Personal Knowledge Graph (Automated)

Obsidian es utilizado en este entorno no solo como un editor de Markdown, sino como la **base de datos local** de un sistema automatizado de captura de ideas (Personal Knowledge Graph).

## Arquitectura del Sistema
El ecosistema completo está diseñado para funcionar de manera silenciosa y bidireccional:
1. **Entrada Móvil:** Notas de voz y texto enviadas a un Bot de Telegram.
2. **Procesamiento en la Nube:** n8n recibe el webhook, usa Whisper para transcribir el audio, y un LLM para dar formato y clasificar la nota.
3. **Almacenamiento Git:** n8n sube el documento final a un repositorio privado de GitHub.
4. **Sincronización Local:** Obsidian, instalado en el PC (Linux), utiliza el plugin `obsidian-git` para hacer *pull* y *push* en segundo plano cada 15 minutos, manteniendo la bóveda local sincronizada sin intervención humana.

## Estructura de Carpetas Recomendada (Orientada a la Acción)
Para evitar la fricción y facilitar la automatización, la bóveda usa esta jerarquía de 4 pilares:

- **`01-Proyectos/`**: Trabajo activo y metas. Cada proyecto tiene internamente:
  - `Documentacion/`
  - `Por_hacer/`
  - `Terminado/`
- **`02-Conocimiento/`**: Biblioteca continua (Desarrollo, DevOps, Idiomas, Repaso).
- **`03-Bandeja_de_Entrada/`**: Punto de aterrizaje automático. Todas las notas de n8n/Telegram caen aquí primero para ser clasificadas después.
- **`04-Papelera/`**: Archivo inactivo (Almacenamiento en frío).

## Restricciones y Reglas
- **Nunca usar contraseñas HTTPS para Git:** El repositorio debe conectarse estrictamente por SSH (`git@github.com...`). Si se usa HTTPS, el *push* en segundo plano fallará silenciosamente porque el hilo no puede pedir contraseña al usuario.
- **Sin Carpetas Vacías:** Git no rastrea carpetas vacías. Siempre inyectar un `README.md` explicativo al crear una nueva categoría.
