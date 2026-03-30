# Catálogo de Reglas — Validador Legal MX v2.0

## Reglas LFT (Ley Federal del Trabajo)

### LFT-001 — Jornada laboral obligatoria
- **Severidad:** ERROR
- **Norma:** Art. 25 LFT — todo contrato debe especificar jornada
- **Verifica:** El perfil incluye tipo de jornada (diurna, nocturna, mixta) y horario
- **Acción si falta:** "El perfil no especifica jornada laboral. Art. 25 LFT requiere definirla. Sugerencia: agregar jornada diurna L-V 9:00-18:00 o la que corresponda."

### LFT-002 — Zona de trabajo
- **Severidad:** ERROR
- **Norma:** Art. 25 LFT — lugar de prestación de servicios
- **Verifica:** El perfil indica zona geográfica, municipio o estado
- **Acción si falta:** "No se especifica zona de trabajo. Art. 25 LFT requiere definir el lugar de prestación de servicios."

### LFT-003 — Funciones específicas
- **Severidad:** WARNING
- **Norma:** Art. 25 LFT — descripción detallada del trabajo
- **Verifica:** Las funciones son específicas y medibles, no genéricas como "actividades afines"
- **Acción si genéricas:** "Las funciones son demasiado genéricas. Especificar tareas concretas para evitar ambigüedad contractual."

### LFT-004 — Discriminación por edad
- **Severidad:** ERROR
- **Norma:** Art. 2, 3, 133 LFT — prohibición de discriminación
- **Verifica:** No hay límites de edad explícitos sin justificación operativa documentada
- **Acción si presente:** "Requisito de edad detectado. Art. 133 fracción I LFT prohíbe discriminar por edad. Eliminar o justificar con base en necesidad operativa demostrable."

### LFT-005 — Discriminación por género
- **Severidad:** ERROR
- **Norma:** Art. 2, 3, 56, 133 LFT
- **Verifica:** No hay requisitos de género sin justificación operativa
- **Acción si presente:** "Requisito de género detectado. Art. 133 LFT prohíbe discriminar por sexo. Eliminar a menos que exista justificación operativa documentada (ej: vestidores en instalaciones)."

### LFT-006 — Discriminación por apariencia/estado civil
- **Severidad:** ERROR
- **Norma:** Art. 133 fracción I LFT
- **Verifica:** No hay requisitos de "buena presentación", estatura, peso, estado civil
- **Acción si presente:** "Requisito de apariencia física o estado civil detectado. Viola Art. 133 LFT. Eliminar completamente."

### LFT-007 — Discriminación por situación familiar/reproductiva
- **Severidad:** ERROR
- **Norma:** Art. 133 fracción XIV y XV LFT
- **Verifica:** No hay referencias a embarazo, número de hijos, planes familiares
- **Acción si presente:** "Referencia a situación familiar/reproductiva detectada. Art. 133 fracciones XIV y XV LFT lo prohíben expresamente. Eliminar."

## Reglas NOM-035

### NOM035-001 — Factores de riesgo psicosocial
- **Severidad:** WARNING
- **Norma:** NOM-035-STPS-2018
- **Verifica:** Si el puesto implica alta presión, atención al público, o jornadas extensas, se mencionan condiciones de bienestar
- **Acción si falta:** "Puesto con indicadores de riesgo psicosocial (atención al público / alta presión). NOM-035 recomienda documentar condiciones de bienestar y carga de trabajo."

## Reglas STPS (Seguridad)

### STPS-001 — Capacitación DC-3 obligatoria
- **Severidad:** ERROR
- **Norma:** STPS — constancias DC-3 para puestos de riesgo
- **Verifica:** Si el puesto implica riesgo físico (alturas, electricidad, maquinaria, campo), se incluye DC-3 como must-have
- **Acción si falta:** "Puesto con riesgo físico identificado pero sin DC-3 como requisito obligatorio. Mover a must-have."

### STPS-002 — Equipo de Protección Personal
- **Severidad:** WARNING
- **Norma:** NOM-017-STPS-2008
- **Verifica:** Si el puesto requiere trabajo físico, se menciona EPP
- **Acción si falta:** "Puesto con riesgo físico sin mención de EPP. NOM-017 requiere especificar equipo de protección."

### STPS-003 — Trabajo en alturas NOM-009
- **Severidad:** ERROR
- **Norma:** NOM-009-STPS-2011
- **Verifica:** Si el puesto implica trabajo en alturas (>1.8m), DC-3 de NOM-009 es must-have
- **Acción si clasificado como nice-to-have:** "Certificación de alturas NOM-009 está como nice-to-have pero es OBLIGATORIA por ley para trabajo en alturas. Mover a must-have."

## Reglas REPSE

### REPSE-001 — Registro de servicios especializados
- **Severidad:** WARNING
- **Norma:** Art. 15 LFT — REPSE obligatorio para subcontratación especializada
- **Verifica:** Si la empresa ofrece servicios especializados/outsourcing, tiene registro REPSE
- **Acción si falta:** "Empresa de servicios especializados sin mención de registro REPSE. Desde 2021 es obligatorio."

### REPSE-002 — Transparencia en subcontratación
- **Severidad:** INFO
- **Norma:** Reforma de subcontratación 2021
- **Verifica:** Si el perfil es para personal subcontratado, se especifica quién es el patrón real
- **Acción si falta:** "Para personal subcontratado, es recomendable especificar la relación contractual para transparencia con el candidato."

## Reglas de Must-Have

### MH-001 — Certificaciones legales mal clasificadas
- **Severidad:** ERROR
- **Verifica:** Certificaciones requeridas por ley (DC-3, NOM-009, licencia de conducir tipo específico) NO están como nice-to-have
- **Acción si mal clasificadas:** "Certificación obligatoria por ley clasificada como nice-to-have. Mover a must-have."

### MH-002 — Must-haves excesivos
- **Severidad:** WARNING
- **Verifica:** No hay más de 5-7 must-haves (más de 7 indica que no se priorizó correctamente)
- **Acción si excede:** "Más de 7 must-haves detectados. Revisar si todos son realmente indispensables. Los must-haves excesivos reducen el pool de candidatos innecesariamente."

### MH-003 — Discriminación en must-haves
- **Severidad:** ERROR
- **Verifica:** Ningún must-have es discriminatorio (edad, género, apariencia, estado civil, religión)
- **Acción si presente:** "Must-have discriminatorio detectado. Viola Art. 133 LFT."

## Reglas de Mejores Prácticas

### BP-001 — Rango salarial
- **Severidad:** INFO
- **Verifica:** El perfil incluye rango salarial orientativo
- **Acción si falta:** "No se incluye rango salarial. Incluirlo mejora la transparencia y reduce candidatos desalineados en expectativa."

### BP-002 — Prestaciones superiores
- **Severidad:** INFO
- **Verifica:** Se mencionan prestaciones superiores a la ley si las hay
- **Acción si falta:** "No se mencionan prestaciones superiores a la ley. Si existen, incluirlas mejora la atracción de talento."

## Reglas para Guías de Evaluación

### EVAL-001 — Preguntas sobre edad
- **Severidad:** ERROR
- **Verifica:** No hay preguntas directas o indirectas sobre edad
- **Acción:** "Pregunta sobre edad detectada. Eliminar."

### EVAL-002 — Preguntas sobre estado civil/familia
- **Severidad:** ERROR
- **Verifica:** No hay preguntas sobre estado civil, embarazo, planes familiares, número de hijos
- **Acción:** "Pregunta sobre situación familiar detectada. Viola Art. 133 LFT."

### EVAL-003 — Preguntas sobre religión/orientación
- **Severidad:** ERROR
- **Verifica:** No hay preguntas sobre religión, orientación sexual, creencias políticas
- **Acción:** "Pregunta sobre creencias personales detectada. Eliminar."

### EVAL-004 — Requisitos físicos como filtro personal
- **Severidad:** WARNING
- **Verifica:** Si hay requisito físico legítimo (cargar peso, alturas), la pregunta se enfoca en capacidad, no en la persona
- **Acción:** "Pregunta sobre capacidad física debe enfocarse en la tarea ('¿puedes cargar 15 kg?'), no en la persona ('¿tienes alguna discapacidad?')."
