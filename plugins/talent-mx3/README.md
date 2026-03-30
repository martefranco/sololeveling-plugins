# talent-mx3

Sistema de Talent Acquisition potenciado por IA para el mercado mexicano.

## Qué hace

talent-mx3 digitaliza y potencia el **Intake Meeting** — el proceso consultivo donde se define lo que realmente necesita el negocio antes de buscar candidatos. No empieza pidiendo un título de puesto; empieza preguntando qué problema de negocio se quiere resolver.

## Componentes

### Commands (lo que el usuario ejecuta)

| Command | Descripción |
|---------|-------------|
| `/inicializar-talent-mx3` | Crea la estructura de carpetas y ontología seed en tu carpeta de trabajo |
| `/crear-perfil` | Inicia un Intake Meeting consultivo para generar un Perfil de Puesto Core |
| `/crear-variacion` | Deriva una variación de un perfil existente (hereda competencias base) |
| `/crear-oferta` | Genera ofertas de empleo adaptadas por plataforma (OCC, LinkedIn, Computrabajo, Indeed) |
| `/vacante-completa` | Flujo completo: perfil → variaciones → ofertas en una sola sesión |
| `/poblar-ontologia` | Carga conocimiento de una industria o área funcional a la ontología |
| `/crear-evaluacion` | Genera guía de entrevista y scorecard de evaluación basados en el perfil |

### Skills (motor interno)

| Skill | Capa | Función |
|-------|------|---------|
| `validador-legal-mx` | Foundation | Valida perfiles contra LFT, NOM-035, STPS |
| `plantillas-industria-mx` | Core | Templates de roles por industria mexicana |
| `constructor-perfil` | Core | Intake Meeting consultivo — genera Core (7 secciones) + Variación (6 secciones) |
| `generador-oferta` | Output | Fórmula de 8 pasos para ofertas por plataforma |
| `enriquecedor-ontologia` | Foundation | Aprende automáticamente durante cada `/crear-perfil` |
| `constructor-ontologia` | Foundation | Poblar ontología de forma intencional |
| `benchmark-salarial-mx` | Core | Rangos salariales por zona, industria y nivel |
| `generador-persona-candidato` | Core | Retrato del candidato ideal para sourcing |
| `constructor-evaluacion` | Output | Guías de entrevista + scorecard + preguntas STAR |

## Primeros pasos

1. Instala el plugin en Claude
2. Ejecuta `/inicializar-talent-mx3` para crear la estructura de datos en tu carpeta
3. Ejecuta `/crear-perfil` para crear tu primer perfil de puesto
4. Opcionalmente, ejecuta `/poblar-ontologia` primero si quieres cargar el conocimiento de tu industria

## Estructura de datos

Al ejecutar `/inicializar-talent-mx3`, se crea esta estructura en tu carpeta de trabajo:

```
data/
├── registro.md                      ← Tabla maestra de códigos SS-AA-PP-VV
├── ontologia/
│   ├── indice.md                    ← Tabla de contenidos (con códigos SS-AA)
│   ├── sectores/
│   │   └── ti-servicios/            ← Sector seed incluido (SS=01)
│   │       ├── industria.md
│   │       ├── areas/               ← Áreas con códigos AA
│   │       └── competencias/
│   └── comun/                       ← Conocimiento transversal MX
│       ├── competencias/
│       └── herramientas/
└── perfiles/                        ← Perfiles Core (SS-AA-PP-slug.md)
    ├── variaciones/                 ← Variaciones (SS-AA-PP-VV-slug--contexto.md)
    └── ofertas/                     ← Ofertas por plataforma
```

## Modelo de herencia

```
Perfil Core (competencias base)
    ├── Variación Amazon (hereda + agrega específico)
    ├── Variación MELI (hereda + agrega específico)
    └── Variación Walmart (hereda + agrega específico)
         ├── Oferta OCC
         ├── Oferta LinkedIn
         └── Oferta Computrabajo
```

## Compliance

Todos los perfiles y ofertas se validan automáticamente contra:
- **LFT** (Ley Federal del Trabajo)
- **NOM-035** (Factores de riesgo psicosocial)
- **STPS** (Seguridad y salud en el trabajo)
- **Anti-discriminación** (Artículos 2, 3, 56, 133 LFT)

## Configuración opcional

### Conexión a ~~git

Para que la ontología persista entre sesiones y se sincronice con tu equipo, configura un MCP server de ~~git apuntando a un repositorio privado.

## Autor

Creado por **Mainbit** — notificacionesbot@mainbit.com.mx
