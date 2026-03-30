---
name: plantillas-industria-mx
description: >
  Biblioteca de templates de roles por industria para el mercado mexicano. Provee puntos de partida con competencias, herramientas, certificaciones y métricas pre-definidas por sector. Se invoca automáticamente durante constructor-perfil cuando el rol del usuario coincide con un template disponible. También se puede consultar directamente. Triggers: "template de puesto", "plantilla de rol", "hay algún template para", "roles de la industria", "templates disponibles".
---

# Plantillas de Industria MX

Proveer templates de roles pre-configurados para el mercado mexicano que sirvan como punto de partida durante la creación de perfiles.

## Cómo funciona

1. Durante `constructor-perfil`, cuando se identifica el sector y tipo de rol del usuario
2. Buscar en `references/templates/` si hay un template que coincida
3. Si hay match → ofrecer al usuario: "Tengo una plantilla base para [rol] en [sector]. ¿Quieres que la usemos como punto de partida? La personalizaremos con tu contexto."
4. Si el usuario acepta → cargar template y usarlo como base para el Intake Meeting (las preguntas se enfocan en lo que el template NO cubre)
5. Si no hay match → informar y continuar construyendo desde cero

## Templates disponibles

Los templates están en `references/templates/`. Cada template incluye:
- 8-10 competencias técnicas con nivel esperado
- 5 competencias conductuales priorizadas
- 5-8 herramientas con nivel de dominio
- 2-3 certificaciones relevantes
- Métricas de desempeño sugeridas
- Rango salarial orientativo (CDMX)
- Notas de compliance

## Reglas

- Los templates son PUNTOS DE PARTIDA, no productos finales
- Siempre personalizar con el contexto del usuario
- Si el usuario no quiere usar el template, respetar su decisión
- Los templates se actualizan conforme la ontología crece
- Cada template debe reflejar el mercado MEXICANO (herramientas, normativas, salarios en MXN)
