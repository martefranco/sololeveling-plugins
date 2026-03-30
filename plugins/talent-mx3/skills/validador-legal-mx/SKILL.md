---
name: validador-legal-mx
description: >
  Validador de compliance laboral mexicano. Usar cuando se genere cualquier perfil de puesto, oferta de empleo, o guía de evaluación para verificar cumplimiento con LFT, NOM-035, STPS y normativa anti-discriminación. Se activa automáticamente — no requiere invocación directa del usuario. Triggers: "validar perfil", "compliance", "cumplimiento legal", "verificar normativa", "LFT", "NOM-035", "STPS", "discriminación".
---

# Validador Legal MX

Validar automáticamente perfiles de puesto, ofertas de empleo y guías de evaluación contra la normativa laboral mexicana. Esta skill se invoca internamente por otras skills — no directamente por el usuario.

## Cuándo se invoca

- Al final de `constructor-perfil` → valida el Perfil Core generado
- Al final de `generador-oferta` → valida la oferta antes de marcarla como lista
- Al final de `constructor-evaluacion` → valida que las preguntas no sean discriminatorias
- Cuando cualquier skill genera un documento que describe un puesto de trabajo

## Flujo de validación

1. Recibir el documento a validar (perfil, oferta, o guía de evaluación)
2. Leer el catálogo de reglas en `references/catalogo-reglas.md`
3. Evaluar cada regla aplicable contra el documento
4. Clasificar hallazgos por severidad: ERROR, WARNING, INFO
5. Presentar resultados al usuario de forma clara y accionable

## Niveles de severidad

- **ERROR** — Viola la ley. DEBE corregirse antes de usar el documento. Ejemplo: requisito de género sin justificación operativa
- **WARNING** — Podría ser problema legal. Revisar y decidir. Ejemplo: no especificar jornada laboral
- **INFO** — Recomendación de mejores prácticas. Ejemplo: incluir prestaciones superiores a la ley

## Formato de reporte

Para cada hallazgo reportar:

```
[SEVERIDAD] CÓDIGO — Descripción
  Regla: Qué dice la norma
  Hallazgo: Qué se encontró en el documento
  Corrección sugerida: Cómo arreglarlo
```

## Reglas de operación

- NUNCA bloquear la generación de un documento — solo reportar hallazgos
- Si hay ERRORs, presentarlos primero y preguntar si el usuario quiere corregir antes de continuar
- Si solo hay WARNINGs e INFOs, presentar el resumen y continuar
- No ser alarmista — presentar los hallazgos de forma profesional y constructiva
- Fundamentar cada hallazgo con el artículo o norma específica
- Si el documento es una guía de evaluación, enfocarse en reglas anti-discriminación en preguntas
