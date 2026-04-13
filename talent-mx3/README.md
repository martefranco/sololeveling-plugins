# talent-mx3 ![v4.1.0](https://img.shields.io/badge/version-4.1.0-blue)

> Sistema de Talent Acquisition potenciado por IA para el mercado mexicano.

Digitaliza el **Intake Meeting** — el proceso consultivo donde se define lo que el negocio realmente necesita antes de buscar candidatos. No empieza por el título de puesto; empieza por el problema de negocio. Genera perfiles, variaciones y ofertas con herencia automática y validación legal MX integrada.

---

## 🚀 Primeros pasos

1. Instala el plugin en Claude
2. Ejecuta `/inicializar-talent-mx3` — crea la estructura de datos en tu carpeta de trabajo
3. Ejecuta `/crear-perfil` — inicia tu primer Intake Meeting consultivo
4. _(Opcional)_ Ejecuta `/poblar-ontologia` primero si quieres cargar el conocimiento de tu industria antes de crear perfiles

---

## ⌨️ Commands

| Command | Descripción |
|---------|-------------|
| `/inicializar-talent-mx3` | Crea la estructura de carpetas y ontología seed |
| `/crear-perfil` | Intake Meeting consultivo → Perfil Core (7 secciones) |
| `/crear-variacion` | Deriva una variación de un perfil existente (hereda base) |
| `/crear-oferta` | Genera ofertas por plataforma (OCC, LinkedIn, Computrabajo, Indeed) |
| `/vacante-completa` | Flujo completo: perfil → variaciones → ofertas en una sesión |
| `/poblar-ontologia` | Carga conocimiento de una industria o área funcional |
| `/crear-evaluacion` | Genera guía de entrevista + scorecard basados en el perfil |

---

## ⚙️ Skills

| Skill | Capa | Función |
|-------|------|---------|
| `validador-legal-mx` | Foundation | Valida perfiles contra LFT, NOM-035, STPS |
| `enriquecedor-ontologia` | Foundation | Aprende automáticamente durante cada `/crear-perfil` |
| `constructor-ontologia` | Foundation | Poblar ontología de forma intencional |
| `plantillas-industria-mx` | Core | Templates de roles por industria mexicana |
| `constructor-perfil` | Core | Intake Meeting consultivo — Core + Variación |
| `benchmark-salarial-mx` | Core | Rangos salariales por zona, industria y nivel |
| `generador-persona-candidato` | Core | Retrato del candidato ideal para sourcing |
| `generador-oferta` | Output | Fórmula de 8 pasos para ofertas por plataforma |
| `constructor-evaluacion` | Output | Guías de entrevista + scorecard + preguntas STAR |

---

## 📁 Estructura de datos

Al ejecutar `/inicializar-talent-mx3`, se crea esta jerarquía en tu carpeta de trabajo:

```
data/
├── indice.md                          ← Tabla de contenidos global
├── registro.md                        ← Tabla maestra de perfiles
├── comun/                             ← Conocimiento transversal MX
│   ├── competencias/
│   └── herramientas/
└── sectores/
    └── ti-servicios/                  ← Sector seed (incluido por defecto)
        ├── industria.md
        ├── competencias/
        └── areas/
            ├── atencion-cliente/      ← Área como directorio
            │   ├── area.md            ← Definición del área
            │   └── perfiles/          ← Perfiles del área
            │       ├── variaciones/   ← Variaciones por cliente/contexto
            │       └── ofertas/       ← Ofertas listas para publicar
            └── operaciones-campo/
                ├── area.md
                └── perfiles/
                    ├── variaciones/
                    └── ofertas/
```

**Convención de nombres:** los archivos de perfil usan el formato `PP-slug.md` donde `PP` es el número de perfil dentro del área. El sector (`SS`) y área (`AA`) se infieren de su ubicación en el árbol — no se repiten en el nombre del archivo.

---

## 🔗 Modelo de herencia

```
Perfil Core (competencias base)
    ├── Variación Amazon   (hereda + agrega específico de cliente)
    ├── Variación MELI     (hereda + agrega específico de cliente)
    └── Variación Walmart  (hereda + agrega específico de cliente)
         ├── Oferta OCC
         ├── Oferta LinkedIn
         └── Oferta Computrabajo
```

Cada nivel hereda del anterior: **Core → Variación → Oferta**. Las variaciones sólo documentan lo que cambia; las ofertas adaptan el lenguaje a cada plataforma.

---

## ✅ Compliance

Todos los perfiles y ofertas se validan automáticamente contra:

| Marco | Alcance |
|-------|---------|
| **LFT** | Ley Federal del Trabajo |
| **NOM-035** | Factores de riesgo psicosocial |
| **STPS** | Seguridad y salud en el trabajo |
| **Anti-discriminación** | Artículos 2, 3, 56, 133 LFT |

---

## 🆕 Novedades en v4.1.0

- **Granularidad de áreas** — nueva regla canónica: un área = un dominio funcional. Prohíbe fusionar dominios (ej. "Ventas y Marketing") en una sola carpeta
- **Protocolo de taxonomía** — paso de validación obligatorio antes de crear carpetas de área en `/poblar-ontologia` (Modos A y B)
- **Guard clauses** — `enriquecedor-ontologia` y `constructor-perfil` validan nombres de área antes de registrar códigos AA
- **Referencia extraída** — `references/taxonomia-granularidad.md` con protocolo de 5 pasos reutilizable

---

## 🆕 Novedades en v4.0.0

- **Jerarquía unificada** — se elimina la separación `ontologia/` / `perfiles/`; todo vive en un único árbol `sectores/`
- **Áreas como directorios** — cada área tiene su propia carpeta con `variaciones/` y `ofertas/` dentro de `perfiles/`
- **Nomenclatura simplificada** — formato `PP-slug.md`; sector y área se derivan de la ruta, no del nombre
- **Compliance canónico** — todas las referencias internas usan `${CLAUDE_PLUGIN_ROOT}`

---

## ⚙️ Configuración opcional

### Persistencia con ~~git

Para sincronizar la ontología entre sesiones y compartirla con tu equipo, configura un MCP server de ~~git apuntando a un repositorio privado.

---

## Autor

Creado por **MarteFranco** — martn00@hotmail.com
