---
name: constructor-perfil
description: >
  Digitaliza y potencia el Intake Meeting — el proceso consultivo donde se define el perfil real de un puesto de trabajo. Usar SIEMPRE que el usuario quiera crear un perfil de puesto, definir una vacante, entender qué tipo de persona necesita contratar, o iniciar un proceso de reclutamiento. También maneja la lógica de herencia para crear variaciones. Triggers: "crear perfil", "nuevo puesto", "necesito contratar", "abrir vacante", "definir puesto", "intake meeting", "qué perfil necesito", "crear variación", "variación para", "adaptar perfil".
---

# Constructor de Perfil — Intake Meeting Potenciado por IA

Guiar al usuario a través de una entrevista consultiva para generar un Perfil de Puesto, separando automáticamente el conocimiento genérico del rol (Core) del contexto específico de la contratación (Variación).

## Principio fundamental

**"Entender, no buscar."** NO empezar pidiendo un título de puesto. Empezar preguntando qué problema de negocio lleva al usuario a buscar a alguien nuevo.

## Modo de operación

Esta skill opera en dos modos:

### Modo 1: Crear Perfil (vía `/crear-perfil`)

Flujo conversacional completo. Genera un Perfil Core genérico y, si el usuario proporcionó contexto específico, también una Variación.

### Modo 2: Crear Variación (vía `/crear-variacion`)

Tomar un Perfil Core existente y generar una variación para un cliente, proyecto o especialidad.

---

## MODO 1: Flujo del Intake Meeting

### Gancho inicial

NO preguntar: "¿Qué puesto necesitas?"
SÍ preguntar: **"¿Qué situación de negocio te lleva a buscar a alguien nuevo?"**

Alternativas del gancho:
- "¿Qué problema estás tratando de resolver con esta contratación?"
- "¿Qué cambió en tu operación que necesitas a alguien más?"

### Consultar template

Antes de profundizar, buscar si existe un template relevante en `plantillas-industria-mx`:
- Si el contexto del usuario coincide con un template → ofrecer: "Tengo una base para [tipo de rol] en [sector]. ¿Quieres que la usemos como punto de partida?"
- Si el usuario acepta → cargar template y personalizar
- Si no hay template o el usuario rechaza → construir desde cero

### Bloque A: Rol y Tareas (5-7 preguntas)

1. Contexto del puesto: ¿Es reemplazo o posición nueva? ¿Qué motivó la necesidad?
2. Tareas del día a día: "Si pudieras ver a esta persona trabajando un martes cualquiera, ¿qué estaría haciendo?"
3. Herramientas: "¿Con qué software, equipos o herramientas trabajaría?"
4. Resultados esperados: "¿Cómo sabrías que esta persona está haciendo bien su trabajo en los primeros 3 meses?"
5. Interacciones: "¿Con quién interactúa? ¿Clientes? ¿Otros equipos?"
6. Reporta a: "¿A quién le reporta y cómo es esa relación?"
7. Sector e industria: Inferir del contexto o preguntar si no es claro

### Bloque B: Contexto del Equipo / Microcultura (3-5 preguntas)

8. Equipo actual: "Cuéntame sobre el equipo donde entraría esta persona. ¿Cuántos son? ¿Cómo trabajan?"
9. Tipo de persona que florece: "¿Qué tipo de persona funciona bien en tu equipo?"
10. Tipo de persona que NO funciona: "¿Has tenido contrataciones que no funcionaron? ¿Qué pasó?"
11. Estilo de liderazgo: "¿Cómo es tu estilo como líder? ¿Supervisión cercana o autonomía?"
12. Ambiente: Horarios, ritmo de trabajo, presión, formalidad

### Bloque C: Requisitos y Compliance (3-5 preguntas)

13. Formación: "¿Necesitas un título específico o lo que importa es la experiencia?"
14. Experiencia: "¿Cuánta experiencia mínima necesitas? ¿En qué específicamente?"
15. Certificaciones: "¿Hay alguna certificación o licencia obligatoria?"
16. Must-have vs nice-to-have: **"De todo lo que hemos hablado, ¿qué es absolutamente esencial y qué sería deseable pero no indispensable?"**
17. Condiciones: Jornada, zona de trabajo, disponibilidad para viajar, trabajo en campo

### Reglas de conversación

Leer `${CLAUDE_PLUGIN_ROOT}/skills/constructor-perfil/references/flujo-conversacional.md` para tono, ritmo y técnicas de profundización.

### Generación del output — Separación Core / Variación

Después de recopilar información, leer `${CLAUDE_PLUGIN_ROOT}/skills/constructor-perfil/references/formato-perfil-core.md` para reglas de separación y formatos de ambos documentos.

**Paso crítico:** Clasificar cada dato recopilado como genérico del ROL o específico de ESTA contratación usando la tabla de clasificación en formato-perfil-core.md.

**Regla:** Si el usuario proporcionó datos específicos (proyecto, jefe directo, salario concreto, métricas a 30/90 días), generar AMBOS documentos automáticamente sin preguntar.

### Asignación de nomenclatura

Leer `${CLAUDE_PLUGIN_ROOT}/skills/constructor-perfil/references/reglas-nomenclatura.md` para asignar códigos SS-AA-PP (y VV si aplica).

1. Consultar `data/registro.md` para obtener códigos de sector y área
2. Si el sector o área no existe → antes de asignar el código, validar la granularidad del nombre del área:
   - Si el nombre del área ya existe en `data/registro.md` → proceder sin validación (área previamente aprobada).
   - Si el área es nueva y el nombre contiene conjunciones (`y`, `e`, `,`, `/`) que sugieran dominios fusionados → pausar, mostrar la regla de granularidad de `${CLAUDE_PLUGIN_ROOT}/skills/constructor-ontologia/references/estructura-ontologia.md`, y pedir al usuario que confirme o divida el nombre antes de registrar.
   - Si el área es nueva y el nombre representa un único dominio → asignar siguiente código y registrar normalmente.
3. Asignar código PP al nuevo Core
4. Si se genera Variación → asignar código VV
5. Actualizar `data/registro.md` con todos los códigos asignados

### Persistencia

- Core → guardar en `data/sectores/<SS-slug>/areas/<AA-slug>/perfiles/PP-titulo-slug.md`
- Variación → guardar en `data/sectores/<SS-slug>/areas/<AA-slug>/perfiles/variaciones/PP-VV-titulo-slug--contexto.md`

> El sector (`<SS-slug>`) y área (`<AA-slug>`) se obtienen del código SS-AA asignado en el paso de nomenclatura. Consultar `data/registro.md` para los slugs correspondientes a cada código.

### Validación legal

Invocar `validador-legal-mx` sobre ambos documentos. Presentar hallazgos al usuario.

### Enriquecimiento de ontología

Invocar `enriquecedor-ontologia` para detectar y agregar elementos nuevos mencionados durante la conversación.

### Ofrecimiento de enriquecimiento post-perfil

Al terminar, ofrecer:
"Los documentos están listos. ¿Te gustaría complementarlos con:
a) Sugerencia de rango salarial para este puesto
b) Retrato del candidato ideal para orientar la búsqueda
c) Guía de evaluación para entrevistas
d) Todos
e) No por ahora"

Si elige (a) o (d) → invocar `benchmark-salarial-mx`
Si elige (b) o (d) → invocar `generador-persona-candidato`
Si elige (c) o (d) → invocar `constructor-evaluacion`

---

## MODO 2: Crear Variación

1. Cargar el Perfil Core existente (el usuario lo indica o se busca en `data/sectores/<sector>/areas/<area>/perfiles/` — sector y área se infieren del contexto de la conversación o se le pide al usuario si no está claro)
2. Presentar resumen de lo heredado: "Este perfil tiene X competencias técnicas, Y blandas, Z herramientas. Todo esto se hereda automáticamente."
3. Preguntar contexto de la variación: "¿Para qué cliente, proyecto o especialidad es esta variación?"
4. Recopilar información contextual: equipo, jefe, métricas, condiciones, herramientas adicionales
5. Consultar `data/registro.md` y asignar código VV
6. Generar la Variación con formato de `${CLAUDE_PLUGIN_ROOT}/skills/constructor-perfil/references/formato-perfil-core.md` (sección Variación)
7. Validar con `validador-legal-mx`
8. Registrar en `data/registro.md`
9. Guardar en `data/sectores/<SS-slug>/areas/<AA-slug>/perfiles/variaciones/PP-VV-titulo-slug--contexto.md`
