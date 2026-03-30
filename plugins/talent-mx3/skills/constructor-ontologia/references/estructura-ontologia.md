# Estructura de la Ontología — talent-mx3

## Estructura de directorios

```
data/
  registro.md                                    ← Tabla maestra de códigos SS-AA-PP-VV
  ontologia/
    indice.md                                    ← Lookup table (SECTORIAL / COMÚN)
    sectores/
      <nombre-sector>/                           ← Una carpeta por sector
        industria.md                             ← Descripción del sector, métricas, empresas
        areas/
          <nombre-area>.md                       ← Roles típicos, funciones, herramientas
        competencias/
          tecnicas/
            <familia-competencia>.md             ← Competencias técnicas agrupadas
    comun/                                       ← Transversal a todos los sectores
      competencias/
        conductuales/catalogo.md                 ← Competencias blandas universales
        certificaciones/regulatorias.md          ← DC-3, NOM-035, LFT, REPSE
      herramientas/
        gestion-clientes.md                      ← CRMs, ticketing, contact center
        gestion-empresarial.md                   ← ERPs, nómina, contabilidad
        plataformas.md                           ← Marketplaces, e-commerce
        regulatorias.md                          ← SAT, IMSS, SUA, CFDI
  perfiles/                                      ← Perfiles Core (archivos SS-AA-PP-slug.md)
    variaciones/                                 ← Variaciones (archivos SS-AA-PP-VV-slug--contexto.md)
    ofertas/                                     ← Ofertas por plataforma
```

## Sistema de códigos SS-AA-PP-VV

Cada sector y área que se crea en la ontología recibe un código numérico en `data/registro.md`. Estos códigos se usan para nombrar los archivos de perfiles y variaciones.

| Nivel | Código | Se asigna al... |
|-------|--------|-----------------|
| Sector (SS) | 01-99 | crear sector en ontología |
| Área (AA) | 01-99 | crear área dentro de un sector |
| Perfil Core (PP) | 01-99 | crear perfil vía /crear-perfil |
| Variación (VV) | 01-99 | crear variación vía /crear-variacion |

**Regla:** Al crear un sector o área nueva, SIEMPRE asignar el siguiente código disponible en `data/registro.md` y registrarlo antes de continuar.

Las carpetas de la ontología mantienen nombres legibles (slugs). El mapeo slug ↔ código vive en `data/registro.md`.

## Formato de industria.md

```markdown
# [Nombre del Sector]

## Descripción general
[2-3 párrafos describiendo el sector en México]

## Áreas funcionales principales
- [Área 1]: [descripción breve]
- [Área 2]: [descripción breve]

## Indicadores del sector
- Rotación promedio: [%]
- Volumen de contratación: [alto/medio/bajo]
- Salario promedio operativo: $[rango] MXN
- Concentración geográfica: [zonas principales]

## Retos de contratación
- [Reto 1]
- [Reto 2]

## Empresas representativas en México
- [Empresa 1]
- [Empresa 2]

## Normativas aplicables
- [Norma 1]: [por qué aplica]
```

## Formato de área funcional

```markdown
# [Nombre del Área Funcional]

## Roles típicos

### [Rol 1]
- **Nivel:** [operativo / intermedio / gerencial]
- **Funciones principales:** [3-5 funciones]
- **Herramientas:** [herramientas típicas]
- **Competencias clave:** [3-5 competencias]
- **Rango salarial orientativo:** $[min]-$[max] MXN brutos mensuales (CDMX)

### [Rol 2]
...
```

## Regla de clasificación

| Pregunta | Si SÍ → | Si NO → |
|----------|---------|---------|
| ¿Lo usaría una empresa de otro sector? | `comun/` | `sectores/<sector>/` |
| ¿Es una norma o regulación mexicana? | `comun/competencias/certificaciones/` | Evaluar por sector |
| ¿Es una herramienta de uso general? | `comun/herramientas/` | `sectores/<sector>/competencias/tecnicas/` |
| ¿Es una competencia conductual? | `comun/competencias/conductuales/` | N/A (las conductuales siempre son comunes) |
