---
description: "Crear perfil de puesto via Intake Meeting"
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(ls:*)
---

Iniciar un Intake Meeting consultivo para crear un Perfil de Puesto.

Lee primero la skill `${CLAUDE_PLUGIN_ROOT}/skills/constructor-perfil/SKILL.md` y sigue el flujo definido ahí.

Pasos:
1. Verificar que existe la carpeta `data/` en el directorio de trabajo del usuario. Si no existe, sugerir ejecutar `/inicializar-talent-mx3` primero.
2. Leer `${CLAUDE_PLUGIN_ROOT}/skills/constructor-perfil/references/formato-perfil-core.md` para conocer los formatos de Core y Variación.
3. Leer `${CLAUDE_PLUGIN_ROOT}/skills/constructor-perfil/references/reglas-nomenclatura.md` para conocer el sistema de códigos SS-AA-PP-VV.
4. Consultar `${CLAUDE_PLUGIN_ROOT}/skills/plantillas-industria-mx/SKILL.md` para verificar si hay templates disponibles.
5. Si hay sectores definidos en `data/sectores/`, leer `data/indice.md` para tener contexto del sector.
6. Leer `data/registro.md` para conocer los códigos ya asignados.
7. Iniciar la conversación consultiva siguiendo el flujo de `constructor-perfil`:
   - Gancho: "¿Qué situación de negocio te lleva a buscar a alguien nuevo?"
   - Bloques A, B, C de preguntas
   - NO aceptar respuestas vagas — profundizar
8. Al terminar la recopilación, SEPARAR la información en dos documentos:
   - **Perfil Core** (7 secciones genéricas del rol) → guardar en `data/sectores/<sector-slug>/areas/<area-slug>/perfiles/PP-slug.md`
   - **Variación** (6 secciones contextuales) → guardar en `data/sectores/<sector-slug>/areas/<area-slug>/perfiles/variaciones/PP-VV-slug--contexto.md`
   - Si el usuario proporcionó contexto específico (proyecto, jefe, salario, métricas), generar AMBOS automáticamente.
9. Asignar códigos SS-AA-PP-VV consultando y actualizando `data/registro.md`.
10. Validar ambos documentos con las reglas de `${CLAUDE_PLUGIN_ROOT}/skills/validador-legal-mx/references/catalogo-reglas.md`.
11. Si se detectaron datos nuevos durante la conversación, agregar a `data/sectores/` siguiendo las reglas de `${CLAUDE_PLUGIN_ROOT}/skills/enriquecedor-ontologia/SKILL.md`.
12. Ofrecer enriquecimiento: benchmark salarial, persona del candidato, o guía de evaluación.

Los documentos generados deben estar en ESPAÑOL y reflejar el mercado mexicano.
