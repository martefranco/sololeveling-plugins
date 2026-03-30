---
name: generador-persona-candidato
description: >
  Genera un retrato del candidato ideal a partir de un Perfil Core completo. Describe quién es la persona que cumple el perfil: qué la motiva, dónde encontrarla, qué la haría rechazar la oferta, y cómo debería ser el primer contacto. Útil para equipos de sourcing y hiring managers. Triggers: "persona del candidato", "candidato ideal", "a quién busco", "dónde buscar candidatos", "sourcing", "perfil del candidato", "retrato del candidato", "cómo atraer candidatos".
---

# Generador de Persona del Candidato

Transformar un Perfil Core técnico en un retrato humano del candidato ideal: quién es, qué lo mueve, dónde buscarlo, y cómo contactarlo.

## Cuándo se invoca

- Al final de `/crear-perfil` como enriquecimiento opcional
- Cuando el usuario pide explícitamente el perfil del candidato ideal
- Antes de una campaña de sourcing activo

## Input

Un Perfil Core completo (7 secciones) y opcionalmente su Variación (6 secciones). Si hay benchmark salarial disponible, también se usa.

## Flujo

1. Recibir el Perfil Core. Si existe Variación, cargarla también.

2. Analizar el Core y la Variación (si existe) para inferir:
   - Nivel de experiencia y etapa de carrera
   - Motivaciones probables
   - Frustraciones en trabajo actual
   - Canales de búsqueda de empleo
   - Objeciones al puesto
   - Tipo de mensaje que resonaría

3. Consultar datos complementarios:
   - `benchmark-salarial-mx`: expectativa salarial
   - Ontología del sector: retos de contratación
   - Competencias conductuales: tipo de personalidad

4. Generar retrato con formato en `references/formato-persona.md`

5. Presentar: "Generé el retrato del candidato ideal para [título]. ¿Quieres que lo guarde?"

6. Guardar en `data/perfiles/` junto al Core: `YYYY-MM-DD-titulo-slug--persona-candidato.md`

## Reglas

- **NO discriminar.** El perfil demográfico es descriptivo ("típicamente personas en primeros 5 años de carrera"), no restrictivo ("debe tener 25-35 años")
- Basarse en DATOS del perfil y ontología, no en estereotipos
- Si no hay suficiente contexto → indicar "insuficiente información — profundizar en el intake meeting"
- El retrato debe ser ÚTIL para sourcing, no un ejercicio académico
- Incluir SIEMPRE un ejemplo de mensaje de primer contacto
