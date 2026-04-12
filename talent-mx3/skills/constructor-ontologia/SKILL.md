---
name: constructor-ontologia
description: >
  Construye y expande la ontología de conocimiento de forma intencional y estructurada. Usar cuando el usuario quiere cargar el conocimiento de una industria, área funcional, o empresa completa antes de crear perfiles individuales. Incluye un modo guiado para el primer sector que usa ejemplos de referencia y búsqueda web opcional. Triggers: "poblar ontología", "cargar industria", "agregar sector", "configurar conocimiento", "cargar mi empresa", "agregar área funcional", "primer sector".
---

# Constructor de Ontología

Guiar al usuario en la construcción intencional de conocimiento sectorial y transversal para enriquecer la base de datos de talent-mx3.

## Cuándo se usa

Se invoca a través del command `/poblar-ontologia`. Es el "Camino 1" (dedicado) de construcción de ontología, complementario al "Camino 2" (automático, vía enriquecedor-ontologia durante /crear-perfil).

Usar cuando:
- El usuario quiere cargar una industria completa antes de crear perfiles
- Se agrega un nuevo sector que no existe en la ontología
- Se quiere profundizar un sector existente con más roles, herramientas o competencias

## Selección de modo

Determinar el modo leyendo el filesystem:

- Verificar con Glob `data/ontologia/sectores/*/industria.md`.
- **Sin resultados** → **Modo A: Primer Sector Guiado** (la ontología no tiene sectores aún).
- **Con resultados** → **Modo B: Sector Adicional** (flujo estándar para agregar o enriquecer sectores).

---

## Modo A: Primer Sector Guiado

Flujo para usuarios que acaban de inicializar el plugin y no tienen ningún sector cargado. Usa los archivos de TI/Servicios Externalizados como ejemplo de referencia para guiar la construcción del primer sector.

### A.1 — Bienvenida y contexto

Presentar mensaje de bienvenida:
"Vamos a construir el conocimiento de tu primera industria. Esto permite que los perfiles, ofertas y evaluaciones que generes tengan contexto real de tu sector."

Explicar brevemente la estructura resultante:
- Un archivo `industria.md` con la descripción del sector
- Al menos una área funcional con roles típicos
- Carpeta de competencias técnicas (se va poblando con el uso)

Leer `${CLAUDE_PLUGIN_ROOT}/skills/constructor-ontologia/references/estructura-ontologia.md` para tener los formatos de archivo.

### A.2 — Identificar la industria del usuario

Preguntar: "¿En qué industria o sector trabaja tu empresa o la mayoría de tus clientes?"

Proporcionar ejemplos generales: Retail, Manufactura, Salud, Logística, Financiero, Alimentos, Construcción, Educación, etc.

NO sugerir TI/Servicios como primera opción — es la referencia, no la elección esperada.

Asignar código SS=01 (primer sector) y derivar slug del nombre proporcionado.

### A.3 — Construir industria.md sección por sección

Leer `${CLAUDE_PLUGIN_ROOT}/data/seed/ontologia/sectores/ti-servicios/industria.md` como ejemplo de referencia.

Para CADA sección del formato `industria.md`, en este orden:

1. **Descripción general**: Mostrar el ejemplo de TI como referencia de formato. Preguntar al usuario que describa su sector en 2-3 párrafos.
2. **Áreas funcionales principales**: Mostrar las áreas de TI como ejemplo. Preguntar cuáles son las áreas clave del sector del usuario.
3. **Indicadores del sector**: Mostrar los indicadores de TI como ejemplo (rotación, volumen, salario, concentración geográfica). Si WebSearch está disponible → ofrecer: "¿Quieres que busque datos del sector [nombre] en México para pre-llenar esta sección?" Si no está disponible → pedir al usuario que aproxime los datos.
4. **Retos de contratación**: Mostrar los retos de TI como ejemplo. Preguntar los retos del sector del usuario.
5. **Empresas representativas**: Mostrar las empresas de TI como ejemplo. Si WebSearch disponible → ofrecer buscar empresas del sector en México. Si no → pedir al usuario.
6. **Normativas aplicables**: Mostrar las normativas de TI como ejemplo. Preguntar qué normativas aplican al sector del usuario.

Agrupar 2-3 secciones por turno de conversación para no saturar al usuario.

**REGLA CRÍTICA**: ACUMULAR toda la información en memoria. NO escribir ningún archivo en este paso.

### A.4 — Construir primera área funcional

Preguntar: "¿Cuál es el área funcional más representativa de tu operación? Es donde más contratas o donde más necesitas perfiles."

Leer `${CLAUDE_PLUGIN_ROOT}/data/seed/ontologia/sectores/ti-servicios/areas/atencion-cliente.md` como ejemplo de formato.

Recopilar para el área:
- Nombre del área
- Mínimo 2 roles típicos, cada uno con: nivel (operativo/intermedio/gerencial), funciones principales, herramientas, competencias clave, rango salarial orientativo en MXN

Si WebSearch disponible → ofrecer buscar rangos salariales y herramientas del sector en México.

Asignar código AA=01 para esta primera área.

**REGLA CRÍTICA**: ACUMULAR. NO escribir archivos.

### A.5 — Validación antes de escribir

Presentar resumen estructurado completo:
- Sector: [nombre] (SS=01, slug=[slug])
- industria.md: [campos completados]
- Primera área: [nombre] (AA=01), [N] roles definidos

Preguntar: "¿Todo correcto? Puedo ajustar cualquier dato antes de crear los archivos."

- Si el usuario ajusta → incorporar cambios, volver a mostrar resumen.
- Si el usuario confirma → proceder a A.6.

### A.6 — Crear archivos

Solo después de confirmación explícita en A.5:

1. Crear `data/ontologia/sectores/<slug>/industria.md` siguiendo formato de `estructura-ontologia.md`.
2. Crear `data/ontologia/sectores/<slug>/areas/<slug-area>.md` con los roles recopilados.
3. Crear carpeta `data/ontologia/sectores/<slug>/competencias/tecnicas/` (vacía, lista para uso futuro).
4. Actualizar `data/ontologia/indice.md` — agregar sección CONOCIMIENTO SECTORIAL con la entrada del nuevo sector.
5. Actualizar `data/registro.md` — agregar fila SS=01 en SECTORES y fila 01-01 en ÁREAS.

### A.7 — Reporte y siguiente paso

Confirmar archivos creados con lista explícita de paths.

Ofrecer: "¿Quieres agregar otra área funcional a [sector] ahora, o prefieres ir a `/crear-perfil` para crear tu primer perfil de puesto?"

### Reglas del Modo A

- MUST leer archivos de TI-Servicios vía `${CLAUDE_PLUGIN_ROOT}` para mostrar ejemplos — NEVER copiar su contenido al workspace.
- MUST acumular toda la información antes de escribir — escribir SOLO después de confirmación en A.5.
- MUST verificar disponibilidad de WebSearch antes de ofrecerlo. Si falla o no está → continuar sin él, indicar que los datos pueden aproximarse y enriquecerse después.
- MUST usar el formato de archivos definido en `${CLAUDE_PLUGIN_ROOT}/skills/constructor-ontologia/references/estructura-ontologia.md`.
- MUST escribir todo el contenido en español con contexto mexicano (MXN, normativas MX, zonas geográficas).

---

## Modo B: Sector Adicional (flujo estándar)

Flujo para agregar sectores o áreas cuando ya existe al menos un sector en la ontología.

### 1. Identificar el alcance

Preguntar: "¿Sobre qué industria o área funcional quieres construir conocimiento?"

Opciones:
- **Nueva industria completa** → crear rama en `sectores/<nuevo-sector>/`
- **Área funcional dentro de un sector existente** → agregar a `sectores/<sector>/areas/`
- **Enriquecer un sector existente** → agregar datos a archivos existentes

### 2. Asignar códigos

Consultar `data/registro.md` para verificar códigos existentes.
- **Nuevo sector** → asignar siguiente código SS disponible, registrar
- **Nueva área** → asignar siguiente código AA dentro del sector, registrar
- **Enriquecimiento** → no se asigna código nuevo

### 3. Recopilar información

Para una **nueva industria**:
- ¿Cómo se llama el sector? (para nombrar la carpeta)
- ¿Cuáles son las áreas funcionales principales?
- ¿Qué roles típicos existen en cada área?
- ¿Qué herramientas se usan comúnmente?
- ¿Qué certificaciones o normativas aplican?
- ¿Cuáles son los retos de contratación del sector?
- ¿Cuál es la concentración geográfica en México?

Para **enriquecer** un sector existente:
- Verificar qué ya existe leyendo `data/ontologia/indice.md`
- Preguntar solo por lo que falta
- No duplicar información existente

### 4. Crear/actualizar archivos

- Crear archivos `.md` siguiendo la estructura en `references/estructura-ontologia.md`
- Cada archivo debe ser autocontenido y legible
- Usar formato consistente con los archivos existentes
- Clasificar correctamente entre sectorial y común

### 5. Actualizar índice y registro

- Actualizar `data/ontologia/indice.md` con las nuevas entradas
- Actualizar `data/registro.md` con los códigos SS y AA asignados

### 6. Reportar

"Agregué X competencias, Y herramientas, Z certificaciones al sector [nombre]. Código asignado: SS=[código]. El índice y el registro están actualizados."

## Reglas

- Antes de crear, SIEMPRE verificar si ya existe en la ontología
- SIEMPRE consultar `data/registro.md` antes de asignar un código nuevo
- Si existe parcialmente, enriquecer sin duplicar
- Seguir la regla de clasificación sectorial/común
- Cada archivo < 200 líneas. Si crece más, dividir en sub-archivos
- Usar español para todo el contenido
- Incluir contexto mexicano siempre que sea relevante (herramientas, normativas, zonas)

## Estructura de referencia

Leer `references/estructura-ontologia.md` para la estructura completa esperada y los formatos de archivo.
