---
name: constructor-ontologia
description: >
  Construye y expande la ontología de conocimiento de forma intencional y estructurada. Usar cuando el usuario quiere cargar el conocimiento de una industria, área funcional, o empresa completa antes de crear perfiles individuales. Triggers: "poblar ontología", "cargar industria", "agregar sector", "configurar conocimiento", "cargar mi empresa", "agregar área funcional".
---

# Constructor de Ontología

Guiar al usuario en la construcción intencional de conocimiento sectorial y transversal para enriquecer la base de datos de talent-mx3.

## Cuándo se usa

Se invoca a través del command `/poblar-ontologia`. Es el "Camino 1" (dedicado) de construcción de ontología, complementario al "Camino 2" (automático, vía enriquecedor-ontologia durante /crear-perfil).

Usar cuando:
- El usuario quiere cargar una industria completa antes de crear perfiles
- Se agrega un nuevo sector que no existe en la ontología
- Se quiere profundizar un sector existente con más roles, herramientas o competencias

## Flujo conversacional

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
