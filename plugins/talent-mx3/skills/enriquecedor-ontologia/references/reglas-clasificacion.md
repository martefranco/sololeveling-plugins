# Reglas de Clasificación — Enriquecedor de Ontología

## Regla principal

Si el dato aplica SOLO a un sector específico → `sectores/<sector>/`
Si el dato aplica a cualquier empresa mexicana → `comun/`

## Ejemplos de clasificación

### Va en sectorial (`sectores/<sector>/`)
- Fusionadora de fibra óptica → `sectores/ti-servicios/competencias/tecnicas/campo-telecom.md`
- Amazon Seller Central → `sectores/ti-servicios/competencias/tecnicas/soporte-cliente.md`
- Métricas de SLA específicas de BPO → `sectores/ti-servicios/industria.md`
- Certificación BICSI → `sectores/ti-servicios/competencias/tecnicas/campo-telecom.md`

### Va en común (`comun/`)
- SAT, CFDI, DIOT → `comun/herramientas/regulatorias.md`
- Excel, Word, PowerPoint → `comun/herramientas/gestion-empresarial.md`
- Zendesk, Freshdesk → `comun/herramientas/gestion-clientes.md`
- DC-3, DC-4, NOM-035 → `comun/competencias/certificaciones/regulatorias.md`
- Comunicación efectiva, trabajo en equipo → `comun/competencias/conductuales/catalogo.md`
- Amazon, Mercado Libre (como plataforma) → `comun/herramientas/plataformas.md`

## Casos ambiguos

Si un elemento podría ser sectorial O común:
- Preguntarse: "¿Lo usaría una empresa de manufactura que no tiene nada que ver con este sector?"
- Si SÍ → común
- Si NO → sectorial
- En duda → común (es más seguro y más reutilizable)

## Formato de entrada

Al agregar una herramienta nueva, usar este formato:

```
### [Nombre de la herramienta]
- **Categoría:** [tipo: CRM, ticketing, ERP, regulatoria, etc.]
- **Uso típico:** [para qué se usa en 1 línea]
- **Roles que la usan:** [qué roles típicamente la necesitan]
- **Nivel de dominio esperado:** [básico / intermedio / avanzado]
```

Al agregar una competencia técnica nueva:

```
### [Nombre de la competencia]
- **Definición:** [qué significa dominar esta competencia]
- **Herramientas asociadas:** [herramientas relacionadas]
- **Cómo se evalúa:** [pregunta o ejercicio para verificar]
- **Niveles:** [básico: X / intermedio: Y / avanzado: Z]
```
