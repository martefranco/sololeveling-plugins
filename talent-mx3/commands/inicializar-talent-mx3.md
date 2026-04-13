---
description: "Crear estructura de carpetas y conocimiento común"
allowed-tools: Read, Write, Edit, Bash(mkdir:*,cp:*,ls:*), Glob
---

Inicializar la estructura de datos de talent-mx3 en la carpeta de trabajo del usuario.

Este comando se ejecuta una sola vez al empezar a usar el plugin. Crea las carpetas y archivos necesarios para que las skills funcionen. Solo instala el conocimiento común (universal para cualquier industria mexicana). Los sectores se construyen después con `/poblar-ontologia`.

Pasos:

1. Verificar si ya existe `data/sectores/` en el directorio de trabajo del usuario.
   - Si ya existe → preguntar: "Ya existe una estructura de talent-mx3 en esta carpeta. ¿Quieres reiniciarla (se perderá lo existente) o solo verificar que esté completa?"
   - Si no existe → continuar con la creación.

2. Crear la estructura de carpetas:
   ```
   data/
   ├── indice.md
   ├── registro.md
   ├── comun/
   │   ├── competencias/
   │   │   ├── conductuales/
   │   │   └── certificaciones/
   │   └── herramientas/
   └── sectores/                        ← Vacío — se puebla con /poblar-ontologia
   ```

3. Copiar los archivos seed desde `${CLAUDE_PLUGIN_ROOT}/data/seed/` a `data/`.
   Archivos seed incluidos (solo conocimiento común):
   - `indice.md` — Tabla de contenidos de la ontología
   - `comun/competencias/conductuales/catalogo.md` — Competencias conductuales universales
   - `comun/competencias/certificaciones/regulatorias.md` — DC-3, NOM-035, STPS
   - `comun/herramientas/gestion-clientes.md` — CRMs y ticketing
   - `comun/herramientas/gestion-empresarial.md` — ERPs y nómina
   - `comun/herramientas/plataformas.md` — Marketplaces y e-commerce
   - `comun/herramientas/regulatorias.md` — SAT, IMSS, SUA

   NO copiar archivos de `sectores/` — los sectores se construyen con `/poblar-ontologia`.

4. Copiar `${CLAUDE_PLUGIN_ROOT}/data/seed/registro.md` a `data/registro.md`.

5. Presentar resumen:
   "Estructura de talent-mx3 creada. Tienes:
   - Conocimiento común del mercado mexicano (regulaciones, herramientas, competencias conductuales)
   - Registro de códigos SS-AA-PP-VV listo para usar

   **Siguiente paso obligatorio:** ejecuta `/poblar-ontologia` para construir el conocimiento de tu industria antes de crear perfiles."

6. Verificar si `data/sectores/` está vacío usando Glob `data/sectores/*/industria.md`.
   - Si no hay resultados → mostrar: "No tienes sectores cargados aún. Ejecuta `/poblar-ontologia` para construir el conocimiento de tu industria. El sistema te guiará paso a paso con ejemplos."
   - Si hay resultados → no mostrar nada adicional.
