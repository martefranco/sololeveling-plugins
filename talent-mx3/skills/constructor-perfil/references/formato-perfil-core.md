# Formato del Perfil de Puesto — Core y Variación

## Principio de separación

El Intake Meeting recopila TODO (genérico + contextual), pero el output se divide en dos documentos:

- **Perfil Core** = Ficha técnica reutilizable del rol. Define QUÉ ES el puesto independientemente de quién lo contrate.
- **Variación** = Contexto específico de ESTA contratación. Hereda del Core y agrega proyecto, equipo, salario, métricas concretas.

### Regla de clasificación al generar output

| Pregunta sobre el dato | Si SÍ → | Si NO → |
|------------------------|---------|---------|
| ¿Cambiaría si el mismo rol se contrata en otro proyecto? | Variación | Core |
| ¿Depende de una estructura organizacional específica? | Variación | Core |
| ¿Incluye nombres de personas, equipos o proyectos? | Variación | Core |
| ¿Es un rango salarial atado a un presupuesto concreto? | Variación | Core |
| ¿Son métricas amarradas a un timeline de proyecto? | Variación | Core |

---

## FORMATO DEL PERFIL CORE (7 secciones)

```markdown
# PERFIL CORE — [Título del Puesto]

**Código:** SS-AA-PP
**Fecha de creación:** YYYY-MM-DD
**Sector:** [sector de la ontología]
**Área funcional:** [área]
**Nivel:** [operativo / intermedio / gerencial]
**Template base:** [nombre del template o "construido desde cero"]

---

## 1. Misión del puesto
En 2-3 oraciones, qué se espera que logre esta persona. No es una lista
de funciones — es el PARA QUÉ del puesto. Redactar de forma genérica,
sin referencias a proyectos o empresas específicas.

## 2. Tareas y responsabilidades principales
5-8 tareas concretas del día a día del ROL (no del proyecto).
Cada tarea debe ser verificable y aplicable en cualquier contexto
donde se necesite este perfil.

## 3. Competencias técnicas
Lista de competencias técnicas requeridas para el ROL:
- Nombre de la competencia
- Nivel esperado (básico / intermedio / avanzado)
- Herramienta o contexto donde se aplica

## 4. Competencias conductuales
5 competencias blandas priorizadas para este tipo de ROL:
- Nombre de la competencia
- Por qué es crítica para ESTE tipo de puesto (no para un proyecto)
- Ejemplo de comportamiento esperado

## 5. Herramientas y tecnología
Lista de software, equipos o herramientas típicas del ROL.
Distinguir entre "debe dominar" y "se capacitará".

## 6. Requisitos Must-Have (indispensables)
Lo que un candidato DEBE tener para este ROL. Máximo 5-7 elementos.
Incluye: formación mínima, experiencia específica, certificaciones,
idiomas. NO incluir datos atados a un presupuesto o proyecto.

## 7. Requisitos Nice-to-Have (deseables)
Lo que sería ideal pero no indispensable para el ROL en general.
```

---

## FORMATO DE LA VARIACIÓN (6 secciones)

```markdown
# VARIACIÓN — [Título del Puesto] — [Contexto]

**Código:** SS-AA-PP-VV
**Perfil Core padre:** [código SS-AA-PP] — [link al archivo]
**Fecha de creación:** YYYY-MM-DD
**Contexto:** [cliente / proyecto / especialidad]
**Tipo de necesidad:** [reemplazo / posición nueva]

---

## 1. Contexto de negocio
Qué situación específica motiva ESTA contratación.
Por qué se necesita a esta persona AHORA, en ESTE proyecto/equipo.

## 2. Ubicación organizacional
- Reporta a: [nombre/puesto del jefe directo]
- Equipo: [descripción del equipo actual]
- Interacciones: [áreas/personas con las que colaborará]
- Estilo de liderazgo del jefe: [descripción]

## 3. Contexto del equipo y microcultura
Quién es el equipo, cómo trabajan, qué tipo de persona florece ahí,
qué tipo NO funciona. Ritmo de trabajo, nivel de formalidad.

## 4. Métricas de éxito específicas
- A los 30 días: [indicador concreto de este proyecto]
- A los 90 días: [indicador concreto]
- Indicadores continuos: [KPIs de este contexto]

## 5. Competencias y herramientas adicionales
Solo lo que se SUMA al Core para este contexto específico:
- Competencias técnicas adicionales (si aplica)
- Herramientas adicionales (si aplica)
- Certificaciones adicionales (si aplica)

## 6. Condiciones y compensación
- Jornada laboral: [tipo y horario]
- Zona de trabajo: [ubicación específica]
- Rango salarial: $[min] — $[max] MXN brutos mensuales
- Prestaciones: [detalle]
- Condiciones especiales: [viajes, campo, horario rotativo]
- Flags de compliance del validador-legal-mx
```

---

## FLUJO DE GENERACIÓN POST-INTAKE

Después de recopilar toda la información del Intake Meeting:

1. **Identificar sector y área** → consultar `data/registro.md` para obtener SS-AA
2. **¿Ya existe un Core para este tipo de rol en esta área?**
   - SÍ → usar el Core existente, ir directo a generar Variación
   - NO → generar Core nuevo + Variación
3. **Generar el Core** aplicando la regla de clasificación (tabla arriba)
   - Asignar código PP siguiente disponible
   - Registrar en `data/registro.md`
   - Guardar en `data/sectores/<SS-slug>/areas/<AA-slug>/perfiles/PP-slug.md`
4. **Preguntar al usuario:** "El perfil genérico del rol está listo. La información específica de tu proyecto/equipo la guardaré como variación. ¿Quieres generar la variación ahora?"
   - SÍ → generar Variación, asignar VV, registrar, guardar en `data/sectores/<SS-slug>/areas/<AA-slug>/perfiles/variaciones/`
   - NO → solo guardar el Core
5. **Validar ambos documentos** con validador-legal-mx

## REGLA IMPORTANTE

Si el usuario proporcionó contexto específico durante el Intake (proyecto, jefe, salario, métricas a 30/90 días), SIEMPRE generar ambos documentos (Core + Variación). No preguntar — el usuario ya dio la información, solo separar.

Solo preguntar si el usuario NO proporcionó contexto específico (ej: "necesito un Especialista en IA" sin mencionar proyecto ni equipo).
