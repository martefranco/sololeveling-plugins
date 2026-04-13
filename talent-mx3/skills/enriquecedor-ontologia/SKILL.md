---
name: enriquecedor-ontologia
description: >
  Enriquece automáticamente la ontología de conocimiento durante las conversaciones de creación de perfiles. Detecta herramientas, competencias, certificaciones y datos sectoriales mencionados por el usuario que no existen en la base de conocimiento, los clasifica y los agrega. Esta skill se invoca en paralelo durante /crear-perfil — no requiere acción del usuario. Triggers: nunca se invoca directamente — se activa automáticamente durante constructor-perfil.
---

# Enriquecedor de Ontología

Detectar y agregar conocimiento nuevo a `data/` durante las conversaciones de creación de perfiles, sin interrumpir el flujo del Intake Meeting.

## Cuándo se activa

Se ejecuta en paralelo durante `constructor-perfil`. Al detectar que el usuario menciona un elemento no registrado en la ontología, lo clasifica y agrega.

## Flujo de detección

1. Durante el Intake Meeting, monitorear menciones de:
   - Herramientas o software no catalogados
   - Competencias técnicas no registradas
   - Certificaciones no conocidas
   - Áreas funcionales nuevas
   - Datos sectoriales (salarios, rotación, empresas competidoras)

2. Para cada elemento nuevo detectado:
   a. Buscar en `data/indice.md` si ya existe
   b. Si NO existe → clasificar y agregar
   c. Si existe parcialmente → enriquecer sin duplicar

3. Clasificar usando la regla sectorial/común:
   - **Sectorial** (`data/sectores/<sector>/`): dato exclusivo de un sector específico
     Ejemplos: fusionadora de fibra óptica, Seller Central de Amazon, SIPRES
   - **Común** (`data/comun/`): dato transversal a cualquier empresa mexicana
     Ejemplos: SAT, CFDI, DC-3, competencias conductuales, Excel

4. Agregar al archivo correspondiente dentro de la ontología

5. Actualizar `data/indice.md` con la nueva entrada

6. **Si se detecta un área funcional nueva:** asignar código AA consultando `data/registro.md`, registrar el nuevo código

7. Notificar sin interrumpir: mensaje breve tipo "Agregué [elemento] a la base de conocimiento en [ubicación]"

## Reglas de clasificación

Leer las reglas detalladas en `${CLAUDE_PLUGIN_ROOT}/skills/enriquecedor-ontologia/references/reglas-clasificacion.md`.

## Reglas de operación

- NUNCA interrumpir el flujo del Intake Meeting con preguntas de clasificación
- Si hay suficiente contexto para clasificar, hacerlo automáticamente
- Si NO hay suficiente contexto, guardar el elemento como "pendiente de clasificación" y preguntar al final del flujo
- No duplicar entradas existentes — verificar siempre contra el índice
- Usar el mismo formato Markdown que los archivos existentes de la ontología
- Priorizar: primero completar el perfil, después enriquecer la ontología
- Al detectar áreas nuevas, SIEMPRE registrar el código AA en `data/registro.md`
