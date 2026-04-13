---
name: generador-oferta
description: >
  Genera ofertas de empleo profesionales adaptadas por plataforma usando la fórmula de 8 pasos del Job Description. Transforma un Perfil Core o Variación en ofertas listas para publicar en OCC, LinkedIn, Computrabajo e Indeed, con tono y formato optimizado para cada canal. Triggers: "crear oferta", "publicar vacante", "generar oferta de empleo", "oferta para OCC", "oferta para LinkedIn", "oferta para Computrabajo", "oferta para Indeed", "adaptar oferta", "job description", "job posting".
---

# Generador de Ofertas de Empleo

Transformar un Perfil Core o Variación en ofertas de empleo profesionales, adaptadas por plataforma, usando la fórmula probada de 8 pasos.

## Input preferido: Variación

La oferta de empleo se genera idealmente desde una **Variación**, porque contiene tanto las competencias genéricas (heredadas del Core) como el contexto específico (proyecto, equipo, salario, métricas) que hace atractiva la oferta.

Si solo existe el Core (sin variación), se puede generar la oferta, pero será más genérica y le faltarán datos de contexto que atraen candidatos (salario, equipo, proyecto).

**Búsqueda de archivos:**
- Primero buscar en `data/sectores/<sector>/areas/<area>/perfiles/variaciones/` (preferido)
- Si no hay variaciones, buscar en `data/sectores/<sector>/areas/<area>/perfiles/` (Cores)
- Si hay un Core con variaciones, preguntar al usuario cuál usar
- El sector y área se infieren del perfil que el usuario proporciona como input

## Fórmula de 8 pasos

Cada oferta sigue esta estructura. Los detalles de cada paso están en `${CLAUDE_PLUGIN_ROOT}/skills/generador-oferta/references/formula-8-pasos.md`.

1. **Título** — Claro, con keywords, sin jerga interna
2. **Resumen del puesto** — 2-3 oraciones que capturan la esencia
3. **Contexto de la empresa** — Quién es la empresa, qué hace, por qué importa
4. **Misión y resultados esperados** — Qué logrará esta persona (de la Variación sección 4)
5. **Responsabilidades principales** — 5-8 tareas concretas (del Core sección 2)
6. **Requisitos** — Must-have (Core sección 6) + nice-to-have (Core sección 7) + adicionales (Variación sección 5)
7. **Compensación y beneficios** — Rango salarial de la Variación sección 6. Si hay benchmark de `benchmark-salarial-mx`, cruzar
8. **Call to Action** — Cómo aplicar + qué esperar del proceso

## Diseño bidireccional

Las ofertas NO son solo para atraer candidatos. También deben permitir que el candidato evalúe a la empresa.

## Nomenclatura de archivos

Seguir las reglas de `${CLAUDE_PLUGIN_ROOT}/skills/constructor-perfil/references/reglas-nomenclatura.md`:
- Desde Variación: `PP-VV-titulo-slug--plataforma.md`
- Desde Core (sin variación): `PP-00-titulo-slug--plataforma.md`

> El prefijo SS-AA ya NO forma parte del nombre del archivo. El sector y área quedan implícitos en la ruta de guardado.

Guardar en `data/sectores/<sector>/areas/<area>/perfiles/ofertas/`.

## Adaptación por plataforma

Las reglas específicas por plataforma están en `${CLAUDE_PLUGIN_ROOT}/skills/generador-oferta/references/reglas-plataforma.md`.

| Plataforma | Tono | Longitud | Enfoque |
|-----------|------|----------|---------|
| OCC | Formal-profesional | 800-1200 palabras | Beneficios detallados, compliance |
| LinkedIn | Profesional-cercano | 400-600 palabras | Keywords SEO, crecimiento, cultura |
| Computrabajo | Accesible-directo | 300-500 palabras | Requisitos claros, beneficios tangibles |
| Indeed MX | Conciso, bullets | 300-400 palabras | Salario visible, ubicación, horario |

## Flujo

1. Recibir Perfil Core o Variación como input
2. Preguntar: "¿Para qué plataforma(s) quieres la oferta?" (puede ser múltiples)
3. Si hay benchmark salarial disponible → usarlo en paso 7
4. Generar oferta(s) adaptada(s) por plataforma
5. Invocar `validador-legal-mx` para verificar la oferta
6. Presentar al usuario para revisión
7. Guardar en `data/sectores/<sector>/areas/<area>/perfiles/ofertas/` con nomenclatura correcta

## Reglas

- NUNCA usar clichés genéricos. Si no hay dato real, omitir en vez de inventar
- El salario debe ser un RANGO, nunca "competitivo" sin número
- Si el usuario no quiere publicar salario → respetar, pero advertir que reduce candidatos
- Cada oferta debe poder leerse de forma independiente (no depender del perfil)
- Validar con `validador-legal-mx` antes de marcar como lista
