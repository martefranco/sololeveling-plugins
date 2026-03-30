---
description: "Cargar conocimiento de industria a la ontologia"
allowed-tools: Read, Write, Edit, Glob, Grep
---

Guiar al usuario en la construcción intencional de conocimiento para la ontología de talent-mx3.

Lee `${CLAUDE_PLUGIN_ROOT}/skills/constructor-ontologia/SKILL.md` y sigue el flujo definido ahí.

Pasos:
1. Verificar que existe `data/ontologia/`. Si no existe, sugerir ejecutar `/inicializar-talent-mx3` primero.
2. Leer `data/ontologia/indice.md` para saber qué ya existe.
3. Leer `data/registro.md` para conocer los códigos SS y AA ya asignados.
4. Leer `${CLAUDE_PLUGIN_ROOT}/skills/constructor-ontologia/references/estructura-ontologia.md` para conocer los formatos.
5. Preguntar: "¿Sobre qué industria o área funcional quieres construir conocimiento?"
6. Según la respuesta:
   - **Nueva industria** → asignar siguiente código SS, guiar la creación de una rama completa en `data/ontologia/sectores/<nuevo-sector>/`
   - **Área funcional en sector existente** → asignar siguiente código AA dentro del sector, agregar a `data/ontologia/sectores/<sector>/areas/`
   - **Enriquecer existente** → agregar datos sin duplicar ni cambiar códigos
7. Recopilar información: roles, herramientas, competencias, certificaciones, normativas.
8. Clasificar usando reglas de `${CLAUDE_PLUGIN_ROOT}/skills/enriquecedor-ontologia/references/reglas-clasificacion.md`.
9. Crear/actualizar archivos .md en la ontología.
10. Actualizar `data/ontologia/indice.md` con las nuevas entradas.
11. Actualizar `data/registro.md` con los nuevos códigos SS y/o AA asignados.
12. Reportar: "Agregué X competencias, Y herramientas, Z certificaciones al sector [nombre]. Código SS=[X], nuevas áreas AA=[Y]."
