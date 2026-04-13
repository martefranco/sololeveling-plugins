---
description: "Generar guia de entrevista basada en perfil"
allowed-tools: Read, Write, Edit, Glob, Grep
argument-hint: "<nombre-del-perfil>"
---

Generar una guía de evaluación para entrevistas basada en un Perfil Core y opcionalmente su Variación.

Lee `${CLAUDE_PLUGIN_ROOT}/skills/constructor-evaluacion/SKILL.md` y sigue el flujo definido ahí.

Pasos:
1. Si el usuario proporcionó argumento `$ARGUMENTS`, buscar el perfil en `data/sectores/` (buscando en `data/sectores/*/areas/*/perfiles/*.md`).
2. Si no, listar perfiles disponibles en `data/sectores/` y pedir que elija.
3. Cargar el Perfil Core. Las secciones clave son:
   - Core sección 3 (competencias técnicas) → preguntas técnicas
   - Core sección 4 (competencias conductuales) → preguntas STAR
   - Core sección 6 (must-haves) → checklist de verificación
4. Si existe Variación para este Core, cargarla también:
   - Variación sección 3 (microcultura) → preguntas de fit cultural
   - Variación sección 4 (métricas) → escenarios prácticos
   - Variación sección 5 (competencias adicionales) → preguntas adicionales
5. Si existe persona del candidato (`*--persona-candidato.md`), cargarla para la sección de red flags.
6. Leer `${CLAUDE_PLUGIN_ROOT}/skills/constructor-evaluacion/references/formato-guia-evaluacion.md` para el formato.
7. Generar:
   - Scorecard con pesos ajustables (técnico 50%, conductual 30%, fit 20%)
   - 1-2 preguntas técnicas por competencia de Core sección 3
   - 1 pregunta STAR por competencia conductual de Core sección 4
   - Checklist de verificación de must-haves de Core sección 6
   - 2-3 preguntas de fit cultural basadas en Variación sección 3 (si existe)
   - Escenario práctico (opcional, recomendado para roles operativos)
   - Preparación de respuestas para preguntas del candidato
8. Validar con `${CLAUDE_PLUGIN_ROOT}/skills/validador-legal-mx/references/catalogo-reglas.md` (reglas EVAL-*).
9. Guardar en `data/sectores/<sector>/areas/<area>/perfiles/` con nomenclatura consistente (la ruta del sector y área se hereda del perfil seleccionado).
