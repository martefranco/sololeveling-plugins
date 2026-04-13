# Revisión de Taxonomía y Granularidad de Áreas

Protocolo de validación que se ejecuta ANTES de crear carpetas de áreas, tanto en Modo A como en Modo B.

## Proceso

1. Presentar al usuario la lista completa de áreas funcionales propuestas como lista numerada.
2. Para cada área, verificar que el nombre represente exactamente **un dominio funcional**, siguiendo la regla de granularidad en `${CLAUDE_PLUGIN_ROOT}/skills/constructor-ontologia/references/estructura-ontologia.md`.
3. Si algún nombre contiene conjunciones (`y`, `e`, `,`, `/`) que sugieran dominios fusionados → marcarlo explícitamente, explicar la regla y proponer la división en áreas separadas.
4. Preguntar: "¿Confirmamos esta lista de áreas antes de continuar? Puedes ajustar cualquier nombre o agregar áreas adicionales."
5. Incorporar los cambios del usuario antes de avanzar a la creación de archivos.

**REGLA CRÍTICA**: NO avanzar a la creación de archivos hasta que el usuario confirme la lista de áreas validada.

## Ejemplos

| Propuesta del usuario | Evaluación | Acción |
|----------------------|------------|--------|
| "Finanzas" | ✅ Un dominio | Aceptar |
| "Ventas y Marketing" | ❌ Dos dominios fusionados | Proponer: "Ventas" + "Marketing" |
| "Operaciones, Logística y Legal" | ❌ Tres dominios fusionados | Proponer: "Operaciones" + "Logística" + "Legal" |
| "Atención al Cliente" | ✅ Un dominio | Aceptar |
