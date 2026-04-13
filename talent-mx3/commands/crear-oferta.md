---
description: "Generar oferta de empleo por plataforma"
allowed-tools: Read, Write, Edit, Glob, Grep
argument-hint: "<nombre-del-perfil> <plataforma>"
---

Generar una oferta de empleo profesional adaptada a una plataforma específica.

Lee `${CLAUDE_PLUGIN_ROOT}/skills/generador-oferta/SKILL.md` y sigue el flujo definido ahí.

Pasos:
1. Leer `${CLAUDE_PLUGIN_ROOT}/skills/constructor-perfil/references/reglas-nomenclatura.md` para la nomenclatura de archivos de ofertas.
2. Si el usuario proporcionó argumento ($ARGUMENTS), buscar primero en `data/sectores/*/areas/*/perfiles/variaciones/` y luego en `data/sectores/*/areas/*/perfiles/` (nivel raíz del área, excluyendo subcarpetas).
3. Si no proporcionó argumento, listar variaciones y perfiles disponibles en `data/sectores/` y pedir que elija. Recomendar usar una variación si existe.
4. Si el usuario elige un Core que tiene variaciones, sugerir: "Este perfil tiene variaciones con contexto específico. ¿Prefieres generar la oferta desde una variación?"
5. Preguntar plataforma(s) destino: OCC, LinkedIn, Computrabajo, Indeed, o todas.
6. Leer `${CLAUDE_PLUGIN_ROOT}/skills/generador-oferta/references/formula-8-pasos.md` para la fórmula.
7. Leer `${CLAUDE_PLUGIN_ROOT}/skills/generador-oferta/references/reglas-plataforma.md` para las reglas de cada canal.
8. Si hay benchmark salarial disponible, usarlo para el paso 7 de la fórmula.
9. Generar la(s) oferta(s) siguiendo los 8 pasos, adaptadas al tono y longitud de cada plataforma.
10. Validar con `${CLAUDE_PLUGIN_ROOT}/skills/validador-legal-mx/references/catalogo-reglas.md`.
11. Guardar cada oferta con nomenclatura correcta en `data/sectores/<sector>/areas/<area>/perfiles/ofertas/` (la ruta del sector y área se hereda del perfil o variación seleccionada).
12. Presentar resumen de ofertas generadas.

REGLA: No usar clichés como "empresa líder" o "salario competitivo" sin dato real.
