---
name: benchmark-salarial-mx
description: >
  Sugiere rangos salariales por zona geográfica, industria y nivel de experiencia para el mercado mexicano. Enriquece el Perfil Core con el dato que el Hiring Manager típicamente no sabe definir con precisión. Triggers: "cuánto debería pagar", "rango salarial", "benchmark salarial", "salario de mercado", "cuánto gana un", "compensación", "sueldo promedio", "paquete salarial".
---

# Benchmark Salarial MX

Sugerir rangos salariales realistas para puestos en el mercado mexicano, ajustados por zona geográfica, industria y nivel de experiencia.

## Cuándo se invoca

- Al final de `/crear-perfil` como enriquecimiento opcional
- Cuando `generador-oferta` necesita el dato de salario (paso 7)
- Cuando el usuario pregunta directamente por rangos salariales

## Dónde se aplica el dato salarial

El rango salarial es un dato **contextual**, no genérico del rol. Por lo tanto:
- Si existe una **Variación** → el rango se incluye en la Variación (sección 6: Condiciones y compensación)
- Si solo existe el **Core** (sin variación aún) → el rango se sugiere al usuario para cuando genere una Variación
- En el **Core** NO se incluye un rango salarial específico — el Core es reutilizable y el salario depende del contexto

## Flujo

1. Recibir datos del perfil: título, sector, área, nivel, zona geográfica

2. Buscar datos salariales (en orden de prioridad):
   a. ¿El template de `plantillas-industria-mx` tiene rango para este rol? → usar como base
   b. ¿El archivo de industria del sector tiene datos salariales? → cruzar con zona
   c. Si no hay datos específicos → usar tabla de rangos base en `${CLAUDE_PLUGIN_ROOT}/skills/benchmark-salarial-mx/references/tabla-rangos-mx.md`

3. Ajustar por zona geográfica:
   - CDMX: referencia base (índice 1.0)
   - Monterrey (NL): +5-10% vs CDMX
   - Guadalajara (JAL): -5-10% vs CDMX
   - Querétaro/Bajío: -10-15% vs CDMX
   - Resto del país: -15-25% vs CDMX

4. Ajustar por nivel de experiencia:
   - Junior (0-2 años): rango bajo del mercado
   - Intermedio (2-5 años): rango medio
   - Senior (5+ años): rango alto
   - Gerencial: rango alto + 20-30%

5. Presentar resultado:
   "Para un [título] en [zona], el mercado mexicano sugiere un rango de $[min] — $[max] MXN brutos mensuales.

   Fuente: [template / ontología / estimación general]
   Ajustes aplicados: [zona] [nivel]

   ¿Quieres incluir este rango en la variación del perfil?"

6. Si el usuario tiene dato propio:
   - Comparar contra benchmark
   - "Tu oferta de $[X] está [por debajo / dentro / por encima] del rango de mercado ($[min]-$[max]). [Análisis de competitividad]."
   - El dato del usuario SIEMPRE tiene prioridad

## Reglas

- NUNCA inventar un número preciso — siempre dar RANGO (min-max)
- Si no hay datos específicos → decir "no tengo datos específicos" y ofrecer rango general por nivel
- El dato del usuario tiene prioridad sobre el benchmark
- Indicar SIEMPRE la fuente: template, ontología, o estimación general
- Los montos son en MXN brutos mensuales
- Tabla de rangos en `${CLAUDE_PLUGIN_ROOT}/skills/benchmark-salarial-mx/references/tabla-rangos-mx.md`
