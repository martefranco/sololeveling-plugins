---
description: "Flujo completo: perfil, variaciones y ofertas"
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(ls:*)
---

Ejecutar el flujo completo de Talent Acquisition en una sola sesión.

Este command orquesta todos los pasos del proceso:

**PASO 1 — Crear Perfil Core + Variación**
Ejecutar el flujo completo de `/crear-perfil` (lee `${CLAUDE_PLUGIN_ROOT}/skills/constructor-perfil/SKILL.md`).
El Intake Meeting recopila toda la información y la separa automáticamente en:
- Perfil Core (genérico del rol, 7 secciones)
- Variación (contexto específico, 6 secciones)
Ambos documentos se generan con nomenclatura SS-AA-PP y SS-AA-PP-VV (el nombre de archivo usa solo PP y VV; SS y AA quedan implícitos en la ruta del directorio).
Al terminar, preguntar si los documentos son satisfactorios antes de continuar.

**PASO 1.5 — Enriquecer (opcional)**
"¿Quieres complementar el perfil con:
a) Benchmark salarial para este puesto
b) Retrato del candidato ideal
c) Guía de evaluación para entrevistas
d) Todos
e) No por ahora"

Si elige opciones → ejecutar las skills correspondientes:
- (a) o (d): Leer `${CLAUDE_PLUGIN_ROOT}/skills/benchmark-salarial-mx/SKILL.md`
- (b) o (d): Leer `${CLAUDE_PLUGIN_ROOT}/skills/generador-persona-candidato/SKILL.md`
- (c) o (d): Leer `${CLAUDE_PLUGIN_ROOT}/skills/constructor-evaluacion/SKILL.md`

**PASO 2 — Variaciones adicionales (opcional)**
"¿Necesitas otra variación de este mismo perfil para otro cliente, proyecto o especialidad?"
Si sí → ejecutar flujo de variación (puede repetirse N veces, cada una con su código VV).
Si no → saltar al paso 3.

**PASO 3 — Ofertas de empleo**
Para cada variación creada, preguntar: "¿En qué plataformas quieres publicar?"
Ejecutar `generador-oferta` para cada combinación variación × plataforma.

**PASO 4 — Resumen final**
Presentar resumen completo:
- Perfil Core creado (código SS-AA-PP en registro; archivo nombrado con PP)
- Variaciones creadas (códigos SS-AA-PP-VV en registro; archivos nombrados con PP-VV)
- Enriquecimientos generados (benchmark, persona, evaluación)
- Ofertas generadas (por variación y plataforma)
- Hallazgos de compliance
- Registro actualizado en `data/registro.md`

Objetivo: completar todo en < 30 minutos para un Core + 1 variación + 2 ofertas.
