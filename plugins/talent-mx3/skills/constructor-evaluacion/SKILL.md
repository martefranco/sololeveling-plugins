---
name: constructor-evaluacion
description: >
  Genera guías de entrevista y criterios de evaluación coherentes con el Perfil Core. Cada pregunta evalúa una competencia específica del perfil — no es un cuestionario genérico. Incluye scorecard, preguntas STAR para conductuales, verificación de must-haves, escenarios prácticos, y preparación para preguntas del candidato. Triggers: "guía de entrevista", "crear evaluación", "cómo evaluar candidatos", "preguntas de entrevista", "scorecard", "rúbrica de evaluación", "criterios de evaluación", "preparar entrevista".
---

# Constructor de Evaluación

Generar guías de entrevista estructuradas y scorecards de evaluación basados en el Perfil Core, con preguntas vinculadas a competencias específicas.

## Principio

Cada pregunta DEBE estar vinculada a una competencia del perfil. No incluir preguntas genéricas que no evalúen algo específico del puesto.

## Input

- Perfil Core completo (7 secciones). Secciones clave: 3, 4, 6
- Variación (6 secciones, opcional). Secciones clave: 3, 4, 5
- Persona del candidato (opcional — para red flags)
- Benchmark salarial (no necesario — el salario no se evalúa en entrevista)

## Flujo

1. Recibir Perfil Core. Si existe Variación, cargarla también.

2. Analizar secciones clave:
   - Core sección 3 (competencias técnicas) → preguntas de validación técnica
   - Core sección 4 (competencias conductuales) → preguntas STAR
   - Core sección 6 (must-haves) → verificaciones obligatorias
   - Variación sección 3 (microcultura) → preguntas de fit cultural (si existe)
   - Variación sección 4 (métricas) → escenarios de evaluación (si existe)
   - Variación sección 5 (competencias adicionales) → preguntas complementarias (si existe)

3. Si existe persona del candidato → usar sección f (red flags) para preguntas trampa

4. Generar guía con formato en `references/formato-guia-evaluacion.md`

5. Invocar `validador-legal-mx` para verificar que ninguna pregunta sea discriminatoria

6. Presentar: "Generé la guía de evaluación para [título] con [N] preguntas técnicas, [N] conductuales, [N] de fit, y 1 escenario práctico."

7. Guardar en `data/perfiles/`: `YYYY-MM-DD-titulo-slug--guia-evaluacion.md`

## Reglas

- Método STAR es OBLIGATORIO para conductuales
- NO preguntar sobre edad, estado civil, embarazo, religión, orientación sexual
- Incluir siempre "qué buscar en la respuesta" para cada pregunta
- Escenario práctico es OPCIONAL pero recomendado para roles operativos
- Si hay persona del candidato, usar objeciones para preparar respuestas al entrevistador
